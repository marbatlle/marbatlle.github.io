---
title: 3. Process Management
---

# 3. Process Management

Process Management Orders
-------------------------

### Process Status

View a list of the active processes on the machine

    $ ps [-efl]
       * -e: displays all running processes
       * -f: displays detailed information of the processes
       * -l: displays even more detailed information about the processes

To see all whose name contains the string <word>:

    $ pgrep | -l word

### Kill Command

It is used to cancel the execution of certain processes whose execution
is not desired to continue:

    $ kill [-signal] PID
    * PID: identifier of the process or not of the task that we want to stop
    * signal: signal to send (by default it is SIGTERM = 15, if the process does not end with this signal, it will be necessary to send it the SIGKILL (9) signal)

### pkill Command

It allows killing processes indicating the name of the process, instead
of its PID pkill sends a SIGTERM signal to the specified process.

    $ pkill [-U username] name_process

### job Command

The job order allows you to see the list of active jobs at that moment.

    $ jobs

### Suspension of work

Any job (foreground or background) can be temporarily suspended and then
resumed from where it left off. To suspend a process that is running in
the foreground:

    $ [Ctrl] -Z

### Resuming jobs

Any suspended job can be resumed, in the background or foreground.

    $ bg %num_job: resumes a suspended job in the background
    $ fg %num_job: resumes in the foreground, it also serves to bring a work from the background to the foreground
