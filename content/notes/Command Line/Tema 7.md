---
title: 7. Advanced Linux
linktitle: 7. Advanced Linux
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Command Line
    weight: 7

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 7
---

Preparing the workspace
--------------

### 1.1. The Conda Environment


**Conda Environments:** Serve to help manage dependencies and isolate
projects, and isolate projects. They are lenguage agnostics; you can use
python, r, bash… \* Install conda and bioconda:
<a href="http://bioconda.github.io/user/install.html" class="uri">http://bioconda.github.io/user/install.html</a>

    #### Creating Environments - example using advshell

    conda create -n -y advshell

    #### Activate your environment

    conda activate advshell

    #### Deactivate environment

    conda deactivate

    #### List all existing environments

    conda env list

    More info about **conda environments**:
    <a href="https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533" class="uri">https://towardsdatascience.com/a-guide-to-conda-environments-bc6180fc533</a>

### 1.2. The Working Directory


To keep our project properly organized, we have to create a specific
working directory.

    #### Create the Directory

    mkdir -p -/adv-shell ls ~/

    #### Change into our working directory

    cd ~/adv-shell pwd

    #### Save our working directory in a variable for convenience

    export WD=$(pwd) echo $WD

    #### Create some directories for our data

    mkdir data log out res ls -l

    See your progress:

    pwd tree

Obtaining our data
--------------

### 2.1. Downloading the sequencing data

One option we have is downloading the data from the European Nucleotide
Archive:
<a href="https://www.ebi.ac.uk/ena/" class="uri">https://www.ebi.ac.uk/ena/</a>.

You need the ID of the experiment to download the FASTQ documents. If
you are analizing *paired-end* RNA-seq data you need to make sure to
download both.

    #### Download the data

    cd $WD/data wget
    <a href="ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR286/002/ERR2868172/ERR2868172_1.fastq.gz" class="uri">ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR286/002/ERR2868172/ERR2868172_1.fastq.gz</a>
    wget
    <a href="ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR286/002/ERR2868172/ERR2868172_2.fastq.gz" class="uri">ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR286/002/ERR2868172/ERR2868172_2.fastq.gz</a>

    #### Uncompress the data - Using -k to keep compressed files

    cd $WD/data gunzip -k ERR2868172\_1.fastq.gz gunzip -k
    ERR2868172\_2.fastq.gz tree $WD

### 2.2. Uncompress and count the reads

    #### Count the lines

    wc -l ERR2868172\_1.fastq

    FASTQ format uses 4 lines per read, so we should divide the total lines in the file by four

    expr 63865896 / 4

    This is a more effective alternative to using gunzip and to manually
    count the lines. Zcat allows you to dump the content of a compressed
    file to stout(similar to what cat does with uncompressed files).

    zcat ERR2868172\_1.fastq.gz | grep “^+$” | wc -l

Quality Control Checks on the Data
--------------
We use the FastQC software to do some quality control checks

    #### Install FastQC

    conda install -y fastqc

    #### Run FastQC on our data

    cd $WD mkdir out/fastqc fastqc -o out/fastqc data/\*.fastq.gz

Take a Random Sample of your Data
--------------

To downsample the reads, we will use the seqtk program. seqtk is a
tooklit for processing FASTQC and FASTA files.

    #### Install FastQC

    conda install -y seqtk

    #### Move original files to a subdirectory

    cd $WD/data mkdir original mv \*.fastq.gz original tree $WD

    You cannow subsample your files into the data directory

    seqtk sample -s100 original/ERR2868172\_1.fastq.gz 300000 | gzip &gt;
    ERR2868172\_1.fastq.gz seqtk sample -s100
    original/ERR2868172\_2.fastq.gz 300000 | gzip &gt;
    ERR2868172\_2.fastq.gz ls -lah $WD/data ls -lah $WD/data/original

Downloading the Genome
--------------

We will be downloading the Escherichia coli reference genome from the
NCBI.

We need to download the genome that matches the experiment that we will
analyse. In order to identify the specific E. coli strain to download,
we should check the metadata available on the ENA project where we
obtained our data.

cd WD mkdir res/genome cd! wget -O ecoli.fasta.gz
<a href="ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz" class="uri">ftp://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/005/845/GCF_000005845.2_ASM584v2/GCF_000005845.2_ASM584v2_genomic.fna.gz</a>
gunzip -k ecoli.fasta.gz

Analysing the data
--------------

We will now use the data we’ve prepared, performing the following steps:
* Remove sequencing adapters from our reads 
* Indexing the genome for
alignment 
* Aligning our reads to the genome 
* Generating a QC report

### 6.1. Adapter trimming
During sequencing experiments, additional molecules are added to our
molecules of interest in order for them to bind to our sequencing
platform. These molecules are called sequencing adapters.

