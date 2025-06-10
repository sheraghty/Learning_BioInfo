# Overview #
This tutorial will go over over some basic ways that we can process and manipulate files in bash. Here we are just going to focus on the basic applications of a few tools, but many of these functions can be used in much more advanced contexts. 

# Getting Started #
The first thing that we need for this tutorial is to have a file that we can manipulate. You can either go to the example files tab in this GitHub and click the download button, or we can use the `wget` function to download our file of interest to our working directory. The latter option is a little quicker, see code below for how to do this. 

```bash
wget https://github.com/sheraghty/Learning_BioInfo/blob/master/Example_files/wnba_24_example.csv
```

The file we just downloaded is the standings from the 2024 WNBA season in the form of a csv file. The file should have four columns for team name, number of wins, number of losses, and winning percentage.

# Whats in the file #
There are a couple of ways that we can look at the contents of a file. We can open it up in a text editor, like we did before with vi, but that is something of a hassel unless we know that we want to edit the file by hand. There are a couple of handy functions that we can employ instead of using `vi`. The first is `head` which will print the first few line of the file to stdout. Alternatively, we can use `tail` which will instead print the last few lines. For both functions the `-n` flag can be used to set how many lines will be printed to stdout. If we want to go through the entire contents of a file, we will need to use the `more` function, which basically lets us scroll through the contents of the file using the `enter` key to move through the file. To exit the file before getting to the end of the file, we simply hit the `q` key. See the code block below for some examples.

```bash
head wnba_24_example.csv #print the first few lines
head -n 5 wnba_24_example.csv #print the first five lines
tail wnba_24_example.csv #Print the last few lines
more wnba_24_example.csv #go through the entire file.
```
# Parsing the file #
## Cut ##
Sometimes we will want to only look at certain parts of the file. For instance, we might only be interested in looking at the team names and the number of wins. To do this, we use the `cut` command which will only print the specified columns to stdout. The mandatory flag for this function is `-k`, which specifies the column(s) that we are interested in. In this case, we will also need to set the `-d` flag. The d stands for delimiter, or in other words, what symbol is being used to separate different columns. The default value for this flag is `tab`, but in this case our example is a comma (,) delimited file so we need to set the flag to be `-d","` (Note, we need to have quotes around the delimiter). If we put this all together, then our command will look like this 

```bash
cut -f1,2 -d"," wnba_24_example.csv
```

## Grep ##
Grep is a flexible tool for looking for lines in a file that match a certain pattern. For instance, if we only wanted to look at the stats of the New York Liberty we could use grep as below.
```bash
grep "New York Liberty" wnba_24_example.csv
#Note we will get the same result if we just use New as our search pattern
grep "New" wnba_24_example.csv
grep -v "New" wnba_24_example.csv #We can also invert the search using the -v flag 
```
