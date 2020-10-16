**Command line tools** range from scripts to libraries to programs, and
can solve a number of problems for users. Categorically, they range from
web dev to utility to entertainment and can provide a lot of
functionality for people working from the command line.

Users and Access to the system
------------------------------

### Password

Change the user’s password

    $ passwd

### Users

Switch to a different user

    $ su [- username] 
       *  Username becomes the specified user
       *  If its omitted it becomes the superuser

### Finish the session

You can exit the session by using one of the following commands

    $ exit
    $ logout

Basic Commands of the System
----------------------------

### Date

Define and show the date and time

    $ date [+format]
       *  %a Abbreviated weekday name (Sun)
       *  %A weekday name (Sun)
       *  %D Date [mm/dd/yy]
       *  %H Hour [00 a 23]
       *  %m Month [01 a 12]
       *  %h Month [Jan]
       *  %y Year [98]
       *  %w Day of the week [Sunday = 0]
       *  %d Day of the month (01 a 31)
       *  %j Day of the year [001 a 366]
       *  %M Minuto [00 a 59]
       *  %S Second [00 a 59]
       *  %T Hora [HH:MM:SS]
       *  %r Time with a.m./p.m. [11:53:29 AM]
       *  %t insert tabulator
       *  %n insert new line

### Time

Shows the CPU time and real time elapsed in the execution of an order

    $ time [command_line]*

### Echo

Echoes the arguments (allows standard C escape sequences). Allows you to
view information on the screen: \* Character strings \* Variable values
\* Order execution results

    $ echo [-n] arg
       *  -n: Does not include line break at the end

### Uname

Prints information about the system name

    $ uname [-snrvmq]
       * -s: Print the name of the operating system
       * -n: Print the node name of the computer
       * -r: Print the operating system revision number
       * -v: Print the version number of the operating system
       * -m: Print the computer type
       * -a: Print all the above information

### Who

Print information about users who have open sessions

    $ who [am I]

### Sleep

Suspend execution for the specified time

    $ sleep [seconds]

### Calendar

Print the calendar of the indicated month and year

    $ cal

### Make Directory

Commands to create directories

    $ md [-p] directorio
    $ mkdir [-p] directorio
       * -p Crea los subdirectorios necesarios

### Change Directory

Change the working directory

    $ cd [directorio]
    $ chdir [directorio]
      * If you don't indicate the destination directory, it changes to the HOME directory

### Remove Directory

Deletes an specified directory

    $ rmdir [directorio]
      * If the directory is not empty, use *rm -r mydir*

### pwd

Shows the working directory

    $ pwd

### Touch

Changes the modification date and/or gives you acces to the file (it
also creates files)C

    $ touch [-acm] [mmddhhmm[aa] ] fichero
      * -a: Update only the access date
      * -c: Does not create file if it does not exist
      * -m: Updates only the modification date

### List

List file and directory names and attributes

    $ ls [-aAcCdfFgilLmnpqrRstux1] [route ... ]
      * -a: list all entries
      * -A: same as -a but does not list directoriess
      * -F: put '/' at the end of directories, '*' at the end of executables and '@' at the end of symbolic links
      * -i: displays i-number in column 1
      * -1: long listing
      * -L: follow the symbolic links
      * -n: with -1 shows UID / GID numbers -o as -1 but does not show GID -p puts '/' at the end of the directory name
      * -q: shows non-displayable characters 
      * -r: invert the sense of order
      * -R: lista recursivamente directorios 
      * -s: recursively list directories
      * -t: sort by dates
      * -u: shows the date of the last access
      * -x: cross-ordered multi-column output
      * -1: force the format of a filename on each line

### Move

Rename and move files and directories

    *$ mv [-f] fuente1 [fuente2 ... ] destiny*
      * -f: suppress destiny no questions asked

### Remove

Removes files

    *$ rm [-fir] route [route ... ]*
      * -r: recursive
      * -f: delete without asking and without issuing messages (scripts)
      * -i: ask for confirmation interactively

### ’\*’ & ‘?’

      * ls apple.*: see all the files about apple
      * ls ?pple.genome: see all the files about pple.genome
      * ls [a-z]*.genome: see all the genome files
      * ls p*.genome
      s* ls {pear, peach}.genome: list all the files either about pear or peach

### Manual

Utiliza **man** orden en para visualizar información sobre el formato,
opciones, utilidad y ejemplos de orden
