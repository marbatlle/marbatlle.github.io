---
# Course title, summary, and position.
linktitle: R for Biostatistics
summary: An introduction to basic statistical concepts and R programming skills necessary for analysing data in the life sciences
weight: 1

# Page metadata.
title: R for Biostatistics
date: "2018-09-09T00:00:00Z"
lastmod: "2018-09-09T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: docs  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
  example:
    name: R for Biostatistics
    weight: 1
---
The dataset
===========

    # Load libraries
    library(knitr)
    library(tinytex)
    library(tidyverse)
    library(ggplot2)
    library(DataExplorer)
    library(nortest)

    # Read the data
    data_bajo_peso <- read.csv("~/Documentos/bioestadistica/datos/Bajo peso al nacer.csv", sep=";") %>%
      data.frame()

    # Let's get an idea of what we're working with 
    glimpse(data_bajo_peso)

    ## Rows: 189
    ## Columns: 10
    ## $ id       <int> 4, 10, 11, 13, 15, 16, 17, 18, 19, 20, 22, 23, 24, 25, 26, 2…
    ## $ bajo_pes <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ edad     <int> 28, 29, 34, 25, 25, 27, 23, 24, 24, 21, 32, 19, 25, 16, 25, …
    ## $ peso     <dbl> 54.43164, 58.96761, 84.82264, 47.62769, 38.55575, 68.03955, …
    ## $ raza     <int> 3, 1, 2, 3, 3, 3, 3, 2, 3, 1, 1, 1, 3, 3, 1, 1, 2, 1, 3, 3, …
    ## $ fumador  <int> 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 1, 1, 0, 1, 0, 0, …
    ## $ part_pre <int> 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 2, 0, 0, 0, 0, 0, 1, 0, 0, …
    ## $ hta      <int> 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ irr_urin <int> 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1, …
    ## $ visi_med <int> 0, 2, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 2, 2, 0, 0, 0, …

and clean the data

    # Clean and adequate the data
    data  <- data_bajo_peso %>%
      drop_na() %>%
      mutate(bajo_pes=factor(bajo_pes,labels=c("normal","bajo")),
             raza=factor(raza,labels=c("blanca","negra","otras")),
             fumador=factor(fumador,labels=c("no", "si")),
             part_pre=factor(part_pre,labels=c("no","1 parto","2 partos","más de 3 partos")),
             hta=factor(hta,labels=c("no","si")),
             irr_urin=factor(irr_urin,labels=c("no","si")))

    glimpse(data)

    ## Rows: 189
    ## Columns: 10
    ## $ id       <int> 4, 10, 11, 13, 15, 16, 17, 18, 19, 20, 22, 23, 24, 25, 26, 2…
    ## $ bajo_pes <fct> bajo, bajo, bajo, bajo, bajo, bajo, bajo, bajo, bajo, bajo, …
    ## $ edad     <int> 28, 29, 34, 25, 25, 27, 23, 24, 24, 21, 32, 19, 25, 16, 25, …
    ## $ peso     <dbl> 54.43164, 58.96761, 84.82264, 47.62769, 38.55575, 68.03955, …
    ## $ raza     <fct> otras, blanca, negra, otras, otras, otras, otras, negra, otr…
    ## $ fumador  <fct> si, no, si, no, no, no, no, no, no, si, si, si, no, no, si, …
    ## $ part_pre <fct> 1 parto, no, no, 1 parto, no, no, no, 1 parto, no, no, no, 2…
    ## $ hta      <fct> no, no, si, si, no, no, no, no, si, si, no, no, no, no, no, …
    ## $ irr_urin <fct> si, si, no, no, si, no, si, no, no, no, no, si, no, no, no, …
    ## $ visi_med <int> 0, 2, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 2, 2, 0, 0, 0, …