# Differential Expression Analysis Using both RNAseq and ChIPseq

Manan Chopra, Archishma Kavalipati, Louisa Black

<p align="center">
  <img src="imgs/diff_expression.png" width="500" height="333" />
</p>

<div align="center">
  <b>Figure 1</b>: Perfectly balanced... looks like 0 fold change! [1]
</div>
<br />

The goal of this chapter is for readers to come away with **four key understandings:**

1. [What is Differential Analysis (DA) and why do we care about it?](#DA)
2. [What is RNAseq, and how do we use it to do DA?](#RNA)
3. [What is ChIPseq, and how do we use it to do DA?](#ChIP)
4. [How does using both RNAseq and ChIPseq together enhance our DA?](#combo)

We will go over all these points in detail, and provide a summary at the end. Let's get started with talking about DEA!

## What is Differential Analysis (DA)? <a name="DA" />

<p align="center">
  <img src="imgs/dea.jpg", style="background-color:white"/>
</p>

<div align="center">
  <b>Figure 2</b>: Depiction of DA. In this image, the circles can represent any metric. We will go over DA of expression data from RNAseq, as well as DA of TF-binding data from ChIPseq. [2]
</div>
<br />

Differential analysis (DA) is an analysis technique that excels at extracting 'significant' data points from a dataset. These points are deemed significant because of their difference in value between two samples of interest. For example, this could refer to the difference in a certain gene's expression between a healthy tissue sample and a tumor tissue sample. This would be an example of Differential **Gene Expression** Analysis, and is often done using RNAseq. Another example of DA would be analyzing the difference in transcription factor (TF) binding between the two sample, healthy and tumor. Through similar logic, we can perform DA on any metric of biological relevance, for which we have information from two datasets.

### What's the point?

It is always a good idea to ask the question: 'Why do we care?'. In this case, we care because oftentimes experimental science boils down to: _What is causing this sample to behave differently than this other sample?_. A good way to answer this question is to investigate everything that is different between the two samples. If two restaurants are selling bean and cheese burritos but one is clearly tastier, we might want to perform Differential Ingredient Analysis to investigate. Similarly, between the healthy and tumor tissue samples mentioned earlier, finding a gene that is expressed highly in tumor cells versus healthy cells could lead us to perform knockdowwn studies on this gene, and provide information on the disease pathway. We could do the same with TF binding data to investigate the binding of different TFs in healthy and tunor tissue.

<br />

In the next sections, we will go over RNAseq and ChIPseq, and delve deeper into how we would perform DA with data sourced from the two technologies.

## What is RNAseq? <a name="RNA" />

### RNAseq Workflow

### What we can learn

### DA Tools/Methods for RNAseq

## What is ChIPSeq? <a name="ChIP" />

### ChIPseq Workflow

### What we can learn

### DA Tools/Methods

## What do we gain by using both technologies together? <a name="combo" />

<p align="center">
  <img src="imgs/chip_rna.png"/>
</p>

<div align="center">
  <b>Figure x</b>: This figure depicts the type of output we would get from both ChIPseq (epigenomics) and RNAseq (transcriptomics). In the next few sections, we will discuss how these outputs play well with each other. [x]
</div>
<br />

In previous sections, we went over how to apply the concept of DA to analyze the different types of data that we obtain as a result of RNAseq and ChIPseq. In this section, we will discuss the motivations behind combining the two technologies, and why this gives us a more robust view of the biological function of the system we are investigating.

### Limitations of RNAseq Alone

<p align="center">
  <img src="imgs/ptm.jpeg"/>
</p>

<div align="center">
  <b>Figure y</b>: This figure summarizes the main mechanisms for post-translational modification of proteins. As we will discuss in this section, RNAseq gene expression data does not account for protein regulation. [y]
</div>
<br />

There is no doubt that RNA sequencing for gene expression data has been one of the most important scientific technologies developed in the last century. The onset of 'the sequencing era' has produced enormous amounts of new knowledge and understanding about a wide variety of systems. However, the technology does not come without its limitations. The most worrisome of these drawbacks is shown in Figure y: post-translation modifications (PTMs). As discussed earlier, RNAseq counts gene expression based on transcripts present at the time of RNA extraction. While this is definitely a decent indicator of a genes importance, it fails to account for the possibility that some of these analyzed transcripts will get translated into proteins, which will then get degraded through some PTM and never havea functional impact. As a result, we could have a gene we think to be important because its expression is differential. when in reality its functional impact does not change. 

Luckily for us, ChIPseq is perfectly suited to help us resolve this uncertainty, albeit only with TF (or other DNA-binding protein) analysis. As discussed before, ChIPseq is a tool for examining the binding of DNA-binding proteins such as TFs, so we can use it only when analyzing this subset of genes. Because of the importance of TFs as regulators of gene expression, however, more often than not we find ourselves interested in these proteins, and so the use of RNAseq + ChIPseq is still relevant. 

We will now dive into exactly how ChIPseq can help us validate our RNAseq findings.

### ChIPseq to the Rescue!

Based on what we discussed previously, it seems that the most concerning limiation of RNAseq that we want to neutralize is its inability to account for post-translation modifications (PTMs). Essentially, this boils down to the fact that RNAseq is not a functional assay; high gene **expression** does not necessarily imply that the gene is going to be highly **functionally active**. ChIPseq, on the other hand, does exactly this, for investigating specific transcription factors (TFs). Keeping in mind the way these two technologies work, we can craft the following broad protocol for this combined workflow:

1. Obtain RNA and DNA from samples of interest
2. Perform RNAseq to get gene expression for the entire genome
3. Perform differential expression analysis to get the top differential DNA-binding proteins 
4. Perform ChIPseq for these proteins of interest
5. Perform differential peak analysis to analyze the differential binding activity of these proteins
6. Compare differential analysis outputs from RNAseq and ChIPseq to make conclusions and prompt further studies.

This workflow would enable us to investigate gene regulatory networks, and how different TFs interact with different loci in different samples to prompt phenotypical changes. Let's look at an example using a toy dataset that will help solidify our understanding of the interaction between RNAseq and ChIPseq.

### Example

<p align="center">
  <img src="imgs/rna_data.png", height="400", width="400"/><img src="imgs/chip_data.png", height="400", width="400"/>
</p>

<div align="center">
  <b>Figure z</b>: An oversimplified example dataset meant to help illustrate the pitfalls of RNAseq alone, and how ChIPseq can help us overcome this. We have an RNAseq gene expression output for three TFs on the left, across two samples A and B, as well as peak counts for the same three TFs and same two samples after running ChIPseq.
</div>
<br />

Let's start by drawing a conclusion as if the ChIPseq data didn't exist. We would probably conclude that all three proteins (TF1,2, and 3) were signficantly upregulated in sample B compared to A, due to their differential expression. We would suggest investigating these proteins further, perhaps with knockdown/knockin studies. 

## References

1. Perrin, H. (2018, April 30). Visualize differential gene expression with ViDGER. Medium. https://medium.com/@HeleneOMICtools/visualize-differential-gene-expression-with-vidger-ee922e1c2a8
2. Harvard Chan Bioinformatics Core. (2017, May 12). Gene-level differential expression analysis with DESeq2. Introduction to DGE - ARCHIVED; GitHub Pages. https://hbctraining.github.io/DGE_workshop/lessons/04_DGE_DESeq2_analysis.html 
 
x. Liuksiala, T. (2022, November 4). Integrative analysis of RNA-seq and ChIP-seq data. Genevia Technologies. https://geneviatechnologies.com/blog/integrative-analysis-of-rna-seq-and-chip-seq-data/

y. Wang, Y.-C., Peterson, S. E., & Loring, J. F. (2014). Protein post-translational modifications and regulation of pluripotency in human stem cells. Cell Research, 24(2), 143–160. https://doi.org/10.1038/cr.2013.151
