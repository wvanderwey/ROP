In case you are interested to skip STEP1 (Quality Control) please use option `--skipQC`. Please note that in this case low quality , low complexity and rRNA reads will not be filtered out. The input reads must be in the FASTA format (`.fa`  or `.fasta` extension)

Please run ROP as follows:

```
python rop.py --skipQC example/test.fa example/ropOut60/
```


In case you are interested in unmapped reads with the reads from QC step to be filtered out, please use `--dev` option to save the `afterQC.fastq`.  

# Analysis of interest 