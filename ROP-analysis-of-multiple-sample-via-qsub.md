In case you have many files you can submit multiple jobs using qsub.

Please follow the following steps:



```
ls run*sh | awk '{i+=1;print "qsub -cwd -V -N rop"i" -l h_data=16G,time=24:00:00 "$1}' > all.sh
```