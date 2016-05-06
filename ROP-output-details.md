
Here we describe the output structure of the ROP pipeline. The details of the ROP pipeline are explain [here] (https://github.com/smangul1/rop/wiki/What-is-ROP). The ROP output consist of six directories corresponding to six steps of the ROP analysis of the unmapped reads. Additionally it contains two directories corresponding to optional modules to characterize the mapped reads. 

This is the typical output of the ROP pipeline

```
ls -l
-rw-r--r-- 1 serghei eeskin 11516 May  5 14:28 dev.log
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostHumanReads
drwxr-xr-x 4 serghei eeskin  4096 May  5 14:24 lostRepeatSequences
drwxr-xr-x 5 serghei eeskin  4096 May  5 14:24 microbiome
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:24 NCL
-rw-r--r-- 1 serghei eeskin    39 May  5 14:28 numberReads_unmappedExample.log
drwxr-xr-x 2 serghei eeskin  4096 May  5 14:28 QC
drwxr-xr-x 6 serghei eeskin  4096 May  5 14:24 immune
-rw-r--r-- 1 serghei eeskin  2050 May  5 14:28 unmappedExample.log
```


### Quality control 