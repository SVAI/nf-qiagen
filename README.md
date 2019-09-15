![logo!](/images/logo2.png "Logo")
## Team QIAGEN

# Inferring regulators and pathways involved in NF1 and NF2 tumors originating from Schwann cells using gene expression data

## Abstract

* Neurofibromatosis Type 1 (NF1) and Neurofibromatosis Type 2 (NF2) present as specific tumor types arising from Schwann cells. Using RNA-Seq data to perform a differential expression analysis we identified signaling pathways and upstream regulators enriched for specific tumor types.

* Using this information we then further developed tumor-specific gene/pathway networks to prioritize potentially significant biology.

* We then mapped the significantly activated upstream regulators to drug-target data to identify compounds that may have tumor-specific activity in these diseases.

* This work provides potential insight into the biology of specific NF1 and NF2 tumor types, prioritizes novel drug targets for further development and establishes an analytic that can be applied to further unravel the biology of other tumor types arising from different cells of origin in NF1 and NF2 patients.

## Introduction

Tumor development in NF1 and NF2 patients can take a number of different clinical courses based on the cell of origin (COO) for the tumor for example:
* Plexiform Neurofibroma (PNF), Cutaneous Neurofibroma (CNF), Malignant Peripheral Nerve Sheath Tumor (MPNST) and Schwanoma arising from Schwann cells in the peripheral nervous system (PNS)
* Glioma and Meningioma arising from the glial precursors in the central nervous system (CNS)

Due to the different COO for these tumors, the underlying biology is likely to be different. This makes therapeutic compound discovery to effectively target these tumors exceptionally difficult.

A better understanding of the biology of the different tumor types will lead to better approaches for identifying rational and effective treatment options. 

## Methods

### Data
We use RNA-Seq data provided by the organizers excluding the 48 new samples that were added on 09/13/19. In addition we also used two independent sets of RNA-Seq data obtained from normal Schwann cells (SRP212780 and SRP094118).

### Data processing and visualization
Data from all 3 resources were merged, omitting genes that were not present in all samples. The final data set contained 15,484 genes. RNA-Seq counts $K_{ij}$ were normalized, i.e. multiplied by a sample-specific factor $s_j$ to account for differences in read depths, using the median-of-ratios method:
\\[s_j=\mbox{median}_{i:K_i^R\neq 0}\frac{K_{ij}}{K_i^R}\;\;\; \mbox{where} \;\;\;K_i^R=\left(\prod_{j=1}^mK_{ij}\right)^{1/m}\\]
Counts where subsequently log2-transformed (after adding a constant of 0.1 in order to handle zero counts). We then performed standard Principal Componant Analysis (PCA) retaining only the 10 top components as input into t-Distributed Stochastic Neighbor Embedding (t-SNE) (default parameter settings).

### Differential gene expression analysis
Differential expression analysis between selected clusters of samples (tumor vs. normal) was performed using DESeq2. 

### Ingenuity Knowledge Base
The Ingenuty Knowledge Base (IKB) (QIAGEN) is a large, structured collection of curated findings from the biomedical literature. IKB content is represented as a network with nodes (genes, drugs and other molecules, biological functions, diseases, and pathways) and edges (representing prior experimental observations).

### Upstream Regulator Analysis
Upstream Regulator Analysis (URA) [Krämer et al. Bioinformatics. 2014 Feb 15;30(4):523-30.  PMID: 24336805] based on the IKB is used to infer activation or inhibition of regulators potentially causing observed gene expression changes.

![upreg!](/images/upreg.png "Upstream Regulator example")

### Machine learning-augmented Pathway Analysis
Machine Learning-augmented Pathway Analysis (MLPA) is used to infer weighted and signed pathway-gene associations. Its method is based on content-driven vector space embedding of genes, with gene feature vectors being used for subsequent training for pathway prediction. 

### Software availability and reproducibility
PCA, t-SNE, as well as data preprocessing was performed in a jupyter notebook running Python 2.7 with libraries pandas, sklearn, numpy and matplotlib. PCA and t-SNE was also run independently using OmicSoft Array Studio (QIAGEN) with similar results. DESeq2 is publicly available (R) but we used it as part of a pipeline in OmicSoft Array Studio. URA and access to the IKB is commercially available in Ingenuity Pathway Analysis (IPA) (QIAGEN). MLPA is in active development and has not yet been made publicly available. The jupyter notebook and all necessary input data is being provided as a gzipped tar bundle on github.

## Results

Our approach involved the following steps:
1. Cluster RNA-Seq expression data using PCA and t-SNE
2. Identify the biology that differentiates the tumor types
3. Create tumor type specific networks to visualize the differences
4. Identify drugs that target molecules in networks

