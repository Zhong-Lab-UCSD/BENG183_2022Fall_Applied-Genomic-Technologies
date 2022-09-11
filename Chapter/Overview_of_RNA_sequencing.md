# Overview of RNA sequencing

This chapter introduces the tools in RNA-seq pipeline and walks you through the steps. The primary focuses will be the RNA-seq outline, downstream analysis tools, challenges and the future, for bioinformatics students to have an overall understanding of the roadmap and the ability to make informed decision on the workflows.

## 1. Overview

RNA-seq is a high throughput sequencing technology. The common goals of RNA-seq are differentially expressed genes identificaiton, transcript discovery, alternative splicing analysis, functional analysis, etc. RNA-seq is versatile and can be modified to adapt to different needs. A wide array of bioinformatics tools support RNA-seq and can be used for different purposes. A typical RNA-Seq experiment contains the following steps:

- Select samples of interest
- Isolate RNAs
- Generate cDNA, fragment and select size, add sequencing adaptors
- Sequence to the end
- Map to genome, transcriptome and predicted exon junctions
- Downstream analysis

The first 4 steps are experimental procedures, while the last 2 steps are computational procedures. The primary focus of this chapter will be on the computational aspect of RNA-seq. 

### 1.1 Experimental Procedure

After cells are lysed, RNA is extracted from the aliquot and purified to retain mRNA. The samples are filtered to remove any artifacts. The RNA is first convereted to a library of cDNA fragments through fragmentation. Then, the sequencng adapters are added to each cDNA fragment, which are subject to high-throughput sequencing using paired-end or single end sequencing. 

### 1.2 Read Alignment

Now we have the reads of cDNA fragments. We need to align them to the reference genome before the processing steps. Thre is a wide range of alignment software. These are the commonly used ones:

- SOAP
  * SOAP allows a threshold of mismatches or continuous gaps for aligning a read to the referene genome. It reports the best high of reach read. For multiple equally good hits, the users can chhose to report all, randomly report one, or discard all.  
- STAR
  * Capable of discovering more complex RNA sequence arrangements, such as chimeric and circular RNA, in addition to detecting annotated and novel splicing juncitons.
- ELAND
  * Illumina ELAND algorithm is designed for fast short sequence alignment and is optimized for detecting SNPs, it has to be used after GA Pipeline.
  * Can do ungapped alignment for reads with size up to 32 bp. With the help of additional scripts, Eland can map reads longer than 32bp.
- BWA-MEM
  * Preferred algorithm for 70 bp to 1 Mbp. It works well with Illumina, 454, Ion Torrent and Sanger reads, assembly contigs and BAC sequences. 
  * It tolerates more errors given longer alignment.

## 2. Downstream Analysis

After we align the reads to the reference genome, now we can process the data. 

### 2.1 Differential Expression Analysis

One primary goal of RNA-seq is to understand what genes are expressed differently in experimental and control groups. This is a critical step because it narrows down the entire pool of genes down to the genes of interest, so we can investigate whether these genes cause the disease, or correlate to the disease. DE genes are expressed differently in experiment group from the control group. Their differences could be the cause of the condition. There are many available tools for calling DE genes. Bioconductor has several packages for that: Limma, DESeq2, edgeR. They use negative binomial distribution as their statistics to identify differentially expressed genes. We can specify the cutoff value as the threshold of selection. 

