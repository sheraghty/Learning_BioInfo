# Overview #
In this tutorial, we will go over what a script is, how to make one, and why using scripts is critical to bioinformatic workflow

# What is a script #
In programming, a script is a file that contains a series of instructions that get passed along to computer when the script is executed, instead of the user manually inputting the commands at the command line. Scripts can be written for any programming language, but there are slight differences in the formatting when using scripts of different languages (see below for more details). The most obvious difference is that the programming language a script is written in determines the file extension that is used. For instance, a bash script will typically end in `.sh` or '.bash' whereas a python script ends in `.py`. This lets people quickly identify what language a script is written in without having to open the file up and take a look at the contents. 

In a unix environment (where most bioinformatics is done), scripts will also almost always have a `shebang` on the first line of the file. The `shebang` is used to tell the computer what interpreter should be used to execute the script, or in other words what programming language is being used. When writing a script to be executed in a typical bash shell the shebang used is `#!/bin/bash`. Since this section is focused on bash basics, we will limit ourselves to writing bash scripts.

# How to make a script #
## vi ##
There are a number of ways that one can create a script, but the basic requirement is to use some sort of text editor, either from the command line or using an external program. In this tutorial we will do all of our script writing from the command line using the built in `vi` function, although there are a number of other built in or otherwise easily accesible text editors like `nano` or `vim`. External text editors like notepad++ or BBedit are also fairly easy to use and come with some usful additional features. 

To create a file with vi we simply us the `vi` command followed by what we want to call the file. See the code block below for an example.
```bash
vi my_first_script.sh
```
This will open up a text editor for us to get started with writing our script, however people we can actually type anything out, we need to press the "i" key. Here, i stands for insert and allows us to start editing the file. For this script we will keep it pretty simple and just make it so the script prints "Hello World" on the screen when its executed. See the code block below for what the contents of our script look like.

```bash
#!/bin/bash

echo 'Hello world'
```

After you finish typing the above, its time to exit vi. To do so, you first press the escape key and then type `:wq`. This lets you leave the file and saves your changes. If you wanted to leave the file without saving your changes, then you would type `:!q` instead. 

## Running the script ##
Now our script is almost ready to go, the last thing we need to do is give it permissions to run. Understanding permissions in a computational setting is beyond the scope of this tutorial and is covered in the data safety section. For our purposes here, all we need to know is that we can give the file permission to be executed using the `chmod` command. 

```bash
chmod 755 my_first_script.sh
```
The 755 that comes after chmod is basically giving our script full permissions. Now we can actually go ahead and run our script which we do by typing `./` before the name of the script as seen in the code block below. 

```bash
./my_first_script.sh
```

## Additonal considerations ##
There are a few other things that we want to think about when we are writing scripts. Although the script we wrote in this tutorial was pretty simply, in more advanced scripts we probably will want to make notes for ourselves and other people that might see and/or use our scripts. This is generally refered to as "commenting" and well commented code is essential for making reproducible science and can also help you to remeber why you did something when you go back to look at code that you may have written months or years ago. To leave a comment in a script you just need to use the `#` sign. This basically hides anything that comes after it from being intrepretted by the commputer. For instance, if we edit our script (again using the `vi` command) to the following 

```bash
#!/bin/bash

#echo 'Hello world'
```

Now, try running the script again. Our newly edited program won't return anything. This is referred to as commenting out code and can be useful when trying to fix bugs in complex scripts. If we just wanted to leave a note about what the script does, we would have something like the code block below.
```bash
#!/bin/bash
#This script will print out hello world
echo 'Hello world'
```

Although in this tutorial we did all of our script writing from the command line, there are a number of external text editors like notepad++ or BBEdit that are very useful and have some extra utilities baked in. There are a few things to watch out for when using these sort of external editors however. The biggest concern is, especially for people using windows based machines, is that the line endings  of a script written in a text editor on a windows machine will not play nicely when executing the script in a unix environment (line endings are sort of beyond the scope o this tutorial ~ all we need to know is that there are "invisible" characters at the end of every line in a file and these characters differ between windows and unix machines). Even for folks that are using local machines with a unix based operating system, you can sometimes pick up weird line endings if you're getting code from online. Fortunately there is a very easy fix for this using the `dos2unix` function. Basically this just converts the line endings from a windows format to a unix one. Its a good trick to pullout whenever you are running a script you you get an error message that is talking about line endings. See below for an example of how this command could be used.

```bash
dos2unix my_first_script.sh
```
There is one other, albiet very small, concern when using external text editors. Often times bioinformatics is done using remote computing resources, but our text editors will typiclly save files locally. This means we need to move any scripts that we write with these editors over to our remote computing severs, so they can be used. Moving files around is very easy and there are number of commandline tools or 3rd party softwares that can be used to this end. 
# Why scripts are important #
Now that we have our scripting basics down, we want to consider why scripts are important. Listed below are some of the biggest reasons why writing and using scripts is crucial for bioinformatics, but there are plenty of other benefits that I don't have listed as well.
1. Efficiency - Writing all a series of commands to a script and then executing the script can save a lot of time as well. If you have a script with lots of time intensive steps, something may finish while you are AFK and the next step can't start until your return. 
2. Repoducibility - Saving all of the commands that you've used in a script makes it such that other folks can take the same starting data and easily produce the same results as you did. When running things directly from the command line, it can be easy to forget exactly what you did and can make it difficult to reproduce you work (or when it comes time to write up the methods for a paper). 
