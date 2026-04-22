# Membrane protein localization states from Human Protein Atlas image embeddings

## Overview

Plasma membrane proteins are commonly treated as a single localization class.  
However, membrane-associated proteins perform highly diverse roles including signaling, adhesion, trafficking, polarity control, and cytoskeletal coupling.

In this project, I used single-cell image embeddings from the Human Protein Atlas (HPA) to test whether proteins annotated as **Plasma membrane** form a homogeneous group or split into distinct latent subcellular states.

## Main Finding

Plasma membrane proteins do **not** form a single cluster.

Instead, they separate into multiple reproducible image-derived states corresponding to:

- cortical membrane scaffolding
- junctional polarity programs
- focal adhesion / motility states
- receptor-endocytic programs
- signaling / remodeling states
- contractile cortex states
- endomembrane-associated membrane states

## Data Source

Human Protein Atlas (Subcellular Section)

- subcellular_location.tsv
- subcell_image_umap_features.tsv

## Methods

1. Merged localization annotations with image embedding features
2. Selected proteins associated with Plasma membrane
3. Standardized numeric features
4. PCA dimensionality reduction (30 components)
5. KMeans clustering
6. Robustness validation using bootstrap ARI
7. Biological interpretation using localization enrichment and marker genes

## Key Results

- Stable latent structure detected
- Mean bootstrap ARI: **0.89**
- Low antibody bias
- Moderate cell-line diversity across clusters
- Strong biological coherence of discovered states

## Example Discovered States

| Cluster | Interpretation |
|--------|----------------|
| 1 | Cortical surface membrane |
| 5 | Junctional polarity membrane |
| 6 | Focal adhesion / motility membrane |
| 3 | Contractile cortex membrane |
| 0 | Receptor-endocytic membrane |
| 4 | Signaling-remodeling membrane |


