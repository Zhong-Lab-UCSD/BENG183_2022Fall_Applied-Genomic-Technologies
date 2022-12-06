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

- **Viewing Alternative Splicing**: 
 <img width="800" alt="IGV1" src="https://user-images.githubusercontent.com/83438583/205523738-d9d3e3f3-efd6-4f2c-8a5a-8b3b7bd557ec.png">

 The graph provides an example of using IGV to observe alternative splicing. Human g18 is used as the reference genome, and the input files are the alignment file from human liver cell tissue and heart cell tissue. From the Coverage track and the Alignment track, it can be observed the sequence fragments align significantly differently in the gene *SLC25A3*, a phosphate transfer gene. This is one example of using IGV to monitor alternative splicing.   

## 2. PCA plot in differential expression analysis


## 3. Heat Map 

## References
1. https://software.broadinstitute.org/software/igv/AlignmentData
2. https://www.google.com/search?q=igv+rna+seq&rlz=1C5CHFA_enUS983US984&biw=1336&bih=1013&tbm=vid&ei=yiyNY5DjAfelqtsPl8CugAY&ved=0ahUKEwiQ8LbFjuH7AhX3kmoFHRegC2AQ4dUDCA0&uact=5&oq=igv+rna+seq&gs_lcp=Cg1nd3Mtd2l6LXZpZGVvEAMyBQgAEJECMgYIABAWEB4yBggAEBYQHjIICAAQFhAeEA8yCAgAEBYQHhAPMgYIABAWEB4yBQgAEIYDMgUIABCGAzoFCCEQoAE6BQgAEIAEOgQIABBDOgcIABCABBANOgYIABAeEA06CAgAEB4QDxANOgoIABAIEB4QDxANOggIABAIEB4QDVCWA1jnMWDrMmgOcAB4AIABbogBjA2SAQQxNi4ymAEAoAEBwAEB&sclient=gws-wiz-video#fpstate=ive&vld=cid:367671eb,vid:awGN-rpLYas
3. Chua, K.Y., Monk, I.R., Lin, YH. et al. Hyperexpression of α-hemolysin explains enhanced virulence of sequence type 93 community-associated methicillin-resistant Staphylococcus aureus . BMC Microbiol 14, 31 (2014). 
4. https://www.youtube.com/watch?v=dx9-N8b9Yj4
5. https://alexslemonade.github.io/refinebio-examples/03-rnaseq/dimension-reduction_rnaseq_01_pca.html
6. https://blog.bioturing.com/2018/06/14/principal-component-analysis-explained-simply/
7. Wang, S., Zhang, Y., Hu, C. et al. Shiny-DEG: A Web Application to Analyze and Visualize Differentially Expressed Genes in RNA-seq. Interdiscip Sci Comput Life Sci 12, 349–354 (2020). https://doi.org/10.1007/s12539-020-00383-7
