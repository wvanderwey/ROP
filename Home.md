Welcome to the rop wiki!

ls run*sh | awk '{i+=1;print "if [ $1 == "i" ];then ./"$1" ;fi"}' > myFunc.sh

chmod 755 myFunc.sh 

chmod 755 *sh

qsub -cwd -V -N rop1 -l h_data=16G,time=06:00:00 -t 1-1706:1 myFuncFastWrapper.sh