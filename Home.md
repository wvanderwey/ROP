Welcome to the rop wiki!

ls */*/*/run*sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh

cp <dirROPisInstalled>/myFuncFastWrapper.sh ./

chmod 755 myFunc.sh 

chmod 755 */*/*/*sh
wc -l 
qsub -cwd -V -N ropGTEX -l h_data=16G,time=24:00:00 -t 1-11746:1 myFuncFastWrapper.sh

----------------------------

while read line; do ; python /u/home/s/serghei/code2/rop/rop.py --qsub --skipQC /u/home/b/brigitta/scratch/africa/data/${line}.fasta $PWD/${line}; done<../samples_26.txt