# Overview #
This tutorial will go over the basics of data compression and how we can use this to better use computational resources for long term storage of data. 

# What is data compression #
All types of compression involve applying some sort of algorithm to take a file and make it occupy less space than the original using one of two generally approaches - lossless and lossy. Lossless compression essentially works by removing redundant information from a file whereas lossy involves removing information that isn't needed/important. Compression is essential in bioinformatics because we are often times going to be working with large datasets that are 100's of gigabytes and only have limited storage available.

# Common tools #
There are many different compression tools that are available for us to use. This tutorial will go over a couple of the ones commonly used, but if you're interested there are plenty of resources online.
## gzip ##
gzip is a lossless compression method, which is built into most unix distributions. Files that have been compressed in this way end in the `.gz` file extension. This is generally a fairly quick method for compression, although it is not the most efficient in terms of reducing file size. Many common bioinformatic tools are able to accept gzipped files as input, making this a useful compression tool for short to medium term storage of data. See below for an example of how to compress and decompress files. 
```bash
gzip example.txt
gunzip example.txt.gz
```
## xz ##

## zip ##

## tar ##
# How to interact with compressed data #
