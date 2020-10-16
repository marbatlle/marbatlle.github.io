---
title: 2. Basic Management
linktitle: 2. Basic Management
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Command Line
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

Software management through repositories
----------------------------------------

### Repository listing update

Recommended to run it daily / weekly

    $ sudo apt-get update
    $ sudo apt-get upgrade

### Updating the operating system

Upgrade to an OS version

    $ sudo apt-get dist-upgrade

### List of available applications

Shows a list of packages that correspond to the chain entered

    $ sudo apt-cache search 

Displays information specific to that package

    $ sudo apt-cache show <package> 

Software management by other means
----------------------------------

### Loose .db files

Install packages

    $ sudo dpkg –i <package>
    $ sudo apt-get install <package>

Delete Packages

    $ sudo apt-get remove <package>
    $ sudo apt-get purge <package>
