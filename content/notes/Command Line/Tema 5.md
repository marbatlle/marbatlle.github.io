---
title: 5. Advanced Commands
linktitle: 5. Advanced Commands
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Command Line
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

File Treatment
--------------

### find function

Find files within the file tree

    $ find directory expression
      * -print: print the current qualified file
      * -name pattern: comparison pattern with file name
      * -perm mask: comparison with permissions
      * -type c: file type: 'c chosen from the set [bcdflp] that corresponds to block, characters, directory, file, link or pipe
      * -links #: has # links
      * -group name: group is name
      * -atime: accessed in # days
      * -ctime #: changed inode in # days
      * -ok command \: as exec; but ask for confirmation before executing order
      * -newer file: modified more recently than file
      * -depth: process directories after contents
      * -xdev: restricts the search to the filesystem of the search directory (does not descend subdirectories) \ (expression \) matches the expression
      * -o: 'logical or' operator between conditions
    user name owner is name
      * -size #: has # blocks (512 byte blocks)
      * -mtime: modified in # days
      * -exec command \: execute command;
      * !: negation operator
      * -a: operator 'and logical' between conditions

### sort function

Sort / Mix Utility

    $ sort [cmu] or file_out] bdfinr] t x] pos1] pos2] file ...
      * -c: Check if input lines are sorted
      * -m: Mix files that are assumed to be pre-ordered, not ordered
      * -u: Does not show duplicate lines
      * -o output_file: Directs the ordered output to output_file
      * -tx: Makes the field separator character x (default is blank: space or tab
      * pos: Key positions
      * m [.n] [options]: Skip m fields (words), n characters to the beginning of the key
      * -b: Skip leading white space for comparisons
      * -d: Dictionary command
      * -f: Not case sensitive
      * -i: Ignore non-ASCII characters and control in comparisons
      * -n: Compare numeric fields (implies b
      * -r: Reverse order

### cut function

Select fields or characters on input lines

    $ cut -c file list ...
    $ cut -f dc list] [s] file ...
      * -f list: Select by fields. The fields are character strings separated by delimiters, i.e. column 1; -f1
      * -dc: c is the field delimiter character (by default the tab)
      * -s: Suppresses lines that do not have field delimiters
      * -c list: Select by columns (character positions on a line)
    lists can contain numbers separated by commas or ranges separated by hyphens

### grep function

Look for a pattern (built on the basis of a limited regular expression)
in a file and shows the lines that contain the pattern

    $ grep [options] limited_regular_expression [file]
      * -c: Show only the total number of lines that contain the pattern
      * -i: Ignore case sensitivity
      * -h: Prevents the filename containing the pattern from appearing
      * -l: Shows only once the name of the files that contain the selected lines
      * -n: Precede each line with its line number within the file
      * -s: Suppresses error messages referring to non-existent files
      * -v: Show all lines except those containing the pattern
      * -w: Show the lines that satisfy the regular expression with a word
      * '^ word': line starts with word

### fgrep function

Look for a string of characters in a file. It differs from grep in that
it searches for strings fixed and not patterns defined by regular
expressions (that’s why it’s “fast grep”)

    $ fgrep [options] string [file]
      * -c, i, h, l, n, s, v: As grep
      * -x: Show only lines that exactly match the string
      * -e: string Search for string (useful for chaining multiple strings of
      * -f: file Search the list of strings contained in file

### egrep function

Look for a pattern (built on the basis of a complete regular expression)
in a file and displays the lines that contain the pattern. Like grep but
with regular expressions complete.

    $ egrep [options] full_regular_expression [file]
      * er +: Represents 1 or more occurrences of er
      * er ?: Represents 0 or 1 occurrence of er
      * eri | erj: Represents either one of the two
      * (er): Regular expression grouping
      * \ m: m-th cluster () above in er
      * -c, i, h, l, n, s, v: As grep
      * -e special_string: Like egrep
      * -f file: Find the list of limited_regular_expression contained in file

### sed command

Flow editor. copies designated files (default, standard output) to
standard output edited according to a script of edit commands.

    $ sed [-n] [-e script] [-f file] [files ...]
      * -f file: The script is collected from file
      * -e script: The script is listed below (by command line)
      * -n: Suppresses the output by default (by default, when processing the lines, it shows them
    per screen. This option avoids this)

    Function:
      * to text: Add text below the lines involved
      * c text: Change the lines involved by text.
      * d: Delete the lines involved.
      * i text: Insert text above the lines involved
      * p: Print. Copy the involved line to standard output.
      * q: Finish.

### awk command

It selects lines from one or more text files and performs on them
processing routines encoded in a language similar to C. It explores in
each input file the lines that meet any of the patterns specified in
prog. With each pattern, it performs an associated action that will be
executed when a file line satisfies that pattern.

    awk [-Fc] [prog | -f prog] [parameters] [files]
      * prog: The action-pattern is directly specified (in single quotes)
      * -f prog: The action-pattern is in the prog file (- means standard input)
      * If a pattern is missing, it is understood that all lines comply with it. If action is missing, the line is printed
      * If a pattern is missing, it is understood that all lines comply with it. If action is missing, the line is printed

Communication between users
---------------------------

### write command

Provides direct communication between two users (or two terminals of the
same user) by sending messages directly to the terminal devices (this is
usually one-way communication)

    $ write luis <message>

#### Wall order

Allows you to send a message to all users connected to the system

    $ wall <message>

#### Talk command

Allows bidirectional communication between users who may be on different
machines

    $ talk address [terminal]

Network connection
------------------

#### Login to a remote machine

Remote terminal service. It does not encrypt communications (not even
passwords), for what is not safe. It is in disuse.

    $ telnet remote_machine_IP_address (or symbolic name)

Remote login (deprecated)

    $ rlogin remote_machine_IP_address (or symbolic name) [-l user]

-   -l: Allows you to specify the username with which you login. If
    nothing is specified, it tries to access with the same username

#### rsh function

Execute an order on a remote machine $ rsh remote\_machine \[-l user\]
command

      * -l: Allows you to specify the username under which the order is executed. If nothing is specified, an attempt is made to access with the same username.

#### rusers function

Information about users connected to remote machines (like doing who on
those machines.) $ rusers \[-l\] remote\_machine\_IP\_address (or
symbolic name)

      * -l: Long format

### File transfer

File Transfer Protocol

    $ ftp remote_machine_IP_address (or symbolic name)
    Main FTP commands:
      * Copy a file on the remote machine
        ftp> put localfile remotefile
        ftp> send localfile remotefile
        Example:
        ftp> put doc 1 txt txt document
      * Copy multiple files onto the remote machine
        ftp> mput localfiles
        Example 
        ftp> mput doc 
      * Get a file from the remote machine
        ftp> get remotefile localfile
        ftp> recv remotefile localfile
      * Bring multiple files from remote machine
        ftp> mget remotefiles
      * Copy a file on the remote machine
        ftp> put localfile remotefile
        ftp> send localfile remotefile
      * Change directory on remote machine
        ftp> cd
      * View current directory
        ftp> pwd
      * List the contents of the directory
        ftp> ls Short listing
        ftp> dir Detailed listing
      * Change directory on local machine
        ftp> lcd

#### Tar order

Packs a set of files or a directory and its entire tree into a single
file of type file.tar. The order DOES NOT COMPRESS, just pack

    $ tar [cxvf] [file.tar] [source files or source directory]
      * -c: Create a tar file
      * -x: Extract a tar file
      * -v: Verbose mode "": informs about the files that are being compressed
      * -f: The name of the tar file or tape drive is listed below

#### Compress, uncompress command (need to install ncompress package)

This command allows you to compress any file and reduce its size between
20 and 80%. When compressed, it is replaced by another file with the
filename.Z extension.

    $ compress [-v] filename
    $ uncompress [-v] filename.Z
      *  -v: "verbose" mode. Reports on the reduction percentage of the compressed file

#### zip / unzip commands (replace compress / uncompress)

This command compresses / decompresses files in zip format.

    $ zip filename1 filename2 filename3 filename4 unzip filename.zip 

#### gzip / gunzip commands

This command compresses / decompresses files in gzip format.

    $ gzip filename1 filename2 filename3 
    $ gunzip filename1.gz filename2.gz filename3.gz 

#### lpr command

Print files using the printer spooler

    $ lpr [-P printer] [-i [indentation]] [-w columns] [file ...] 
      * -P: select the printer
      * - #: set number of copies
      * -w: sets the width of the lines

#### lpq command

Displays the print job queue

    $ lpq [-P printer] [-l] [user] 
      * -P: select the printer queue
      * -l: long format

#### lpc order

Printer control program

    $ lpc
