## What is ROP?

Read Origin Protocol (ROP) is a computational protocol aimed to discover the source of all reads, which originate from complex RNA molecules, recombinant antibodies and microbial communities. The ROP accounts for the vast majority of all reads across different library preparation protocols protocols. ROP explores mapped and unmapped reads profiles repeats, circRNAs, gene fusions, trans-splicing events, recombined B/T-cell receptor sequences and microbial communities.  The ROP is not limited to RNA-Seq technology and might be applied to whole-exome and whole-genome sequencing (special parameters might be required, please contact Serghei Mangul, smangul@ucla.edu, if you are planning to use ROP for whole-exome or whole-genome sequencing).


<img src="http://serghei.bioinformatics.ucla.edu/wp-content/uploads/sites/6/2015/10/rop.png" width="350">

## How ROP works

The ROP is able to explore both mapped(optional) and unmapped reads. Please mapped the reads with any of available high-throughput aligners (e.g. [tophat2](https://ccb.jhu.edu/software/tophat/index.shtml), [STAR](https://github.com/alexdobin/STAR)). 

ROP protocol consists of two steps to categorize the mapped reads:

** Categorize human reads into genomic categories (CDS, UTR3/UTR5, intons, junctions, introns, etc).
** We developed rprofile, a tool to profile repetitive elements (e.g. SINEs, LINEs, LTRs).