Depending on the experiment, these sequencing adapters can actually be
sequenced along with our molecules. We should then look for them and
remove any we find. To do this, we will use the cutadapt software.

    #### Install cutadapt

    conda install -y cutadapt

    Remove adapter, discard any reads shorter than 20 nucleotides after trimming and redirect cutadapt’s standard output to a log file

    cd $WD mkdir out/cutadapt mkdir log/cutadapt cutadapt -m 20 -a
    AGATCGGAAGAGCACACGTCTGAACTCCAGTCA -A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT  
    -o out/cutadapt/ERR2868172\_1.trimmed.fastq.gz  
    -p out/cutadapt/ERR2868172\_2.trimmed.fastq.gz  
    data/ERR2868172\_1.fastq.gz data/ERR2868172\_2.fastq.gz &gt;
    log/cutadapt/ERR2868172.log

    ### 6.2. Indexing the genome and aligning our reads

    In order to align our reads, we need to pre-process our genome by
    generating an index. This index will work just like an index in a book:
    it will allow us to find parts of the genome faster, without having to
    go through all of its bases. Indexing is usually performed by the same
    software we use to align. In this case, we will be using STAR. Let’s
    start by installing it.

    #### Instalr STAR

    conda install -y star

    #### Index our genome

    cd $WD mkdir res/genome/star\_index STAR –runThreadN 4 –runMode
    genomeGenerate  
    –genomeDir res/genome/star\_index/  
    –genomeFastaFiles res/genome/ecoli.fasta  
    –genomeSAindexNbases 9

### 6.3. Aligning our reads to the genome

With our index ready, we can now align our reads to it.

    cd $WD mkdir -p out/star/ERR2868172 STAR –runThreadN 4 –genomeDir
    res/genome/star\_index/  
    –readFilesIn out/cutadapt/ERR2868172\_1.trimmed.fastq.gz
    out/cutadapt/ERR2868172\_2.trimmed.fastq.gz  
    –readFilesCommand zcat  
    –outFileNamePrefix out/star/ERR2868172/

    #### Check what your project looks like

    tree $WD

    #### Check STAR log file to see what it did.

    more $WD/out/star/ERR2868172/Log.final.out

    See details on the SAM format:
    <a href="https://samtools.github.io/hts-specs/SAMv1.pdf" class="uri">https://samtools.github.io/hts-specs/SAMv1.pdf</a>

    #### Look at the output alignments

    head -10 $WD/out/star/ERR2868172/Aligned.out.sam | cut -c1-80

### 6.4. Creating a report for the pipeline

In order to get an overview of what happened with the pipeline, and how
well it worked, we’ll create a report summarizing all the output. For
this, we’ll use the MultiQC software.

MultiQC parses a directory for output and log files from software it
recognizes, and generates a report summarising its finds.

    #### Install multiqc

    conda install -y multiqc

    #### Run MultiQC on your workdir

    multiqc -o out/multiqc $WD

Building a pipeline
--------------

In this section we will be automating the steps that you just performed
manually, so that they can be applied to any input files.

### 7.1. Shell scripts

A shell script is a file text that contains shell commands, variables
and control structures, you can run a script (.sh) by passing bash

**Exercice 1.** Create a shell script that runs all the commands in the previous section, from cutadapt to the STAR alignment.

    echo “Running cutadapt…” cutadapt -m 20 -a
    AGATCGGAAGAGCACACGTCTGAACTCCAGTCA -A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT
    -o out/cutadapt/ERR2868172\_1.trimmed.fastq.gz -p
    out/cutadapt/ERR2868172\_2.trimmed.fastq.gz data/ERR2868173\_1.fastq.gz
    data/ERR2868173\_2.fastq.gz &gt; log/cutadapt/ERR2868172.log echo
    “Running STAR index…” STAR –runThreadN 4 –runMode genomeGenerate
    –genomeDir res/genome/star\_index/ –genomeFastaFiles
    res/genome/ecoli.fasta –genomeSAindexNbases 9 echo “Running STAR
    alignment…” STAR –runThreadN 4 –genomeDir res/genome/star\_index/
    –readFilesIn out/cutadapt/ERR2868172\_1.trimmed.fastq.gz
    out/cutadapt/ERR2868172\_2.trimmed.fastq.gz –readFilesCommand zcat
    –outFileNamePrefix out/star/ERR2868172/

