---
title: 2-Public data analysis tips
author: Ryo Niwa
date: 2024-09-06
category: Tips
layout: post
---

### Performing Public data Analysis Using NCBI GEO

#### 1. Data Collection

- **Utilizing Public Databases**: Retrieve data from GEO (Gene Expression Omnibus)
- **Setting Dataset Selection Criteria**: Determine conditions (e.g., tissue type, disease state, technical variables) based on research objectives. Generally, it's better to unify comparable factors. As RNA-Seq data tends to be variable, try to standardize aspects like species or cell lines when possible.
- **Leveraging AI Tools**: Tools like ResearchRabbit and ConnectedPapers are extremely useful for literature discovery and connecting related studies.

#### 2. Data Preprocessing

- **Verifying TSV Files**: Check TSV files downloaded from GEO and extract necessary metadata. As of 2023, human RNA-Seq data submitted to GEO is standardized and analyzed by NCBI using consistent methods. Count data is typically uploaded within a week of registration.

References:
1. https://www.ncbi.nlm.nih.gov/geo/info/rnaseqcounts.html
2. https://academic.oup.com/nar/article/52/D1/D138/7337616

> Note: For SRA execution data of human (Homo sapiens) transcriptomics, HISAT2 is used for alignment to the genome assembly GCA_000001405.15. Execution data achieving over 50% alignment rate is further processed with Subread's featureCounts to generate raw count files for each run.
>
> Values in the raw count matrix are rounded to serve as suitable input for common differential expression analysis software. GEO calculates FPKM (RPKM) and TPM normalized values using the raw counts as input.

#### 3. Dataset Integration

- **Using R or Similar Tools**: Combine datasets using R or other programming tools. Excel can also be used for simpler integrations. While correcting for batch effects in RNA-Seq data is sometimes necessary, it's often not required for drawing general conclusions.

- **Basic Quality Control**: Use tools like Degust or iDEP to get an overview and ensure the analyzed samples are credible. These tools can also be used to examine DEGs (Differentially Expressed Genes) if needed. GEO2R is another option for basic data inspection. Generally, as long as the overall count values don't deviate significantly, the data should be usable.

Reference: https://togotv.dbcls.jp/en/20230328.html

#### 4. Data Analysis

- **Normalization**: Apply appropriate normalization methods (e.g., TPM, FPKM) to account for differences in sequencing depth and gene length when you compare the value quickly.
- **Batch Effect Correction**: If necessary, use methods like ComBat or RUVSeq to correct for batch effects between different studies (But you have to start from fastq then).
- **Differential Expression Analysis**: Employ tools like DESeq2, edgeR to identify differentially expressed genes across conditions or studies. Use the raw counts.

You may set certain threshold in case of the meta-analysis to define DEGs here (mostly a simple mathematics). Or you can use stats to combine the p-value with a package like metaRNASeq (https://pubmed.ncbi.nlm.nih.gov/24678608/).

### 5. Functional Analysis

- **Gene Ontology Enrichment**: Perform GO enrichment analysis to identify overrepresented biological processes, molecular functions, or cellular components.
- **Pathway Analysis**: Use tools like KEGG or Reactome to identify significantly enriched pathways.
- **Gene Set Enrichment Analysis (GSEA)**: Conduct GSEA to identify sets of genes that show statistically significant differences between biological states.

### 6. Visualization and Interpretation

- **Heatmaps**: Create heatmaps to visualize expression patterns across samples and genes.
- **Principal Component Analysis (PCA)**: Use PCA to visualize overall similarities and differences between samples.
- **Network Analysis**: Construct gene co-expression networks to identify modules of genes with similar expression patterns.
