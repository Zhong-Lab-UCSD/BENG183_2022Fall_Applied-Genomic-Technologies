# RNA-seq visualization

## Overview

This handout will illustrate the introduction for RNA-sequencing and cover detailed information on three related visualizations.

## Usage for RNA-sequencing and Visualization
With the development of the Next Generation sequencing technique, RNA sequencing is becoming an essential tool to quantify the RNA at a given moment for our sample of interest(wikipedia). It is also an effective tool for understanding gene expression levels. The visualization helps researchers unpuzzle complex data and allows us to display experimental findings more effectively. This handout will provide examples of the visualizations commonly used in RNA-seq, concentrating on three graphs: 
1. The Genome Alignment Graph
2. Principal Component Analysis Plot 
3. Heat Map

## 1. The Genome Alignment Graph
### Tools to Generate Genome Alignment Graph:
- Integrative Genomics Viewer(IGV)
- UCSC Genome Browser
The graph from this handout would use visualization produced by IGV as the example for illustration.
### Purpose and Usage (from IGV official website): 
The Genome Alignment graph is a typical visualization widely used to help researchers analyze data from sequencing techniques such as Chip-seq and RNA-seq. It allows researchers to visualize how the genome from their samples aligns with the reference genome. 
- **Input Data**: Aligned reads from sequencing with format using BAM, SAM, or CRAM. IGV requires index files from BAM (with *bai* extension) and CRAM (with *crai* extension ) files.
- **Coverage Track**: Displays the depth of the reads as bar graph.
- **Alignment Track**: Displays the alignment details of the reads. This track provides information including insertions and deletions. 
- **Splice Junction Track**: Show the break of read coverage due to splicing. 
<img width="800" alt="IGV2" src="https://user-images.githubusercontent.com/83438583/205523473-177ed52a-d6fd-40f9-9437-6efa285b206f.png">
    
**Figure 1.** This image depicts IGV screenshot for genome sequence of human liver cell tissues. 

- **Viewing Alternative Splicing**: 
 <img width="800" alt="IGV1" src="https://user-images.githubusercontent.com/83438583/205523738-d9d3e3f3-efd6-4f2c-8a5a-8b3b7bd557ec.png">
 
**Figure 2.** It shows IGV screeshot for genome sequence of human liver cell and heart cell tissue.

 The graph provides an example of using IGV to observe alternative splicing. Human g18 is used as the reference genome, and the input files are the alignment files from human liver cell tissues and heart cell tissues. From the Coverage track and the Alignment track, it can be observed the sequence fragments align significantly differently in the gene *SLC25A3*, a phosphate transfer gene. This is one example of using IGV to monitor alternative splicing.   

## 2. Principal Component Analysis (PCA)
To simplify large genomic data such as the transcriptomes, Principal Component Analysis (PCA) is a useful classical dimension reduction approach that is often used to reduce the dimensionality of large data sets, by transforming a large set of variables into a smaller one while still capturing most of the information and variation in the large data sets. The reduction of large data sets is achieved by transforming the variables to a new set of variables, known as the principal components (PCs), which are orthogonal to each other. It is ordered such that the retention of variation present in the original variables decreases as moving down in the order. Therefore, most variation in the dataset would be along the first PC. After controlling for PC1, most remaining variation would be along the second PC. 

 <img width="800" alt="Screen Shot 2022-12-06 at 12 20 26 AM" src="https://user-images.githubusercontent.com/72646231/206057696-2592bfb5-48d1-477e-bed6-786008c842dc.png">
 
 **Figure 3.** Since PC1 and PC2 are perpendicular to each other, rotation is needed to make them straight so they can be the axes to construct a PCA plot.
 
 ### Purpose and Usage
The purpose of PCA is to reduce dimensionality of large data sets while preserving as much variation as possible, making it possible to see strong patterns. Though it is not a clustering algorithm itself, the PCA plot often provides visually clustering for data exploration, which would be critical for differential expression analysis. It entails if the dataset has any outliers, any batch effect strongly influencing the dataset, or which samples are similar to one another, or which ones are different. Furthermore, by looking at the PCA loadings, which are the coefficients of the linear combination of the original variables from which the PCs are formed, researchers can identify the genes that are responsible for such similarities and differences. Since the first two PCs explain the most variation, so plotting the first 2 PCs would be essential in initial exploration of the dataset to determine the main driver for transcriptomic changes. 
 
 - **Tools and Packages**: R's prcomp() function and ggplot2 package to generate PCA plot
 - **Input Data**: normalized data that follows a gaussian/binomial distribution. Since RNA-seq data is negative binomial distribution, log normalized data would be needed.