### Step 1: Cluster RNA-Seq expression data using PCA and t-SNE

Initially, the combination of RNA-Seq expression data and two sources of normal Schwann cells was clustered using PCA and t-SNE.
![first tsne!](/images/tsne1-3.png "Initial t-SNE plot")
This first attempt highlighted a few issues:
* Some specimens separate into clear tumor type clusters, but others do not.
* There is ambiguity around which samples represent true ‘normal’ tissue of origin.
* There is potential for significant separation to be based on batch effect or technical artificats.

We noted that the tumor types descended from different ancestor cells (http://oncotree.mskcc.org), which could lead to problems with comparing their data, so we choose to focus on tumors originating from Schwann cells.
![tumor type taxonomy!](/images/taxonomy3.png "Tumor type taxonomy")

After reducing to descendants of Schwann cells, all tumor types and normal cells separate into distinct clusters.
![second tsne!](/images/tsne2-3.png "t-SNE of Schwann-decended tumor types")
Note that some types appear to subdivide further, so for our purposes, we split MPNST into two sub-groups.
Also, both sets of normal Schwann cells clustered together, which gives confidence that the clustering is based on real biology rather than just experimental methods.

### Step 2: Identify the biology that differentiates the tumor types

Five differential expression datasets were created, each of which compared normal Schwann cells to one of the tumor types, such as the following compared against the MPNST1 cluster:
![volcano!](/images/volcano.png "MPNST1 vs. normal Schwann")

Analysis of these datasets in IPA shows significant pathway and regulator differentiation between NF1 and NF2 tumors, but NF1 types appear relatively similar.
![5 tumor comparison!](/images/nf1-nf2_comparison.png "Pathway and regulator comparison across tummor types")

### >>> need image of entire heatmap
### >>> need exported spreadsheet

To further differentiate between NF1 types, we created three more differential expression datasets matching cutaneous nf against mpnst1, mpnst2, and neurofibroma each.
![3 tumor comparison!](/images/nf1_comparison.png "Pathway and regulator comparison across NF1 tummor types")
Now differences between the NF1 types appear.

### >>> need image of entire heatmap
### >>> need exported spreadsheet

### Step 3: Create tumor type specific networks to visualize the differences

MLPA was then used to generate tumor-context networks inferred from content.  Upstream regulators are connected to pathways for different tumors, and the resulting networks depict the differences between the tumor types.
![networks!](/images/networks.png "Comparison of MPNST1 and Schwannoma")
Signaling through these pathways potentially explains gene expression changes.

### >>> Links to all tumor type networks

### Step 4: Identify drugs that target molecules in networks

By combining the regulator results above with the Harmonized Drug Screening Data, drug targets can be matched with tumors and their effect can be predicted.
![drugs!](/images/drugs.png "Sample of targeted regulators per tumor")
The table above shows significant upstream regulators identified in different tumor types that are also targets in available drug screening data.
* All upstream regulators are predicted to be activating except those shown in parentheses
* Genes in bold are known to function in regulation of chromatin
* Coloring is to highlight tumor type specificity of the upstream regulator

SMARCA4 is a particularly interesting target for NF1.

## Conclusion/Discussion: 

* NF1 and NF2 are clearly differentiated.
* This approach can discriminate between tumor types by identifying drivers and signaling cascades.
* Content-driven Machine Learning can generate tumor-specific networks involving inferred gene-pathway associations.
* This approach identified potential therapeutic targets, including the following SMARCA4 hypothesis:
### SMARCA4 could be a potential drug target for NF1
SMARCA4, commonly thought of as a tumor suppressor, is emerging as a potential driver of tumorigenesis.  The gene has the potential to drive CTNNB1, which is another NF1 upstream regulator in the results above.  Compounds that target SMARCA4 are already available, so in this context, SMARCA4 is a potential drug target.
![smarca4!](/images/smarca4.png "SMARCA4")

### Additional Questions:
#### 1. What additional data would you like to have?
* Data from uniform sources
* Counts at transcript level
* More samples of normal tissue data
* Single cell data

#### 2. What are the next rational steps?
* Perform same analysis on glioma tumor types by comparing to their origin cells
* Compare proposed networks to additional known research
* Consider suggested drugs, such as those targeting SMARCA4

#### 3. What additional tools or pipelines will be needed for those steps?
* Normal tissue data for glioma tumor types
* Techniques such as mean-variants modeling (e.g. voom) could be used to compare against DESeq2
* Time :-)

#### 4. What skills would additional collaborators ideally have?
* Experts in NF

## Reproduction:

[Duck Duck Go](https://duckduckgo.com).

[NF1](/resources/nf1-nf2_comparison.png "Pathway and regulator comparison across tummor types")

