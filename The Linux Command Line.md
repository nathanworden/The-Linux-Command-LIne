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

## Chapter 4 - Manipulating Files and Directories

```bahs
cp  - copy files and directors
mv  - move/rename files and directors
mkdir - create directors
rm - remove files and directories
ln - Create hard and symbolic links
```

These five commands are among the most frequently used Linux commands. They are used for manipulating both files and directories.

While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs.

Example:

Copy all the HTML files from one directory to another but only copy files that do not exist in the destination or are newer than the versions in the destination directoy.

```bash
cp -u *.html destination
```

**Wildcards**

The shell provides special characters to help us rapidly specify groups of filenames. These special characters are called wildcards. Using wildcars (also known as globbing) allows us to select filenames based on patterns of characters.



| Wildcard      | Meaning                                                      |
| ------------- | ------------------------------------------------------------ |
| *             | Matches any characters                                       |
| ?             | Matches any single character                                 |
| [characters]  | Matches any character that is a member of the set characters |
| [!characters] | Matches any character that. is not a member of the set characters |
| [[:class:]]   | Matches any character that is a member of the specified class |

Commonly Used Character Classes:

| Character Class | Meaning                            |
| --------------- | ---------------------------------- |
| [:alnum:]       | Matches any alphanumeric character |
| [:alpha:]       | Matches any alphabetic character   |
| [:digit:]       | Matches any numeral                |
| [:lower:]       | Matches any lowercase letter       |
| [:upper:]       | Matches any uppercase letter       |

Wildcard Examples

| Pattern                               | Matches                                                      |
| ------------------------------------- | ------------------------------------------------------------ |
| *                                     | All files                                                    |
| g*                                    | An file beginning with "g"                                   |
| b*.txt                                | Any file beginning with "b" followed by any characters and ending ending with ".txt" |
| Data???                               | Any file beginning with "Data" followed by exactly three characters |
| [abc]*                                | Any file beginning with either an "a", a "b", or a "c"       |
| BACKUP. [ 0 - 9 ] [ 0 - 9 ] [ 0 - 9 ] | Any file beginning with "BACKUP" followed by exactly three numerals |
| [[:upper:]]*                          | ANy file beginning with an uppercase letter                  |
| [![:digit:]]*                         | Any file not beginning with a numeral                        |
| *[[:lower:]123]                       | Any file ending with a lowercase letter or the numerals "1", "2", or "3" |

**mkdir - Create Directories**

```bash
mkdir directory...
```

**cp - Copy Files and Directors**

```bash 
cp item1 item2
```

**Useful Options and Examples for `cp`** 

| Option | Long Option   | Meaning                                                      |
| ------ | ------------- | ------------------------------------------------------------ |
| -a     | --archive     | Copy the files and directories and all of their attributes, including ownerships and permissions. Normally, copies take on the default attributes of the user performing the copy. We'll take a look at file permissions in Chapter 9 "Permissions" |
| -i     | --interactive | Before overwriting an existing file, promt the user for confirmation. If this option is not specified, cp will silenty (meaning there will be no warninig) overwrite files. |
| -r     | --recursive   | Recursively copy directories and their contents. This option (or the -a) option is required when copying directories. |
| -u     | --update      | When copying files from one directory to another, only copy files that either don't exist or are newer than the existing corresponding files, in the destination directory. This is useful when copying large numers of files as it skips files that don't need to be copied. |
| -v     | --verbose     | Display informative messages as the copy is performed.       |





## Chapter 7 Seeing the World as the Shell Sees It

Expansion and quoting are one of the most important subjects to learn about the shell. Without proper understanding of expansion, the shell will always be a source of mystery and confusion, with much of its potential power wasted.

- The "magic" of the `Enter` key

```bash
echo
```

- When you type a command and press the `Enter` key, `bash` performs several substitutions upon the text before it carries out our command. 
- Expansion is when we enter something and it is expanded into someting else before the shell acts upon it.
- `echo` is a shell builtin that prints arguments on standard output.

```bash
echo this is a test
```

- If you say `echo *` you get a printout of the files in your current working directory.
- The shell expands the `*` into something else, in this instance, the names of the files in the current working directory. When the `Enter` key is pressed, the shell automatically expands any qualifying characters on the command line before the command is carried out, so the `echo` command never saw the `*`, only its expanded result.

**Pathname Expansion**

- The mechanimsm by which wildcards work is called pathname expansion. 

- Given a home directory that looks like this:

  ```bash
  [me@linuxbox ~]$ ls
  Desktop ls-output.txt Pictures Templates Documents Music Public Videos
  ```

  You can carry out the following expansions:

  ```bash
  [me@linuxbox ~]$ echo D* Desktop Documents
  ```

  ```bash
  [me@linuxbox ~]$ echo *s
  Documents Pictures Templates Videos
  ```

  ```bash
  [me@linuxbox ~]$ echo [[:upper:]]*
  Desktop Documents Music Pictures Public Templates Videos
  ```

  ```bash
  [me@linuxbox ~]$ echo /usr/*/share /usr/kerberos/share /usr/local/share
  ```

  **Pathname Expansion of Hidden Files**

- Filenames that begin with a period are hidden. Pathname expansion does not reveal hidden files.

