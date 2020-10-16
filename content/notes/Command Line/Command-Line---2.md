Software management through repositories
----------------------------------------

#### Repository listing update

Recommended to run it daily / weekly

    $ sudo apt-get update
    $ sudo apt-get upgrade

#### Updating the operating system

Upgrade to an OS version

    $ sudo apt-get dist-upgrade

#### List of available applications

Shows a list of packages that correspond to the chain entered

    $ sudo apt-cache search 

Displays information specific to that package

    $ sudo apt-cache show <package> 

Software management by other means
----------------------------------

#### Loose .db files

Install packages

    $ sudo dpkg –i <package>
    $ sudo apt-get install <package>

Delete Packages

    $ sudo apt-get remove <package>
    $ sudo apt-get purge <package>
