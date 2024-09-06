---
title: 5-iDEP
author: Ryo Niwa
date: 2024-09-06
category: Packages
layout: post
---

### Description
Ref: [iDEP website](http://bioinformatics.sdstate.edu/idep/)

Ref: [iDEP: an integrated web application for differential expression and pathway analysis of RNA-Seq data.](https://doi.org/10.1186/s12859-018-2486-6)

> iDEP (integrated Differential Expression and Pathway analysis) seamlessly connects 63 R/Bioconductor packages, 2 web services, and comprehensive annotation and pathway databases for 220 plant and animal species. The workflow can be reproduced by downloading customized R code and related pathway files.

### Docker commands
```
# https://github.com/gexijin/idepGolem
# go to localhost:3838 once you run the command below
docker run --pull always -d --name idep -p 3838:3838 gexijin/idep:latest 
```

#### Tutorial

A comprehensive tutorial is available on YouTube: 
[iDEP installation tutorial](https://www.youtube.com/watch?v=u8Gdog4VAGc)
[iDEP analysis tutorial](https://www.youtube.com/watch?v=Hs5SamHHG9s)

#### Pros

- Comprehensive analysis pipeline from data pre-processing to pathway analysis
- Supports various types of gene IDs and multiple species
- Integrates multiple R/Bioconductor packages for robust analysis
- Provides interactive visualizations
- Regular updates and maintenance
- Cited more than 1000 times
- Has a sister tools called shinyGO

#### Cons

- A bit heavy and difficult to execute on my computer (16GB memory)
- May have limitations for extremely large-scale meta-analyses
- Since they have so many functions, learning takes a bit of time