- If you try to include hidden files in an expansion by doing this: `echo .*` you will likely see incorrect results, because `.` and `..` appear in the results, and these names refer to the current working directory and its parent directory. To better perform pathname expansion, we have to use a more specific patter, like `echo .[!.]*`. This pattern expands into every filename that begins with only one period followed by any other characters. This will work correctly with most hidden files (thought it still won't include filenames with multiple leading periods).The ls command with the -A option ("almost all") will provide a correct listing of hidden files. `ls -A`

**Tilde Expansion **

- The tilde character (~) has a special meaning. When used at the beginning of a word, it expands into the name of the home directory of the named user or, if no user is named, the home directory of the current user.

**Arithmetic Expansion**

- The shell allows arithmetic to be performed by expansion. This allows us to use the shell prompt as a calculator.

```bash
echo $((2 + 2))
```

- Arithmetic expansion uses the following form: `$((expression))`
- Arithmetic expansion supports only integers (no decimals) but can perform additon, subtraction, multiplication, division (it rounds down since results are integers), modulo (remainder), and exponentiation
- Spaces are not significant in arthmetic expressions and expressions may be nested. For example:

```bash
echo $(($((5**2)) * 3))
```

- Single parentheses may be used to group multiple subexpressions. With this techniquwe, we can reqwrite the previous example and get the same result using a single expansion instead of two:

```bash
echo $(((5**2) * 3))
```

**Brace Expansion**

- We can create multiple text strings from a pattern containing braces. Here's an example:

```bash
echo Front-{A,B,C}-Back 
=> Front-A-Back Front-B-Back Front-C-Back
```

- Patterns to be brace expanded may contain a leading portion called a preamble and a trailing portion called a postscript. The brace expression itself may contain either a comma-separated

- Range of Integers:

```bash
echo Number_{1..5} 
Number_1 Number_2 Number_3 Number_4 Number_5
```

- Integers can be zero-padded, like so:

```bash
[me@linuxbox ~]$ echo {01..15}
01 02 03 04 05 06 07 08 09 10 11 12 13 14 15
[me@linuxbox ~]$ echo {001..15}
001 002 003 004 005 006 007 008 009 010 011 012 013 014 015
```

- You can do a range of letters in reverse order:

```bash
[me@linuxbox ~]$ echo {Z..A}
Z Y X W V U T S R Q P ON M L K J I H G F E D C B A
```

- Brace expansions can be nested

```bash
[me@linuxbox ~]$ echo a{A{1,2},B{3,4}}b aA1b aA2b aB3b aB4b
```

- You can use this to make directories:

```bash
[me@linuxbox ~]$ mkdir Photos
[me@linuxbox ~]$ cd Photos
[me@linuxbox Photos]$ mkdir {2007..2009}-{01..12} [me@linuxbox Photos]$ ls
2007-01 2007-07 2008-01 2008-07 2009-01 2009-07 2007-02 2007-08 2008-02 2008-08 2009-02 2009-08 2007-03 2007-09 2008-03 2008-09 2009-03 2009-09 2007-04 2007-10 2008-04 2008-10 2009-04 2009-10 2007-05 2007-11 2008-05 2008-11 2009-05 2009-11 2007-06 2007-12 2008-06 2008-12 2009-06 2009-12
```

**Parameter Expansion**

- The variable named `USER` contains our username:

```bash
[me@linuxbox ~]$ echo $USER 
nathanworden
```

- To see a list of available vairables, try this:

```bash
[me@linuxbox ~]$ printenv | less
```

**Command Substitution**

- Command Substitution allows us to use the output of a command as an expansion

```bash
[me@linuxbox ~]$ echo $(ls)
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

- You can pass the results of `which cp` as an argument to the ls command, thereby getting the listing of the `cp` program without having to know its full pathname.

```bash
me@linuxbox ~]$ ls -l $(which cp)
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

**Quoting**

- Parameter expansion substitutes the $100 with an empty string because it saw it as an undefined variable. The shell provides a method called quoting to selectivley suppress unwanted expansions.

```bash
[me@linuxbox ~]$ echo The total is $100.00 
The total is 00.00
```

- The first type of quoting we will look at is double quotes. If we palce text inside double quotes, all the special characters used by the shell lsoe their special meaning and are treated as ordinary characters. The expections are $, \ and ` This means that word-splitting, pathname expansion, tilde expansion, and brace expression are suppressed, but parameter expansion, arithmetic expansion, and command substitution are stil lcarried out. 

**Single Quotes**

If we need to suppress all expansions, we use single quotes. Here is a comparison of un-quoted, double quotes, and single quotes:

```bash
[me@linuxbox ~]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER text /home/me/ls-output.txt a b foo 4 me
[me@linuxbox ~]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER" text ~/*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER' text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```

**Escaping Characters**

Sometimes we want to quote only a single character. To do this, we can precede a character with a backslash, which in this context is called the escape character. Often this is done inside double quotes to selectivley prevent an expansion.

```bash
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00" 
The balance for user me is: $5.00
```

It is also common to use escaping to eliminate the special meaning of a character in a filename. For example, it is possible to use characters in filenames that normally have special meaning in the shell. These would include $, !, &, spaces, and others.

```bash
[me@linuxbox ~]$ mv bad\&filename good_filename
```

To allow a backslash character to appea, escape it by typing \\. Note that within single quotes, the backslash loses its speical meaning and is treated as an ordinary character.