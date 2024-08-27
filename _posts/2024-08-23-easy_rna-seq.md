---
title: 20240823 count data from NCBI
author: Ryo Niwa
date: 2024-08-23
category: RNA-Seq
layout: post
---

> ##### Aim for this page
> Know NCBI's service: auto-generated RNA-seq count data
{: .block-tip }

## Quick answer of this page: Use NCBI generates RNA-seq count data

> You are very fortunate.

NCBI launched a new service to make [the count matrix of RNA-Seq](https://ncbiinsights.ncbi.nlm.nih.gov/2023/04/19/human-rna-seq-geo/?utm_source=ncbi_twitter&utm_medium=referral&utm_campaign=geo-human-rna-seq-20230419) available!

Count data generation occurs under [the following conditions](https://www.ncbi.nlm.nih.gov/geo/info/rnaseqcounts.html#raw):

```bash=
1. The sample is registered in the Sequence Read Archive (SRA)
2. The sample is registered in the Gene Expression Omnibus (GEO)
3. The sample is derived from either human or mouse
```

A count matrix is automatically generated approximately one week after sample registration.
For each GEO Series, two main types of files are generated, raw counts and normalized counts. 

### RNA-seq Raw Count Matrix:

| Aspect | Description |
|--------|-------------|
| Format | Tab-delimited text file |
| Purpose | Suitable for input into differential expression analysis tools like DESeq2, edgeR, or limma voom |
| Structure | - First column: Gene IDs (matching the Human gene annotation table)<br>- Remaining columns: Raw counts for each GEO Sample |


### RNA-seq Normalized Count Matrix:

| Aspect | Description |
|--------|-------------|
| Format | Tab-delimited text file |
| Purpose | Suitable for qualitative analysis and visualization of gene expression abundance |
| Structure | - First column: Gene IDs (matching the Human gene annotation table)<br>- Remaining columns: Normalized counts for each GEO Sample |
| Normalization | FPKM (RPKM) and TPM |


### How the analysis works?

NCBI uses HISAT2 and featureCounts. Details are [here](https://www.ncbi.nlm.nih.gov/geo/info/rnaseqcounts.html#how).

> Briefly, SRA runs where the organism is Homo sapiens and type is Transcriptomic are aligned to genome assembly GCA_000001405.15 using HISAT2. Runs that pass a 50% alignment rate are further processed with Subread featureCounts which outputs a raw count file for each run. For Human data, the Homo sapiens Annotation Release 109.20190905 was used for gene annotation. GEO further processes these SRR raw count files into GEO Series raw counts matrices. Data derived from single cell samples are skipped. In cases where there is more than one SRA run per GEO Sample, the raw counts are summed. Values in the raw count matrices are rounded so that they are compatible input for common differential expression analysis software. Using the raw counts as input, GEO then computes FPKM(RPKM) and TPM normalized values.

Please note that our in-house RNA-Seq pipeline provides the same format of results. You need to handle these data by yourself for data exploration anyway. 