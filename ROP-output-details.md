
Here we describe the output structure of the ROP pipeline. The details of the ROP pipeline are explain [here] (https://github.com/smangul1/rop/wiki/What-is-ROP). The ROP output consist of six directories corresponding to six steps of the ROP analysis of the unmapped reads. Additionally it contains two directories corresponding to optional modules to characterize the mapped reads. 

This is the typical output of the ROP pipeline

```
-rw-r--r-- 1 serghei eeskin 11516 May  5 14:28 dev.log
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostHumanReads
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostRepeatSequences
drwxr-xr-x 5 serghei eeskin  4096 May  5 14:24 microbiomeProfile
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:24 NCL
-rw-r--r-- 1 serghei eeskin    39 May  5 14:28 numberReads_unmappedExample.log
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:28 QC
drwxr-xr-x 6 serghei eeskin  4096 May  5 14:24 antibodyProfile
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

The directory contains the output of [Step 2. Remap to human sequences] (https://github.com/smangul1/rop/wiki/What-is-ROP%3F).  The lost human reads mapped to the human reference genome are saved into the `_genome.sam` and reads mapped to the transcriptome reference are saved into the `_transcriptome.sam`.


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

An example of the unmapped read mapped to L1 retrotransposon

```
SRR1146076.9992259      L1PA4-L1-Homo   97.44   78      2       0       2       79      795     872     3e-33    134

```

## NCL directory

This directory contains the output of Step 4 (Non-co-linear (NCL) RNA profiling). More details will be posted soon

## antibodyProfile directory

This directory contains the output of [Step 5. B and T lymphocytes profiling](https://github.com/smangul1/rop/wiki/What-is-ROP%3F). It contains a separate directory for B cell receptors (BCR) : `BCR` directory and a separate directory for T cell receptor (TCR) :  `TCR` directory. 

BCR directory contains:

* IGH a directory for immunoglobulin heavy locus profile 
* IGK a directory for IGK IGK immunoglobulin kappa locus
* IGL a directory for immunoglobulin lambda locus profile 

TCR directory contains:

* TCRA a directory for T cell receptor alpha locus
* TCRB a directory for T cell receptor beta locus
* TCRD a directory for T cell receptor gamma locus
* TCRG a directory for T cell receptor delta locus

Reads spanning antigen receptor gene rearrangement in the variable domain are identified using [IgBLAST](http://mirrors.vbi.vt.edu/mirrors/ftp.ncbi.nih.gov/blast/executables/igblast/release/1.4.0/).  IgBLAST reports
alignment of the reads to the variable (V) gene, the diversity (D) gene and the joining (J) gene, or the recombination of those. Reads alignment is saved into the `_igblast.csv` (modified tabular output format 6).

n | id| What does it mean? 
:-- | :-- | :--
0 | VDJ | gene segment 
1 | qseqid |read name  
2 | sseqid |reference genome   
3 | pident |percentage of identical matches  
4 | length |alignment length
5 | mismatch | number of mismatches
6|	 gapopen	| number of gap openings
 7|	 qstart	| start of alignment in query
 8|	 qend	| end of alignment in query
 9|	 sstart	| start of alignment in subject
 10|	 send	| end of alignment in subject
 11|	 evalue	| expect value
 12|	 bitscore	| bit score

An example of the unmapped read aligned to the immunoglobulin heavy variable 1-46 gene (IGHV1-46)

```
V       SRR1146076.56325        IGHV1-46*01     93.67   79      5       0       0       1       79      203     281     7e-27     109
```

## microbiomeProfile directory

This directory contains the output of [Step 6. Microbiome profiling](https://github.com/smangul1/rop/wiki/What-is-ROP%3F). It contains a separate directory for each class of microbial organisms. Reads mapped to the microbial genomes are saved in `_blastFormat6.csv`. Microbial reads are further filter to save high confident alignments in `Filtered_blastFormat6.csv`

* viralProfile
* bacteriaProfile
* eukaryoticPathogenProfile

An example of the unmapped read aligned to the Cryptosporidium muris(DS989729), a species of coccidium

```
SRR1146076.9993022      DS989729        85.92   71      9       1       1       70      454894  454964  5e-13   75.0
```

###genomicProfile directory 

This directory contains the output of optional module which determines genomic profile of RNA-Seq. It categorizes the mapped reads into genomic categories based on the compatibility of each read with the features defined by gene annotations.

It will estimate relative proportions of genomic categories (e.g. CDS, introns) based on the number of reads from the category. Those are the categories used by the ROP (more details are [here](https://github.com/smangul1/rop/wiki/What-is-ROP%3F))

* multi-mapped read
* CDS
* intron
* UTR3
* UTR5 
* UTR
* junction read
* inter-genic read
* deep inter-genic read
* mitochondrial DNA
* fusion reads

An example of the genomic profile of a RNA-Seq sample 

```
sampleName,nTotalMapped,nJunction,nCDS,nUTR3,nUTR5,nUTR_,nMixed,nIntron,nIntergenic,nDeep,nFussion,nrRNA,nMT,nMultiMapped
--,57012335,6698066,4632060,7223406,2342899,1298331,0,28870771,2382707,2336668,534336,7441,337688,1646293
```

This module also provide the option to get the detailed information about the reads assignment to the genomic categories. Choose the `--perCategory` option and get the genomic category for each mapped read.  A separate file per chromosome will be created (e.g. `mappedReads.22.genomicFeature`).

An example of a file corresponding to chr22 i.e. reads assigned to genomic features from chr22 

```
SRR1146076.3540543,22,junction
SRR1146076.17070789,22,UTR5
SRR1146076.21758998,22,UTR5
SRR1146076.20543213,22,UTR5
SRR1146076.9808865,22,DEEP
SRR1146076.16863731,22,INTERGENIC
SRR1146076.968340,22,UTR3
```




### repeatProfile directory 

ROP has the functionality to output the genomic feature for each mapped read, which can be saved into a separate file. Be aware that it might take the significant space from the cluster. More details are [here](https://github.com/smangul1/rop/wiki/Additional-options)


It will estimate relative proportions of repeat categories (e.g. LINE. SINE, LTR) based on the number of reads from the category. More details about the repeat categories used by ROP are [here](https://github.com/smangul1/rop/wiki/What-is-ROP%3F/)

The ROP provided three levels of repeat profile, i.e class level (e.g SINE, LINE); family level (e.g. Alu, L1); gene level (e.g. L1P4c). Those the output files created for each level 

* Class level  : `<sampleName>_repeat.repeatClass.csv`
* Family level : `<sampleName>_repeat.repeatFamily.csv`
* Gene level   : `<sampleName>_repeat.repeatGene.csv`


An example of the repeat profile from one [GTEX](www.gtexportal.org/) sample:

```
sample,LINE?,LTR,Satellite,Retroposon,DNA,SINE?,RNA,DNA?,RC,LINE,SINE,LTR?
G42480.GTEX-QESD-0426.2,0,258615,2036,7691,163674,122,347,3115,439,570393,790630,32
```