### Interpretation of the PCA Plot
 
As PCA is a way to bring out strong patterns from large and complex datasets, it can show cluster similarity. The samples with similar gene expression profiles will cluster together. 

![Blog_pca_8](https://user-images.githubusercontent.com/72646231/206060115-817dc790-4b75-4223-9f41-ffb394082234.png)
 
**Figure 4.** This image shows a PCA plot of cluster similarity such that there are 3 clusters. The first PC (explains most variation): Group 3 vs. Group 1 vs. Group 2&4. 
  
### Application of the PCA Plot in Differential Expression Analysis

As PCA is critical in determining the main driver for transcriptomic changes in RNA-seq data, it provides useful information for researchers to decide the appropriate model for differential expression analysis. Below is a PCA plot of the first two PCs on 175 RNA-seq samples obtained from 20 patients with prostrate cancer who underwent different types of androgen deprivation therapy (ADT) treatments. The PCA plot clearly shows distinct clusters between the different types of androgen deprivation therapy treatments as well as distinct clusters between pre-ADT and post-ADT. Such information is essential for choosing the model for differential expression analysis. If interested in genes that are differentially expressed between pre-ADT and post ADT and there is a clear variation between the different types of ADT treatments, researchers can potentially divide the dataset into three different types of ADT treatments and run differential expression analysis seperately, or can use ADT treatment type as a fixed effect (covariate). 

<img width="800" alt="Screen Shot 2022-12-06 at 4 01 16 PM" src="https://user-images.githubusercontent.com/72646231/206061393-6bbdae85-1c4f-4132-ac87-043c1a9cfddf.png">

**Figure 5.** This image depicts a PCA plot of the first two PCs on 175 RNA-seq samples obtained from 20 patients with prostrate cancer who underwent different types of androgen deprivation therapy (ADT) treatments and RNA-seq samples include pre-ADT biopsies and post-ADT prostatectomy specimens.

## 3. Heat Map


## References
1. https://software.broadinstitute.org/software/igv/AlignmentData
2. https://www.google.com/search?q=igv+rna+seq&rlz=1C5CHFA_enUS983US984&biw=1336&bih=1013&tbm=vid&ei=yiyNY5DjAfelqtsPl8CugAY&ved=0ahUKEwiQ8LbFjuH7AhX3kmoFHRegC2AQ4dUDCA0&uact=5&oq=igv+rna+seq&gs_lcp=Cg1nd3Mtd2l6LXZpZGVvEAMyBQgAEJECMgYIABAWEB4yBggAEBYQHjIICAAQFhAeEA8yCAgAEBYQHhAPMgYIABAWEB4yBQgAEIYDMgUIABCGAzoFCCEQoAE6BQgAEIAEOgQIABBDOgcIABCABBANOgYIABAeEA06CAgAEB4QDxANOgoIABAIEB4QDxANOggIABAIEB4QDVCWA1jnMWDrMmgOcAB4AIABbogBjA2SAQQxNi4ymAEAoAEBwAEB&sclient=gws-wiz-video#fpstate=ive&vld=cid:367671eb,vid:awGN-rpLYas
3. Chua, K.Y., Monk, I.R., Lin, YH. et al. Hyperexpression of α-hemolysin explains enhanced virulence of sequence type 93 community-associated methicillin-resistant Staphylococcus aureus . BMC Microbiol 14, 31 (2014). 
4. https://www.youtube.com/watch?v=dx9-N8b9Yj4
5. https://builtin.com/data-science/step-step-explanation-principal-component-analysis
6. https://www.projectpro.io/data-science-in-python-tutorial/principal-component-analysis-tutorial
7. https://alexslemonade.github.io/refinebio-examples/03-rnaseq/dimension-reduction_rnaseq_01_pca.html
8. https://blog.bioturing.com/2018/06/14/principal-component-analysis-explained-simply/
9. https://scentellegher.github.io/machine-learning/2020/01/27/pca-loadings-sklearn.html#:~:text=PCA%20loadings%20are%20the%20coefficients,components%20(PCs)%20are%20constructed.
10. Wang, S., Zhang, Y., Hu, C. et al. Shiny-DEG: A Web Application to Analyze and Visualize Differentially Expressed Genes in RNA-seq. Interdiscip Sci Comput Life Sci 12, 349–354 (2020). https://doi.org/10.1007/s12539-020-00383-7
