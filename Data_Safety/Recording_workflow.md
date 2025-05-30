# Overview #
It is critical to maintaining a good digital lab notebook that you record the specific order various programs/scripts/software are used. There are several ways that we can do this using a variety of tools and platforms. This vignette will focus on the `history` and `script` functions that are built into most unix distributions. These tools are good for recording what is actually being typed into the terminal, but these tools typically will not give great context for the why behind the action. In order to get this context, its important to write good README files and keep good GitHub repositories where you can write up the entire workflow and provide insight into why you are doing what you're doing. 

# Using the history function #
The unix shell automatically records all of the commands input into the shell using the `history` function. Simply type `history` will bring up a numbered list of all the commands used with higher number indicating the more recent commands. This list can be very helpful to consult when writing up and summarizing your workflows since it provides an exact record of what you did and in what order. See below for an example of how to use history 
```bash
history
history 10 #only shows the 10 most recent inputs
```

We can also use grep to look for specific inputs as well. This is especially useful if the input we are interested in is something that might be buried deep in the history file. See below for an example 
```bash
history | grep "cat" # get instances of when we used the cat command
```

## rerunning previous commands ##
There are a couple of ways that we can rerun a previous command. The easiest way is to press the `up arrow` on the key board which bring up the previous input to the command line. Hitting the up arrow multiple times will continue to go to increadingly older inputs (e.g. hitting the up arrow 10 times brings up the 10th most recent input). Using the up-arrow to bring up old inputs, returns the text to the command line and it can be editted as necessary. As an alternative to the up-arrow, we can also use notation involved the exclaimation point. See code below for examples

```bash
!! #repeat previous input
!-10 #repeat the 10th most recent input
```
This notation can be especially useful if we forget to put the name of the command before the file we want to manipulate. For instance, maybe we want to look at a file with the `cat` function, but we forgot to invoke the command. We can simply fix this as seen below 

```bash
echo "This is an example" > example.txt #make a file with some text to look at
example.txt #this is the file we want to see, but we forgot the appropriate command
cat !!
```

We can also get more specific which commands that we want to rerun. If we use the `history` function, then we get a number listed of the previous inputs. Using this number, we can then repeat a particular command as below 
```
!10 #repeats input numbered 10 in the history file
```
## Modifying the history file ##
There are going to be several situations in which we want to to delete parts of the history file (or the entire thing). The most obvious situation would be if you need to put some sort of sensitive information into the command line (e.g. the password for something). See below for several examples

```
history -d 10 #Delete input number 10
history -d 10 20 #Dlete inputs 10-20
history -d -5 #Delete the last 5 inputs
history -c #clear the entire history file
```

# Using the script function #
The `history` command that we have discussed so far is an excellent way to record what you've done in the terminal since it retains records of all your inputs by default. The biggest limitation of the `history` function is that it only records the input and not things printed to stdout or stderr. If we want to create a more complete record of what we've done in a given shell session, we can use the `script` command which records everything across stdin, stdout, and stderr. Unlike the `history` function, the `script` function needs to be actively turned on and off. See below for an example of how to invoke this function as well as turn it off
```bash
script my_script.txt #this starts the script
#now we'll run a few commands
echo "testing 1 2 3"
pwd
ls -l
exit #this closes the script
cat my_script.txt #Look at what was recorded
```

There are a couple of other settings for the `script` function that might be of interest, see [this article](https://www.geeksforgeeks.org/script-command-in-linux-with-examples/) for more information 
