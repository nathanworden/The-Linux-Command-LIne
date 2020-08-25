# The Linux Command Line

[toc]

## Chapter 1 What is the Shell?

- Press the up-arrow key for Command History
- The book said don't use `Ctrl-c` and `Ctrl-v` because they don't work. But they do. Huh?
- Simple commands:
  - `date`
  - `cal`
  - `df` - shows the current amount of free space on your disk drive
  - `free` - shows the amount of free memory. (This didn't work for me).
  - `exit` - end a terminal session



## Chapter 2 Navigation

- `pwd` - print the name of the current working directory
- `cd` - change directory
- `ls` - list the directory contents

Linux organizes its files in what is called a hierarchical directory structure. This means they are organized in a tree-like pattern of directories.

Storage devices are attached (aka mounted) at various points on the tree according to the whims of the system administrator.

**Changing the Current Working Directory**

- Type `cd` followed by the pathname of the desired working directory.
- We can specify pathnames in either *absolute pathnames* or *relative pathnames*
- An absolute pathname begins with the root directory and follows the tree branch by branch until the path to the desired directory or file is completed.
- A relative pathname starts from the working directory. To do this it uses a couple of special notations to represent relative positions in the file system tree. The notations are '.' and '..'
  - The "." refers to the working directory and the ".." refers to the parent of the working directory.

**Some Helpful Shortcuts**

| Shortcut      | Result                                                       |
| ------------- | ------------------------------------------------------------ |
| cd            | changes the working directory to your home directory         |
| cd -          | changees the working directory to the previous working directory |
| cd ~user_name | Changes the workign directory to the home directory of *user_name* |

## Exploring the System

- `file` - Determine file type
- `less` - View view contents
- `ls` - List Directory contents
  - You can specify multiple directories: `ls ~ /usr` In this example we list both the user's home directory (symbolized by the "~" character) and the /usr directory.
  - You can change the format output to reveal more detail using `ls -l`

**Options and Arguments** 

Commands are often followed by one or more options that modify their behavior, and further, by one or more arguments, the item upon which the command acts. Most commands look kind of like this:

```bash
command -options arguments
```

**Determinig a File's Type with file** 

```bash
file filename
```

**Viewing File Contents with `less `**

```bash
less filename
```

```bash
less /etc/passwd
```

