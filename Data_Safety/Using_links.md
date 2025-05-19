# Overview #

Creating links using the `ln` or the link function can be a great way to more efficiently organize data across your computing resources. There are two types of links that we can create - hard links and soft links. These two different types have their own advantages and disadvantages, which we discuss in more detail below (alternative, see [this explaination](https://www.geeksforgeeks.org/difference-between-hard-link-and-soft-link/)). From a data safety perspective, we can use links to more effectively share data across file systems without having multiple copies of data floating around. We generally want to avoud having multiple copies of working data floating around since this can be more likely to result in errors. An additional reason to avoid this is because of the amount of memory that large NGS datasets can occupy (increasing memory costs $$). Finally copying datasets multiple times increases the chances something goes wrong during the copying process (granted this is unlikely, but one never knows). 

## Hard links ##
When we create a hard link, we are basically creating a new paths to our file of interest, although the file keeps the same inode. In other words, this means the file is two (or more) places at once, but it does not increase memory usage. This means we can view/manipulate/edit the file from either the original or linked location. Additionally, even if the file is deleted from the original location, it doesn't actually delete the file from the system as long as at least one hard link exists. 

There are a few limits to this. Hard links cannot be made across file systems nor can they be used on directories (unless you have the correct permissions ~ usually the owner of the system). 
## Soft links ##
Creating a softlink is more akin to creating a shortcut to a directory/file. Unlike a hard link, soft links can be made across file systems as well as can be made with directories. The soft links do not have the same inode as the file/directory of interest, so this means if the original gets deleted the link becomes non-functional. These sort of links can be especially useful in conjunction with GUI's that are used to visualize file systems (e.g. cyberduck, filezilla, or winSCP). 

# Making the links #
Lets get some practice using the `ln` function. To set things up, we'll create two different directories and then read in an example file into one of our new directories.
```bash
mkdir Dir_1
mkdir Dir_2
cd Dir_1
wget EXAMPLE
```
Now, we'll go ahead and create a hard link between the file we read in the other directory using `ln`
```bash
ln EXAMPLE ../Dir_2/
```
Now, to double check that we successfully created the link, we can switch directory and take a peak with `head`

```bash
cd ../Dir_2
head EXAMPLE
```
Now we are going to illustrate that the file will persist, even if we delete the original
```bash
rm ../Dir_1/EXAMPLE
ls #shows that the example file is still here
head EXAMPLE #prove the example file still looks the same
```
Now, we will go ahead and practice creating a softlink (or short cut) from Dir_2 (where we currently are) to Dir_1 and then use the link to move into Dir_1
```bash
ln -s ../Dir_1 .
cd Dir_1
```

