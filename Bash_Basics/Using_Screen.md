# Overview #
This is a tutorial for using the `screen` function to help manage what what programs and scripts you might have running at any given time. Briefly, we will go over how to create and delete screen sessions, why screen is a vital tool for bioinformatics, and how to monitor the status of your scripts.

# What is screen #
Screen is a terminal multiplexer, which essentially lets you have multiple concurrently running shells. This is especially useful when you want to either run multiple programs at once or have a task that is going to take a considerable amount of time. Screen allows you to create seperate instantances that are basically standalone terminal/shell session that you can disconnect from and reconnect from at will. This means you can use screen to start a session, run a program that might take a day or two, disconnect and do something else in the interim. This is safer than opening up multiple terminal instances for a few reasons. Its much easier to accidentally close a terminal window and kill whatever process is running when you have multiple instances open. However, with screen you don't have that issue as after you detach from a given session, your program will keep on running even if you close the the terminal window. There are some obvious caveats to this - your screen session will still get terminated if the computer gets turned off or restarted. Additionally, your program can still fail on its own. An important final note, screen is very useful when used on personal machines or certain remote computing platforms. It really is not going to be very useful when using a remote computing cluster that has a workload manager like `SLURM`, so you should be aware of how your computional resources are configured to get the best out of them. 
# Screen commands #
The most important commands are going to be starting, reconnecting, and ending sessions. There are a lot of other functions as well that might be of interest to folks. This is simply meant to be a starting point, but interested people should google around to see all of the useful functions the screen has.
## Starting and reconnecting ##
In order to start a session, the best way is to use the `-S` flag as seen below. 
``` bash
screen -S test
```
This starts a screen session that is named test. You don't necessarily need to name the session, you can simply start a session by typing screen, but giving it a name makes it easier to connect later. When you want to disconnect from a session that easiest way to do this is `Ctrl + a + d`, although you can see the manual page for other ways of doing this. When you want to reconnect, its bascially the same as befor but you use the `-R` flag instead.
```bash
screen -R test
```
## Ending sessions ##
To end a session there are two ways this can be done. If you are already connected to the screens session you wish to end, then you can simply press `Ctrl + d`. If you aren't connect to the session that you want to end, and don't want to connect to it, then you can use the following `screen -X -S test kill`

# How to monitor progress #
The easiest way to monitor if a job is running or not is to simply use the `top` function that is built in to most unix distrubtions. This command will give you an activate table showing the various commands that are currently being run on the machine (as well as some that were recently completed). The key things to look for with this table are the last four columns which show `%CPU` `%MEM` `Time+` and `COMMAND`. The `%CPU` column gives reports how much CPU power is actively being using by a given comment with values over 100 indicating multiple CPUs are being used. Likewise the `%MEM` column shows how much memory is being used by a given command. The `Time+` column shows how long a given command has been running for. Although it is important to note that `Time+` is showing total CPU time, which is likely to be different from real time (e.g. if multiple CPUs are running on a given process then CPU time will be > than real time elapsed). Finally the `COMMAND` column shows the program that is actually being run. This column may not present a ton of information depending on the situation. For instance, if you are simply compressing files with something like `gzip` then the `COMMAND` column will say gzip. If you're running a python script, it won't tell you what function is currently being used in python, it will simply say `python`

Depending on if there are other users on your computing platform, you can use the `-u` flag with top to see the processes being run by a given user. For example `top -u Sam`

Alternatively, we can also use the `htop` to look at what processes are running and how many resources are being used. There function can provide a good bit more information for users as well as things that can be customized. See [this article](https://www.howtogeek.com/how-to-use-linux-htop-command/) for some more information.