**Exercice 2.** Modify your pipeline script so that it takes the sample ID as an argument.


    In this case, instead of directly using the “$1” special variable in every line of code, we first assign it to a new variable “sampleid”. This will help make our code clearer.

    The problem is that we sometimes insert our variable before characters that could also be part of a valid variable name. In the case of “$sampleid\_1.trimmed.fastq.gz" and "$sampleid\_2.trimmed.fastq.gz”, the shell would think that the variables we are asking for are “sampleid\_1” and “sampleid\_2”. The dot (.) is not allowed in variable names, so the rest of the string would not be considered.

    To prevent this from happening, we simply surround our variable name with curly braces when inserting it into the strings, as you can see below.


    sampleid=$1

    echo “Running cutadapt…” cutadapt -m 20 -a
    AGATCGGAAGAGCACACGTCTGAACTCCAGTCA -A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT
    -o
    out/cutadapt/*s**a**m**p**l**e**i**d*<sub>1</sub>.*t**r**i**m**m**e**d*.*f**a**s**t**q*.*g**z* − *p**o**u**t*/*c**u**t**a**d**a**p**t*/{sampleid}\_2.trimmed.fastq.gz
    data/*s**a**m**p**l**e**i**d*<sub>1</sub>.*f**a**s**t**q*.*g**z**d**a**t**a*/{sampleid}\_2.fastq.gz
    \#&gt;
    log/cutadapt/${sampleid}.log echo "Running STAR index..." STAR --runThreadN 4 --runMode genomeGenerate --genomeDir res/genome/star\_index/ --genomeFastaFiles res/genome/ecoli.fasta --genomeSAindexNbases 9 echo "Running STAR alignment..." STAR --runThreadN 4 --genomeDir res/genome/star\_index/ --readFilesIn out/cutadapt/${sampleid}\_1.trimmed.fastq.gz
    out/cutadapt/*s**a**m**p**l**e**i**d*<sub>2</sub>.*t**r**i**m**m**e**d*.*f**a**s**t**q*.*g**z* −  − *r**e**a**d**F**i**l**e**s**C**o**m**m**a**n**d**z**c**a**t* −  − *o**u**t**F**i**l**e**N**a**m**e**P**r**e**f**i**x**o**u**t*/*s**t**a**r*/{sampleid}/

### 7.2. Control structures in the shell

Control structures are statements in programming languages that control
the flow of the program depending on the outcome of certain conditions.

    #### The if structure

    if allows us to take one action or another depending on the result of a
    condition. In this case, we are comparing a and b for equality (-eq).
    Other possible numerical comparison operators are greater than (-gt),
    less than (-lt), and not equal to (-ne).

    a=1 b=10

    if \[ “$a" -eq "$b” \] then echo “$a is equal to $b" else  echo "$a is
    not equal to $b” fi

**Exercice 3.** Modify your pipeline so that it prints usage information and exits if there is no input argument.

    if \[ “$\#” -eq 1 \] \#check if the number of arguments received equals
    1 then sampleid=$1

    echo "Running cutadapt..."
    cutadapt -m 20 -a AGATCGGAAGAGCACACGTCTGAACTCCAGTCA -A AGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGT -o out/cutadapt/${sampleid}_1.trimmed.fastq.gz -p out/cutadapt/${sampleid}_2.trimmed.fastq.gz data/${sampleid}_1.fastq.gz data/${sampleid}_2.fastq.gz > log/cutadapt/${sampleid}.log
    echo "Running STAR index..."
    STAR --runThreadN 4 --runMode genomeGenerate --genomeDir res/genome/star_index/ --genomeFastaFiles res/genome/ecoli.fasta --genomeSAindexNbases 9
    echo "Running STAR alignment..."
    STAR --runThreadN 4 --genomeDir res/genome/star_index/ --readFilesIn out/cutadapt/${sampleid}_1.trimmed.fastq.gz out/cutadapt/${sampleid}_2.trimmed.fastq.gz --readFilesCommand zcat --outFileNamePrefix out/star/${sampleid}/

    else echo “Usage: $0 <sampleid>” \#the special variable $0 contains the
    name of the script

    # In the next line, return an error signal instead of the default OK signal.
    # This allows us to run something like
    #       bash ex03.sh && bash nextscript.sh
    # where the second script will only run if the first one finishes OK, or
    #       bash ex03.sh || bash cleanup.sh
    # where the second script will only be run if the first one fails.
    exit 1

    fi

    #### The for structure

    for allows you to loop parts of your script for different values of a
    variable.

    for name in {Erwin,Max,Rosalind,Marie} do echo Hi, my name is $name done

    for i in {001..005} do echo sample$i done

    #### Control structures in the command line

    Any shell command that you see inside a script can also be used in the
    command line directly. The challenge is that you input things one line
    at a time, and long scripts can become complicated really quickly. Some
    control structures are very useful though. As an example, let’s see how
    we could write a for loop in single-line format to copy all our
    subsampled files to the /tmp/datafiles directory.

    cd $WD mkdir /tmp/datafiles for file in data/\*.fastq.gz; do cp $file
    /tmp/datafiles/; done; ls /tmp/datafiles

**Exercice 4.** Write a command line for loop that generates all sample ids from your data.

    for sample in $(ls data/\*.fastq.gz | cut -d"\_" -f1 | sed “s:data/::” |
    sort | uniq); do echo $sample; done;

**Exercice 5.** Use the loop in the previous exercise to run your pipeline for all your samples.

    for sid in $(ls data/\*.fastq.gz | cut -d"\_" -f1 | sed “s:data/::” |
    sort | uniq) do bash scripts/pipeline.sh $sid done
