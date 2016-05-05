## ROP analysis of one RNA-Seq sample

In this step we will show how to analyze one RNA-Seq sample. We use RNA-Seq sample of normal skin (SRR1146076)  downloaded from [here](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE54456). Please note 
that proposed sample is not necessarily the most typical RNA-Seq sample and is provided for demonstration purposes. 

Please make sure that the basic unix commands (wget) are available on the cluster. The size of the original reads (.fastq) is 6.5G. Please mapped the reads with any of available high-throughput aligners (e.g. [tophat2](https://ccb.jhu.edu/software/tophat/index.shtml), [STAR](https://github.com/alexdobin/STAR)). Please save the unmapped reads in .fastq (text format) or .bam (binary file, requires less space) formats.  

The instructions how to map the reads and save the unmapped reads are provided [here](https://github.com/smangul1/rop/wiki/How-to-map-reads-and-save-unmapped-reads). 

The instructions how to install ROP are provided [here](https://github.com/smangul1/rop/wiki/How-to-install-ROP%3F) 

The size of the unmapped reads in .fastq format is  1.4G. The size of the unmapped reads in .bam format is 0.3G
The size of the mapped reads (.bam) is 1.2G. 


The first operation consists in navigating to ROP directory and creating a subdirectory for storing the training data. 

```
cd rop
mkdir tutorial
cd tutorial
mkdir data
```

Now, download the mapped and unmapped reads from RNA-Seq

```
wget (to fix)
```

Now we are ready to analyze the RNA-Seq sample using ROP. We are running ROP using the default options. ROP is an intensive pipeline requiring substantial amount of computations resources. Thus you aren't supposed to run ROP from login nodes (expect running ROP for toy sample as described [here](https://github.com/smangul1/rop/wiki/Get-started)). Please check the policy of you cluster, from where to run the ROP pipeline. For hoffman2 (UCLA cluster) read the policy [here] (http://ccn.ucla.edu/wiki/index.php/Hoffman2:Interactive_Sessions). 

ROP has advanced options to paralyze the analysis by scheduling multiple computing jobs. More details about advances options are available [here](https://github.com/smangul1/rop/wiki/Advanced-options).



## ROP output details
## ROP analysis of single and multiple samples

