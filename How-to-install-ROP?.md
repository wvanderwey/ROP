#How to install ROP?

Please get the latest release from [here](https://github.com/smangul1/rop/releases).

Please make sure that the basic unix commands (tar) are available on the cluster. The package  can be downloaded as zip or tar.gz compressed archives. In a Unix environment, you can obtain and uncompress it from the command line:

```
wget https://github.com/smangul1/rop/archive/v0.2.tar.gz
tar -zxvf v0.2.tar.gz
mv rop-* rop
```

No installation is required. The ROP comes with no pre-requirements except Python. Python is required to be installed on the cluster you are planning to perform the analysis. ROP is distributed with several open source components that were developed by other groups (see section Third Party software from [here](http://serghei.bioinformatics.ucla.edu/rop/)).

ROP requires the prepared reference databases for human and microbial sequences, which can be download as shown bellow. First please navigate to ROP directory as follows

```
cd rop
python install.py
```
 
The 'installation' might take up to  45 minutes on average and requires 30Gb of available space to download the references.



