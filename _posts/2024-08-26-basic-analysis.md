---
title: 20240826 Analysis
author: Ryo Niwa
date: 2024-08-26
category: RNA-Seq
layout: post
mermaid: true
---

> ##### Aim for this page
> Understand the basic of RNA-Seq analysis
{: .block-tip }

## Quick answer of this page: Mapping, quantification, normalization

Must-read paper: [RNA sequencing: the teenage years](https://www.nature.com/articles/s41576-019-0150-2)

### Phase 1 — alignment/mapping of sequencing reads
> After sequencing has been completed, the starting point for analysis is the data files, which contain base-called sequencing reads, usually in the form of FASTQ files. The most common first step in processing these files is to map sequence reads to a known transcriptome (or annotated genome), converting each sequence read to one or more genomic coordinates. This process has traditionally been accomplished using distinct alignment tools, such as TopHat, STAR or HISAT, which rely on a reference genome.

People typically call this first step, alignment or mapping. Long story in short, mapping means: 

![SRA_structure](/assets/mapping.png)

Mostly we use reference genomes such as GRCh38 for the reference in mapping. In NCBI, SRA runs where the organism is Homo sapiens and type is Transcriptomic are aligned to genome assembly GCA_000001405.15 ([link](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000001405.26/)) using HISAT2. 

A. Bianchi, A. Di Marco and C. Pellegrini, "Comparing HISAT and STAR-based pipelines for RNA-Seq Data Analysis: a real experience," 2023 IEEE 36th International Symposium on Computer-Based Medical Systems (CBMS), L'Aquila, Italy, 2023, pp. 218-224, doi: 10.1109/CBMS58004.2023.00220.

The paper above describes two major mapping tools in RNA-Seq field, STAR and HISAT.

> HISAT2 uses graph FM index (GFM) [14], has a smaller index size, is faster but has limited multi-threading capabilities, and is optimized for both single-end and paired-end reads. 

> STAR2 uses Spliced Transcripts Alignment [11] as a reference algorithm, has a larger index size, higher sensitivity, and better multi-threading, but it is slower, and it is optimized for spliced reads.

Each algorithm creates distinct characteristics in mapping. It has been noted that different mapping tools can lead to variations in the identification of DEGs (differentially expressed genes). It is important to choose the appropriate tool based on one's available computational resources, the volume of data to be processed, and the specific research objectives.

> ##### DO NOT USE TopHat anymore even it was a legend
> Developers tweeted (maybe I should say 'posted') "Please stop using Tophat" multuiple times. 
> https://x.com/lpachter/status/937055346987712512
> https://x.com/lpachter/status/1762004715678957910
> HISAT2 is the one you should use if you want to use Tophat-like mapping. 
{: .block-warning }

> ##### Assembly of transcripts - why?
> Some analysis pipeline deploys StringTie as an assembler of transcripts. The main reason is this paper published on nature protocols.
> Pertea, M., Kim, D., Pertea, G. et al. Transcript-level expression analysis of RNA-seq experiments with HISAT, StringTie and Ballgown. Nat Protoc 11, 1650–1667 (2016). https://doi.org/10.1038/nprot.2016.095
>
> Due to alternative splicing, a single gene can produce multiple types of transcripts. Therefore, when estimating gene expression levels from mapping results, you can decide whether you ignore transcript isoforms and counts per gene, or consider isoforms and count for each isoform separately. De novo assembler such as StringTie makes isoform quantification possible. 
> https://ccb.jhu.edu/software/stringtie/index.shtml?t=faq
{: .block-tips }

### Phase 2 — quantification of transcript abundance
> Once reads have been mapped to genomic or transcriptomic locations, the next step in the analysis process is to assign them to genes or transcripts, to determine abundance measures. Diverse comparative studies have shown that the approach taken at the quantification step has perhaps the largest impact on the ultimate results, even greater than the choice of aligner. The quantification of read abundances for individual genes (that is, all transcript isoforms for that gene) relies on counting sequence reads that overlap known genes, using a transcriptome annotation.

The next step is to count how many times genes are sequenced. 