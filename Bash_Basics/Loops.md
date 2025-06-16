# Overview #
Loops are a useful programming tool that allows use to iterate the same process multiple times when certain conditions are true. There are three basic types of loops: for, while, and until. This tutorial will go over these basic types as well as how we can combine these different times. 

# For loops #
The for loop allows us to loop over a set range of data or set number of files. The basic format or a a for loop is `for i in RANGE; do echo $i ;done` where the i is the variable that that will take the value of whatever values that we are going to iterate through. There are several ways that we can specify the range that we want to loop over, either specifying values directly or using a range. See below for examples of both. In both bases we are going to print out the numbers 1 through 5 to stdout.

```bash
for i in 1 2 3 4 5; do echo $i ;done
for i in {1..5}; do echo $i ;done
```
Note: For simple loops like those from our frist example, its easy to just write it on a single line. More complex loops will require multiple lines (simple loops can also be written in a multi-line style as well)

For loops don't need to be set up to loop over numbers, they can also loop through a set of strings as seen below
``` bash
for i in ant bee beetle moth butterfly;
do
echo $i
done
```
We can also use regrex to do something like, loop through all of the text files in your current directory
```bash
#Create a few text files
echo "Testing 1" > test.txt
echo "Testing 2" > test2.txt
for file in *.txt;
do
cut -f1 $file
done
```

# While Loop #
A while loop continues to run a given bit of code while a particular condition is true. 

```bash
x=1 #This starts a variable that will be our counter 
while [ $x -le 5 ] #the condition is x less than 5 or equal to 5
do
  echo "$x is a number less than 6"
  x=$(( $x + 1 )) #This adds one more to X
done
```
We can also use a while loop to go through all of the lines of a file. We will practice doing so with our example file that we downloaded in a previous tutorial.

```bash
while read line
do
  echo ${line} 
done < wnba_24_example.csv
```
# Until Loop #
The until loop is more or less the samething as a while loop, but instead of running while something *is* true the until loop runs *until* something is true. 
```
x=1
until [ $x -gt 5 ] #the condition is x less than 5 or equal to 5
do
  echo "$x is a number less than 6"
  x=$(( $x + 1 )) #This adds one more to X
done
```
# Advance looping #
In the first part of this tutorial we just went through the basic types of loops, now we'll go ahead and look at some more advanced options when it comes to constructing loops
## Nesting loops ##
It is possible to have loops within loops. This means for one iteration of the first loop to complete that the entire second loop must be completed. This can be a little confusing to understand, but we can look at the example below to get a better understanding of how this works. Note: I used tabs to make the different loops obvious how they were set up, but you don't need to do this.
```bash
for i in {1..5}; 
do
	for j in {1..5};
	do
		echo "The first/outter loop is on iteration $i and the second/inner loop is on iteration $j"
	done
done
```
## elif statements ##
`elif` stands for else if and these statements are used when we want one action to take place under certain parameters and a different action to take place under different parameters. For instance, if a number if above or below a certain value, we can print different text. 

```bash
numb=120
if [ $numb -gt 100 ]; then
	echo "$numb is greater than 100"
else
	echo "$number is less than 100"
fi
```

We can also implement this into a loop as below

```bash
for i in {1..10}; do
	if [ $i -lt 5 ]; then
 	  echo "$i is less than 5"
	fi
	if [ $i -eq 5 ]; then
	  echo "$i equal to 5"
	fi
	if [ $i -gt 5 ]; then 
	echo " $i is greater than 5"
	fi
done
```
