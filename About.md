## What is ROP?

Read Origin Protocol (ROP) is a computational protocol aimed to discover the source of all reads, which originate from complex RNA molecules, recombinant antibodies and microbial communities. The ROP accounts for the vast majority of all reads across different library preparation protocols protocols. ROP explores mapped and unmapped reads profiles repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities.  The ROP is not limited to RNA-Seq technology and might be applied to whole-exome and whole-genome sequencing (special parameters might be required, please contact Serghei Mangul, smangul@ucla.edu, if you are planning to use ROP for whole-exome or whole-genome sequencing).


<img src="http://serghei.bioinformatics.ucla.edu/wp-content/uploads/sites/6/2015/10/rop.png" width="350">

## How ROP works

The ROP is able to explore both mapped(optional) and unmapped reads. Please mapped the reads with any of available high-throughput aligners (e.g. [tophat2](https://ccb.jhu.edu/software/tophat/index.shtml), [STAR](https://github.com/alexdobin/STAR)). 

ROP protocol consists of two steps to categorize the mapped reads:
* We developed [gprofile](https://github.com/smangul1/gprofile), a  tools to categorize mapped reads into genomic categories (CDS, UTR, intons, etc)  (details)
* We developed [rprofile](https://github.com/smangul1/rprofile), a tool to profile repetitive elements (e.g. SINEs, LINEs, LTRs)

ROP protocol consist of six steps to characterize the unmapped reads:

* Quality control. Exclude low-quality, low-complexity and rRNA reads ([FASTX](http://hannonlab.cshl.edu/fastx_toolkit/commandline.html), [SEQCLEAN](https://sourceforge.net/projects/seqclean/), [Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/))
* Identify lost human reads, which are missed due to the heuristics implemented for computational speed in conventional aligners. These include reads with mismatches and short gaps relative to the reference set, but can also include perfectly matched reads ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/))
* Identify lost repeat sequences, by mapping unmapped reads onto the database of repeat sequences ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) )
* Identify ‘non-co-linear’ RNAs reads from circRNAs, gene fusions, and trans-splicing events, which combine sequence from distant elements (ncSplice, [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) , [CIRI](https://github.com/Frenzchen/ncSplice))
* Identify reads from recomobinations of B and T cell receptors i.e. V(D)J recombinations ([IgBLAST](http://mirrors.vbi.vt.edu/mirrors/ftp.ncbi.nih.gov/blast/executables/igblast/release/1.4.0/))
* Profile taxonomic composition of microbial communities using the microbial reads mapped onto the microbial genomes and marker genes ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/), [MetaPhlAn](http://huttenhower.sph.harvard.edu/metaphlan))


##Genomic profile of RNA-Seq

We developed [gprofile](https://github.com/smangul1/gprofile) to categorize the reads into genomic categories based on the compatibility of each read with the features defined by gene annotations. Genomic profile can be used to benchmark different sequencing platform and library preparation methods, as well as assess the efficiency of rRNA depletion and level of the sample degradation.  

Those are the categories of the genomic profile:  

a.	Read mapped to multiple locations on the reference genome is categorized as a multi-mapped read.
b.	Read fully contained within the CDS, intron, UTR3, or UTR5 boundaries of a least one transcript is classified as a CDS, intronic, UTR3, or UTR5, respectively.
c.	Read simultaneously overlapping UTR3 and UTR5 regions is classified as a UTR read.
d.	Read spanning exon-exon boundary is defined as a junction read.
e.	Read mapped outside of gene boundaries and within a proximity of 1Kb is defined as a (proximal) inter-genic read.
f.	Read mapped outside of gene boundaries and beyond the proximity of 1Kb is defined as a deep inter-genic read.
g.	Read contained within mitochondrial DNA (MT tag in hg19) is classified as a mitochondrial read.
h.	Read which has a pair which two ends are mapped to different chromosomes is classified as a fusion read.

