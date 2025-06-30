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

gzip ordinarily only uses a single CPU, however, we can alternatively use `pigz` which enables us to use multiple CPUs in parallel to achieve much faster compression/decompression times. Unlike gzip, you'll likely need to install this software separately. 
## xz ##
xz utils is another lossless method of data compression that can achieve higher compression ratios than other tools, like gzip, but may be slower. Like gzip, this tool can only be used on individual files, not on directories. Files compressed using this tool end in the .xz extention. We can also add the `-c` flag if we want to push the compressed/decompressed file to stdout instead of a file.

```bash
xz example.txt
xz -d example.txt.xz #Alternatively unxz example.txt.xz
```
Like gzip, there is also an additional software, `pixz` that we can download to enable multi-CPU processing.
## zip ##
The `zip` command is a commonly used lossless method for the compression of multiple files/folders. This is also useful in moving files across different operating systems (e.g. unix versus windows). 
## tar ##
This is also a method for compressing multiple files together, but unlike zip, it requires several steps for compression (although they can be issued in the same command). A tarball (a .tar file) produced by the `tar` command is not actually compressed yet, the tarball only represents the files that have been combined into a single file. Typically compression is added using `gzip`. Overall a gziped tarball can achieve a higher compression ratio than using `zip`, but it is a little more complicated to use. 
# How to interact with compressed data #
Generally speaking after data is compressed, it is no longer human readable (this is in part how the compression is achieved). This means if we want to interact with data after its been compressed, we need to use some sort of tool that makes the data readable. One way would be to simply uncompress the data, although frequent compression/decompression is probably inefficient. If we want to do some basic manipulations of single compressed files, we can use things like `xzcat`, which works exactly like the `cat` command, but is compatable with xz compressed data. In the context of bioinformatics, many common programs like `STAR` or `BWA` can work with gzipped data as well. In instances where we want to use compressed data in a function that doesn't ordinarily accept it, we can use a subshell to decompress the data and feed it directly into whatever command we are interested in using. See the code block below for an example of this. 
