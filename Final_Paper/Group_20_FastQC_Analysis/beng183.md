# FastQC Analysis

FastQC is an important and easy to use tool for quality control on raw input data. It can import data from SAM, BAM, and FastQ files and create an HTML file presenting information about the read quality and sequences of the input file. The FastQC report features several diagrams that represent different metrics of read quality specific to the input file. In this section, each of these metrics will be discussed in detail, including how to interpret their associated diagrams.

## How to use FastQC

FastQC can be used in two different ways depending on your operating system or general preference. Either can be downloaded as an application (Fig 1.) or as a java application that can be used in multiple coding environments.

![Image](fastqc_hp.png)
- ###### **Figure 1**: FastQC desktop application start screen (1)

When using the java application, the following command produces a FastQC HTML file when given a FastQ, SAM or BAM file as input:

`fastqc file.fastq|bam|sam`  
- Command to produce fastqc files from reads

For example, if the input file were named "my_bam_file.bam", the proper command would be:
`fastqc my_bam_file.bam`
If there are multiple files that need to be independently analyzed by FastQC, the filenames can simply be listed one after the other, with spaces to separate them:

`fastqc my_fastq_file1.fastq my_fastq_file2.fastq my_fastq_file3.fastq`

Running the above command would result in a set of FastQC quality control reports, one for each input file (1).

If something other than the standard FastQC report is needed or if different options need to be specified for a run, the following command opens the FastQC help file which contains detailed descriptions of all FastQC program options (1):`fastqc -h`   


# FastQC results: what makes a good vs. bad report?

![Image](new_fastqc_summary.png)
- ###### **Figure 2**: Two FastQC summaries side by side. The first summary has all green checks (2). The second summary includes green checks, yellow exclamations, and red crosses (3).

## Phred Quality Score

Before we dive into each figure produced by FastQC,we must first talk about an important score used to grade each read's quality. When illumina sequencing produces a FastQ file, each base 
pair includes a character score (Fig 3.). 

![Image](new_fastq_line.png)
- ###### **Figure 3**: An example of a cluster in a FastQ file. The first line designates the sequence id, the second line is the sequence, the third line is a plus sign and the final sequence is the corresponding score for each base pair.

This score is called the Phred Quality Score and is designated by ASCII+33 characters. This means that the score starts at the thirty third character in an ASCII table, the exclamation point (Fig 4.). 

![Image](asciipq.png)
- ###### **Figure 4**: Phred Score Table for new Illumina(4). Q is the score value, P_error is the chance of error, and ASCII is the number in ASCII and the character corresponding with it.

These scores are associated with equations and the idea is the higher the Q score, the less likely the base pair is wrong. For example, if your base pair has a score of 30, then there is a 99.9% chance that it is the correct base pair. This score is used throughout FastQC, most importantly in Per Base Sequence Quality graphs.

## Basic Statistics

![Image](basic_stats.png)
- ###### **Figure 5**: An example of Basic Statistics

Basic Statistics is the first figure in the FastQC file (Fig. 5). It is self explanatory, with a table featuring two columns, Measure and Value and the subsequent title for each measure and the value associated with that measure. It includes the filename, the file type, the type of encoding, the total number of sequences, the number of sequences flagged for poor quality, sequence length and percent of GC content.
## Analyzing FastQC Output: Per Base Sequence Quality

A key FastQC metric that should be accounted for is **per base sequence quality**. Per base sequence quality refers to the Phred quality score at each position in a read (see Fig. 6 for graphs). FastQC summarizes this information in graph form, with the X axis corresponding to what position the base is in the read, and the Y axis corresponding to the quality score. So, the values at position “1” on the X axis would represent the distribution of Phred quality scores for the first base of a read, across every read.


Other notable features of this graph are listed below (see Fig. 6):
1. **Yellow Boxes**: The yellow boxes at each position encompass the middle 25th to 75th percentile of the quality score distribution at that position.
2. **Whiskers**: The whiskers on each side of a yellow box represent the data outside the middle 25th to 75th percentile. Both the size of the yellow boxes, and the size of the whiskers indicate how spread out the quality scores are from each other
3. **Red line**: The red line in each yellow box corresponds to the median quality score for that base position

### Per Base Sequence Quality: Good vs Bad Report

Below is an image depicting two FastQC Per Base Sequence Quality outputs: a "good" one (left), and a "bad" one (right).
![Image](good_bad_qs.png)
- ###### **Figure 6**: (Left) A good per base sequence quality plot that passes this module (13). (Right) A poor per base sequence quality plot that fails this module (13).

When put side-by-side, it is clear why the left graph is better. All of the quality scores, even the biggest outliers, are above 30. On the right graph, we can see that even the middle 50% for the distribution of many positions is below 20 (the red zone). 

So, if our output looks like the graph on the right, do we have to throw out our data and generate new reads? No, of course not: we can utilize **read trimming**!

