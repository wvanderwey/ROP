In release 1.0.5 we have added additional options for gprofile. 

* --perCategory option reports assignment of each read in the following format:

```
readName,chr,category, geneID,geneName
4029592_h_0_TCTGATG_CGAT,10,CDS,ENSMUSG00000015202,Cnksr3
```




This is an example how to run gprofile with `--perCategory` and `--mouse` options:

```
python /u/home/s/serghei/collab/code/rop/gprofile.py mapped_SJV040_CGAT.bam gProfile8/mapped_SJV040_CGAT.csv --perCategory --mouse
``` 
