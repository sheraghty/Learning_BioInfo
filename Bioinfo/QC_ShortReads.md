# Overview #
In this tutorial, we will go over some basic quality control steps one can consider when they first begin working with sequencing data. Additionally, we will only be focusing on Illumina short read sequencing in this tutorial. Given this focus, it is important to understand the gist of how Illumina sequencing works. For people that are not familiar with the sequencing process, [Here is a short video](https://www.youtube.com/watch?v=CZeN-IgjYCo) that gives a brief overview on everything that we need to know for this tutorial. Also as a general note, while this is the first quality control step in working with sequencing data, it is certainly not the last. Many data analysis pipeline lines will have further QC checks that are necessary to make sure that the data are suitable 

# Getting a Sense of the Data #
## File Sizes ##
The first step when doing initial quality control on sequencing data is to simply look at the file size of our fastq files. There are a number of possible scenarios that can result in a given sample essentially failing to be sequenced to an adequate level. We can pretty easily tell this by looking to see if any of the file sizes are anomalously low compared to other samples. If there are any such files, the easiest thing to do will be to simply toss them out to prevent them from causing issues in subsequent analyses (although there are some instances where these data may still be useful).  

## FastQC ##
After making sure that our fastq files contain a useful amount of data, we next want to make sure that data is of sufficient quality. Recall that each read in a fastq file is broken down into four parts: the header, the actual DNA/RNA sequence, a `+` sign, and quality scores (See below for an example of what a single read might look like in this format)

```bash
@VH00301:224:AACHLVJM5:1:1101:18459:1076 1:N:0:CGTCATAACT+CAACAACCAT
GCTACCTTTGCACAGTTAATATACTGCGGCTATTTAATTAATCATTGAGCAGACTAGACCTAAAATTATTAACTATAGGACATGTTTTTGTTAAACAGGCGAGAATAAAAATTGCCGTGTTACTTTGCTCAAATTATCTAATCTACTTATT
+
CC;CCCCCCCCC;;CCCCCCCCC;CCCCCCCC;CCCCCCCCCCCCCCCCCCCCCC;;CCCC-CCCCCCCCC;CCCC-C-CCCCCCCCCCCCCC;CCCCCCCCC-CCCC-C;CC-;CC;-;C;CCCCCCC;-;;CC--C;C-CCC-CCCC;C
```

Each position in the read is assigned a quality score as it is sequencing, which basically corresponds to how likely that position is to be "correct". There are some general trends with quality scores that are worth knowing. First, quality scores tend to decrease towards the end of the read, which is due to [a known issue referred to as phasing](https://www.ecseq.com/support/ngs/why-does-the-sequence-quality-decrease-over-the-read-in-illumina). Secondly, reverse reads tend to have worse quality scores than forward reads, which is due to [an issue with amplification](https://www.ecseq.com/support/ngs/why-has-reverse-read-a-worse-quality-than-forward-read-in-Illumina-sequencing). 

We can quickly summarize the per postion quality scores for an entire fastq file using [fastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/). The information provided by fastQC will be useful in the next section of the tutorial where we decide if we need to do any trimming. See below for an example of how to use fastQC from the command line

```bash
./fastqc #if you want to run in interactive mode
./fastqc my_file.fq #If you want to generate an html report for a given fastq file
```

# Trimming #
As we saw in the video linked in the overview section, before the sequencing process beings we ligate adapters to our DNA fragments (we also add in index sequences so we can identify which fragements correspond to which sample). Trimming generally refers to removing these adaptor and index sequences from the DNA fragments of interest as well as removing low quality positions. 

## Should I trim? ##
If you should trim or not depends on what you're using the data for as well as what type of software you're using. [A general rule of thumb](https://dnatech.ucdavis.edu/faqs/when-should-i-trim-my-illumina-reads-and-how-should-i-do-it) is that pipelines that involve read counting don't require trimming whereas pipelines that involve variant calling does require trimming. In the case of the read counting pipelines, many of the aligners have built in ways of automatically "ignoring" adapater/index/low quality sequences. 

## How to Trim ##
After deciding if you need to trim your data or not, the next thing to decide is what trimming software you want to use. There are a number of different options at this point, but we will use [BBDuk](https://archive.jgi.doe.gov/data-and-tools/software-tools/bbtools/bb-tools-user-guide/bbduk-guide/) in this example. BBDuk uses kmer based trimming (see link to BBDuk website for more information) and allows us to trim adaptors as well as low quality bases in the same command. The most important thing to remember when trimming is that we want to make sure that our forward and reverse reads remain identical after trimming (if they aren't, this will cause problems down the line), which means we need to make sure we read in the files together and trim them simulataneously. See below for an example of using BBDuk to remove adaptors and trim low quality reads and for an explaination of what the various flags mean.

```bash
bbduk.sh in1=Example.R1.fq in2=Example.R2.fq out1=Exampled_trimmed.R1.fq out2=Exampled_trimmed.R2.fq ktrim=r k=23 mink=11 hdist=1 tpe tbo ftm=5 qtrim=rl trimq=10 minlen=25
```
* the in and out flags are used to indicate what inputs are and the desired output names
* the ktrim flag is used to indicate if we want to remove 3' or 5' adaptors using the values r or l respectively (in this case we used r)
* the k flag is used to set the kmer size and the max value is the length of the adaptor sequence
* mink
* the hdist flag sets the hamming distance, which in this case allows for there to be a one bp difference between the adaptor reference and the sequence
* tpe requires that the forward and reverse reads are trimmed to the same length
* tbo enables trimming via adaptor overoverlap
* ftm essentially states the the read length needs to end in a multiple of 5 (see BBDuk documentation for why)
* qtrim sets what side the quality trimming is to be done on (in this case the right side)
* trimq sets the minimum quality score for a postion to be retained (i.e. if a position has a quality score of 9 it would be trimmed off)
* minlen sets the minimum readlength to be retained after trimming. In this instance, if trimming would cause a read to be less than 25bp that read would be removed.

There are several other options that we did not use in this example. We can provide a reference file with the adaptors used with the `ref` flag, but BBDuk has some of these adaptors built in by default (see which ones by reading the BBDuk documentation). Additionally, we can also give the software extra memory using something like `-Xmx300g prealloc`, which would allow BBDuk to use 300gb of memory. 

# Optional Sanity checks #
A final quick check that you may do, is to make sure that you recieved the correct sequencing data. If there was an issue on this front (e.g. you sent off bee DNA for sequencing, but your samples got mixed up with those from a fish DNA project), it would quickly become appartent in your downstream analyses (e.g. when the fish reads don't align to your bee reference genome). However, we can do a few quick optional checks before we waste time and resources in later steps. Depending on the type of data you have, you can simply BLAST a few of your reads and make sure you get results that generally match with your expectations (e.g. if you BLAST reads from a bee you sequences, you'd expect BLAST results from other bee species or at the very least other insects). This is just a quick rough check and wouldn't necessarily provide definite proof you got the right data back, but would at least catch any major issues right off the back. 
