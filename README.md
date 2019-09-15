# nf-qiagen

# GoodDocData -- A Template for Simple and Clear Documentation of Hackathon Analyses!

*adapted from [NCBI-Hackathons/GoodDoc](https://github.com/NCBI-Hackathons/GoodDoc) with some tweaks for analysis-driven projects*

*instructions in italics can be deleted as sections are filled in*

*most fields are optional, Conclusion and Important Resources are required*

## Please cite our work -- here is the ICMJE Standard Citation:

### ...and a link to the DOI: *You can make a free DOI with zenodo, synapse, figshare, or other resources <link>*

## Awesome Logo *(if applicable)*

## Website *(if applicable)*

## Abstract

Using the RNASeq data, we differentiated between the tumor types that descend from Schwann cells and identified drugs that target those differences.

The following steps were followed:
1. Cluster RNASeq expression data using PCA and t-SNE
2. Identify the biology that differentiates the tumor types
3. Create a network for each type, emphasizing the differences
4. Identify drugs that target key molecules in the tumor types

## Introduction *: What's the problem? Why should we solve it?*

Seems like we could skip this

## Methods *: How did we go about solving it?*

### Step 1: Cluster RNASeq expression data using PCA and t-SNE

We started with the RNASeq data provided in the Harmonized Genomics Dataset section of the Hackathon site. The data is a union of results from multiple different studies, so the data needed to be normalized.

*insert lines/link about standardizing the data*

This resulted in the following t-SNE plot:

## Results *: What did we observe? Figures are great!*

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

