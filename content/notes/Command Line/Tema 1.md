---
title: Introduction to Linux
linktitle: Introduction to Linux
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Command Line
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---


Users and Access to the system
------------------------------

#### Password

Change the user’s password

    $ passwd

#### Users

Switch to a different user

    $ su [- username] 
      *  Username becomes the specified user
      *  If its omitted it becomes the superuser

#### Finish the session

You can exit the session by using one of the following commands

    $ exit

    $ logout

Basic Commands of the System
----------------------------

#### Date

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

#### Time

Shows the CPU time and real time elapsed in the execution of an order

    $ time [command_line]*

#### Echo

Echoes the arguments (allows standard C escape sequences). Allows you to
view information on the screen: \* Character strings \* Variable values
\* Order execution results

    $ echo [-n] arg
       *  -n: Does not include line break at the end

#### Uname

Prints information about the system name

    $ uname [-snrvmq]

      * -s: Print the name of the operating system
      * -n: Print the node name of the computer
      * -r: Print the operating system revision number
      * -v: Print the version number of the operating system
      * -m: Print the computer type
      * -a: Print all the above information

#### Who

Print information about users who have open sessions

    $ who [am I]

#### Sleep

Suspend execution for the specified time

    $ sleep [seconds]

#### Cal

Print the calendar of the indicated month and year

    $ cal
