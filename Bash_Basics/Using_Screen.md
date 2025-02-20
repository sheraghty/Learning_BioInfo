# Overview #
This is a tutorial for using the `screen` function to help manage what what programs and scripts you might have running at any given time. Briefly, we will go over how to create and delete screen sessions, why screen is a vital tool for bioinformatics, and how to monitor the status of your scripts.

# What is screen #

# Screen commands #
## Starting and reconnecting ##
## Ending sessions ##

# How to monitor progress #
The easiest way to monitor if a job is running or not is to simply use the `top` function that is built in to most unix distrubtions. This command will give you an activate table showing the various commands that are currently being run on the machine (as well as some that were recently completed). The key things to look for with this table are the last four columns which show `%CPU` `%MEM` `Time+` and `COMMAND`. The `%CPU` column gives reports how much CPU power is actively being using by a given comment with values over 100 indicating multiple CPUs are being used. Likewise the `%MEM` column shows how much memory is being used by a given command. The `Time+` column shows how long a given command has been running for. Although it is important to note that `Time+` is showing total CPU time, which is likely to be different from real time (e.g. if multiple CPUs are running on a given process then CPU time will be > than real time elapsed). Finally the `COMMAND` column shows the program that is actually being run. This column may not present a ton of information depending on the situation. For instance, if you are simply compressing files with something like `gzip` then the `COMMAND` column will say gzip. If you're running a python script, it won't tell you what function is currently being used in python, it will simply say `python`
