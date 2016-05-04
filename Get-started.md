##About the ROP tutorial 

This tutorial focuses on performing a comprehensive analysis analysis of unmapped reads to profile repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities. This tutorial is a step-by-step description of the ROP (Read Origin Protocol) pipeline to explore the unmapped reads left from you study.

We assume you have a basic knowledge of sequence analysis and of Unix-based operating systems (although you should be able to run the pipeline on MacOS, some commands may require modification). If you have limited knowledge of UNIX, we encourage you to follow the online [video tutorial](http://qcb.ucla.edu/collaboratory/workshops/collaboratory-workshop-1/) for UNIX . The UNIX tutorial is 9 hour video tutorial covering the basic concepts of UNIX operating system. After completing the tutorial you should be able to confidently use the command line interface on either a local (laptop) or remote (cluster) Unix system and to navigate around the Unix file system from the command line and use a number of basic, common Unix commands. The UNIX tutorial is supplemented with many hands-on exercises. Python is required to be installed on the cluster you are planning to perform the analysis.


#How to install ROP?

Please get the latest release from [here](http://serghei.bioinformatics.ucla.edu/rop/).

No installation is required. The ROP comes with no pre-requirements except Python. Python is required to be installed on the cluster you are planning to perform the analysis.ROP is distributed with several open source components that were developed by other groups (see section Third Party software from here).

ROP requires the prepared refference databases for human and microbial sequences, which can be download as follows:

```
python install.py
```
 
The 'installation' takes 45 minutes on average and requires 30Gb of available space to download the refference.