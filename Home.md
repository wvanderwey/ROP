
<img src="http://serghei.bioinformatics.ucla.edu/wp-content/uploads/sites/6/2015/10/rop.png" width="500">


## What is ROP?

Read Origin Protocol(ROP) is a computational protocol aimed to discover the source of all reads, which originate from complex RNA molecules, recombinant antibodies and microbial communities. The ROP accounts for the vast majority of all reads across different library preparation protocols protocols. ROP explores mapped and unmapped reads profiles repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities.  The ROP is not limited to RNA-Seq technology and might be applied to whole-exome and whole-genome sequencing (special parameters might be required, please contact Serghei Mangul, smangul@ucla.edu, if you are planning to use ROP for whole-exome or whole-genome sequencing).

## Get started 
This tutorial focuses on performing a comprehensive analysis analysis of unmapped reads to profile repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities. 
This tutorial is a step-by-step description of the ROP (Read Origin Protocol) pipeline to explore the unmapped reads left from you study. 

We assume you have a basic knowledge of sequence analysis and of Unix-based operating systems (although you should be able to run the pipeline on MacOS, some commands may require modification). If you have limited knowledge of UNIX, we encourage you to follow the [online video tutorial](http://qcb.ucla.edu/collaboratory/workshops/collaboratory-workshop-1/) for UNIX . The UNIX tutorial is 9 hour video tutorial covering the basic concepts of UNIX operating system. After completing the tutorial you should be able to confidently use the command line interface on either a local (laptop) or remote (cluster) Unix system and to navigate around the Unix file system from the command line and use a number of basic, common Unix commands. The UNIX tutorial is supplemented with many hands-on exercises. Python  is required to be installed on the cluster you are planning to perform the analysis.

Please do not hesitate to contact us if you have any comments, suggestions, or clarification requests regarding the tutorial or if you would like to contribute to this resource. 

## How do I Install ROP?

Please get the latest release from [here](http://serghei.bioinformatics.ucla.edu/rop/).


No installation is required. The ROP comes with no pre-requirements. Instead ROP is distributed with several open source components that were developed by other groups (see section Third Party software from [here](http://serghei.bioinformatics.ucla.edu/rop/)). 

ROP requires the prepared refference databases for human and microbial sequences, which can be download as follows:

```bash
python install.py 
``` 

The 'installation' takes 45 minutes on average and requires 30Gb of available space to download the refference. 

## Toy example

Small training data (3000 unmapped reads saved in <fastq> format) is distributed with the ROP package and can access under this directory:

 ```bash
<dir>/rop/example/unmappedExample.fastq
``` 

ROP requires 2 command line parameters, i.e. the unmapped reads and the directory to save the results of ROP. 

```
usage: python rop.py [-h] [--qsub] [--qsubArray] [--b] [--skipLowq] [--skipQC]
                     [--circRNA] [--immune] [--gzip] [--quiet] [--dev]
                     [--license]
                     unmappedReads dir
```
To test ROP for the small training data use the following command under the ROP directory: 

 ```bash
rop.py example/unmappedExample.fastq example/<out>/
```

where <out> is the directory the results to be saved 
 
You expect the following output of the ROP pipeline:

```
*********************************************
ROP is a computational protocol aimed to discover the source of all reads, originated from complex RNA molecules, recombinant antibodies and microbial communities. Written by Serghei Mangul (smangul@ucla.edu) and Harry Taegyun Yang (harry2416@gmail.com), University of California, Los Angeles (UCLA). (c) 2016. Released under the terms of the General Public License version 3.0 (GPLv3)

For more details see:
http://serghei.bioinformatics.ucla.edu/rop/
*********************************************
Processing 2505 unmapped reads
1. Quality Control...
--filtered 2193 low quality reads
--filtered 2 low complexity reads (e.g. ACACACAC...)
--filtered 22 rRNA reads
In toto : 2217 reads failed QC and are filtered out
2. Remaping to human references...
--identified 6 lost human reads from unmapped reads 
3. Maping to repeat sequences...
-Identify 1 lost repeat sequences from unmapped reads
***Note : Repeat sequences classification into classes (e.g. LINE) and families (e.g. Alu) will be available in next release
3. Non-co-linear RNA profiling
Please use --circRNA options to profile circular RNAs
***Note : Trans-spicing and gene fusions  are currently not supported, but will be in the next release.
4a. B lymphocytes profiling...
--identified 0 reads mapped to immunoglobulin heavy (IGH) locus
--identified 0 reads mapped to immunoglobulin kappa (IGK) locus 
--identified 0 reads mapped to immunoglobulin lambda (IGL) locus
4b. T lymphocytes profiling...
--identified 0 reads mapped to T cell receptor alpha (TCRA) locus
--identified 0 reads mapped to T cell receptor beta (TCRB) locus
--identified 0 reads mapped to T cell receptor delta (TCRD) locus
--identified 0 reads mapped to T cell receptor gamma locus (TCRG) locus
In toto : 0 reads mapped to antibody repertoire loci
***Note : Combinatorial diversity of the antibody repertoire (recombinations of the of VJ gene segments)  will be available in the next release.
5.  Microbiome profiling...
--identified 0 reads mapped bacterial genomes
--identified 0 reads mapped viral genomes
--identified 4 reads mapped ameoba genomes
--identified 1 reads mapped crypto genomes
--identified 0 reads mapped giardia genomes
--identified 0 reads mapped microsporidia genomes
--identified 0 reads mapped piroplasma genomes
--identified 1 reads mapped plasmo genomes
--identified 1 reads mapped toxo genomes
--identified 0 reads mapped trich genomes
--identified 0 reads mapped tritryp genomes
In toto : 7 reads mapped to microbial genomes
Summary:   The ROP protocol is able to account for 2231 reads
``` 

## Running the ROP