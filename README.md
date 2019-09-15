# nf-qiagen

# GoodDocData -- A Template for Simple and Clear Documentation of Hackathon Analyses!

*adapted from [NCBI-Hackathons/GoodDoc](https://github.com/NCBI-Hackathons/GoodDoc) with some tweaks for analysis-driven projects*

*instructions in italics can be deleted as sections are filled in*

*most fields are optional, Conclusion and Important Resources are required*

## Please cite our work -- here is the ICMJE Standard Citation:

### ...and a link to the DOI: *You can make a free DOI with zenodo, synapse, figshare, or other resources <link>*

## Awesome Logo *(if applicable)*

## Website *(if applicable)*

# Inferring regulators and pathways implicated in NF1 and NF2 tumors originating from Schwann cells using gene expression data

## Abstract

* NF1 and NF2 present as specific tumor types arising from Schwann cells. Using RNA-seq data to perform a differential expression analysis we identified canonical pathways and upstream regulators enriched for specific tumor subtypes.

* Using this information we then further developed disease-specific gene/pathway networks to prioritize potentially significant biology.

* We then mapped the significantly activated upstream regulators to drug-target data to identify compounds that may have tumor-specific activity in these diseases.

* This work provides potential insight into the biology of specific NF1 and NF2 tumor subtypes, prioritizes novel drug targets for further development and establishes an analytical that can be applied to further deconvolve the biology of other tumor subtypes arising from different cells of origin in NF1 and NF2 patients.

## Introduction

Tumor development in NF1 and NF2 patients can take a number of different courses based on the cell of origin (COO) for the tumor for example:
* pNF, cNF, MPNST and Schwanoma arising from Schwann cells in the PNS
* Glioma and Menigioma arising from othe glial precursors in the CNS

Because of the different COO for these tumors the underlying biology is likely to be different. This makes therapeutic compound discovery to effectively target these tumors exceptionally difficult.

A better understanding of the biology of the different tumor subtype will lead to better approaches for identifying rational and effective treatment options. 

## Methods

### Data
We use RNAseq data provided by the organizers excluding the 48 new samples that were added on 09/13/19. In addition we also used two independent sets of RNAseq data obtained from normal Schwann cells (GSM3923266-8 and PRJNA355561).
### >>> can we link to this data or provide downloaded files?

### Data processing and visualization
Data from all 3 resources were merged, omitting genes that were not present in all samples. The final data set contained 15484 genes. RNAseq counts $K_{ij}$ were normalized, i.e. multiplied by a sample-specific factor $s_j$ to account for differences in read depths, using the median-of-ratios method:
$$s_j=\mbox{median}_{i:K_i^R\neq 0}\frac{K_{ij}}{K_i^R}\;\;\; \mbox{where} \;\;\;K_i^R=\left(\prod_{j=1}^mK_{ij}\right)^{1/m}$$
Counts where subsequently log2-transformed (after adding a constant of 0.1 in order to handle zero counts). We then performed standard Principal Componant Analysis (PCA) retaining only the 10 top components as input into t-Distributed Stochastic Neighbor Embedding (t-SNE) (default parameter settings).

### Differential gene expression analysis
Differential expression analysis between selected clusters of samples (tumor vs. normal) was performed using DESeq2. 

### Ingenuity Knowledge Base
The Ingenuty Knowledge Base (IKB) (QIAGEN) is a large, structured collection of curated findings from the biomedical literature. IKB content is represented as a network with nodes (genes, drugs and other molecules, biological functions, diseases, and pathways) and edges (representing prior experimental observations).

### Upstream Regulator Analysis
Upstream Regulator Analysis (URA) (CITATION) based on the IKB is used to infer activation or inhibition of regulators potentially causing observed gene expression changes.
### >>> cite paper
### >>> (COULD ADD SMALL DRAWING FROM OUR PAPER HERE)

### Machine learning-augmented Pathway Analysis
Machine learning-augmented Pathway Analysis (MLPA) is used to infer weighted and signed pathway-gene associations. Its method is based on content-driven vector space embedding of genes, with gene feature vectors being used for subsequent training for pathway prediction. 

### Software availability and reproducibility
PCA, t-SNE, as well as data preprocessing was performed in a jupyter notebook running Python 2.7 with libraries pandas, sklearn, numpy and matplotlib. PCA and t-SNE was also run independently using Omicsoft ArrayStudio (QIAGEN) with similar results. DESseq2 is publicly available (R) but we used it as part of a pipeline in Omicsoft ArrayStudio. URA and access to the IKB is commercially available in Ingenuity Pathway Analysis (IPA) (QIAGEN). MLPA is in active development and has not yet been made publicly available. The jupyter notebook and all necessary input data is being provided as a gzipped tar bundle on github.

## Results

Our approach involved the following steps:
1. Cluster RNASeq expression data using PCA and t-SNE
2. Identify the biology that differentiates the tumor types
3. Create a network for each type, emphasizing the differences
4. Identify drugs that target molecules in networks

### Step 1: Cluster RNASeq expression data using PCA and t-SNE

Initially, the combination of RNASeq expression data and two sources of normal Schwann cells was clustered using PCA and t-SNE.
![first tsne!](/images/tsne1.png "Initial t-SNE plot")
This first attempt highlighted a few issues:
* Some specimens separate into clear tumor type clusters, but others do not.
* There is ambiguity around which samples represent true ‘normal’ tissue of origin.
* There is potential for significant separation to be based on batch effect or technical artificats.

We noted that the tumor types descended from different ancestor cells (http://oncotree.mskcc.org), which could lead to problems with comparing their data, so we choose to focus on tumors originating from Schwann Cells.
![tumor type taxonomy!](/images/taxonomy2.png "Tumor type taxonomy")
### >>> is it possible to provide a link to this specific image rather than just the site? If so, let's include

Since we will compare to normal Schwann cells, we chose to focus on only on those tumors descended from those cells.  After this decision, the resulting t-SNE suggested clear differences between the tumor types and the normal cells.
![second tsne!](/images/tsne2.png "t-SNE of Schwann-decended tumor types")
Note that some types appear to subdivide further, so for our purposes, we split MPNST into two sub-groups.
Also, both sets of normal Schwann cells clustered together, which gives confidence that the clustering is based on real biology rather than just experimental methods.

## Conclusion/Discussion: 

### Please make sure you address ALL of the following:

#### *1. What additional data would you like to have*

#### *2. What are the next rational steps?* 

#### *3. What additional tools or pipelines will be needed for those steps?*

#### *4. What skills would additional collaborators ideally have?*

## Reproduction: *How to reproduce the findings!*

### Docker

*The Docker image contains <R/jupyter> notebooks of all analyses and the dependencies to run them. *Be sure to note if you need any special credentials to access data for these analyses, **don't package restricted data** in your containers!*

Instructions for running the following notebooks: *be sure to adjust these instructions as necessary! check out https://github.com/Sage-Bionetworks/nf-hackathon-2019 for example containers and instructions*

1. `docker pull <your dockerhub repo>/<this container>` command to pull the image from the DockerHub
2. `docker run <your dockerhub repo>/<this container>` Run the docker image from the master shell script

### Important Resources *: primary data, github repository, Synapse project, dockerfile link etc.*

