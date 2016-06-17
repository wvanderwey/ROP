More details will be added ...

Here we explain how to compare the immune and microbiome profiles across multiple sample corresponding to different phenotypes or disease groups.  

```
while read line ; do echo "python ~/collab/code/rop/rop.py $PWD/unmaaped/${line}.fastq $PWD//rop/${line} --qsubArray">run_${line}.sh;done<sample.txt
```

The proposed command will create individual `.sh` file for each sample. To run all `.sh` via qsub, use the following commands

```
ls run*sh | awk '{i+=1;print "qsub -cwd -V -N ropBrain"i" -l h_data=16G,time=10:00:00 "$1}' > all.sh
```

```
chmod 755 all.sh
```

```
nohup ./all.sh &
```

In case you have filtered fasta files (after step 1-2 of ROP) and you are planning to do microbiome profiling only, use this command:

```
while read line ; do python ~/collab/code/rop/rop.py --skipPreliminary --microbiome  --qsub $PWD/afterQC/${line}.fasta $PWD//rop2/${line};done<samples.txt
```

If the number of samples is larger then the number of jobs allowed on the cluster use  `--qsubArray`


```
while read line ; do python /u/home/s/serghei//collab/code/rop/rop.py --skipPreliminary --microbiome  --qsubArray $PWD/data/${line}.fasta $PWD//rop/${line};done<sample.txt
```