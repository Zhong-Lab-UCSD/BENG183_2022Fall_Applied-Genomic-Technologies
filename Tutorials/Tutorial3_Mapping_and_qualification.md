# Tutorial3 Mapping and Quantification
In this tutorial you're gonna learn how to map the RNAseq data to a drosophila reference genome and quantify each gene's expression level. 

## 1.Introduction of Reads mapping
http://chagall.med.cornell.edu/RNASEQcourse/Slides_July2019_Day2.pdf

## 2.Different mapping strategy 
### 2.1 Alignment based
### 2.2 Alignment free
More info here: [Alignment-free sequence comparison: benefits, applications, and tools](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-017-1319-7)

## 3.Get raw data and reference sequences ready
### 3.1 Raw data downloading
We will use RNAseq data from [FlyAtlas2 database](http://flyatlas.gla.ac.uk/FlyAtlas2/index.html), which collects hundreds of RNAseq data of drosophila melanogaster. You can search by gene, category or tissue.

The raw RNAseq data can be found on the [resource page](https://github.com/jsolvason/beng183/blob/master/readme.md) for the homework tutorials.

### 3.2 Raw data cleaning and preprocessing
The next step is to trim and clean the raw data using the techniques you learned from [Tutorial 2](https://github.com/Irenexzwen/BIOE183/blob/master/Tutorial2_RawData.md) or Discussion session 3 (See [Canvas](https://canvas.ucsd.edu) Files and Media Gallery for more details).

### 3.3 Reference sequences
You could download reference genome / transcriptome / gtf files of your familiar species from [ENSEMBLE](https://uswest.ensembl.org/info/data/ftp/index.html).
If you are analyzing Human or Mouse, you could also try Genecode.

```Shell
# Download drosophila genome reference sequence 
wget ftp://ftp.ensembl.org/pub/release-97/fasta/drosophila_melanogaster/dna/Drosophila_melanogaster.BDGP6.22.dna.toplevel.fa.gz
gzip -d Drosophila_melanogaster.BDGP6.22.dna.toplevel.fa.gz  # decompress .gz file 

# Download drosophila transctiptome (cDNA) sequence
wget ftp://ftp.ensembl.org/pub/release-97/fasta/drosophila_melanogaster/cdna/Drosophila_melanogaster.BDGP6.22.cdna.all.fa.gz
gzip -d Drosophila_melanogaster.BDGP6.22.cdna.all.fa.gz

# Download drosophila annotation gtf file
wget ftp://ftp.ensembl.org/pub/release-97/gtf/drosophila_melanogaster/Drosophila_melanogaster.BDGP6.22.97.chr.gtf.gz
gzip -d Drosophila_melanogaster.BDGP6.22.97.chr.gtf.gz
```
## 4.Align to the genome and quantification
We will use STAR to align reads to the whole genome.
```Shell
conda install star

# check if STAR has been successfully installed.
STAR -h 

# build index
STAR --runThreadN 16 --runMode genomeGenerate --genomeDir genome_STARidx/ --genomeFastaFiles Drosophila_melanogaster.BDGP6.22.dna.toplevel.fa --sjdbGTFfile Drosophila_melanogaster.BDGP6.22.97.chr.gtf --sjdbOverhang 100
```
(Change the file paths to reflect where the respective files are located on your computer.)

`--runThreadN` Number of threads you use to run on your computer.  

`--genomeDir` The place you want to put your reference. (Make sure the location already exists; the command does not make a new folder.)

`--genomeFastaFiles` The genome fasta file we've just downloaded and uncompressed.  

`--sjdbGTFfile` Gtf file.  

`--sjdbOverhang` Usually equals read length minus 1.  

It might take some time to finish the alignment, and the total Memory usage peak at 10g during this process. If this memory requirement is beyond your computer, you could download the [pre-computed index](https://github.com/jsolvason/beng183/blob/master/readme.md) from our resource page. 

After we build the index, we're gonna map our reads towards the genome.
```Shell
STAR --runThreadN 16 --genomeDir genome_STARidx --readFilesIn female_midgut1_R1_clean.fastq female_midgut1_R2_clean.fastq --outSAMtype BAM SortedByCoordinate --outFileNamePrefix ./female_midgut1_R1_STAR_genome
```
This will give you two important results:
1) A sorted [bam file](https://support.illumina.com/help/BS_App_RNASeq_Alignment_OLH_1000000006112/Content/Source/Informatics/BAM-Format.htm) based on the coordinates.
2) A final \*Log.final.out file that includes mapping results information: total mapping ratio / unique mapping ratio / number of mapped reads etc. 
 
#### Quantify gene expression level using FeatureCount
Once you get the bam file (which records each reads align to which specific locations of the genome), you may want to summarize reads abundance for each gene.   
```Shell
featureCounts -p -a Drosophila_melanogaster.BDGP6.22.97.chr.gtf -T 16 -o female_midgut1_count.txt bam/female_midgut1_R1_STAR_genomeAligned.sortedByCoord.out.bam

```
`-p` Check validity of paired-end distance.  

`-a` Name of an annotation file. GTF/GFF format by default.