### Trimming Poor Reads

Looking again at the "good" vs "bad" graph outputs, we can see that there is a trend reflected in both of these graphs (although much more clearly in the right one). **The read quality scores tend to become poorer near the end of reads**. This is a common artifact of read collection, and can result in seemingly awful quality distributions. So, to remove this experimental noise, we can remove these poor quality end positions from our reads.

**Read Trimming**: To remove these poor quality bases, various existing bioinformatics packages can be utilized. One such package is *Scythe*, which uses a machine-learning based algorithm to classify regions that drop off significantly in quality and are likely experimental artifacts. After applying one of these tools to our fastq file and then generating a new FastQC report, we should see a significant reduction in steep drop-offs near the end of these graphs. A sample before and after graph can be seen below.

![Image](trimmed.png)
- ###### **Figure 7**: A per base sequence quality plot before (left) vs. after (right) quality trimming (14). We can see the quality improve significantly after trimming.

## Per Tile Sequence Quality

This figure will only be available if the file has the Illumina sequence identifiers, however, it is a helpful image in figuring out possible areas of issue in the flow cell. This figure is better known as a heatmap, with the cooler colors (shades of blue) representing bases with a quality higher than the average and the warmer colors (red, yellow, orange) representing reads with quality worse than the average read of the sequence (5).
An ideal Per Tile Sequence Quality heatmap would be entirely dark blue, unlike Figure 8 which includes both good and bad reads and where they are located (Fig. 8).

![Image](tile.png)
- ###### **Figure 8**: Quality per tile heatmap example (5). There is an area of the flow cell that is producing lower quality reads.

## Per Sequence Quality Scores

Per Sequence Quality Score graphs represent quality scores over all the sequences with the red lining representing the average quality per read. The Y axis is the number of reads and the X axis is the quality score. 

A good library has an exponential graph, ideally with a peak at a quality score greater than 35 (Fig. 9). This would mean the majority of base pairs are statistically likely to be correct. A bad library peaks early or has many peaks, at lower quality score values. 

![Image](psqs.png)
- ###### **Figure 9**: The first graph shows a worse average quality with more than 1000 reads having a score of around 16 to 20 with the read quality falling off afterwards (6). The second graph shows high quality reads with nearly all reads with a quality score of 38.

## Per Base Sequence Content

Per base sequence content demonstrates the percent of each base is featured in the library. A correct library would have the percent for each being around the same value and the lines staying parallel over all base pairs (Fig. 10). A graph that has bias in the library has spikes and dips which can result in the system giving a warning or error. If there are peaks, it means there can be overrepresented sequences (7).

![Image](pbsc.png)

- ###### **Figure 10**: The first graph features parallel lines and similar percentages (7). The second graph has great peaks at the beginning which shows bias, but evens out later in the graph.

## Per Sequence GC Content

Overall GC content distribution is another important metric to take into account. When the GC distribution over all sequences is plotted, it should look roughly normally distributed. In the graphs below, the blue line represents the known distribution of GC content for an organism, and the red line shows how the experimental reads fit to this distribution.

![Image](gc.png)
- ###### **Figure 11**: (Left) Good GC content distribution. (Right) Bad GC content distribution.(6)

The left graph above is an example of a “good” GC content distribution, whereas the graph on the right is a “bad” example. In the “bad” graph, we can see that certain sections of the red line fit relatively well with the theoretical distribution, however multiple peaks that stray far from the theoretical distribution are also present. These peaks are often due to experimental contaminants (8).

## Per Base N Content

Per base N content gives information about whether there are any uncalled bases in the input read library. The symbol “N” is used to represent an uncalled base, and the corresponding plots show % N content for each base pair position in the reads.

![Image](n_content.png)
- ###### **Figure 12**: a) A good per base N content plot (2). b) A decent, but not ideal, per base N content plot (3). 

A good read library should have very little, if any, uncalled bases. In the best case, the per base N content plot shows a completely flat line staying at 0% N content throughout all base pair positions (Fig. 12a).

An elevated percentage of uncalled bases (Fig. 12b) may be seen in a read library where the sequencer was unable to make one or more base calls with sufficient confidence (9). In our example, the module still passes, but the user might find the slight peak between base pairs 25 and 31 worth investigating.


## Sequence Length Distribution

![Image](lengthd.png)
- ###### **Figure 13**: A good sequence length distribution plot for a read library with reads of length 40 (2).

The sequence length distribution module informs on the length of the reads in the input library. Before any modifications are made to the original library e.g. read trimming, all read lengths should most likely be the same. However, different read lengths are standard for some sequencing platforms so plots that differ from the example are not necessarily indicative of a sequencing error (10). In the above example, the plot indicates that all read lengths are the same as there is a single peak at sequence length 40, so this would be a good result if the corresponding sequencing platform produced reads of uniform length. If the user subjects their initial read library to read trimming (as discussed previously), they might expect to see different plots between runs.

