# About KewHPC

Kew HPC is our main compute cluster with 576 cores across 14 nodes.

It has a variety of bioinformatic analysis packages installed. To get access, or for general queries/software requests, please contact [Matt Clarke](mailto:m.clarke@kew.org).

## Technical Specifications
Runs CentOS 7.7

Total 576 cores and 7.6TB RAM across 14 nodes

12x Compute nodes with:

* 2 x18 core Intel Xeon CPU @ 2.6GHz
* 384 GB RAM

2 x High Memory nodes with:

* 4 x 18  core Intel Xeon CPU @ 2.6GHz
* 1.5 TB RAM


# Quick Start Guide
To get access to the bioinformatic resources contact [Matt Clarke](mailto:m.clarke@kew.org)

Once you have access you can:

## Log in
### From Windows
Using [PuTTY](https://putty.org), enter kewhpc into the hostname box

Enter "yes" or "y" if asked to confirm adding KewHPC to hosts list.

log in using your username and password

### From MacOS / Linux

open a terminal window and type

	ssh username@KewHPC

Type "yes" if prompted to confirm adding hatta to your hosts list

enter your password.

## Transfer Data
### From Windows
using an SFTP client such as [FileZilla](https://filezilla-project.org/download.php?platform=win64)

In Filezilla use the Quickconnect bar:
Host: sftp://KewHPC
Username: your Kew username
Password: your Kew password
Port: 22 

### From MacOS / Linux
[FileZilla](https://filezilla-project.org) also works the same on Linux and Mac.

For larger files or many files you can use rsync via the terminal
Copying to hatta:

	rsync -avP /local/file/or/directory username@KewHPC://directory/to/copy/to

Copying from hatta:

	rsync -avP username@kewhpc://file/or/directory/to/copy /local/destination/for/files

If you want to copy a directories contents and not the directory itself add a trailing "/" to the first argument.
If the rsync command is interupted just re-run the exact command and its should continue from the file it was last transfering.

## Submit Jobs
KewHPC uses slurm to manage job submissions
to submit jobs you need to create a submission script
for example test_script.sh: 

	#!/bin/bash 
	#SBATCH -c 1
	#SBATCH -p all
	#SBATCH -J test_job
	#SBATCH -t 0-3:00:00
	#SBATCH -o /data/users_area/myname/test.log
	echo "hello world!"

you submit the job using the command:

	sbatch test_script.sh

you can see the jobs currently running by using the command 

	squeue

For more details see [this page](./software/slurm.md) or the [slurm documenation](https://slurm.schedmd.com/)

# Data Storage
There are 3 main places you can stor your data

## /home 
Your Home directory is the place you'll land when you login.
This is a god place to save your scripts and some configuration files.
It is Limited to 10GB so it's best not to store any data or programs here.
## /data
This is the cluster attached storage, Its fast and the best place to store the data your currently analysing
there are 2 main areas /data/projects for shared data and analysis /data/users_area for single user data and analysis.

## /science
This is the slower, longer term sorage for your data. Its attached to both HATTA and KewHPC allowing datta to be accessed by both machines.
Please move any data stored here to a directory in /data before running analysis
There are /science/projects and /science/users_area directories as in /data
# Installed Software
Software is installed using lmod see [this page](./software/lmod.md) to load and unload different software
| Name | Version |
| :------ | ------: |
| blast | 2.10.0 |
| exonerate | 2.4.0 |
| RAxML | 8.2.12 |
| samtools | 1.10 |
| Slurm | 19.05.5 |
| SPAdes | 3.14 |


