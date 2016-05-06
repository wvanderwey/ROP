
Here we describe the output structure of the ROP pipeline. The details of the ROP pipeline are explain [here] (https://github.com/smangul1/rop/wiki/What-is-ROP). The ROP output consist of six directories corresponding to six steps of the ROP analysis of the unmapped reads. Additionally it contains two directories corresponding to optional modules to characterize the mapped reads. 

This is the typical output of the ROP pipeline

```
-rw-r--r-- 1 serghei eeskin 11516 May  5 14:28 dev.log
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostHumanReads
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostRepeatSequences
drwxr-xr-x 5 serghei eeskin  4096 May  5 14:24 microbiome
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:24 NCL
-rw-r--r-- 1 serghei eeskin    39 May  5 14:28 numberReads_unmappedExample.log
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:28 QC
drwxr-xr-x 6 serghei eeskin  4096 May  5 14:24 immune
-rw-r--r-- 1 serghei eeskin  2050 May  5 14:28 unmappedExample.log
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 genomicProfile
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 repeatProfile

```


### QC directory

The directory contains the output of Step 1 (Quality Control) . It contains details about the number of low quality, low complexity, and rRNA reads detected.

The information about number of low quality reads in  `_QC.log` logfile obtained using [FASTX](http://hannonlab.cshl.edu/fastx_toolkit/commandline.html

```
Quality cut-off: 20
Minimum percentage: 75
Input: 2505 reads.
Output: 312 reads.
discarded 2193 (87%) low-quality reads.
```

The information about number of low complexity reads in  `_QC.log` logfile obtained using [SEQCLEAN](https://sourceforge.net/projects/seqclean/)

```
Sequences analyzed:       312
-----------------------------------
                   valid:       310  (1 trimmed)
                 trashed:         2
**************************************************
----= Trashing summary =------
              by 'shortq':        1
                by 'dust':        1
------------------------------

```

The information about number of rRNA reads in  `_QC.log` logfile obtained using [Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/)

```
Identified 22 reads mapped to rRNA repeat sequence
```

The reads failed QC are filtered out and the remaining reads are passed to the next step of the ROP analysis. 


### lostHumanReads directory

The directory contains the output of Step 2 (Remap to human sequences).  The lost human reads mapped to the human reference genome are saved into the `_genome.sam` and reads mapped to the transcriptome reference are saved into the `_transcriptome.sam`.


### lostRepeatSequences directory

The directory contains the output of Step 3 (Map to repeat sequences). Reads mapped to the repeat sequences are saved into the  `_blastFormat6.csv` in [tabular output format 6](http://www.metagenomics.wiki/tools/blast/blastn-output-format-6).

n | id| What does it mean? 
:-- | :-- | :--
1 | qseqid |read name  
2 | sseqid |reference genome   
3 | pident |percentage of identical matches  
4 | length |alignment length
5 | mismatch | number of mismatches
5 | mismatch | number of mismatches
6|	 gapopen	| number of gap openings
 7|	 qstart	| start of alignment in query
 8|	 qend	| end of alignment in query
 9|	 sstart	| start of alignment in subject
 10|	 send	| end of alignment in subject
 11|	 evalue	| expect value
 12|	 bitscore	| bit score

## NCL directory

This directory contains the output of Step 4 (Non-co-linear (NCL) RNA profiling). More details will be posted soon

## immune directory

This directory contains the output of [Step 5. (B and T lymphocytes profiling)](https://github.com/smangul1/rop/wiki/What-is-ROP%3F). It contains a separate directory for B cell receptors (BCR) : `BCR` directory and a separate directory for T cell receptor (TCR) :  `TCR` directory. 


