---
title: [3] TCC-GUI
author: Ryo Niwa
date: 2024-09-06
category: Packages
layout: post
---

#### Description
Ref: [TCC-GUI GitHub](https://github.com/swsoyee/TCC-GUI)

Ref: [TCC-GUI: a Shiny-based application for differential expression analysis of RNA-Seq count data](https://doi.org/10.1186/s13104-019-4179-2 )

> TCC-GUI is implemented in R and encapsulated in Shiny application. It contains all the major functionalities of TCC, including DE pipelines with robust normalization and simulation data generation under various conditions. It also contains (i) tools for exploratory analysis, including a useful score termed average silhouette that measures the degree of separation of compared groups, (ii) visualization tools such as volcano plot and heatmap with hierarchical clustering, and (iii) a reporting tool using R Markdown.

#### Docker commands
MacOS; Intel chip user

```bash=
https://github.com/geedrn/TCC-GUI-Docker
docker run \
  --rm -e DISABLE_AUTH=true \
  -p 8787:8787 \
  geedrn/tcc
```

MacOS; Apple Silicon user

```bash=
# https://github.com/geedrn/TCC-GUI-Docker_Apple
docker run \
  --rm -e DISABLE_AUTH=true \
  -p 8787:8787 \
  sayaka0710/tcc
```

#### Tutorial

A step-by-step tutorial is available in the GitHub repository:
[TCC-GUI Tutorial](https://github.com/swsoyee/TCC-GUI/blob/master/README.md)

#### Pros

- User-friendly graphical interface
- Implements the robust TCC method for differential expression analysis
- Provides various normalization methods (TMM, TbT, DEGES)
- Includes both MA-plot and Volcano plot visualizations
- Offers flexible sample grouping options
- Supports multi-group comparisons
- Easy to use
- Provides downloadable analysis reports (They generate a lab note for you)

#### Cons

- More focused on differential expression analysis, with less emphasis on downstream pathway analysis compared to some other tools
- May have limitations for very large datasets, depending on the user's computational resources
- No updates anymore
