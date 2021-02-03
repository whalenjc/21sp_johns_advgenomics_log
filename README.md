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
Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git add README.md

Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git commit -m 'updating readme'
1 file changed, 54 insertions(+), 11 deletion(-)
Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git push -u origin main
Logon failed, use ctrl+c to cancel basic credential prompt.
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 797 bytes | 797.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/whalenjc/21sp_johns_advgenomics_log.git
   22798ce..140f434  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

## Day02 Homework 2021-Jan-22

1- Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory
John-HADB02
```
[jwhal002@coreV2-25-072 data]$ nano DBcopylane02.sh
```
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
```
[jwhal002@coreV1-22-016 data]$ sbatch DBcopylane02.sh
Submitted batch job 9271688
[jwhal002@coreV1-22-016 data]$ squeue -u jwhal002
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           9271688      main DBcopyla jwhal002  R       0:02      1 coreV2-25-047
           9271631      main       sh jwhal002  R    1:34:06      1 coreV1-22-016
[jwhal002@coreV1-22-016 data]$
```
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

## Day03 Homework 27-Jan-2021
day03 homework

```
[jwhal002@coreV1-22-016 john]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john
```
1. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03 directory (and files) to your sandbox
```
[jwhal002@coreV1-22-016 john]$ cp -r /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/ .
```
2. mkdir a fastq directory in your data directory and mv all the .fastq files into this directory
```
[jwhal002@coreV1-22-016 john]$ cd data
[jwhal002@coreV1-22-016 data]$ mkdir fastq
[jwhal002@coreV1-22-016 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data
[jwhal002@coreV1-22-016 data]$ mv *fastq.gz ./fastq/
```
3. cp the renamingtable_complete.txt from the day03 directory into your fastq directory and the /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py script into your sandbox scripts folder and less the new script and check out the usage statement
```
[jwhal002@coreV1-22-016 data]$ cp ../day03/renamingtable_complete.txt fastq/
[jwhal002@coreV1-22-016 data]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py ../scripts/
[jwhal002@coreV1-22-016 data]$ less -s ../scripts/renamer_advbioinf.py 
```
4. run the renamer_advbioinf.py script in your fastq folder using the renamingtable_complete.txt as practice and verify the output to the screen by hand
```
[jwhal002@coreV1-22-016 data]$ cd fastq/
[jwhal002@coreV1-22-016 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq
[jwhal002@coreV1-22-016 fastq]$ ../../scripts/renamer_advbioinf.py renamingtable_complete.txt 
mv HADB02-A_S33_L003_R1_001.fastq VA_W_02_14.fastq
mv HADB02-B_S34_L003_R1_001.fastq VA_B_02_14.fastq
mv HADB02-C_S35_L003_R1_001.fastq RI_W_02_14.fastq
mv HADB02-D_S36_L003_R1_001.fastq RI_B_02_14.fastq
mv HADB02-E_S37_L003_R1_001.fastq VA_W_02_22.fastq
mv HADB02-F_S38_L003_R1_001.fastq VA_B_02_22.fastq
mv HADB02-G_S39_L003_R1_001.fastq RI_W_02_22.fastq
mv HADB02-H_S40_L003_R1_001.fastq RI_B_02_22.fastq
mv HADB02-I_S41_L003_R1_001.fastq VA_W_02_18.fastq
mv HADB02-J_S42_L003_R1_001.fastq VA_B_02_18.fastq
mv HADB02-K_S43_L003_R1_001.fastq RI_W_02_18.fastq
mv HADB02-L_S44_L003_R1_001.fastq RI_B_02_18.fastq
mv HADB02-M_S45_L003_R1_001.fastq VA_W_09_SNP.fastq
mv HADB02-N_S46_L003_R1_001.fastq VA_B_08_SNP.fastq
mv HADB02-O_S47_L003_R1_001.fastq RI_W_09_SNP.fastq
mv HADB02-P_S48_L003_R1_001.fastq RI_B_09_SNP.fastq

```
5. Uncomment the last line of the renaming script in your scripts folder that starts with os.popen and comment out the next to last line that starts with print
```
[jwhal002@coreV1-22-016 fastq]$ nano renamer_advbioinf.py                                                                              [jwhal002@coreV1-22-016 fastq]$ cat renamer_advbioinf.py
#!/usr/bin/env python
####usage renamer.py renamingtable
#### this script take the entries in the first column of table and renames (mv's) them to files with the names in the second column
import sys
import os

fin=open(sys.argv[1],'r')
linecount=0
for line in fin:
        linecount+=1
        if linecount>=2:
                cols=line.rstrip().split('\t')
#               print 'mv %s %s' %(cols[0], cols[1])
                os.popen('mv %s %s' %(cols[0], cols[1]))
```
6. write a sbatch script and submit it to rename all the .fastq files according to the renaming table using your renamer_advbioinf.py script
```
[jwhal002@coreV1-22-016 fastq]$ cat john_renamer.sh
#!/bin/bash -l

#SBATCH -o john_renamer.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=fastqrenamer

renamer_advbioinf.py renamingtable_complete.txt
[jwhal002@coreV1-22-016 fastq]$ sbatch john_renamer.sh
Submitted batch job 9271704
[jwhal002@coreV1-22-016 fastq]$ squeue -u jwhal002
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
           9271704      main fastqren jwhal002 PD       0:00      1 (Priority)
           9271631      main       sh jwhal002  R    2:06:23      1 coreV1-22-016
```
7. Make sure this is all documented on your github page
```
Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ pwd
/c/Users/Ava/courses/21sp_advgenomics/21sp_johns_advgenomics_log

Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git add README.md
warning: LF will be replaced by CRLF in README.md.
The file will have its original line endings in your working directory

Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git commit -m 'updating readme'
[main 2f6d26b] updating readme
 1 file changed, 138 insertions(+), 12 deletions(-)

Ava@Ava-PC MINGW64 ~/courses/21sp_advgenomics/21sp_johns_advgenomics_log (main)
$ git push -u origin main
Logon failed, use ctrl+c to cancel basic credential prompt.
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 3.28 KiB | 839.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/whalenjc/21sp_johns_advgenomics_log.git
   140f434..2f6d26b  main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```
