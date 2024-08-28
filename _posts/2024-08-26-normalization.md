---
title: How can I normalize RNA-Seq count matrix?
author: Ryo Niwa
date: 2024-08-26
category: RNA-Seq
layout: post
mermaid: true
---

> ##### Aim for this page
> Understand methods of normalization in RNA-Seq
{: .block-tip }

## Quick answer of this page: Use TPM first

Before discussing this topic, this [QA](https://bioinformatics.ccr.cancer.gov/btep/questions/what-is-the-difference-between-rpkm-fpkm-and-tpm) is must-read! 

RPKM and FPKM are virtually the same concept. RPKM is basically for single-end sequencing and FPKM is for pair-end sequencing. 
> With paired-end RNA-seq, two reads can correspond to a single fragment, or, if one read in the pair did not map, one read can correspond to a single fragment. The only difference between RPKM and FPKM is that FPKM takes into account that two reads can map to one fragment (and so it doesn’t count this fragment twice).

For RPKM (Reads Per Kilobase Million):

$$\text{RPKM} = \frac{\text{Number of reads mapped to a gene}}{\text{Total reads in sample} \times 10^{-6}} \times \frac{10^3}{\text{Length of gene in bp}}$$

For FPKM (Fragments Per Kilobase Million):

$$\text{FPKM} = \frac{\text{Number of fragments mapped to a gene}}{\text{Total fragments in sample} \times 10^{-6}} \times \frac{10^3}{\text{Length of gene in bp}}$$

For TPM, there are two steps:

Calculate RPK (Reads Per Kilobase):

$$\text{RPK} = \frac{\text{Number of reads mapped to a gene}}{\text{Length of gene in kb}}$$

Calculate TPM (Transcripts Per Kilobase Million):

$$\text{TPM} = \frac{\text{RPK for a gene} \times 10^6}{\text{Sum of all RPK values in the sample}}$$

> when calculating TPM, the only difference is that you normalize for gene length first, and then normalize for sequencing depth second. However, the effects of this difference are quite profound. When you use TPM, the sum of all TPMs in each sample are the same. This makes it easier to compare the proportion of reads that mapped to a gene in each sample. In contrast, with RPKM and FPKM, the sum of the normalized reads in each sample may be different, and this makes it harder to compare samples directly.

### Examples and details

Let's try some examples from this [blog](https://bi.biopapyrus.jp/rnaseq/analysis/normalizaiton/fpkm.html). 

Example table: 

| length | 1000 bp | 1200 bp | 800 bp | 500 bp | 2000 bp |
|----------|---------|---------|--------|--------|---------|
| sample A (count) | 20 | 30 | 20 | 50 | 150 |
| sample B (count) | 100 | 60 | 140 | 120 | 180 |

Results (computed by claude):

| Transcript Length | 1000 bp | 1200 bp | 800 bp | 500 bp | 2000 bp | Total |
|-------------------|---------|---------|--------|--------|---------|-------|
| Sample A (Read Count) | 20 | 30 | 20 | 50 | 150 | 270 |
| FPKM (A) | 74,074 | 92,593 | 92,593 | 370,370 | 277,778 | 907,408 |
| TPM (A) | 81,633 | 102,041 | 102,041 | 408,163 | 306,122 | 1,000,000 |
| Sample B (Read Count) | 100 | 60 | 140 | 120 | 180 | 600 |
| FPKM (B) | 166,667 | 83,333 | 291,667 | 400,000 | 150,000 | 1,091,667 |
| TPM (B) | 152,672 | 76,336 | 267,176 | 366,412 | 137,404 | 1,000,000 |

### Why are FPKM and TPM different? 

Wagner, G.P., Kin, K. & Lynch, V.J. Measurement of mRNA abundance using RNA-seq data: RPKM measure is inconsistent among samples. Theory Biosci. 131, 281–285 (2012). [https://doi.org/10.1007/s12064-012-0162-3](https://doi.org/10.1007/s12064-012-0162-3)

> The reason for the inconsistency of RPKM across samples arises from the normalization by the total number of reads. While rmc as well as qPCR results are ratios of transcript concentrations, the RPKM normalizes a proxy for transcript number by

$$ \frac{r_g \cdot 10^3}{l_g \cdot \frac{R}{10^6}} $$

> the number of sequencing reads in millions, 

$$\frac{R}{10^6}$$ 

> The latter, however, is not a measure of total transcript number. The relationship between $$R$$ and the total number of transcripts sampled depends on the size distribution of RNA transcripts, which can differ between samples. In a sample with, on average, longer transcripts the same number of reads represents fewer transcripts.

While TPM is essentially the ratio of each gene's RPK to the total RPK, RPKM (FPKM) can be considered as the ratio of each gene's RPK to the total number of reads. When longer genes have more reads, the overall RPK effectively becomes smaller, resulting in a discrepancy in the total values. Also please note that when you perform DEG (differentally expressed gene) analysis, you need to put different assumptions. While TPM is useful to compare gene count internally or externally, previous studies suggested DEG analysis require other statistical models. 