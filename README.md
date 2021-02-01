John's Notebook
================

## Day01 Exercises 2021-Jan-20

## Day02 Exercises 2021-Jan-22

Exercise day02:
1- Logon to the cluster @turing.hpc.odu.edu
```
Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics (master)
$ ssh jwhal002@turing.hpc.odu.edu
jwhal002@turing.hpc.odu.edu's password:
Last login: Mon Feb  1 10:21:58 2021 from 10.254.223.22
[jwhal002@turing1 ~]$
```

2- Make a directory in your course workspace called data
```
[jwhal002@turing1 john]$ mkdir data
```
3- Make a directory called exercises in your data directory
```
[jwhal002@turing1 data]$ mkdir exercises
```
4- execute a pwd command and start a log of your commands with a header for today's date in your README.md github logfile in your workspace
```
[jwhal002@turing1 exercises]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/exercises
```
5- cp the Exercise2.fasta.gz and Exercise2.fastq.tar.gz files into your exercises directory from the 
```
/cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02 directory
[jwhal002@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02/Exercise2* .
```
6- unzip and untar the files
```
[jwhal002@turing1 exercises]$ gunzip Exercise2.fasta.gz
[jwhal002@turing1 exercises]$ tar -xvzf Exercise2.fastq.tar.gz
Exercise2.fastq
```
8- calculate how many sequences are in each file and add these results to your notebook file
```
[jwhal002@turing1 exercises]$ grep -c '>' Exercise2.fasta
138
[jwhal002@turing1 exercises]$ wc -l Exercise2.fastq
245216 Exercise2.fastq
[jwhal002@turing1 exercises]$ echo 245216/4 |bc
61304
```
9- cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory
```
[jwhal002@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py ../../scripts/
```
10- start an interactive compute session and re-navigate to your exercises directory
```
[jwhal002@turing1 exercises]$ salloc                              salloc: Pending job allocation 9271631
salloc: job 9271631 queued and waiting for resources
salloc: job 9271631 has been allocated resources
salloc: Granted job allocation 9271631
[jwhal002@coreV1-22-016 exercises]$
```
11- run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name
```
[jwhal002@coreV1-22-005 exercises]$ ../../scripts/avg_cov_len_fasta_advbioinf.py Exercise2.fasta
The total number of sequences is 138
The average sequence length is 126640
The total number of bases is 17476447
The minimum sequence length is 1122
The maximum sequence length is 562680
The N50 is 187037
Median Length = 92612
contigs < 150bp = 0
contigs >= 500bp = 138
contigs >= 1000bp = 138
contigs >= 2000bp = 135
```
13- push your notebook file to your github page
```

```



##Day 02 Homework

1- Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory
   Kristina-HADB01
   Ivan-HADB02
   KatieP-HADB03
   KatieC-HADB04
   Stephanie-HADB05
   Areej-HADB06
   Andrew-HADB01
   John-HADB02
   dan-All
2- Add the content of your sbatch script to your logfile

```
[jwhal002@coreV2-25-072 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data
[jwhal002@coreV2-25-072 data]$ cat DBcopylane02.sh
#!/bin/bash -l

#SBATCH -o DBcopylane02.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=DBcopylane02

cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/HADB02* .
[jwhal002@coreV2-25-072 data]$
```

3- submit the slurm script (sbatch scripname.sh) and verify that it's working (by squeue -u yourusername multiple times and checking the destination directory to make sure the files are being created)
4- Make sure this is all documented on your github notebook
5- Write a sbatch script to gunzip all the fastq.gz files in your data directory
```
[jwhal002@coreV2-25-072 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data
[jwhal002@coreV2-25-072 data]$ cat DBgunziplane02.sh
#!/bin/bash -l

#SBATCH -o DBgunziplane02.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=DBgunziplane02

gunzip *fastq.gz
[jwhal002@coreV2-25-072 data]$ sbatch DBgunziplane02.sh
Submitted batch job 9270464 
```
6- Push your notebook file to your github page (document everything on your github notebook, drink a beer, and realize that all that work was just to get the data organized to start looking at it!)
