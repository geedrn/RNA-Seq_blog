---
title: Chapter1. What kind of magic does a bioinformatician perform to convert fastq to count matrix?
author: Ryo Niwa
date: 2024-09-06
category: RNA-Seq
layout: post
mermaid: true
---

> ##### Aim for this page
> Understand the basic of RNA-Seq analysis
{: .block-tip }

## Quick answer of this page: Mapping, quantification, normalization

Must-read paper: [RNA sequencing: the teenage years](https://www.nature.com/articles/s41576-019-0150-2)

**Stark, R., Grzelak, M. & Hadfield, J. RNA sequencing: the teenage years. Nat Rev Genet 20, 631–656 (2019). https://doi.org/10.1038/s41576-019-0150-2**

### Phase 1 — alignment/mapping of sequencing reads
> After sequencing has been completed, the starting point for analysis is the data files, which contain base-called sequencing reads, usually in the form of FASTQ files. The most common first step in processing these files is to map sequence reads to a known transcriptome (or annotated genome), converting each sequence read to one or more genomic coordinates. This process has traditionally been accomplished using distinct alignment tools, such as TopHat, STAR or HISAT, which rely on a reference genome.

People typically call this first step, alignment or mapping. Long story in short, mapping means: 

![SRA_structure](/assets/mapping.png)

Mostly we use reference genomes such as GRCh38 for the reference in mapping. In NCBI, SRA runs where the organism is Homo sapiens and type is Transcriptomic are aligned to genome assembly GCA_000001405.15 ([link](https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000001405.26/)) using HISAT2. 

**A. Bianchi, A. Di Marco and C. Pellegrini, "Comparing HISAT and STAR-based pipelines for RNA-Seq Data Analysis: a real experience," 2023 IEEE 36th International Symposium on Computer-Based Medical Systems (CBMS), L'Aquila, Italy, 2023, pp. 218-224, doi: 10.1109/CBMS58004.2023.00220.**

The paper above describes two major mapping tools in RNA-Seq field, STAR and HISAT.

> HISAT2 uses graph FM index (GFM), has a smaller index size, is faster but has limited multi-threading capabilities, and is optimized for both single-end and paired-end reads. 

> STAR2 uses Spliced Transcripts Alignment as a reference algorithm, has a larger index size, higher sensitivity, and better multi-threading, but it is slower, and it is optimized for spliced reads.

Each algorithm creates distinct characteristics in mapping. It has been noted that different mapping tools can lead to variations in the identification of DEGs (differentially expressed genes). It is important to choose the appropriate tool based on one's available computational resources, the volume of data to be processed, and the specific research objectives.

> ##### DO NOT USE TopHat anymore even it was a legend
> Developers tweeted (maybe I should say 'posted') "Please stop using Tophat" multuiple times. 
> https://x.com/lpachter/status/937055346987712512
> https://x.com/lpachter/status/1762004715678957910
><br/>
><br/>
> HISAT2 is the one you should use if you want to use Tophat-like mapping. 
{: .block-warning }

> ##### Assembly of transcripts - why?
> Some analysis pipeline deploys StringTie as an assembler of transcripts. The main reason is this paper published on nature protocols.
><br/>
><br/>
> **Pertea, M., Kim, D., Pertea, G. et al. Transcript-level expression analysis of RNA-seq experiments with HISAT, StringTie and Ballgown. Nat Protoc 11, 1650–1667 (2016). 
> https://doi.org/10.1038/nprot.2016.095**
><br/>
><br/>
> Due to alternative splicing, a single gene can produce multiple types of transcripts. Therefore, when estimating gene expression levels from mapping results,
> you can decide whether you ignore transcript isoforms and counts per gene (gene-level quantification), or consider isoforms and count for each isoform
> separately (transcript-level quantification). De novo assembler such as StringTie makes isoform quantification possible. 
><br/>
><br/>
> https://ccb.jhu.edu/software/stringtie/index.shtml?t=faq
{: .block-tip }

### Phase 2 — quantification of transcript abundance
> Once reads have been mapped to genomic or transcriptomic locations, the next step in the analysis process is to assign them to genes or transcripts, to determine abundance measures. Diverse comparative studies have shown that the approach taken at the quantification step has perhaps the largest impact on the ultimate results, even greater than the choice of aligner. The quantification of read abundances for individual genes (that is, all transcript isoforms for that gene) relies on counting sequence reads that overlap known genes, using a transcriptome annotation.

The next step is to count how many times genes are sequenced. Some methods are available here including HTSeq and RSEM. There are a couple of papers testing differences (The list below is a few examples). 

**Chandramohan R, Wu PY, Phan JH, Wang MD. Benchmarking RNA-Seq quantification tools. Annu Int Conf IEEE Eng Med Biol Soc. 2013;2013:647-50. doi: 10.1109/EMBC.2013.6609583.**

**Corchete LA, Rojas EA, Alonso-López D, De Las Rivas J, Gutiérrez NC, Burguillo FJ. Systematic comparison and assessment of RNA-seq procedures for gene expression quantitative analysis. Sci Rep. 2020 Nov 12;10(1):19737. doi: 10.1038/s41598-020-76881-x.**

**Wu, D., Yao, J., Ho, K. et al. Limitations of alignment-free tools in total RNA-seq quantification. BMC Genomics 19, 510 (2018). https://doi.org/10.1186/s12864-018-4869-5**

Here are the general ideas of two major tools. Please note that the table below is not always true depending on users' options. 

| Characteristic | HTSeq (featureCounts) | RSEM |
|----------------|-------|------|
| Algorithm | Simple counting method | Probability model-based estimation |
| Multi-mapping reads | Ignored or equally distributed | Probabilistically assigned |
| Isoform quantification | Not supported | Supported |
| Use case | Simple gene expression analysis | Detailed transcriptome analysis |

The figure on [HTSeq website](https://htseq.readthedocs.io/en/release_0.11.1/count.html) illustrates how case divisions in mappingis complicated. 

### Phase 3 — filtering and normalization
Nomalization is documented in [a different post](2024-08-26-normalization.html).