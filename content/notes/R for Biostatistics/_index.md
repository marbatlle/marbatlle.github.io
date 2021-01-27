---
# Course title, summary, and position.
linktitle: R for Biostatistics
summary: An introduction to basic statistical concepts and R programming skills necessary for analysing data in the life sciences
weight: 3

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
    weight: 3
---

Load libraries
--------------

    # Load libraries
    library(knitr)
    library(tinytex)
    library(tidyverse)
    library(ggplot2)
    library(DataExplorer)
    library(nortest)

The dataset: Low weight at birth
--------------------------------

**Goal of the study**: establish which factors are associated with low
weight on newborns, present in women who have given birth.

    # Read the data
    low_weight_births <- read.csv("~/Documentos/bioestadistica/datos/Bajo peso al nacer.csv", sep=";") %>%
      data.frame()
    # Let's get an idea of what we're working with 
    glimpse(low_weight_births)

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

As you can see, the set of variables present in this dataset contains
are described in english, to make it easier to understand, here you can
see the meaning of each variable and its corresponding categories: 

-   **id**: identification
-   **bajo\_pes**: low weight at birth (categories: 0 = normal weight (&gt;= 2500g), 1 = low weight (&lt; 2500g))
-   **edad**: age
-   **peso**: weight
-   **raza**: race
 categories: 1 = white, 2 = black, 3 = other)
-   **fumador**: smoker (categories: 0 = no, 1 = yes) 
-   **part\_pre**: premature birth
(categories: 0 = no, 1 = 1 birth, 2 = 2 births, 3 = more than 3)
-   **hta**: hipertension (categories: 0 = no, 1 = yes)
-   **irr\_urin**: urinary irritability (categories: 0 = no, 1 = yes)
-   **visi\_med**: number of medical visits

To condinue with the analysis, we'll clean the data while modifying
it’s variable names and categories.

    # Clean and adequate the data
    data  <- low_weight_births %>%
      drop_na() %>%
      rename(low_weight = bajo_pes,
             age = edad,
             weight = peso,
             race = raza,
             smoker = fumador,
             prem_birth = part_pre,
             urin_irr = irr_urin,
             med_vis = visi_med) %>%
      mutate(low_weight = factor (low_weight, labels = c("normal","low")),
             race = factor (race, labels = c("white","black","others")),
             smoker = factor (smoker, labels = c("no", "yes")),
             prem_birth = factor (prem_birth, labels=c("no","1_birth","2_births","more2_births")),
             hta = factor (hta, labels=c("no","yes")),
             urin_irr = factor (urin_irr, labels=c("no","yes")))

    glimpse(data)

    ## Rows: 189
    ## Columns: 10
    ## $ id         <int> 4, 10, 11, 13, 15, 16, 17, 18, 19, 20, 22, 23, 24, 25, 26,…
    ## $ low_weight <fct> low, low, low, low, low, low, low, low, low, low, low, low…
    ## $ age        <int> 28, 29, 34, 25, 25, 27, 23, 24, 24, 21, 32, 19, 25, 16, 25…
    ## $ weight     <dbl> 54.43164, 58.96761, 84.82264, 47.62769, 38.55575, 68.03955…
    ## $ race       <fct> others, white, black, others, others, others, others, blac…
    ## $ smoker     <fct> yes, no, yes, no, no, no, no, no, no, yes, yes, yes, no, n…
    ## $ prem_birth <fct> 1_birth, no, no, 1_birth, no, no, no, 1_birth, no, no, no,…
    ## $ hta        <fct> no, no, yes, yes, no, no, no, no, yes, yes, no, no, no, no…
    ## $ urin_irr   <fct> yes, yes, no, no, yes, no, yes, no, no, no, no, yes, no, n…
    ## $ med_vis    <int> 0, 2, 0, 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 2, 2, 0, 0, 0…
