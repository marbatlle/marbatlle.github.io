---
title: 4. File System
---

# 4. File System

File system organization
------------------------

### Access routes

Absolute path: Taking the root as the starting point

    /home/user2/dir1/datafile

Relative path: Taking the current directory as the starting point

    home/user2/dir1/datafile (from directory)
    user2/dir1/datafile (from the / directory)
    dir1/datafile (from the / home / directory)
    datafile (from the / home / directory / user2)

### Show i-nodes

The filesystem is organized into a single single root tree structure /,
but there is the possibility of linking between files (links).

    $ ls -i

### List directory contents

    $ ls -l*
      * User-Groups-Others
      * r-: read permission
      * w-: write permission
      * x-: execute permission

### Metacharacters or wildcard characters

-   Wildcard \*: can be replaced by any string of characters
-   Wildcard ?: can be replaced by any character (only one)
-   Characters in brackets: you can specify a list of characters in
    brackets that can correspond to a character in the file name

File and directory security
---------------------------

### Modify the protection properties of a file

Change the permission bits (1 = Enabled, 0 = Disabled):

    $ chmod file_permissions

Change the owner:

    $ chown file_owner

Change group:

    $ chgrp file_group

### User’s mask

View or change the user mask. Allows you to modify the permissions that
are activated by default when creating a new file or directory. In this
case, specify the files that should be activated (1: deactivated, 0:
Activated

    $ umask [value]

File and Directory Orders
-------------------------

### File Command

Determine the type of file

    $ file [-c] [-f file] [-m file] archive
      * -c: check the validity of the magic file (/ etc / magic) and exit
      * -f file: file contains the list of files to examine
      * -m file: use file instead of '/ etc / magic' for type information

### Concatenate

Concatenate and display text files

    $ cat [-s] [-v[et] ] [file ... ]
      * -v: print escape sequences
      * -s: no error messages
      * -t: print tabs as ^ I under -v
      * -e: print $ at the end of each line under -v

Create new file:

    $ cat > <file>

### Tee command

Read the standard input and write the standard output and files.

    $ tee [OPTION]... [FILE]...

    You can edit the file: $ prompt> tee <file>
    You can create and edit file: $ prompt> tee > <new file>

      * -a: do not overwrite the file but append to the given file
      * -help: it gives the help message and exit
      * -version: it gives the version information and exit

### cmp command

Compare two files in binary

    $ cmp [-ls] file1 file2
      * -l: Show all differences (by default it only shows the first one)
       -s: Silent; returns as exit status 0 if they are the same, 1 if they are different and 2 if there is an error

### Differences

Compare two tecto files and show the smallest differences

    $ diff [-bihtw] [-c [n]] file1 file2
      * -b: Ignore blanks (space and tab) at the end of the line
      * -w: Ignore all targets
      * -c [n]: Show the differences with n context lines
      * -h: Fast algorithm
      * -i: Ignore differences between upper and lower case

### Word Count

Counts lines, words and characters

    $ wc [-clw] file ... 
      * -c: Character count
      * -l: Count lines
      * -w: Counts words

### Head

Show the first lines of one or more files

    $ head [-options] pathname
      * -n: we indicate the number of lines that we want it to show us, -n 20 or 20
      * -c: print the first bytes indicated

### Tail

Show the last lines of a file

    $ tail [- [n] [bc]] [f] [file]
      * -n: Sample from n lines counted from the end
      * bc: n is in units of blocks or bytes
      * -f: tail refresh the contents of the file as it appears
      * -c: show a given number of bytes

### Size

Displays the text and data sizes of an object file (binary)

    $ size file> 

### uniq

Eliminate duplicate lines in an ordered file

    $ uniq [-u] [-d] [-c] [-n] [+ n] [input_file [output_file]] 
      * -u: Show lines that only appear once
      * -d: Show a copy of the repeated lines
      * -c: Show each line preceded by the number of occurrences

### more

Display text files on screen page by page

    $ more [-dpcsu] [-num] [+ / pattern] [+ linenum] [file ...]
      * -num: Specify the screen size (in lines)
      * -d: Displays the message "[Press space to continue, 'q' to quit.]"
      * -p: Does not "scroll", but cleans the screen and displays the text
      * -c: Does not "scroll", it displays line by line from top to bottom
      * -s: Replaces several consecutive blank lines with a single one
      * -u: Delete underscore
      * + / pattern: Begins with the line containing the pattern string
      * + linenum: Starts at the linenum line

### less

Less is a command line utility capable of showing us the content of a
file, or the output of a command page by page.

    $ less [OPTIONS] file
      * -N: If we want it to show the line numbers
      * -X: If we want the content to remain printed when returning to the console with the (q) key
      * + F: If we want to see log files that are constantly updated

### df command

Shows the amount of free space left on the device where a file is
located

    $ df file

### du command

Summarize the disk space that users use

    $ du [-ars] [file / directory]
      * -a: List all
      * -r: Show error messages if you cannot access subdirectories
      * -s: Returns a single value for each argument

### Copy Order

Command used to copy files or groups of files or directories, creates an
exact image of the file on disk with a different name

    $ cp <file1> <file2>

### Vim: Text editor

If the file does not exist, create it

    $ vim [options] file1 file2 ... 
      * +45: start viewing on line 45
      * + $: starts on the last line
      * + / string: starts at the first occurrence of the string (after + you can specify any vim command to run before the edit screen appears)

*Order mode*

      * Delete a character: x
      * Delete n characters: nx
      * Replaces a character: r
      * Delete a line: dd
      * Delete n lines: ndd
      * Insert a line below: o (we enter text mode)
      * Insert a line above: O (we enter mode)
      * Go to insert mode: i
      * Go to overwrite mode: R
      * Save and exit:: wq
      * Exit without saving:: q!

*Text mode*

      * We go to this mode with: i, o, O,
      * We return to command mode with: CNTRL + C, ESCAPE key
      * We go to overwrite mode: R
