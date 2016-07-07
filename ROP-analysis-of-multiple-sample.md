Run ROP for all the samples at once :

while read line; do ; python /u/home/s/serghei/code2/rop/rop.py --qsubArray --skipQC /u/home/b/brigitta/scratch/gtex/data/${line}.fasta $PWD/${line}; done<../samples_26.txt


ls */*CR/*/run*sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh

cp /u/home/s/serghei/code2/rop/myFuncFastWrapper.sh ./
chmod 755 myFunc.sh 

chmod 755 */*CR/*/*sh
wc -l 
qsub -cwd -V -N rop -l h_data=16G,time=24:00:00 -t 1-2002:1 myFuncFastWrapper.sh

----------------------------

while read line; do ; python /u/home/s/serghei/code2/rop/rop.py --qsub --skipQC /u/home/b/brigitta/scratch/africa/data/${line}.fasta $PWD/${line}; done<../samples_26.txt

#####
while read line ; do echo "python /u/home/s/serghei/code2/rop/rop.py --qsubArray /u/home/s/serghei/collab/bloodMicrobiome_Oct20/data/replicationRNASeq/data/unmapped/unmapped_${line}.fastq $PWD/${line}/">run_${line}.sh;done<../samples.txt


1.  ls *sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh
2. chmod 755 myFunc.sh
3. chmod 755 *sh
4. wc -l myFunc.sh
5. qsub -cwd -V -N tophat2 -l h_data=8G,express,time=10:00:00 -t 1-x:1 myFuncFastWrapper.sh
