##About the ROP tutorial 

This tutorial focuses on performing a comprehensive analysis analysis of unmapped reads to profile repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities. This tutorial is a step-by-step description of the ROP (Read Origin Protocol) pipeline to explore the unmapped reads left from you study.

We assume you have a basic knowledge of sequence analysis and of Unix-based operating systems (although you should be able to run the pipeline on MacOS, some commands may require modification). If you have limited knowledge of UNIX, we encourage you to follow the online [video tutorial](http://qcb.ucla.edu/collaboratory/workshops/collaboratory-workshop-1/) for UNIX . The UNIX tutorial is 9 hour video tutorial covering the basic concepts of UNIX operating system. After completing the tutorial you should be able to confidently use the command line interface on either a local (laptop) or remote (cluster) Unix system and to navigate around the Unix file system from the command line and use a number of basic, common Unix commands. The UNIX tutorial is supplemented with many hands-on exercises. 

Alternatively you can use slides from the UNIX tutorial : [Day1](https://www.dropbox.com/s/ggv7ijwateim7zt/day1_Unix.pdf?dl=0), [Day2](https://www.dropbox.com/s/xorsuvk1cugiyw8/day2_Unix.pdf?dl=0), [Day3] (https://www.dropbox.com/s/88wu7svvfur8upw/day3_Unix.pdf?dl=0)

Please do not hesitate to contact us (smangul@ucla.edu) if you have any comments, suggestions, or clarification requests regarding the tutorial or if you would like to contribute to this resource.

#How to install ROP?

Details are [here](https://github.com/smangul1/rop/wiki/How-to-install-ROP%3F)

#Toy example

Small training data (3000 unmapped reads saved in .fastq format) is distributed with the ROP package. Please note 
that selected reads are randomly selected and might not represent the typical reads of RNA-Seq experiment. The reads are provided for demonstration purposes and can be accessed under ROP directory:

```
/rop/example/unmappedExample.fastq
```

ROP requires two mandatory command line arguments, i.e. (1) the unmapped reads and (2) the directory to save the results of ROP.

```
usage: python rop.py [-h] [--qsub] [--qsubArray] [--b] [--skipLowq] [--skipQC]
                     [--circRNA] [--immune] [--gzip] [--quiet] [--dev]
                     [--license]
                     unmappedReads dir
```

To test ROP for the small training data use the following command under the ROP directory, where results will be saved to example/ropOut/ directory

```
python rop.py example/unmappedExample.fastq example/ropOut/
```

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
3. Mapping to repeat sequences...
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

##Genomic profile of RNA-Seq

To get the genomic profile of the mapped reads use `gprofile.py`. To get the genomic profile of the toy bam file (reads from chr22) use the following command:

```
python gprofile.py example/mappedReads_chr22.bam /example/mappedReads_chr22.csv
```

The output of the module is number of reads assigned to each genomic category saved into the `/example/mappedReads_chr22.csv`

```
sampleName,nTotalMapped,nJunction,nCDS,nUTR3,nUTR5,nUTR_,nIntron,nIntergenic,nDeep,nMT,nMultiMapped
mappedReads,397134,129580,101541,96210,7457,22473,19420,3084,649,0,16720
```

You can use `/example/mappedReads_chr22.csv` to create pie chart. The  pie chart corresponding to `/example/mappedReads_chr22.csv` is presented bellow:

![Genomic profile of toy .bam file](https://sergheimangul.files.wordpress.com/2016/05/gprofile.png?w=1280)

Read more about Genomic Profile of RNA-Seq [here](https://github.com/smangul1/rop/wiki/ROP-output-details).

