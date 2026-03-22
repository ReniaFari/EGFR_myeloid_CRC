# EGFR Deletion in Myeloid Cells Reprograms the Immunosuppressive Landscape of Colorectal Cancer

Updated 2026-03-22

This repository contains R Markdown analyses for a manuscript focused on how EGFR positive myeloid cells promote an immunosuppressive environment in colorectal cancer (CRC).

The analyses span single-cell RNAseq, proteomics, and patient cohorts with survival information.

These analyses center on CRC tumor microenvironment biology across human cohorts and mouse models. Key outputs include:

- Cell-type annotation and immune profiling from scRNA-seq data.
- Differential expression and pathway analyses across bulk RNA-seq and proteomics.
- Cross-omics integration with clinical association and survival modeling.

## Repository hierarchy

```text
EGFR_myeloid_CRC/
├── README.md
└── scripts/
    ├── 01_scrna_mouse/
    │   ├── scRNA_Analysis_Renia.Rmd
    │   ├── limma_GSVA.Rmd
    │   ├── Cell_Commun_iTalk.Rmd
    │   └── Pathway_Analysis_PROGENy.Rmd
    ├── 02_scrna_human/
    │   └── Lee_Dataset_Analysis.Rmd
    ├── 03_proteomics/
    │   └── Comparison_Proteomics.Rmd
    └── 04_survival/
        └── Survival.Rmd
```

## Repository contents

- `scripts/01_scrna_mouse/scRNA_Analysis_Renia.Rmd`  
  Main scRNA-seq analysis workflow for the mouse CRC model using Seurat: QC, normalization, dimensional reduction, clustering, and cell-type annotation.
- `scripts/01_scrna_mouse/limma_GSVA.Rmd`  
  Differential expression and gene-set variation analysis (GSVA) on scRNAseq cell clusters using limma contrasts.
- `scripts/01_scrna_mouse/Cell_Commun_iTalk.Rmd`  
  Cell-cell communication analysis using iTALK with mouse-to-human orthology mapping.
- `scripts/01_scrna_mouse/Pathway_Analysis_PROGENy.Rmd`  
  PROGENy-based pathway activity scoring on mouse scRNA-seq data.
- `scripts/02_scrna_human/Lee_Dataset_Analysis.Rmd`  
  scRNA-seq analysis of the human CRC Lee dataset: alignment, integration, clustering, and immune profiling.
- `scripts/03_proteomics/Comparison_Proteomics.Rmd`  
  Proteomics data processing and differential protein expression comparisons across conditions.
- `scripts/04_survival/Survival.Rmd`  
  Survival modeling and GSVA-based signature validation on the human CRC cohort GSE39582.

## Analysis workflow

```mermaid
graph TD
    %% Node Definitions
    Start([Cell Sorting])

    %% sc-RNA Path
    scRNA[10x sc-RNA sequencing]
    Align[Alignment Cell ranger]
    FiltRNA[Filtering according to cell size and mitochondrial gene expression]
    Norm[Normalize data]
    Integ[Sample integration]
    Scale[Scaling of data and cell cycle regression]
    PCA[PCA UMAP]
    Clust[Manual cluster identification and/or subclustering]

    %% sc-RNA Downstream Analysis
    Path[Pathway activation analysis PROGENY]
    GSEA[Gene set enrichment analysis]
    DGEA[Differential gene expression analysis]
    CIA[Cell Interaction Analysis]

    %% Proteomics Path
    Prot[Proteomics]
    Raw[Raw data processing Spectonaut 17.3]
    Ref[Reference spectra Pulsar, Uniprot]
    FiltProt[Filtering]
    Quant[Protein quantification]
    DPEA[Differential protein expression analysis]

    %% Connections
    Start --> scRNA
    Start --> Prot

    scRNA --> Align --> FiltRNA --> Norm --> Integ --> Scale --> PCA --> Clust

    Clust --> Path
    Clust --> GSEA
    Clust --> DGEA
    Clust --> CIA

    Prot --> Raw --> Ref --> FiltProt --> Quant --> DPEA

    %% Styling to match the original image
    style Start fill:#b19cd9,stroke:#333,stroke-width:1px

    style scRNA fill:#fff,stroke:#333,stroke-width:1px
    style Prot fill:#fff,stroke:#333,stroke-width:1px

    style Align fill:#4a76c5,color:#fff
    style FiltRNA fill:#4a76c5,color:#fff
    style Norm fill:#4a76c5,color:#fff
    style Integ fill:#4a76c5,color:#fff
    style Scale fill:#4a76c5,color:#fff
    style PCA fill:#4a76c5,color:#fff
    style Clust fill:#4a76c5,color:#fff

    style Raw fill:#4a76c5,color:#fff
    style Ref fill:#4a76c5,color:#fff
    style FiltProt fill:#4a76c5,color:#fff
    style Quant fill:#4a76c5,color:#fff

    style Path fill:#99d9be,color:#333
    style GSEA fill:#99d9be,color:#333
    style DGEA fill:#99d9be,color:#333
    style CIA fill:#99d9be,color:#333
    style DPEA fill:#99d9be,color:#333
```
