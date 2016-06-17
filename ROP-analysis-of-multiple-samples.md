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

