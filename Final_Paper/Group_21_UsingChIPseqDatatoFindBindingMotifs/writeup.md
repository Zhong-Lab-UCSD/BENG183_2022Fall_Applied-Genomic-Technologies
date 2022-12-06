# ChiP-Seq
<hr>

## History of ChIP-seq
First developed by Gordon Robertson et al. in 2007 while working at the British Columbia Cancer Agency.  Their lab developed as a way to globally profile the binding of sites of STAT1 throughout the entire genome.  ChIP-seq superseded the standard protein-DNA association assay of the time: ChIP-on-chip—usually shortened to the silly sounding “ChIP-chip”—by replacing the final microarray hybridization step with next generation sequencing.  ChIP-seq has become the standard to study protein-DNA interactions in regulation studies.
## Advantages of ChIP-seq (Illumina)
ChIP-Seq delivers genome-wide profiling with parallel sequencing that generates millions of counts across multiple samples for cost-effective, precise, and unbiased investigation of epigenetic patterns. 
Additional advantages include:
* Captures DNA targets for transcription factors or histone modifications across the entire genome
* Defines transcription factor binding sites
* Reveals gene regulatory networks in combination with RNA-seq and methylation analysis
* Offers compatibility with various input DNA samples
## General Applications
### Analysis of DNA Transcription Factor Binding Sites
First described in [G. Robertson et al., 2007](https://pubmed.ncbi.nlm.nih.gov/17558387/). 

The rate of mRNA transcription is controlled by transcription factors that bind to specific DNA motifs in promoter regions upstream of protein coding genes. ChIP-seq is essential in determining the TF binding sites as these are important for gene regulation. The application was first described in “Genome-wide profiles of STAT1 DNA association using chromatin immunoprecipitation and massively parallel sequencing” (G. Robertson et al., 2007). An example of this would be the whole-genome mapping of DNase I-hypersensitive sites (DHSs) used to understand the regulatory mechanisms that underlie the enormous cell-type diversity of the CNS. The study utilised ChIP-seq coupled with DNase I hypersensitivity mapping in order to identify cis-regulatory regions in the brain. The addition of DNase I hypersensitivity increased the number of cis-regulatory regions by approximately 10 times, and they were able to identify a set of ‘base’ DHSs that were common to the CNS tissues, as well as cis-regulatory elements within the CNS that displayed regional and temporal specificity.  See [this example paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4157307/) if you are interested.



### Analysis of Histone Modifications
Described by [T. Milne et al., 2009]((https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4157307/))

Because ChIP uses immunoprecipitation, you can use an antibody that binds to a specific histone modification to map that modification throughout the genome.  These modifications help dictate the expression of DNA by changing the strength with which histones associate with the DNA strand; some modifications wind the chromatin tighter, and some loosen it.  Researchers can use ChIP-seq to see if a certain gene is in a highly condensed area or vice versa, and use that information to suggest mechanisms by which that gene is regulated.
Check out [this example](https://link.springer.com/article/10.1186/1471-2105-11-396).

### Finding Histone Associations by Histone Association Assay 
There have been many modifications to the ChiP protocol for specialized uses, and one modification to the protocol allows us to find histone associations. This new protocol, the Histone Association Assay, utilizes the fact that, when treated with a chemical crosslinker, chromatin-associated histone proteins immunoprecipitate with core histones in order to detect the relative amount of protein bound to chromatin. This method ensures that a protein’s intrinsic solubility will not affect its detection.

An example of this method used in other research is done by [Benhamed, et al.](https://www.nature.com/articles/ncb2443) In this paper, Benhamed and their colleagues investigate whether siRNAs and argonaute (AGO) proteins have a role in senescence-associated repression of the E2F-target genes, which regulate the E2F-RB1 complex. The scientists used the histone association assay to determine the partitioning of AGO2 between heterochromatin and euchromatin and found that AGO2 predominantly coprecipitates with heterochromatin histone markers H3K27me3 and H3K9me2 compared to pre-senescent control cells.
<hr>

# Genome Browser 
## Introduction to Genome Browser
Genome Browser can be accessed using the following link and choosing any of the genomes listed under the species tree and pressing “GO”: UCSC Genome Browser Gateway
### Ways to navigate Genome Browser

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/img0.png>
    <br>Personal Screenshot From Genome Browser: The hg38 Reference Genome Search Bar

</p>


We can click on the chromosome coordinates next to the search bar which will automatically copy and paste the coordinates and then we can adjust the coordinates to our needs. Other common ways to enter desired input into the search bar:
Entering the gene name
Entering: “[gene name] p[# amino acid]”
Entering: “chr[# chromosome]:[# first nt]-[# last nt]”
Entering: “[# chromosome] [# first nt] [# last nt]”
### Introns and exons in Genome Browser
In the Genome Browser, introns are expressed as thin lines with arrows on them and exons are expressed as thicker lines. If you hover the mouse over a part of a gene track, then it will tell you the exon or intron number of that transcript. 

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/img1.png>
    <br>Personal Screenshot From Genome Browser: Three Transcript Variants of the CHRAC1 gene
</p>


### Splicing variants in Genome Browser
You might find that when you search up a gene in the Genome Browser, you get multiple tracks corresponding to the same gene (ex. TP53 or CHRAC1 as above). This is because genes can have different mRNA transcript variants. If you click on the track, it will tell you the transcript variant of the gene if there is a variant. To get the canonical sequence only and get rid of transcript variants, you can right click any of the tracks, press “Configure GENECODE V41”, and then click on “splice variants.”
### Obtaining a PDF of your window
You might want a high resolution image of your window or chromosome ideogram for a publication. To do this, we can go to the “View” button on the top and click on “PDF/PS.”
### Highlighting and zooming in the Genome Browser window
To highlight a section of interest in your window, click on the top of the window (around where it says “Scale”) and drag over the entire section of interest. A prompt will then appear which will give you various options to modify that window. Some modifications include highlighting that section with a specific color or zooming into that section.

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/img2.png>
    <img width="50%" src=writeup_photos/img3.png>
    <br>Personal Screenshot From Genome Browser: Section Highlighted from Click and Drag and the Corresponding Pop-up

</p>


### Finding and searching sequences in Genome Browser
In Genome Browser, we can obtain the DNA sequence, mRNA sequence, and protein amino acid sequence (in singular letters) by clicking on any gene of interest in the window and clicking any of the options in the red box of the image below. In our example, we copied the highlighted mRNA sequence and pasted it into the search bar. The search bar uses BLAT to find the best matches for the sequence given and it tolerates some mismatches. If you want to find 2-30 nucleotide matches of a sequence, then you can go to the Mapping and Sequencing dropdown and press “Short Match.”

<p align="center" width="50%">
    <img width="50%" src=writeup_photos/img4.png>
    <img width="50%" src=writeup_photos/img5.png>
    <img width="50%" src=writeup_photos/img6.png>
    <img width="50%" src=writeup_photos/img7.png>
    <br>Personal Screenshots From Genome Browser: (1) Human Gene ZDHHC13 After Clicking It on the Window; 
    <br>(2) Section Highlighted From Its mRNA sequence; (3) BLAT Search Results From mRNA Sequence; 
    <br>and (4) Short Match Under the Mapping and Sequencing Dropdown Which Takes You to Match 2-30 Nucleotides

</p>

## Checking ChIP seq data with genome browser
One important function of the genome browser is as a way to double check that your ChIP-seq data has been sequenced and aligned correctly.  This is a fairly simple process that can save you hours of hassle down the line.  
### BED files
In order to view your aligned data on the Genome Browser, you must first create a BED file.  Every track on the genome browser is defined by an associated BED file.  The format is a tab separated file with at least three fields: chromosome name, start position, and end position.  There are other fields that can be added (see this [UCSC page](https://genome.ucsc.edu/FAQ/FAQformat.html) for more detail), but for our purposes, this is all we need for now.
### Making BED files from BAM files
After aligning our reads, the hard part has been done for us.  The BAM files output by an aligner already contains the chromosome, start, and length of each read, and it is trivial to convert these numbers into the data required for a BED file. The R package bedToBam can do this easily.  From there we can upload our BED file to the genome viewer.  The result should be something like this:
<p align="center" width="100%">
    <img width="50%" src=writeup_photos/img8.png>
</p>
If your data does not look like this, it is an indication that some part of the ChIP-seq pipeline has gone wrong.

<hr>

# Interesting Applications of the Genome Browser
## The phylogenetic network of the SARS-CoV2 genome
By entering the UCSC Genome Browser > Genomes > SARS-CoV-2 (Fig 3.1), two particular tracks visualizes the phylogenetic tree of SARS-CoV-2 viruses, namely the Nextstrain Clades and Mutations. (Fig 3.2)

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.1.png>
    <br>Fig 3.1 UCSC Genome Browser Home Page
</p>

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.2.png>
    <br>Fig 3.2 Nextstrain Tracks
</p>
 
### SARS-CoV-2 Genome
This data is from a project that accumulates SARS-CoV-2 viruses affecting humans from all parts of the world and shows their relationships to each other in a phylogenetic tree based on shared variants. This can be used to trace the transmission pattern of viruses from one place to another.
 
### Nextstrain Mutation Track
The data lines represent places where the isolate does not match the SARS-COV-2 reference. The individual variance that defines a clade can be seen graphically here where the isolates in a particular group have certain variants in common and certain subgroups have certain variants in common that identify them as being related to each other. Red lines represent non-synonymous alternate alleles whilst green lines represent synonymous ones.
 
<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.3.png>
    <br>Fig 3.3 Alternate Alleles
</p>
 
If you compare the colors on the left with the colors in the clades track in Fig 3.4, there is a visible qualitative relationship between the two. Clicking into one of the clades, it opens a list of samples belonging to the clade, including the country of origin of each variant and more. 

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.4.png>
    <br>Fig 3.4 Clades and Mutations Track
</p>


## The role of phylogenetics as a tool in molecular epidemiology of infectious disease
### Traditional Application of Phylogenetics
 
The phylogenetic tree is traditionally used to study the evolutionary paths of organisms and is mostly known for reconstructing the prehistoric population movements of humans and for ecological studies that date back millions of years. (P. Foster et al,. 2020)
 
They can be interpreted by distance from a shared branch point, that represents a divergence event. The evolutionary path can be traced backwards and the ‘relatedness’ of one species or strain from another can be compared by looking at when the divergence event occurred. The closer it is, the more related the two species or strains are. The development of NGS has vastly propagated the accuracy of data used to build phylogenetic trees. 

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.5.png>
    <br>Fig 3.5 Fundamentals of Phylogenetic Trees
</p>

### Application in Virology
 
For the present, phylogenetics has been applied to virological data to monitor the evolution of SARS-CoV-2. This was carried out using GISAID data from across the globe. The network faithfully traces routes of infections for documented coronavirus disease 2019 (COVID-19) cases, indicating that phylogenetic networks can likewise be successfully used to help trace undocumented COVID-19 infection sources, which can then be quarantined to prevent recurrent spread of the disease worldwide. (P. Foster et al,. 2020)
The transmission of disease can been visualized on the world map and can even be played over a set period of time. Check it out at <https://nextstrain.org/ncov/gisaid/global/6m?transmissions=show>

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/fig3.6.png>
    <br>Fig 3.6 Transmission of SARS-CoV-2 by region
</p>

<hr>

# Using ChIP-seq to find probable binding motifs
## FASTQ to BED
After performing NGS on the library prepared in section 2, we will be left with a FASTQ file containing many sequences of DNA, along with the quality scores for each base that has been called.  It should look something like this: (INCLUDE IMAGE EXAMPLE).  It is now time to put this data in the context of the cell.
### Quality Control
Many of the reads that come out of the sequencer will be be low quality.  We have to remove these, as failure to do so will result in both noisy and unreliable results further down the line.  We need to both remove failed reads, as well as remove the tails of almost every read, as current NGS methods are not reliable for sequences longer than about 100 bp. The command line program FASTQC will take our FASTQ files and output a very handy report of the quality of our data.  (Take note: FASTQC functions differently if our sequencer is outputting paired-end or non-paired sequences. Know which you are doing, and check FASTQC documentation to make sure you are properly analyzing your data). From there, use a FASTQ cleaning tool like FQTRIM or FASTQCLEANER to remove bad reads and remove the unreliable ends of your reads.
### Aligning Reads
With our data cleaned, we can finally place the sequences in their correct place in the genome.   Using an alignment tool (i.e. STAR or BWA), we can feed it our FASTQ files (again, make sure you are properly using the paired-end option if your data calls for it) as well as a reference genome that we wish to them to be aligned with.  The output of this will be a BAM file, which is similar to a FASTQ file, except that each line also contains the chromosome number and base number that each read was found to have a match, as well as various other metadata about the quality of the match. 
### BAM files
If you try to read a BAM file, you will have trouble.  The B in BAM stands for “Binary” reflecting the fact that BAM files are the compressed version of the human readable SAM files.  Use a tool like SAMTOOLS in order to check that your BAM files are what you expected them to be.
## Peak Calling
Due to the nature of ChIP-seq, the only reads that will be aligned to the genome are those that were associated with the protein/histone modification of interest during the cross-linking phase.  As a result, when visualized by the Genome Browser, the aligned sequences should look something like this:

In order to computationally make a record of where in the genome that reads have been mapped to, we need to perform peak calling.
The short story of peak calling is that we are essentially using an algorithm to determine which locations with mapped reads are actual binding sites, and which are artifacts of the ChIP-seq pipeline.  The actual algorithm is a complicated statistical analysis ([you can read more here](https://www.mybiosource.com/learn/testing-procedures/peak-calling/)), but the gist is that the more reads aligned to a location, the more likely it is that it is a true transcription factor binding site.  
When it comes to implementation, there are many bioinformatics tools that can be used for peak calling.  The review published by [Jan Gert et al.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2900203/) is a quite comprehensive look at the various options.  For the most part, using them is pretty simple; input aligned BAM file, output is a BED file of highly mapped regions (see the section about BED files).
## Motif enrichment analysis with MEME
Now that we have a list of genomic regions that we know our transcription factor binds to, we can mine the genetic code for the sequences that the transcription factors are likely to interface with. This is done by finding short genetic sequences (motifs) that are more common in the regions we found than they are in the genome at large.  
### Finding Known Motifs
There are databases of motifs that have been found by earlier ChIP-seq experiments.  If all we want is to detect the presence of previously discovered motifs, we can simply check for enrichment of known sequences.
### De Novo Motif Finding
More interesting for us is the finding of motifs that have not been previously identified by past experiments.  This is a much more difficult task for the simple reason that the space of all possible 4 - 10 base pair motifs is much larger (more than 4^10, or over a million) than the set of all previously recorded motifs.  The program will then output a couple given sequences base probabilities.  These sequences are often presented like this example:

<p align="center" width="100%">
    <img width="50%" src=writeup_photos/img9.png>
</p>

Here the height of the letter indicates the likelihood that a given base will appear at that position in the motif.  In terms of transcription factors, this means that the factor uses those bases most strongly to know where to bind, and vice versa.  In the example above, the bases in positions 3-5, 7, 13, 16, 17 were found in this pattern often enough that we can be fairly certain that the transcription factor uses them to recognize the regulatory region.  In contrast, the lack of consensus on 11, 12, 14, and 15, indicates that the structure of the transcription factor allows for a lot of wiggle room in this location. 

### Motif Analysis Software
When it comes to bioinformatics software that perform motif analysis, there are a couple options.  HOMER (developed at UCSD!) is a command line tool with a variety of options for more advanced analysis.  Alternatively, the MEME suite offers a browser based tool for quick motif analysis without having to deal with installation and learning a new tool.  Both of these tools are capable of both known motifs and de novo motif analysis.

# Congratulations!
### You now know how to take ChIP-seq all the way from the sample to the discovery of motifs.  Have Fun!







## References
Benhamed, M., Herbig, U., Ye, T., Dejean, A., & Bischof, O. (2012). Senescence is an endogenous trigger for microRNA-directed transcriptional gene silencing in human cells. Nature Cell Biology, 14(3), 266–275. https://doi.org/10.1038/ncb2443

Ricke, R., & Bielinsky, A.-K. (2005). Easy detection of chromatin binding proteins by the histone association assay. Biological Procedures Online, 7, 60–69. https://doi.org/10.1251/bpo106

UCSC Genome Browser Basics, Part 2: Configuring the Browser. (2020, April 19). Www.youtube.com. https://www.youtube.com/watch?v=cYys5iXN0NY&ab_channel=UCSCGenomeBrowser

UCSC Genome Browser Basics. Part 1: Getting around in the Browser. (2020, April 9). Www.youtube.com. https://www.youtube.com/watch?v=NBDMNv2KFik&ab_channel=UCSCGenomeBrowser

UCSC Genome Browser Basics. Part 3: Configuration + DNA navigation. (2020, May 26). Www.youtube.com. https://www.youtube.com/watch?v=I25Q136d6NU&ab_channel=UCSCGenomeBrowser

UCSC Genome Browser Gateway. (2018). Ucsc.edu. https://genome.ucsc.edu/cgi-bin/hgGateway

Amgen Foundation. (n.d.). Phylogenetic trees | evolutionary tree (article). Khan Academy. Retrieved December 4, 2022, from https://www.khanacademy.org/science/ap-biology/natural-selection/phylogeny/a/phylogenetic-trees

Forster, P., Forster, L., Renfrew, C., & Forster, M. (2020). Phylogenetic network analysis of SARS-COV-2 genomes. Proceedings of the National Academy of Sciences, 117(17), 9241–9243. https://doi.org/10.1073/pnas.2004999117

Illumina. (n.d.). Precise analysis of DNA–protein binding sequences. Chromatin immunoprecipitation sequencing (chip-seq). Retrieved December 4, 2022, from https://www.illumina.com/techniques/sequencing/dna-sequencing/chip-seq.html

NextStrain. (n.d.). Genomic epidemiology of SARS-CoV-2 with subsampling focused globally over the past 6 months. NextStrain. Retrieved December 4, 2022, from https://nextstrain.org/ncov/gisaid/global/6m

Robertson, G., Hirst, M., Bainbridge, M., Bilenky, M., Zhao, Y., Zeng, T., Euskirchen, G., Bernier, B., Varhol, R., Delaney, A., Thiessen, N., Griffith, O. L., He, A., Marra, M., Snyder, M., & Jones, S. (2007). Genome-wide profiles of STAT1 DNA association using chromatin immunoprecipitation and massively parallel sequencing. Nature Methods, 4(8), 651–657. https://doi.org/10.1038/nmeth1068

UCSC. (n.d.). SARS-COV-2 WUHCOR1 NC_045512V2:1-29,903 UCSC genome browser V440. Retrieved December 4, 2022, from https://genome.ucsc.edu/cgi-bin/hgTracks?db=wuhCor1&lastVirtModeType=default&lastVirtModeExtraState=&virtModeType=default&virtMode=0&nonVirtPosition=&position=NC_045512v2%3A1-29903&hgsid=1509952909_LlU0ZKv8W6uv4mXOoPbkxHklv6On

Wilken, M. S., Brzezinski, J. A., La Torre, A., Siebenthall, K., Thurman, R., Sabo, P., Sandstrom, R. S., Vierstra, J., Canfield, T. K., Hansen, R. S., Bender, M. A., Stamatoyannopoulos, J., & Reh, T. A. (2015). DNase I hypersensitivity analysis of the mouse brain and Retina identifies region-specific regulatory elements. Epigenetics & Chromatin, 8(1). https://doi.org/10.1186/1756-8935-8-8 


## Image Credit:

Amgen Foundation. (n.d.). Phylogenetic trees | evolutionary tree (article). Khan Academy. Retrieved December 4, 2022, from https://www.khanacademy.org/science/ap-biology/natural-selection/phylogeny/a/phylogenetic-trees
ChIP-seq: Strand NGS. ChIP-Seq| Strand NGS. (2010, September 29). Retrieved December 3, 2022, from https://www.strand-ngs.com/features/chip-seq 

NextStrain. (n.d.). Genomic epidemiology of SARS-CoV-2 with subsampling focused globally over the past 6 months. NextStrain. Retrieved December 4, 2022, from https://nextstrain.org/ncov/gisaid/global/6m

UCSC. (n.d.). SARS-COV-2 WUHCOR1 NC_045512V2:1-29,903 UCSC genome browser V440. Retrieved December 4, 2022, from https://genome.ucsc.edu/cgi-bin/hgTracks?db=wuhCor1&lastVirtModeType=default&lastVirtModeExtraState=&virtModeType=default&virtMode=0&nonVirtPosition=&position=NC_045512v2%3A1-29903&hgsid=1509952909_LlU0ZKv8W6uv4mXOoPbkxHklv6On
