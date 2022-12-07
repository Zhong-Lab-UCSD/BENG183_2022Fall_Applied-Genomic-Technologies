
# 3D Genome Structure And Hi-C Analysis

Kaifu Yang, Tingwen Zheng, Jiayi Chen


1. [Introduction](#231)
2. [3D Chromosome Structure](#232)<br>
    2.1. [Chromosomal Territories](#2321)<br>
    2.2. [A/B Compartment](#2322)<br>
    2.3. [Chromatin Loops](#2323)<br>
    2.4. [TADs](#2324)<br>
    2.5. [LADs](#2325)<br>
    2.6. [NADs](#2326)
3. [Hi-C Analysis](#233)<br>
    3.1. [Pipeline](#2331)<br>
    3.2. [Hi-C Data Mapping Format](#2332)<br>
    3.3. [Analyzation Tool: Juicer](#2333)
5. [Real-life Example](#234)
6. [Reference](#235)




## 1. Introduction<a name="231"></a> 

From a 3D perspective, the genome has different genomic conformation, showing different interaction patterns that can be revealed by Hi-C results.<br>
The Larger scale conformations are structures like: chromosome territories and A/B compartments.<br>
The smaller scale conformations are structures like: loop, TADs, LADs, etc.<br>
![](Structure.png) [[1]](https://en.wikipedia.org/wiki/Nuclear_organization)


## 2. 3D Chromosome Structure <a name="232"></a>

#### 1) Large Conformations - Chromosomal Territories<a name="2321"></a>
Each chromosome occupies specific regions of the nucleus, forming individual territories and rarely intermix. As a result, the interaction between loci on the same chromosome is more frequent. The chromosomal territory helps regulate gene expression by redistributing genes and co-localizing genes with their transcription machinery.

![](LargeConformation.png)
[[2]](https://doi.org/10.1007/978-1-4020-6754-9_3025)

#### 2) Large Conformations - A/B Compartments<a name="2322"></a>
The whole genome can be separated into two self-interacting spatial compartments: A and B. Usually, the A compartments tend to be gene-rich and contain histone markers for active transcription. In other words, A compartments are open and expression-active chromatins. B compartments, on the other hand, tend to be gene-poor and contain histone markers for gene silencing. In general, B compartments are closed and expression-inactive chromatins. Usually, we expect interactions between loci to occur within the same compartment. Regions in compartment A tend to interact with regions in compartment A, and regions in compartment B tend to interact with regions in compartment B. 

#### 3) Small Conformations - Chromatin Loops<a name="2323"></a>
Genome forms a loop structure to bring together two far away elements to a spatial proximity in order to facilitate regulatory effect.
A loop is a site where a protein specifically binds to two different sequences in the genome. As a result, we can see strong associations/interactions between these sites. 

![](Loop.png)
[[3]](https://seas.harvard.edu/news/2014/12/scientists-map-human-loop-ome)

#### 4) Small Conformations - Topologically Associating Domains<a name="2324"></a>
TADs are self-interacting genomic regions. DNA sequences interact with each other more frequently within TADs. Many studies indicate that TADs restrict interactions of regulatory sequences to their target genes. Moreover, TAD boundaries are associated with high CTCF binding and more frequent appearance of certain genes such as the housekeeping genes. However, the function of TADs is still not fully understood and we need more research. According to the computer simulation, we find that chromatin loop extrusion can help generate TADs through cohesin motors. [[4]](https://www.annualreviews.org/doi/10.1146/annurev-genet-112618-043633)

![](TAD.png)
[[5]](https://www.eurekalert.org/news-releases/662819)

#### 5) Small Conformations - Lamin Associated Domains<a name="2325"></a>
Genomic regions that are adjacent to the nuclear lamina, in which DNA heavily interacts with NL and form a condensed chromatin layer. LADs are associated with gene repression because the post-translational histone modification, H3K27me3, is enriched in LADs chromatin. 

![](LAD.png)
[[6]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5532494/)

#### 6) Small Conformations - Nucleolar Associated Domains<a name="2326"></a>
NADs are regions in which DNA sequences interact with nucleolus. This structure, frequently including large multi-gene clusters, usually express characteristics of constitutive heterochromatin and are correlated with low gene expression. The part of the chromosome that contains ribosomal RNA genes is usually inside the NADs. NADs can be further differentiated into two types. Type I NADs are usually associated with both nucleolar periphery and nuclear lamina. This type of NADs are usually constitutive heterochromatin, leading to late DNA replication and little gene expression. Type II NADs are usually associated with nucleoli. This type of NADs, in contrast, leads to earlier DNA replication and greater gene expression. [[7]](https://doi.org/10.1186/1756-8935-8-3)


## 3. Hi-C Analysis<a name="233"></a>



### 3.1 Pipeline<a name="2331"></a>

![](WorkFlow.png)
[[8]](https://journal.hep.com.cn/qb/EN/10.1007/s40484-017-0113-6)





### 3.2 Hi-C Data Mapping Format<a name="2332"></a>

![](Structure_VS_HiC.png)

[[9]](https://www.researchgate.net/figure/Multiscale-chromatin-folding-a-Schema-of-the-features-of-chromatin-folding-at-different_fig1_338025861)

The graphs here show the general shape of mapping of the data from a larger scale to the smaller scale. As we can see in the graph: the x and y axis represent the sequence of the part of the genome we are looking at, and they are identical. The intensity of the shadow represents the contact frequency of two positions on the sequence. That’s why we have a completely dark line that goes from top left to bottom right. The line is at the position where the sequence of x and y is at the same position. The gray square on the graph represents a self-interacting genomic sequence. As explained above, chromosome territories, A/B compartments and TADs all have this property. Moreover, for the loops, we can see that it is at the corner of some TADs, and it is very dark.  We also observe that the corner of the TAD represents the contact frequency of its head and tail, so we understand that the loop is formed by the head and tail of this TAD interacting with each other. The part of chromatin bends to make this interaction happen while also bringing other parts to each other. That’s why these TADs are also called loop domains.

### Analyzation Tool: Juicer<a name="2333"></a>

Tools like Juicer can be used to visualize Hi-C data and annotate mapping format. 

![](Juicer.png) [[10]](https://doi.org/10.1016/j.cell.2014.11.021)

A) Sequenced read pairs (horizontal bars) are aligned to the genome in parallel. Color indicates genomic position. Read pairs aligning to more than two positions are excluded. Those remaining are sorted by position and merged into a single list, at which point duplicate reads are removed. The hic file stores contact matrices at many resolutions and can be loaded into Juicebox for visualization. 

(B) Contact domains (yellow) are annotated using the Arrowhead algorithm.

(C) Loops (cyan) are annotated using HiCCUPS. [[10]](https://doi.org/10.1016/j.cell.2014.11.021)

#### Arrowhead algorithm:
Arrowhead algorithm is used for contact domain(TADs, territories, etc.) annotation. The matrix transform equation is: $$A_{i,i+d}=\frac{M_{i,i-d}-M_{i,i+d}}{M_{i,i-d}+M_{i,i+d}}=1-\frac{2*M_{i,i+d}}{M_{i,i+d}+M_{i,i-d}}$$ In which M denotes the normalized contact matrixm, A is the arrowhead matrix, i is the point (i, i) at the center of the Matrix, and d is some distance that needs to be defined. $A_{i,i+d}$ will be strongly positive if i − d is inside a domain and locus i + d is not. If the situation is the reverse then $A_{i,i+d}$ will be strongly negative. If the two is both inside or outside the domian the $A_{i,i+d}$ will be close to 0. The resulting graph of A will be arrowhead like. [[10]](https://doi.org/10.1016/j.cell.2014.11.021)


#### HiCCUPS:
HiCCUPS is used for loops annotation. It looks at every pixel in the contact matrix and compqare each pixel with the region nearby it. If the pixel has significantly more contacts than expected when compared to nearby region, it is an enriched pixel. The resulting enriched pixels tend to form contiguous interaction regions comprising 5–20 pixels each. We define the “peak pixel” (or simply the “peak”) to be the pixel in an interaction region with the most contacts. [[10]](https://doi.org/10.1016/j.cell.2014.11.021)


## 4. Real-life Example<a name="234"></a> 
This [paper](https://doi.org/10.1186/s13045-021-01131-0) looks at 3D epigenome reprogramming during pancreatic cancer metastasis.
They compared 3D epigenome structure between non-metastatic (primary cancer cells) and metastatic pancreatic cancer cells.
With Hi-C, they are able to identify, for example, changes in A/B compartment, contact domains, and chromatin loops in the metastatic samples. Specifically, this figure shows the emergence of enhancer-promoter loops that are specific to metastatic cells.
 
![](Application.png)
[[11]](https://doi.org/10.1186/s13045-021-01131-0)

The figures above are Hi-C contact heat maps from primary cancer cells (left) and metastatic cancer cells (right). Compared to the primary sample, the metastatic sample has additional red points labeled by black arrows. As introduced above, these are DNA loops. For example, there are enhancers looped to the KLF5 promoter region in metastatic cancer cells, which cannot be found in primary cancer cells on the left. According to Ren et al., these metastasis-specific loops can mediate additional enhancer-promoter loops to upregulate genes associated with pancreatic cancer metastasis. (Ren et al.) 

This example demonstrates the significance of Hi-C analysis: it helps to identify 3D epigenome reprogramming during pancreatic cancer metastasis and expand our knowledge of mechanisms of gene regulation during pancreatic cancer metastasis.


## 5. Reference<a name="235"></a>
[1] “Nuclear Organization.” Wikipedia, Wikimedia Foundation, 20 June 2022, https://en.wikipedia.org/wiki/Nuclear_organization. 
<br>

[2] (2008). Chromosome Territories. In: Encyclopedia of Genetics, Genomics, Proteomics and Informatics. Springer, Dordrecht. https://doi.org/10.1007/978-1-4020-6754-9_3025

[3] Scientists Map the Human Loop-Ome, Harvard School of Engineering https://seas.harvard.edu/news/2014/12/scientists-map-human-loop-ome. 

[4] K;, Yatskevich S;Rhodes J;Nasmyth. “Organization of Chromosomal DNA by SMC Complexes.” Annual Review of Genetics, U.S. National Library of Medicine, https://pubmed.ncbi.nlm.nih.gov/31577909/.<br>

[5] UNC_Health_Care. “Whole Genome Sequencing Reveals Genetic Structural Secrets of Schizophrenia.” EurekAlert!, https://www.eurekalert.org/news-releases/662819. 

[6] van Steensel, Bas, and Andrew S Belmont. “Lamina-Associated Domains: Links with Chromosome Architecture, Heterochromatin, and Gene Repression.” Cell, U.S. National Library of Medicine, 18 May 2017, https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5532494/. 

[7] Saksouk, N., Simboeck, E. & Déjardin, J. Constitutive heterochromatin formation and transcription in mammals. Epigenetics & Chromatin 8, 3 (2015). https://doi.org/10.1186/1756-8935-8-3

[8] Computational tools for Hi-C data analysis https://journal.hep.com.cn/qb/EN/10.1007/s40484-017-0113-6

[9] Multiscale Chromatin Folding. A) Schema of the Features of Chromatin... https://www.researchgate.net/figure/Multiscale-chromatin-folding-a-Schema-of-the-features-of-chromatin-folding-at-different_fig1_338025861. 

[10] A 3D Map of the Human Genome at Kilobase Resolution Reveals Principles of Chromatin Looping https://doi.org/10.1016/j.cell.2014.11.021

[11] Ren et al. J Hematol Oncol (2021) 14:120 https://doi.org/10.1186/s13045-021-01131-0
