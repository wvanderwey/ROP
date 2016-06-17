More details will be added ...

Here we explain how to compare the immune and microbiome profiles across multiple sample corresponding to different phenotypes or disease groups.  

```
while read line ; do echo "python ~/collab/code/rop/rop.py $PWD/unmaaped/${line}.fastq $PWD//rop/${line} --qsubArray">run_${line}.sh;done<sample.txt
```