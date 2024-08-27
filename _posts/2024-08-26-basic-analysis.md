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

Must-read paper: [RNA sequencing: the teenage years](https://www.nature.com/articles/s41576-019-0150-2#Sec17)

### Phase 1 — alignment and assembly of sequencing reads
> After sequencing has been completed, the starting point for analysis is the data files, which contain base-called sequencing reads, usually in the form of FASTQ files111. The most common first step in processing these files is to map sequence reads to a known transcriptome (or annotated genome), converting each sequence read to one or more genomic coordinates. This process has traditionally been accomplished using distinct alignment tools, such as TopHat, STAR or HISAT, which rely on a reference genome. Because the sequenced cDNA is derived from RNA, which may span exon boundaries, these tools perform a spliced alignment allowing for gaps in the reads when compared to the reference genome (which contains introns as well as exons).

People typically call this step, alignment or mapping. Long story in short, mapping means: 

![SRA_structure](/assets/mapping.png)