8. The naming convention for the files is as follows:
  * SOURCEPOPULATION_SYMBIOTICSTATE_GENOTYPE_TEMPERATURE.fastq
  * There are 2 sources: Virginia and Rhode Island
  * There are 2 symbiotic states: Brown and White
9. Next, you're going to start the process of adapter clipping and quality trimming all the renamed .fastq files in batches, by lane
10. cp the script /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py into your scripts directory
```
[jwhal002@coreV1-22-016 fastq]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py ../../scripts/
```
11. Less/head the new script and check out the usage statement
```
[jwhal002@coreV1-22-016 fastq]$ head -5 ../../scripts/Trimclipfilterstatsbatch_advbioinf.py
#!/usr/bin/env python
# Written by Dan Barshis

import sys, os
```
12. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt into the working directory with your fastq files
```
[jwhal002@coreV1-22-016 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq
[jwhal002@coreV1-22-016 fastq]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt .
```
13. Make a sbatch script for the Trimclipfilter... script and run it on your fastq files
```
[jwhal002@coreV1-22-016 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq
[jwhal002@coreV1-22-016 fastq]$ cat TestTrimClip.sh
#!/bin/bash -l

#SBATCH -o jcw_testTrimclip.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=jcwTrimTest

../../scripts/Trimclupfilterstatsbatch_advbioinf.py adapterlist_advbioinf.txt *.fastq
[jwhal002@coreV1-22-016 fastq]$
[jwhal002@coreV2-25-035 fastq]$ sbatch FullTrimClip.sh
Submitted batch job 9271757
```
14. This will take a while (like days)
15. Now might be a good time to update everything on your github

## Day04 Homework 29-Jan-2021
1-Add your trimclipstats.txt output to the full class datafile /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt using the following steps
```

```
1a-run /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h to examine usage
```
[jwhal002@coreV2-22-007 fastq]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h
Written by Peter Schafran pscha005@odu.edu 5-Oct-2015

This script takes a stats output file from fastx_clipper and converts it into a table.

Usage: Schafran_trimstatstable.py [-c, -v, -h] inputfile.txt outputfile.txt

Options (-c and -v must be listed separately to run together):
-h      Display this help message
-c      Use comma delimiter instead of tabs
-v      Verbose mode (print steps to stdout)
```
1b-Run the script on your data with the outputfilename YOURNAME_trimclipstatsout.txt
```
[jwhal002@coreV2-22-007 filteringstats]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py trimclipstats.txt jcw_trimclipstatsout.txt
```
1c-Add YOURNAME_trimclipstatsout.txt to the class file by running tail -n +2 YOURNAME_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt
```
[jwhal002@coreV2-22-007 filteringstats]$ tail -n +2 jcw_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt
```
2-Now we're going to map our reads back to our assembly using
3-write a sbatch script to do the following commands in sequence on your _clippedtrimmedfilterd.fastq datafiles from your lane of data
```
[jwhal002@coreV2-22-007 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs
[jwhal002@coreV2-22-007 QCFastqs]$ cat bowtielane2.sh
#!/bin/bash -l

#SBATCH -o jcwbowtie2.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=jcwbow

module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/18AdvBioinf/classdata/Astrangia_poculata/refassembly/ast_hostsym -U $i \
> ${i%_clippedtrimmedfilterd.fastq}.sam; done
[jwhal002@coreV2-22-007 QCFastqs]$ sbatch bowtielane2.sh
Submitted batch job 9272171
```


