---
title: 4. What kind databases are available in RNA-Seq studies?
author: Ryo Niwa
date: 2024-08-23
category: RNA-Seq
layout: post
mermaid: true
---

> ##### Aim for this page
> Know what kind of databases in expression analysis are available
{: .block-tip }

## Quick answer of this page: Raw=SRA, Processed=GEO

I want you to recoginie two important databases, SRA and GEO. Typical differences of the 2 databases:

| Aspect | SRA (Sequence Read Archive) | GEO (Gene Expression Omnibus) |
|--------|-----------------------------|-----------------------------|
| Purpose | Raw sequence data repository | Functional genomics data repository |
| Data type | Raw sequencing data (fastq, bam) | Processed data, metadata, and raw data links |
| Scope | All sequencing platforms and applications | Primarily gene expression data, but includes other functional genomics data |
| Data size | Typically larger files (raw data) | Usually smaller files (processed data) |
| Search capability | Sequence-based searches | Expression and metadata-based searches |

SRA description: [https://www.ncbi.nlm.nih.gov/sra/docs/](https://www.ncbi.nlm.nih.gov/sra/docs/)

GEO description: [https://www.ncbi.nlm.nih.gov/geo/info/overview.html](https://www.ncbi.nlm.nih.gov/geo/info/overview.html)

### Databases are linked to each other

[GSE275240](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE275240) is our lab's previous paper's data accession ID. This GSE275240 is connected to another database called BioProject under [PRJDB15620](https://www.ncbi.nlm.nih.gov/bioproject/PRJDB15620). BioProject contains SRA Run as sequence data and BioSample to explain what each sequence data is derived from. Certainly. SRA 'Experiment' describes the sequencing library derived from a specific sample and the sequencing method used. Much of the publicly available information about the data is recorded in the Experiment. SRA 'Run' is an object that groups together data files that should be linked to an Experiment. It contains little descriptive information about the data itself. All data files listed in a Run are merged into an SRA file for archiving (and into fastq files for distribution).

### Database structure

This is an overall structure of SRA/BioSample/BioProject. The picture below is cited from [DDBJ](https://www.ddbj.nig.ac.jp/biosample/overview.html).

![SRA_structure](/assets/sra_object.png)

Since it does not contain GEO, I just added in a mermaid plot. BioProject is a database designed to organize research projects and their associated data. By citing the BioProject accession number, data can be grouped on a project-by-project basis. BioSample and GEO Sample (GSM) ultimately explains the identical information. 

```mermaid
graph TD
    subgraph BioProject["BioProject"]
        BP[BioProject PRJD]
    end

    subgraph BioSample["BioSample"]
        BS1[BioSample SAMD]
        BS2[BioSample SAMD]
        BS3[BioSample SAMD]
    end

    subgraph SRA["Sequence Read Archive"]
        E[Experiment SRX-DRX]
        E --> LL["Library layout"]
        E --> SP["Sequencing platform"]
        R1[Run SRR-DRR]
        R2[Run SRR-DRR]
        R3[Run SRR-DRR]
        SDF["Sequence data files fastq, BAM"]
        R1 -.-> SDF
        R2 -.-> SDF
        R3 -.-> SDF
    end

    subgraph GEO["Gene Expression Omnibus"]
        GSE[GEO Series GSE]
        GSM1[GEO Sample GSM]
        GSM2[GEO Sample GSM]
        GSM3[GEO Sample GSM]
        GSE --> GSM1
        GSE --> GSM2
        GSE --> GSM3
        GSM3 --> GD["Gene expression data"]
    end

    BP --> BS1
    BP --> BS2
    BP --> BS3
    BP --> E
    BP --> GSE

    GSM1 -.-> R1
    GSM2 -.-> R2
    GSM3 -.-> R3
    
    BS1 --> E
    BS2 --> E
    BS3 --> E

    E --> R1
    E --> R2
    E --> R3

    classDef bioproject fill:#e6ffe6,stroke:#333,stroke-width:2px;
    classDef biosample fill:#fff0e6,stroke:#333,stroke-width:2px;
    classDef sra fill:#e6e6ff,stroke:#333,stroke-width:2px;
    classDef geo fill:#ffe6e6,stroke:#333,stroke-width:2px;

    class BP,PD,G,Pub bioproject;
    class BS1,BS2,BS3,SD biosample;
    class E,LL,SP,R1,R2,R3,DF,SDF sra;
    class GSE,GSM1,GSM2,GSM3,GD geo;

    style BioProject fill:#e6ffe6,stroke:#333,stroke-width:4px;
    style BioSample fill:#fff0e6,stroke:#333,stroke-width:4px;
    style SRA fill:#e6e6ff,stroke:#333,stroke-width:4px;
    style GEO fill:#ffe6e6,stroke:#333,stroke-width:4px;
```

> ##### DRA/SRA differences?
> DRA (DDBJ Sequence Read Archive) is an archive of raw read sequences and maintained by DDBJ. 
> DRA (DDBJ Sequence Read Archive) is a member of the International Nucleotide Sequence Database Collaboration (INSDC) and is operated in international cooperation with NCBI SRA and EBI Sequence Read Archive (ERA). The data is mirrored (synchronized). If you can find the same dataset in SRA and DRA, downloading from DRA is geographically much faster.
{: .block-tip }