![Figure1](https://github.com/Zhong-Lab-UCSD/BENG183_FA18/blob/master/Final%20Paper%20Submission_jdl044_attempt_2018-12-14-23-52-30_Final%20Project/Final%20Project/Capture.JPG)

Figure 1: This is the output of DE genes from Limma and edgeR. It contains lots of information we can work with. These tools are quite popular so there are well-developed workflows and documentation online. They are in R and are easy to use when used in Jupyter notebook. 

![Figure2](https://github.com/Zhong-Lab-UCSD/BENG183_FA18/blob/master/Final%20Paper%20Submission_jdl044_attempt_2018-12-14-23-52-30_Final%20Project/Final%20Project/Capture2.JPG)

Figure 2: This is an interactive mean-difference plot generated using Glimma. log-FCs versus log-CPM values of the individual values per sample for a selected gene. 

These tools can generate a mean-difference plot. We can easily visualize the differential expressed genes. The red dots represent up-regulated genes. The blue dots represent down-regulated genes. The gray dots represent genes with significance lower than the threshold value.

### 2.2 Functional/Pathway Analysis

After learning which genes are differentially expressed. We are interested in knowing the functions and pathways they control in the genome. Functional analysis determines enrichment of known biological functions, interactions, or pathways. 

Characterization of DE genes with molecular functions or pathways: 
- Enrichment analysis
- Overrepresented analysis
- Pathway analysis
- Gene set enrichment analysis (GSEA)
- Gene set variation analysis (GSVA)

![Figure3](https://github.com/Zhong-Lab-UCSD/BENG183_FA18/blob/master/Final%20Paper%20Submission_jdl044_attempt_2018-12-14-23-52-30_Final%20Project/Final%20Project/Capture3.JPG)

Figure 3: The top differential gene sets are plotted in the heatmap. The gene sets are clustered with the expression level in each functional category. This analysis allows us to easily know which pathways are different in the tumor sample from the normal sample. We can then narrow our focus of investigation on a few pathways of interest.

### 2.3 Visualization

Tools for visualizaing read alignment
- UCSC genome browser
- Broad Institute IGV

![Figure4](https://github.com/Zhong-Lab-UCSD/BENG183_FA18/blob/master/Final%20Paper%20Submission_jdl044_attempt_2018-12-14-23-52-30_Final%20Project/Final%20Project/Capture4.JPG)

This is a screenshot of UCSC genome browser. Visualization gives information about the location and the distribution of the reads. We can also use it for sanity check on the data to make sure the format is correct. 

### 2.4 Other Analysis

There are many other analysis we can do with RNA-seq data. These are some tools and their corresponding features.  

|Tool | Feature | 
|-----------|:----------------:|
|Transcript discovery:| 		SOAPdenovo, Oases|
|Alternative splicing analysis:| 	CuffDiff2|
|Gene fusion discovery:|		INTEGRATE, deFuse|

Other types of RNA-seq: 
- Single-cell RNA-seq (more precise RNA information)
- Other types of RNA

## 3. Challenges of RNA-seq

### 3.1 Challenges

Library construction: 
- Biased outcome of RNA and cDNA fragmentation

Difficulties of retrieving, storing and processing data from RNA-Seq:
- Shorter transcriptome (polyA tails, splice junctions)
- Large transcriptome (short sequences can be mapped to multiple sites)

Sequence coverage: 
- larger the genome, the more complex the transcriptome, the more sequencing depth is required for adequate coverage.

Data interpretation:
- With lower sequencing cost, the amount of data increases exponentially. Now, the focus switches the ability of filtering genomic data, understanding the results and making interpretation. 
 
### 3.2 Solutions

PolyA tails: can be identified by the presence of multiple As or Ts.

Junctions: create junction library

Multi-matched reads: assign them based on the number of reads mapped to their unique neighbours.

## 4 The Future

RNA-seq analysis has been well developed such that it is highly standardized and streamlined. There are many well-developed pipelines available online. It has advantages over previously developed transcriptomic methods. With RNA-seq, scientists enjoy benefits such as independence of existing genome data (for transcript discovery and de novo gene identification) and high capacity of quantification. Scientists are working on targeting more complex transcriptomes to identify and track the expression of all genes. In the future, RNA-Seq is expected to help us analyze and determine more complex structure of transcriptome at lower cost. The future will be integrating RNA-seq with other types of high-throughput sequencing techniques.


## Reference

1. Wang, Zhong et al. “RNA-Seq: a revolutionary tool for transcriptomics” Nature reviews. Genetics vol. 10,1 (2009): 57-63. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2949280/
2. A survey of best practices for RNA-seq data analysis: https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0881-8
3. RNA-seq analysis is easy as 1-2-3 with limma, Glimma and edgeR: https://f1000research.com/articles/5-1408/v2
4. Li H. and Durbin R. (2009) Fast and accurate short read alignment with Burrows-Wheeler Transform. Bioinformatics, 25:1754-60. [PMID: 19451168]
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2705234/
5. A. Dobin, T.R. Gingeras “Mapping RNA-seq reads with STAR” Curr. Protoc. Bioinformatics, 51 (2015), pp. 11.14.1-11.14.19 https://currentprotocols.onlinelibrary.wiley.com/doi/full/10.1002/0471250953.bi1114s51
6. A. Dobin, Carrie A. Davis, Felix Schlesinger, Jorg Drenkow, Chris Zaleski, Sonali Jha, Philippe Batut, Mark Chaisson, Thomas R. Gingeras; STAR: ultrafast universal RNA-seq aligner, Bioinformatics, Volume 29, Issue 1, 1 January 2013, Pages 15–21, https://doi.org/10.1093/bioinformatics/bts635 
7. Subramanian, Aravind et al. “Gene set enrichment analysis: A knowledge-based approach for interpreting genome-wide expression profiles” PNAS Oct 2005, 102 (43) 15545-15550 https://doi.org/10.1073/pnas.0506580102
8. Mootha, Lindgren, et al. “PGC-1α-responsive genes involved in oxidative phosphorylation are coordinately downregulated in human diabetes” Nature Genetics vol. 34 (2003): 267–273 https://www.nature.com/articles/ng1180
9. Tarca AL, Kathri P, Draghici S (2018). SPIA: Signaling Pathway Impact Analysis (SPIA) using combined evidence of pathway over-representation and unusual signaling perturbations. R package version 2.34.0
http://bioinformatics.oxfordjournals.org/cgi/reprint/btn577v1.
10. Leong, Hui Sun and David Kipling. “Text-based over-representation analysis of microarray gene lists with annotation bias” Nucleic acids research vol. 37,11 (2009): e79.
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2699530/
11. Li R, Li Y, Kristiansen K, Wang J. SOAP: short oligonucleotide alignment program. Bioinformatics. 2008;24:713–714. [PubMed] 
https://academic.oup.com/bioinformatics/article/24/5/713/203564
