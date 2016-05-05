## What is ROP?

Read Origin Protocol (ROP) is a computational protocol aimed to discover the source of all reads, which originate from complex RNA molecules, recombinant antibodies and microbial communities. The ROP accounts for the vast majority of all reads across different library preparation protocols protocols. ROP explores mapped and unmapped reads profiles repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities.  The ROP is not limited to RNA-Seq technology and might be applied to whole-exome and whole-genome sequencing (special parameters might be required, please contact Serghei Mangul, smangul@ucla.edu, if you are planning to use ROP for whole-exome or whole-genome sequencing).


<img src="http://serghei.bioinformatics.ucla.edu/wp-content/uploads/sites/6/2015/10/rop.png" width="350">

## How ROP works

The ROP is able to explore both mapped(optional) and unmapped reads. Please mapped the reads with any of available high-throughput aligners (e.g. [tophat2](https://ccb.jhu.edu/software/tophat/index.shtml), [STAR](https://github.com/alexdobin/STAR)). 

ROP protocol consists of two steps to categorize the mapped reads:
* Categorize human reads into genomic categories (CDS, UTR3/UTR5, intons, junctions, introns, etc). 
* Profile repeat elements (e.g. SINEs, LINEs, LTRs)

ROP prococol consist of six steps to characterize the unmapped reads:

* Quality control. Exclude low-quality, low-complexity and rRNA reads ([FASTX](http://hannonlab.cshl.edu/fastx_toolkit/commandline.html), [SEQCLEAN](https://sourceforge.net/projects/seqclean/), [Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/))
*Identify lost human reads, which are missed due to the heuristics implemented for computational speed in conventional aligners. These include reads with mismatches and short gaps relative to the reference set, but can also include perfectly matched reads ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/))
*Identify lost repeat sequences, by mapping unmapped reads onto the database of repeat sequences ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) )
Identify ‘non-co-linear’ RNAs reads from circRNAs, gene fusions, and trans-splicing events, which combine sequence from distant elements (ncSplice, [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) , [CIRI](https://github.com/Frenzchen/ncSplice))
Identify reads from recomobinations of B and T cell receptors i.e. V(D)J recombinations ([IgBLAST](http://mirrors.vbi.vt.edu/mirrors/ftp.ncbi.nih.gov/blast/executables/igblast/release/1.4.0/))
Profile taxonomic composition of microbial communities using the microbial reads mapped onto the microbial genomes and marker genes ([Megablast](ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/), [MetaPhlAn](http://huttenhower.sph.harvard.edu/metaphlan))