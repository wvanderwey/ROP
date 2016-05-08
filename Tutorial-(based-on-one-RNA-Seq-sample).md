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

Now we are ready to analyze the RNA-Seq sample using ROP. We are running ROP using the default options. ROP is an intensive pipeline requiring substantial amount of computations resources. Thus you aren't supposed to run ROP from login nodes (expect running ROP for toy sample as described [here](https://github.com/smangul1/rop/wiki/Get-started)). Please check the policy of you cluster, from where to run the ROP pipeline. For hoffman2 (UCLA cluster) read the policy [here] (http://ccn.ucla.edu/wiki/index.php/Hoffman2:Interactive_Sessions).  ROP has advanced options to parallelize the ROP analysis by scheduling multiple computing jobs. More details about advances options are available [here](https://github.com/smangul1/rop/wiki/Advanced-options).

To run ROP for unmapped reads in .bam format 
```
python rop.py --b tutorial/data/unmapped_SR_1146076.bam /tutorial/ropOut/
```

To run ROP for unmapped reads in .fastq format 

```
python rop.py  tutorial/data/unmapped_SR_1146076.fastq /tutorial/ropOut/
```

Please refer to the ROP help ($ python rop.py -h) 

```
python rop.py -h
usage: python rop.py [-h] [--qsub] [--qsubArray] [--b] [--skipLowq] [--skipQC]
                     [--circRNA] [--immune] [--gzip] [--quiet] [--dev]
                     [--license] [--version]
                     unmappedReads dir

positional arguments:
  unmappedReads  unmapped Reads in the fastq format
  dir            directory (absolute path) to save results of the analysis

optional arguments:
  -h, --help     show this help message and exit
  --qsub         submit qsub jobs on hoffman2 cluster
  --qsubArray    prepare qsub scripts to be run later using job array
  --b            if unmapped reads are in bam format
  --skipLowq     skip filtering step
  --skipQC       skip entire QC step : filtering low-quality, low-complexity
                 and rRNA reads (reads matching rRNA repeat unit)
  --circRNA      enable CIRI for circular RNA detection
  --immune       Only TCR/BCR immune gene analysis will be performed
  --gzip         Gzip the fasta files after filtering step
  --quiet        suppress progress report and warnings
  --dev          keep intermediate files
  --license      Show ROP License Information
  --version      Show ROP version
```

The ROP pipeline consist of two optional modules to characterize the mapped reads. To activate the genomic profile module, use --gprofile option. To activate the genomic profile module, use --rprofile option. Make sure to provide the mapped reads in .bam format. TO download the mapped reads in .bam format use this command 


```
cd tutorial/data/
wget (to fix)
```

After the bam file was downloaded run the following ROP command 

```
python rop.py --gprofile --rprofile --mapped tutorial/data/mapped_SR_1146076.bam tutorial/data/unmapped_SR_1146076.fastq /tutorial/ropOut/
```

You should expect the following output of the ROP pipeline on your screen: 

```
*********************************************
ROP is a computational protocol aimed to discover the source of all reads, originated from complex RNA molecules, recombinant antibodies and microbial communities. Written by Serghei Mangul (smangul@ucla.edu) and Harry Taegyun Yang (harry2416@gmail.com), University of California, Los Angeles (UCLA). (c) 2016. Released under the terms of the General Public License version 3.0 (GPLv3)

For more details see:
http://serghei.bioinformatics.ucla.edu/rop/
https://github.com/smangul1/rop/wiki
*********************************************
Processing 7687003 unmapped reads
1. Quality Control...
--filtered 6966209 low quality reads
--filtered 12457 low complexity reads (e.g. ACACACAC...)
--filtered 55299 rRNA reads
In toto : 7033965 reads failed QC and are filtered out
2. Remaping to human references...
--identified 16278 lost human reads from unmapped reads 
3. Maping to repeat sequences...
-Identify 3862 lost repeat sequences from unmapped reads
***Note : Repeat sequences classification into classes (e.g. LINE) and families (e.g. Alu) will be available in next release
3. Non-co-linear RNA profiling
***Note : Trans-spicing and gene fusions  are currently not supported, but will be in the next release.
```


 
More details about additional options and strategies of the ROP are available [here](https://github.com/smangul1/rop/wiki/Additional-options)


The ropOut directory now contains the output of ROP. The structure of the output is explained [here](https://github.com/smangul1/rop/wiki/ROP-output-details)



After running the ROP output is saved in a single directory (specified as a second command line argument). After running ROP in the previous section, output was saved in the ropOut directory. 

To navigate to the ropOut directory use this command 

```
cd /tutorial/ropOut/
```

The directory contains individual directions for each individual analysis. For example there is a separate directory with the analysis of the antibody repertoire. 


#Genomic profile of RNA-Seq

```
sampleName,nTotalMapped,nJunction,nCDS,nUTR3,nUTR5,nUTR_,nIntron,nIntergenic,nDeep,nMT,nMultiMapped
mapped_SR_1146076,17904083,5425835,4535762,3589107,362853,963938,765359,195246,32345,1061075,972563
```

![](https://sergheimangul.files.wordpress.com/2016/05/gprofile1.png?w=1280)
