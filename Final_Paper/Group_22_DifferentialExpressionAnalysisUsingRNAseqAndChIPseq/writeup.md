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

It is always a good idea to ask the question: 'Why do we care?'. In this case, we care because oftentimes experimental science boils down to: *What is causing this sample to behave differently than this other sample?*. A good way to answer this question is to investigate everything that is different between the two samples. If two restaurants are selling bean and cheese burritos but one is clearly tastier, we might want to perform Differential Ingredient Analysis  to investigate. Similarly, between the healthy and tumor tissue samples mentioned earlier, finding a gene that is expressed highly in tumor cells versus healthy cells could lead us to perform knockdowwn studies on this gene, and provide information on the disease pathway. We could do the same with TF binding data to investigate the binding of different TFs in healthy and tunor tissue.

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

There is no doubt that RNA sequencing for gene expression data has been one of the most important scientific technologies developed in the last century. The onset of 'the sequencing era' has produced enormous amounts of new knowledge and understanding about a wide variety of systems. However, the technology does not come without its limitations. The most glaring 

### Example



## References

1. Perrin, H. (2018, April 30). Visualize differential gene expression with ViDGER. Medium. https://medium.com/@HeleneOMICtools/visualize-differential-gene-expression-with-vidger-ee922e1c2a8
2. Harvard Chan Bioinformatics Core. (2017, May 12). Gene-level differential expression analysis with DESeq2. Introduction to DGE - ARCHIVED; GitHub Pages. https://hbctraining.github.io/DGE_workshop/lessons/04_DGE_DESeq2_analysis.html
3. 



