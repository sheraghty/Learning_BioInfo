# Overview #
In this tutorial, we will be going over how to navigate your computers file structure as well as how to move files around. 

# File system Structure #
The file system of a computer is typically structured in a hierarchical way, in which one directory has many sub directories (directory = folder). For instance, most computers come with a documents folder, which in turn users often times will make many folders within for their various projects. For most people, we move between these various folders with the click of the mouse (e.g. clicking on the folder icon of interest on your desktop screen). When working from the command line, which is a text based interface, this means we cannot navigate around by clicking on icons, rather we need to use built in unix functions. 

# Moving around #
## Where am I? ##
When we first activate our shell, we will typically start off in the home directory. We can double check this by using the `pwd` function, which prints the path to the directory you're in to stdout. When you're in the home directory, this command should return the `~` character, which is the symbol that represents home. See the code block below for how this all should look
```bash
pwd
~ #This is the output you should get
```

## Making new directories ##
Generally speaking, we wont want to do very much in our home directory, rather we will want to create new directories to better organize all of our files. To do this, we use the `mkdir` function, which stands for make directory. This is a fairly straight forward function, as in the code block below. The only real catch with this function is make sure any directory that you're trying to make has a unique name, otherwise you'll get an error (you can however, change the settings to override this using the -p flag. 

When naming both files and directories, it is typically best practice to avoid having any spaces within the name. This is because some programs have difficulty interpreting spaces and this can create headaches down the line. Best practice is to substitute any spaces you might want to have with either a dash (-) or an underscore (_). Alternatively, you can omit spaces altogether and have captial letters indicate new words (e.g. MyFirstDirectory)

```bash
mkdir my_first_directory
```

## changing directories ~ cd ##
Now that we've made our directory, its time to move into it. This is done using the `cd` function, which stands for change directory. See the code block below for how to change directories and how to verify that we've moved using the pwd function.
```bash
cd my_first_directory
pwd
```
If we want to go back to the home directory, we have two different options. We can either use the `~` character as a shortcut to get back or we can use `..` which means to go up directory higher. Both will get the job done and can be used as follows 

```bash
cd ~ #Use the home symbol
cd ../ #go up one
```

### Relative and absolute paths ###
When using the cd command to move directories, we can specify where we want to go using either absolute or relative paths. The absolute path is specified which directory we want to go to with respect to the home directory. For instance, the absolute path for the directory we made above is `~/my_first_directory` (this is also what was returned by the pwd command). The relative path is specified with respect to the directory that you are currently in and is often times much shorter than using the absolute paths. Using the relative paths is quicker if you want to just go up one directory (e.g. `cd ../` or if you just want to move to a subdirectory of the directory that you're currently in (e.g. when we used the `cd my_first_directory` command. To further illustrate this, we can go and make another directory and then move into this new directory.

```bash
mkdir second_dir
cd second_dir
```

Now lets say that we want to go back to the firest directory that we made. I'll illustrate how to use this using both an absolute path and a relative path. 
```bash
cd ~/my_first_directory #absolute path
cd ../my_first_directory #relative path
```
# Moving files #
Now that we are comfortable with making new directories and moving around between them, we want to start moving files as well. For this part of the tutorial, we will stay in `my_first_directory`
## Whats here? ##
The first thing we want to do is figure out what files are in a given directory using the `ls` function, which will list all the files in the current directory. However, since we just made this directory, there isn't anything in it or us to find. The first thing we need to do is make a file to look at, which we can do with the `touch` function to make a blank file as seen below
```bash
touch example.txt
ls
example.txt #This is the output you should see
```
The `ls` function has tons of different options that are very useful, so its a good idea to check out the manual page. The most useful flag (in my opinion) is the -l flag, which changes the output to be in a list format and adds in a lot more information, like file size, permissions, date made, etc. 

## using mv ##
Now that we have a file that we can move around, we will do so using the `mv` function. We need to be careful with this function, because it is a somewhat destructive action, since it does not preserve the the original file. Like with the  `cd` function, when we specify where we want to move our file to, we can use either absolute or relative paths. Unlike the previous commands that we've used, this function requires two inputs - the path to the file we want to move and the destination. See below for an example of how to move out file from the directory we are currently in to the second_dir.
```bash
mv example.txt ../second_dir #moving a file with the relative path
```
The `mv` function also has a second use. We can use it to rename a file. either while moving it to a new directory or while keeping it in the same directory. See below for an example where we make another blank file and change the name.

```bash
touch example_2.txt
mv example_2.txt renamed_file.txt
```
## using cp ##
The other way we often might want to move files around is to copy them into other directories using the `cp` function. This function is similar to `mv` as cp also requires two inputs. Unlike the `mv` function, the `cp` function keeps the file in the original location as well. See below for an example of copying the first file we made and moved into the `second_dir`. 

```bash
cp ../second_dir/example.txt . #Note: the "." character is the relative term for the current directory
```

There are a couple of considerations when copying files (especially if they are large) to multiple directories. Having multiple copies of large files (like the output of next generation sequencing) can take up lots of hard drive space, which is not something that we really want. One way around this is to use the `ln` function to create multiple links to the same file (this is much more memory efficient). This function is a little too advanced to go over in this tutorial, but see [this tutorial](../Data_Safety/Using_links.md) for more details.

