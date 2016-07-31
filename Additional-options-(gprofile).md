In release 1.0.5 we have added additional options for gprofile. 

* --perCategory option reports assignment of each read in the following format:

```
readName,chr,category, geneID,geneName
4029592_h_0_TCTGATG_CGAT,10,CDS,ENSMUSG00000015202,Cnksr3
```

* --mouse option allows to run gprofile for mouse samples. Make sure to allign to genome/transcriptome from NCBIM37 release. 


This is an example how to run gprofile with `--perCategory` and `--mouse` options:

```
python /u/home/s/serghei/collab/code/rop/gprofile.py mapped_SJV040_CGAT.bam gProfile8/mapped_SJV040_CGAT.csv --perCategory --mouse
``` 

By using --perCategory option `gprofile.py` will generate the following:




```
geneName,chr,nJunction,nCDS,nUTR3,nUTR5,nUTR_,nIntron
Plekhg1,2,22,0,0,0
Cand1,16,86,0,0,0
2510003E04Rik,16,76,1,0,0
Tmcc3,0,8,0,2,0
Spryd4,0,1,0,0,0
Msl3l2,0,4,0,0,0
Asf1a,0,8,0,0,0
F630110N24Rik,1,2,0,0,0
```



