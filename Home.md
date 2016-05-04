
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

## Small Training Data

Small training data is distributed with the ROP package and can assess under this directory:

 ```bash
<dir>/rop/example/unmappedExample.fastq
``` 

## Running the ROP


