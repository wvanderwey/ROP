## ROP analysis of one RNA-Seq sample

In this step we will show how to analyze one RNA-Seq sample. We use RNA-Seq sample of normal skin (SRR1146076)  downloaded from [here](http://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE54456). Please note 
that proposed sample is not necessarily the most typical RNA-Seq sample and is provided for demonstration purposes. 

Please make sure that the basic unix commands (wget, tar) are available on the cluster. 

The size of the original reads (.fastq) is 6.5G. Please mapped the reads with any of available high-throughput aligners (e.g. [tophat2](https://ccb.jhu.edu/software/tophat/index.shtml), [STAR](https://github.com/alexdobin/STAR)). Please save the unmapped reads in .fastq (text format) or .bam (binary file, requires less space) formats.  

The instructions how to map the reads and save the unmapped reads are provided here. 

The size of the unmapped reads in .fastq format is  1.4G. The size of the unmapped reads in .bam format is 0.3G
The size of the mapped reads (.bam) is 1.2G. 


The first operation consists in obtaining the last version of ROP from [here](http://serghei.bioinformatics.ucla.edu/rop/), which can be downloaded as zip, gz, or bz2 compressed archives. In a Unix environment, you can obtain and uncompress it from the command line:

```
$ wget https://github.com/smangul1/rop/archive/v0.2.tar.gz
$ tar -zxvf v0.2.tar.gz
$ mv rop-* rop
```



## ROP output details
## ROP analysis of single and multiple samples

