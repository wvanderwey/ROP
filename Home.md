Welcome to the rop wiki!

Run ROP for all the samples at once :

while read line; do ; python /u/home/s/serghei/code2/rop/rop.py --qsubArray --skipQC /u/home/b/brigitta/scratch/gtex/data/${line}.fasta $PWD/${line}; done<../samples_26.txt


ls */microbiome/[v,b]*/run*sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh

cp /u/home/s/serghei/code2/rop/myFuncFastWrapper.sh ./
chmod 755 myFunc.sh 

chmod 755 */*/*/*sh
wc -l 
qsub -cwd -V -N ropGTEX -l h_data=16G,time=24:00:00 -t 1-6716:1 myFuncFastWrapper.sh

----------------------------

while read line; do ; python /u/home/s/serghei/code2/rop/rop.py --qsub --skipQC /u/home/b/brigitta/scratch/africa/data/${line}.fasta $PWD/${line}; done<../samples_26.txt

#####
while read line ; do echo "python /u/home/s/serghei/code2/rop/rop.py --qsubArray /u/home/s/serghei/collab/bloodMicrobiome_Oct20/data/replicationRNASeq/data/unmapped/unmapped_${line}.fastq $PWD/${line}/">run_${line}.sh;done<../samples.txt


TO DO :+1: 
Metahplan
upload inndexes on sourceforge
make instalation command 
