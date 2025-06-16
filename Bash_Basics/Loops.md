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
