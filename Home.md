Welcome to the rop wiki!

ls */*/run*sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh

cp <dirROPisInstalled>/myFuncFastWrapper.sh ./

chmod 755 myFunc.sh 

chmod 755 */*/*sh

wc -l 
qsub -cwd -V -N ropTest -l h_data=16G,time=24:00:00 -t 1-11:1 myFuncFastWrapper.sh