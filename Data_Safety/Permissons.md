# Overview #
This tutorial goes over the different sorts of permissions in unix environments and how to change these settings. We will keep things fairly straight forward and only focus on modifying the permissions of files we create so that we (and others) are able to view and look at them. We will also look at the various ways that permissions can be used to protect data from accidental deletion. There are plenty of other more "advanced" ways that permissions can be modified (e.g. permissions being set at the group level and using ACLs).

# Types of permissions #
Normally, there are three types of permission that can be set for a file and/or directory - read, write, and execute. Read permission allows a user to view the contents of a file. Write permission allows a uder to edit the contents of the file (this includes being able to delete the file). Execute permissions allow a user to execute a file, which is only really relevant for script files (basically this allows you to use a script or not). Each of these permissions can be set at three different levels - user, group, and other. The user permissions are *your* settings (e.g. can you read a file). The group setting refers to specific groups of users on a machine. Defining these groups is beyond the scope of this tutorial and isn't really worth bothering with unless you're incharge of a multi-user system. Finally, the others setting is for anyone else that isn't you or in a specified group. 

There are also specicial permissions that can be set. For our purposes, the most relevant special permission is the "sticky bit" which we can use to make it such that only the owner of a directory has the power to delete the files within. This can be a very useful tool for helping to protect data from accidential deletion 

## Viewing permissions ##
The easiest way to see the permissions that are set for all files in a directory is to use the `ls -l` where the first column shows the permissions for each file. This column is broken into 10 slots which each slot indicating if the permission being granted to each level. The first slot tells us if there is anything special about the file in question, like if its a directory (denoted by a "d"). The next 9 slots indicate the permssions given the user (slots 2-4), the group (slots 5-7) and other (slots 8-10). For each level, the first slot shows read permission (denoted by an r), the second slow shows write permission (denoted by a "w") and the last slow shows execute permissions (denoted by a "x"). So for example, if a file had the following `-rwxr-x-r-x` this would be that our file of interest had full permissions given to the user and that group and other levels were granted read and execute permissions, but not write permissions (the `-` character indicates no permissions). 
# Setting Permissons #
The easiest way to set permissions is to use the `chmod` command. There are two different notations for setting pemissions ~ symbolic and octal. 
## Symbolic ##
When using symbolic notation, the general formula for altering permissions is to first decided who we are modifying the permissions for using the following symbols: u ~ user, g ~ group, and o ~ other. We then need to set if we will be adding permisions or taking away permissions using the + and - characters respectively. Finally we need to set what permissions we are giving using the r,w,x characters for read, write, and execute respectively. So for instance, if we want to give the user execute permissions for our file (we'll call this file example.txt), then we would use the following command. 
```bash
chmod u+x example.txt
```

We can also set permissions for multiple levels at once as follows.
```bash
chmod ugo+x example.txt #give execute permissions to everyone
```

## Octal ##
When using octal notation, we use a numeric value to set permissions for all levels at once. Each permission has a specific value with read = 1, write = 2, and execute = 4. We then take the sum of the values of each permission we want to give for a given level (e.g. if we want to give a particular level full permissions, then the value is 7). The argument that we feed into the chmod funtion is ultimately going to be a three digit number, where the first number is permissions for the user, the second digit for the group, and the third digit for other. If we wanted to give all permissions for the user and read and execute permissions for the group and other levels, then the octal notation would be 755. See below for an example of how to do this with chmod as above

```bash
chmod 755 example.txt
```

Personally, I prefer using this notation, because it is a little bit cleaner and requires fewer characters (less of a chance for typos) when setting permissions at all levels. Both notation types are functionally equal otherwise.
# Special cases #
There are a number of different ways that we can modify permissions outside of what we have already covered in this tutorial. However, we really don't need most of these extras, although see [this article](https://www.geeksforgeeks.org/set-file-permissions-linux/) if you're interested. The only special case we are going to look at is the `sticky bit`, which is a special permission that can be set on a directory that makes it such that the contents of that directory can only be deleted/renamed by the owner. This is useful in helping to protect data folders, and can be set as follows 
```bash
chmod +t my_directory
```

# Other considerations #
There are a couple of extra things that we are going to want to consider when thinking about permissions, especially when using shared computational resoruces. Typically the owner of a system has "root" or administrator privileges that lets them supercede the permissions set up others in many cases. Having root priviledges is mostly useful for installing various softwares, but it can also be useful if someone accidentally locks themselves out of a directory or file. If you are working on a personal labtop, then you likely have access to root priviledges, but if you're working on a shared resource, its likely you will not have such priviledges.  
