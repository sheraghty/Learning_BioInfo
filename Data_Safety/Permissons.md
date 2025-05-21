# Overview #
This tutorial goes over the different sorts of permissions in unix environments and how to change these settings. We will keep things fairly straight forward and only focus on modifying the permissions of files we create so that we (and others) are able to view and look at them. We will also look at the various ways that permissions can be used to protect data from accidental deletion. There are plenty of other more "advanced" ways that permissions can be modified (e.g. permissions being set at the group level and using ACLs).

# Types of permissions #
Normally, there are three types of permission that can be set for a file and/or directory - read, write, and execute. Read permission allows a user to view the contents of a file. Write permission allows a uder to edit the contents of the file (this includes being able to delete the file). Execute permissions allow a user to execute a file, which is only really relevant for script files (basically this allows you to use a script or not). Each of these permissions can be set at three different levels - user, group, and other. The user permissions are *your* settings (e.g. can you read a file). The group setting refers to specific groups of users on a machine. Defining these groups is beyond the scope of this tutorial and isn't really worth bothering with unless you're incharge of a multi-user system. Finally, the others setting is for anyone else that isn't you or in a specified group. 

There are also specicial permissions that can be set. For our purposes, the most relevant special permission is the "sticky bit" which we can use to make it such that only the owner of a directory has the power to delete the files within. This can be a very useful tool for helping to protect data from accidential deletion 

## viewing permissions ##
The easiest way to see the permissions that are set for all files in a directory is to use the `ls -l` where the first column shows the permissions for each file. This column is broken into 10 slots which each slot indicating if the permission being granted to each level. The first slot tells us if there is anything special about the file in question, like if its a directory (denoted by a "d"). The next 9 slots indicate the permssions given the user (slots 2-4), the group (slots 5-7) and other (slots 8-10). For each level, the first slot shows read permission (denoted by an r), the second slow shows write permission (denoted by a "w") and the last slow shows execute permissions (denoted by a "x"). So for example, if a file had the following `-rwxr-x-r-x` this would be that our file of interest had full permissions given to the user and that group and other levels were granted read and execute permissions, but not write permissions. 
# Setting Permissons #

# Special cases #

# Other considerations #
