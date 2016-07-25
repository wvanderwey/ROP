Please make sure that the basic unix commands (tar or zip) are available on the cluster. The package  can be downloaded as zip or tar.gz compressed archives. In a Unix environment, you can obtain and uncompress it from the command line:

```
wget https://sourceforge.net/projects/rop2/files/latest/download/rop.tar.gz
tar -zxvf rop.tar.gz
```

No installation is required. The ROP comes with no pre-requirements except Python 2.7. Python 2.7 is required to be installed on the cluster you are planning to perform the analysis. ROP is distributed with several open source components that were developed by other groups (see section Third Party software from [here](https://sergheimangul.wordpress.com//rop/)).

ROP requires the prepared reference databases for human and microbial sequences, which can be download as shown bellow. 

```
cd rop
python getDB.py ~/
```

In the versions prior to 1.0.3 the `getDB.py` was named as `installation.py`. Upgrading to the latest version is strongly encouraged. 
 
Downloading reference databases (refDB) might take up to  45 minutes on average and requires 50Gb of available space to download the references.

The 'getDB.py' provides the possibility to connect the current version of ROP to the existing database. Please use `--link2db` option. 

Prior to the release 1.0.3 refDB was downloaded to the ROP directory. Now the location to download refDB is a choice of the user. This allows to store the refDB independently from ROP and connect the current version of ROP to the refDB. As you get a new version of ROP there is no need to download refDB again, instead you can just connect the new version of ROP to the existing database (via `--link2db` option).


The full list of parameters of 'getDB.py' can be accessed from the help message:

```
usage: python rop.py [-h] [--repeat] [--immune] [--metaphlan] [--circRNA]
                     [--microbiome] [--link2db] [--f]
                     dirDB

optional arguments:
  -h, --help    show this help message and exit

Necessary Inputs:
  dirDB         directory where the reference databases will be downloaded

Select Database (multi-selection is possible):
  --repeat      Set up database for repeat sequences ONLY (lost repeat reads)
  --immune      Set up database for VDJ gene segments of B cell and T cell
                receptors ONLY (immune reads)
  --metaphlan   Set up database for Metaphlan2 ONLY
  --circRNA     Set up database for circular RNAs ONLY
  --microbiome  Set up database for microbime ONLY

Connect database with the new release:
  --link2db     Connect the existing reference database with ROP
  --f           Reconnects the ROP to the new database. Please note the
                existing link will removed
```