## Sequence Duplication Levels

![Image](sdl.png)
- ###### **Figure 14**: a) A good sequence duplication plot (2). b) A bad sequence duplication plot (3). 

Sequence duplication levels provide information on how unique the sequences in a library are. Most sequences will only occur once. The title of the plot indicates what percentage of sequences are unique by detailing the percentage of sequences that would remain if the library were deduplicated.

In the good example, we can see a peak at 1 which indicates that most sequences are unique as they are only found once (Fig. 14a). There is a minor peak at 10 which may be worth investigating but it is also possible to see naturally occurring duplicate sequences in the genome, so the module still passes.

In the flagged example, we can see that only about 70% of sequences are unique (Fig. 14b). There are peaks at 10 and 1000 duplications which indicates something problematic in the library, most likely either the result of technical duplicates from PCR artifacts or naturally occurring biological duplicates (11). There is no way to distinguish between these two origins of duplication based only on the sequences and as such both instances will be reported. 

## Overrepresented Sequences

![Image](ose.png)
- ###### **Figure 15**: A flagged overrepresented sequences module (3).

The overrepresented sequences module looks for individual sequences that are overrepresented in the library i.e. represent more than 0.1% of the total sequences. 

For a read library which passes the overrepresented sequences module, the user will only see a message which indicates that no overrepresented sequences were found.
If the module has a warning associated with it, there is at least one sequence that makes up >0.1% of the read library, and if the module fails, there is at least one sequence that makes up >1% of the read library (12). In the flagged example, we can see that there are a number of sequences that make up more than 0.1% of the library (Fig. 15). The table provides the overrepresented sequence itself, the number of times it is observed in the library, the percentage of the library it composes, and the possible source or contaminant that led to the overrepresentation of the sequence. Most of the sources in this example are unknown. 


## Conclusion

Checking read quality with FastQC is quick, easy and good practice regardless of whether the quality report turns out good or bad. Read quality control comes in handy in any experiment that requires raw sequencing data as an input or an output e.g. DNA sequencing, RNA sequencing, ChIP-seq, differential expression analysis, functional enrichment analysis and Hi-C.

If the quality report gives mostly positive feedback, the user can feel confident about moving onto the next step of their experiment. FastQC can serve as a checkpoint once the results of an experiment are attained, and the scientist can rule out the possibility that any results seen are the result of a poor sequencing run. If the quality report gives negative feedback, the user can use it as a guide to uncover potential errors or biases in the experiment and mitigate them before next steps obscure their source.

## References
1. Andrews, S. (n.d.). Babraham Bioinformatics - FastQC a quality control tool for high throughput sequence data. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/  
2. Andrews, S. (n.d.). GOOD_SEQUENCE_SHORT.TXT FASTQC report. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/good_sequence_short_fastqc.html#M6 
3. Andrews, S. (n.d.).BAD _SEQUENCE_SHORT.TXT FASTQC report. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/bad_sequence_fastqc.html#M6
4. Edgar, R. (n.d.). Quality (phred) scores. Retrieved December 6, 2022, from https://www.drive5.com/usearch/manual/quality_score.html   
5. Andrews, S. (n.d.). Per Tile Sequence Quality. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/12%20Per%20Tile%20Sequence%20Quality.html 
6. FASTQC Tutorial & FAQ.Michigan State University. (n.d.). Retrieved December 6, 2022, from https://rtsf.natsci.msu.edu/genomics/tech-notes/fastqc-tutorial-and-faq/  
7. Andrews, S. (n.d.) Per Base Sequence Content. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/4%20Per%20Base%20Sequence%20Content.html 
8. Andrews, S. (n.d.). Per Sequence GC Content. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/5%20Per%20Sequence%20GC%20Content.html
9. Andrews, S. (n.d.). Per Base N Content. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/6%20Per%20Base%20N%20Content.html 
10. Andrews, S. (n.d.). Sequence Length Distribution. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/7%20Sequence%20Length%20Distribution.html 
11. Andrews, S. (n.d.). Duplicate Sequences. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/8%20Duplicate%20Sequences.html
12. Andrews, S. (n.d.). Overrepresented Sequences. Retrieved December 6, 2022, from https://www.bioinformatics.babraham.ac.uk/projects/fastqc/Help/3%20Analysis%20Modules/9%20Overrepresented%20Sequences.html 
13. Assessing read quality. Assessing Read Quality – Data Wrangling and Processing for Genomics. (n.d.). Retrieved December 6, 2022, from https://datacarpentry.org/wrangling-genomics/02-quality-control/
14. FASTQ utilities. Fastq Utilities - PATRIC Documentation. (n.d.). Retrieved December 6, 2022, from https://docs.patricbrc.org/tutorial/fastq-utilities/fastq-utilities.html 

Note: All graphs and images not cited were produced by Joseph Vellutin. He could not figure out how to include his produced FastQC file, but can send it if requested