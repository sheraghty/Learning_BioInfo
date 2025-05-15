# Overview #

This tutorial goes over the basics of using a bash shell including how to get to the shell, what the command line is, and finally using a few basic functions. 

# What is the shell #
In computing, a shell is an interface that allows one to interact with the your computers operating system and run various commands and programs (see [this link](https://techterms.com/definition/shell) for a more complete definition). The most common unix shell is Bash, which is what comes with most unix distributions (bioinformatics typically happens in a unix environment). However, there are a number of other unix shells (for instance, Mac users have the zsh shell by default) as well. All of these shells tend to be broadly similar, although there can be important differences. For the purposes of this, and the subsequent tutorials, we will assume that everyone is working in a bash shell, although most things will probably be interchangable between different unix shells. 

## What is the command line ##
The command line is where the user can interactively give commands for the shell to interpret and then execute. The command line is a fairly bare bones, text based method of interacting with the computing. The user types the desired commands into the command line, hits enter and then the computer does its thing.  

# How to get to the shell #
For bioinformatics, we are mostly going to be interested in getting to a unix shell and how we get there will depend on your computers operating system. For people with that map computers running the Mac iOS, this is as simple as opening the terminal app that comes with your computer. For people with windows computers, getting to a unix shell is a little more complicated, but there are two ways we can go about this. Starting with Windows 10, there is now a function where windows users can install a bash shell (see [this tutorial](https://www.geeksforgeeks.org/use-bash-shell-natively-windows-10/) for how to do this). Alternatively, most bioinformatics relies on remote computing resources that are almost always going to have a unix operating system. People with windows machines can install a software called PuTTy and simply connect to their remote resources (and gain access to the shell associated with the remote server). 

# Some basic commands #
Now that we have access to the shell, we can start with some basic commands. Like in most programming tutorials, our first task will be to ask the computer to print the phrase "Hello world" to the screen. However, we first need to define three terms.
1. stdin ~ this refers to text input from the user into the command line
2. stdout ~ this refers to the text output from the machine based on the stdin
3. stderr ~ this refers to text output from the machine that involves any error codes

So in other words our first task will be to figure out what stdin will result in a stdout of "Hello world". 

## echo ##
In Bash when we want to have repeat text from stdin to stdout we can use the echo function. See the code block below for how we can do this. 

```bash
echo "Hello world"
```
If you copied and pasted the above code above into your command line, you should have recieved the "Hello world" message on your screen.

# Directing output #

In many cases, we are going to want the output of a function to be saved in a file and not sent to stdout (note: we are also going to be interested in saving the output of stderr when errors occur since this can make trouble shooting a little bit easier. However, this is a little too advanced for this introduction tutorial, so we will revisit it later). When we want to save the output of a function to a file, we used the `>` character as seen below 
```bash
echo "Hello world" > hello.txt
```
Now you should have a file called hello.txt where the first (and only) line says hello world. Sometimes we want to append the output of a function to a file that already exists. In that case instead of using the `>` character we use `>>`. For instance, if you change the above code to the following:
```bash
echo "Hello world" >> hello.txt
```
and then run it a few times, the hello.txt file will now have multiple lines of "Hello world".
## learning more about functions ##
There are many many useful functions built into the bash shell by default and many more that can easily be installed. Many of these functions will also have settings that can be modified via the use of flags. To learning more about a function and the various settings that can be altered, we can use the `man` function. Man stands for manual and will give a complete describtion of the function as well as all settings and how to change them. See below for an example

```bash
man echo
```
