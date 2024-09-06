---
title: [4] RNASeqChef
author: Ryo Niwa
date: 2024-09-06
category: Packages
layout: post
---

### Description
Ref: [Github](https://github.com/Kan-E/RNAseqChef/wiki)

Ref: [A web-based integrative transcriptome analysis, RNAseqChef, uncovers the cell/tissue type-dependent action of sulforaphane](https://doi.org/10.1016/j.jbc.2023.104810)

> RNAseqChef, RNA-seq data controller highlighting gene expression features, a web-based platform of systematic transcriptome analysis which can automatically detect, integrate, and visualize the differentially expressed genes and their biological function without bioinformatics skills. Furthermore, Users can analyze not only a single dataset but also integrate and evaluate multiple datasets.

### Docker commands

```bash=
docker run --rm -p 3838:3838 omicschef/rnaseqchef:latest
```

JPN demo: [YouTube](https://www.youtube.com/watch?v=W4XJc1WAcMU)

### Pros

- Ongoing maintenance
- Great visualization in pair-wise or 3 conditions DEG
- Actions are light
- Can manage promoter motif analysis
- TogoTV is available in Japanese

### Cons

- Difficulty in multi DEGs
- Less citations (Because the tool is new)
- Only Japanese movie manual available (Their wiki has sufficient info for English speakers)