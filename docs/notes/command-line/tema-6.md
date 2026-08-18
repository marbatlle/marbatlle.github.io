---
title: 6. User Configuration
---

# 6. User Configuration

General characteristics of shells
---------------------------------

### Redirection of input / output

-   Redirection of standard output: “&gt;, 1&gt;” (to overwrite the
    file), “&gt;&gt;, 1 &gt;&gt;” (to add the output to the end of the
    file)
-   Redirection of the error output: “2&gt;” (to overwrite the file),
    “2 &gt;&gt;” (to add the output to the end of the file)
-   Redirection of standard input: “&lt;or 0&gt;”

### Order sequencing

You can enter a series of commands on the same line separated by a
semicolon “;”, the shell executes them sequentially from left to right.

    Example
    $ prompt> ps; date; quien

### Order grouping

A sequence of orders can be grouped by placing them in parentheses, a
group of orders can be redirected as if it were a single order.

    Example
    $ prompt> (ps; date; who)> output

### Channels or “pipes”

You often want to use the output of one command as input to another
command, for example: *ps aux&gt; output*, but the shell offers a more
powerful and elegant way to do this: pipes. The pipe operator is *|*.

    The general format of a pipe is as follows:
    order A | order B; i.e. ps aux | more

The standard output of order A is used as input of order B, you can
chain as many orders as you want.

Shell variables (Bourne, Korn and Bash)
---------------------------------------

### Local or private shell variables

-   They are defined, used and deleted within the shell
-   They are usually used to configure the main aspects of the
    particular shell
-   Their values are NOT transmitted to the daughter subshells

### Global or environment variables

-   They are normally defined before entering the shell (although others
    can be redefined or added from within the shell)
-   They are usually used to configure the main aspects of the session
-   Their values ARE transmitted to the daughter subshells
-   If a child subshell changes the name of an environment variable,
    when exiting it, the variable takes its original value in the parent
    shell

### Definition, elimination and visualization of variables

<table>
<thead>
<tr class="header">
<th style="text-align: center;">Operation to be performed</th>
<th style="text-align: center;">Environment Variables</th>
<th style="text-align: center;">Local variables</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: center;">Definition of a variable</td>
<td style="text-align: center;">VAR = value,export VAR</td>
<td style="text-align: center;">var=valor</td>
</tr>
<tr class="even">
<td style="text-align: center;">Delete a variable</td>
<td style="text-align: center;">unset VAR</td>
<td style="text-align: center;">unset var</td>
</tr>
<tr class="odd">
<td style="text-align: center;">Visualization of all variables</td>
<td style="text-align: center;">env or export</td>
<td style="text-align: center;">set (also env.)</td>
</tr>
<tr class="even">
<td style="text-align: center;">Viewing the value of a variable</td>
<td style="text-align: center;">echo $VAR</td>
<td style="text-align: center;">echo $var</td>
</tr>
</tbody>
</table>

### Main variables predefined by the shell

<table>
<thead>
<tr class="header">
<th style="text-align: center;">Variable Name</th>
<th style="text-align: center;">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: center;">EDITOR</td>
<td style="text-align: center;">Default editor</td>
</tr>
<tr class="even">
<td style="text-align: center;">HOME</td>
<td style="text-align: center;">HOME directory</td>
</tr>
<tr class="odd">
<td style="text-align: center;">HOSTNAME</td>
<td style="text-align: center;">Host Name</td>
</tr>
<tr class="even">
<td style="text-align: center;">LOGNAME, USER</td>
<td style="text-align: center;">Username</td>
</tr>
<tr class="odd">
<td style="text-align: center;">MAIL</td>
<td style="text-align: center;">Directory where the existence of mail is checked</td>
</tr>
<tr class="even">
<td style="text-align: center;">PATH</td>
<td style="text-align: center;">Path where executable files are searched</td>
</tr>
<tr class="odd">
<td style="text-align: center;">PRINTER</td>
<td style="text-align: center;">Default printer</td>
</tr>
<tr class="even">
<td style="text-align: center;">PS1</td>
<td style="text-align: center;">Defines the system prompt</td>
</tr>
<tr class="odd">
<td style="text-align: center;">PWD</td>
<td style="text-align: center;">Defines the current directory</td>
</tr>
<tr class="even">
<td style="text-align: center;">SHELL</td>
<td style="text-align: center;">Shell type</td>
</tr>
<tr class="odd">
<td style="text-align: center;">TERM</td>
<td style="text-align: center;">Terminal type</td>
</tr>
<tr class="even">
<td style="text-align: center;">UID</td>
<td style="text-align: center;">Number of username</td>
</tr>
</tbody>
</table>

