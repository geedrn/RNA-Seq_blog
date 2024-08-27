---
title: How you can obtain easy-to-handle RNA-Seq data from databases without bioinformatician?
author: Ryo Niwa
date: 2024-08-23
category: RNA-Seq
layout: post
---


> ##### Aim for this page
> Know what kind of databases in expression analysis are there and how you can use them
{: .block-tip }

### 1. What kind of database is available in expression analysis?

> You are very fortunate.

What NCBI-generated RNA-seq count files are available
Counts have been generated for all historical human RNA-seq runs submitted to GEO. For each GEO Series, the following files are generated:

Series RNA-seq raw counts matrix
Series RNA-seq raw counts matrices are tab-delimited text files that may be suitable for input for differential expression analysis tools like DESeq2, edgeR or limma voom. The first column in the matrix contains unique Gene IDs that match the Gene ID column in the accompanying Human gene annotation table (see below). Remaining columns contain raw counts for each GEO Sample in the Series.

Series RNA-seq normalized counts matrix
Series RNA-seq normalized counts matrices are tab-delimited text files that may be suitable input for qualitative analysis and visualizing gene expression abundance. The first column in the matrix contains unique Gene IDs that match the Gene ID column in the accompanying Human gene annotation table (see below). Remaining columns contain counts for each GEO Sample in the Series.

These counts are normalized according to sequencing depth and gene length.

The FPKM counts represent Fragments Per Kilobase Million (for paired-end sequencing data) or Reads Per Kilobase Million (single end). Note that file is named FPKM in both cases. The TPM counts represent Transcripts Per Kilobase Million.

For more information about normalized counts, see FPKM, RPKM and TPM, and be aware of misuses.