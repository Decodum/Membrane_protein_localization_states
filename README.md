# Membrane Protein Localization States from Human Protein Atlas Image Embeddings

## Overview

Plasma membrane proteins are often treated as a single subcellular localization class.
However, proteins associated with the plasma membrane participate in very different biological processes, including receptor signaling, adhesion, membrane trafficking, epithelial polarity, cytoskeletal coupling, and cortical contractility.

This project explores whether proteins annotated as **Plasma membrane** in the Human Protein Atlas form a homogeneous image-derived group, or whether they separate into distinct latent localization patterns based on microscopy-derived embedding features.

The analysis is intended as an exploratory bioinformatics project: it does not claim to define new experimentally validated membrane compartments, but aims to identify biologically interpretable structure in existing large-scale imaging data.

## Research question

Do plasma membrane-associated proteins form a single homogeneous localization class, or can image-derived embeddings reveal reproducible subgroups corresponding to different membrane-related biological programs?

## Data source

Data were obtained from the **Human Protein Atlas — Subcellular Section**:

* `subcellular_location.tsv`
* `subcell_image_umap_features.tsv`

The analysis focuses on proteins with plasma membrane-associated localization annotations and uses image-derived embedding features from HPA microscopy data.

Human Protein Atlas:
https://www.proteinatlas.org/

## Method summary

The pipeline performs the following steps:

1. Load Human Protein Atlas subcellular localization annotations.
2. Load image-derived embedding features.
3. Merge localization metadata with image feature data.
4. Select observations associated with **Plasma membrane** localization.
5. Standardize numeric image-derived features.
6. Apply PCA dimensionality reduction.
7. Cluster plasma membrane-associated observations using KMeans.
8. Evaluate cluster robustness using bootstrap Adjusted Rand Index.
9. Summarize clusters at both observation and gene levels.
10. Interpret clusters using:


## Main result

The analysis suggests that plasma membrane-associated proteins are not represented by a single uniform image-derived pattern.
Instead, the embedding space contains several reproducible but moderately separated clusters that correspond to biologically interpretable membrane-associated programs.

The strongest signals are observed for clusters associated with:

* cortical membrane scaffolding,
* junction and polarity organization,
* focal adhesion and motility,
* contractile cortex coupling,
* vesicle/receptor-associated membrane patterns,
* broad signaling and remodeling programs.

These clusters should be interpreted as **latent image-derived localization regimes**, not as definitive experimentally validated biological states.

## Validation 

Several tests were performed to assess whether the observed structure is meaningful and not purely technical:

* clustering stability was evaluated using bootstrap Adjusted Rand Index;
* gene-level summaries were used to reduce observation-level redundancy;
* antibody distribution was inspected across clusters;
* biological coherence was assessed using known marker genes and functional annotation patterns.

In the current analysis, the mean bootstrap ARI is approximately **0.89**, suggesting that the clustering structure is reproducible under resampling.
However, internal cluster separation is modest, so the results should be treated as hypothesis-generating rather than definitive.

## Examples of states

| Cluster | Proposed interpretation                                     |
| ------: | ----------------------------------------------------------- |
|       1 | Cortical / junctional surface membrane-associated state     |
|       5 | Junction and polarity-associated membrane state             |
|       6 | Focal adhesion / motility-associated membrane state         |
|       3 | Contractile cortex-associated membrane state                |
|       0 | Vesicle / receptor / trafficking-associated membrane state  |
|       4 | Broad signaling and remodeling-associated membrane state    |
|       2 | Mixed nuclear / plasma membrane-associated annotation state |

The cluster names are descriptive labels assigned after inspecting enriched localizations, representative genes, and functional patterns. They are not intended to represent formally established biological compartments.

## Biological interpretation

Several clusters contain biologically coherent marker genes.

For example, one cluster is enriched for cortical membrane scaffolding and junction-associated proteins, including genes related to membrane–cytoskeleton coupling. Another cluster contains proteins associated with actomyosin organization and contractile cortical structures. A smaller cluster shows patterns consistent with focal adhesion and motility-related membrane localization.

These findings are consistent with the idea that the plasma membrane annotation contains multiple functional and spatial subprograms rather than a single homogeneous category.

## Important limitations

This project is exploratory and has several limitations:

1. **Clustering does not prove biological state identity.**
   The detected groups are image-derived clusters and require experimental validation before being interpreted as true biological states.

2. **Cluster separation is moderate.**
   Although bootstrap stability is high, internal separation metrics suggest that some clusters overlap substantially.

3. **HPA annotations are observation-dependent.**
   The same gene may appear in different contexts depending on antibody, cell line, staining quality, and image-derived features.

4. **Cell line and antibody effects may influence the embedding space.**
   Basic checks were performed, but a more rigorous technical-bias analysis would be needed for publication-level claims.


This project demonstrates how large-scale imaging resources can be used not only for supervised localization classification, but also for unsupervised discovery of structure within broad localization categories.


The project is designed as a portfolio-level demonstration of computational biology reasoning using real public data.

## Possible Future Improvements

* perform clustering only on raw image embedding features, excluding precomputed UMAP coordinates;
* repeat the analysis at gene level as the primary clustering unit;
* use a custom plasma membrane-associated gene background for functional enrichment;
* compare KMeans with Leiden, HDBSCAN, or Gaussian mixture models;
* validate selected clusters against external protein interaction or pathway databases;
* inspect representative microscopy images for each cluster;


## Requirements

The analysis uses Python and common scientific computing libraries, including:

* pandas
* numpy
* scikit-learn
* scipy
* matplotlib
* seaborn
* gprofiler-official