### Variable PS1: PROMPT customization

The variable PS1 defines the prompt or command line inductor

    Examples:
    $ PS1 = 'HELLO>'
    $ PS1 = '$ USER>'
    $ PS1 = '`whoami`>'
    $ PS1 = '$ HOSTNAME>'
    $ PS1 = '$ USER @ $ HOSTNAME: $ PWD>

### PATH variable: search for executables

The PATH variable is very important as it allows locating executable
commands in directories in the order set in the variable.

    Definition of the PATH variable:
    P $ ATH = directory1: directory2: directory3: ...
    $ export PATH
    Examples:
    $ PATH = / usr / bin: / usr / openwin / bin: / etc :.
    $ export PATH
    $ echo $ PATH
    / usr / bin: / usr / openwin / bin: / etc :.

*The whereis command* This command allows you to search the file system
for all the directories in which a certain command appears. This command
does not search in the directories of the PATH variable but in all the
directories of the system

    Syntax:
    $ whereis command
    Example:
    $ whereis vim
    vi: / usr / bin / vim / usr / ucb / vim

Usefulness of the \* whereis \* command: It allows knowing all the
versions of the same command and correctly defining the PATH

Advanced shell features
-----------------------

### Order history

The HISTFILE command defines the history file, in which the last entered
commands are stored

    To change its value it is necessary to redefine the variable, for example
    $ HISTFILE = $ HOME / new_history_file
    $ export HISTFILE
    * Its default value is HISTFILE = $ HOME / .bash_history

The HISTSIZE command defines the history file, in which the last
commands entered are stored

    $ HISTSIZE = 500
    $ export HISTSIZE
    Its default value is HISTSIZE = 1000

To view command history

    $ history [n]
      * Shows the last n entered commands with the corresponding command number. If no arguments are specified, it shows the last 100 orders.
      * To rerun a command from the history list:
        * Option 1: Re-run the command corresponding to command_num
          $! [command_num]
        * Option 2: Re-run the most recent command in history whose first letters match string
          $! [string]
        * Option 3:: Using the cursor keys (Bash only)

### Automatic order completion (Bash only)

The \[Esc\] and \[Tab\] keys allow autocomplete orders

### Definition of aliases

The shell allows you to assign a pseudonym (alias) for a command

    Syntax:
    alias <name> = <order>
    defines an alias for the specified order
    unalias <name>
    remove a previously defined alias

    Examples:
    * alias h = history
    * alias c = clear
    * alias ll = 'ls al'
    * alias home = 'cd -ls'
    * alias rm = 'rm -i'
    * alias cd = 'cd; pwd'

User configuration files
------------------------

### .profile file

Typical contents of $ HOME / .profile files:

    * Definition of environment variables that are exported to all shells that are executed during the session:
      * PATH, for example:
        *PATH=$PATH:/usr/ucb:/usr/local/bin/:usr/openwin/bin:.*
        *export PATH*
      * HISTFILE and HISTSIZE, for example:
        *HISTFILE=$HOME/new_history_file*
        *HISTSIZE=256*
        *export HISTFILE; export HISTSIZE*
      * Variables to define the default text editor, for example:
        *EDITOR=vi*
        *export EDITOR*
      * Variables to define the default printer, for example:
        *PRINTER=laser1*
        *export PRINTER*
      * Variables needed to run certain programs, for example:
        *OPENWINHOME=/usr/openwin;*
        *LD_LIBRARY_PATH=$OPENWINHOME/lib*
        *export OPENWINHOME; export LD_LIBRARY_PATH*
    * Main session configuration commands:
      * umask. To define the default permissions for files and directories:
        *umask 027*
      * stty. To define keyboard settings:
        *stty erase "^H" kill "^U" intr "^C"*
        *stty susp "^Z" dsusp "^Z" eof "^D"*

### .bashrc file

Typical contents of the $ HOME / .bashrc file

    * Definition of local shell variables
      * Definition of prompt (PS1)
      * Other local user variables
    * Definition of aliases
       *alias h = history*
       *alias c = clear*
       *...*
    * Enable / disable shell options
       *set -o noclobber*
