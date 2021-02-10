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
4-Submit and add everything to your logfile

## Day05 Homework 03-Feb-2021

Homework day05 (document all this in your logfile, don't forget to pwd before each entry to remind yourself where you were working):
1-Team up with a partner for this one and work only on a combined set of data for your two lanes of sequences
2-Run the Trinity denovo assembler on your clippedtrimmed.fastq files for your two lanes together
3-Modify the below sbatch script (note the differences in the header compared to the previous one)
```
[jwhal002@coreV3-23-002 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs
[jwhal002@coreV3-23-002 QCFastqs]$ cat jcw_trinity.sh
#! /bin/bash -l

#SBATCH -o jcw_trinity.txt
#SBATCH -n 32
#SBATCH -p himem
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=jcw_trinity

enable_lmod
module load container_env trinity

crun Trinity --seqType fq --max_memory 768G --normalize_reads --single RI_B_05_18_clippedtrimmed.fastq,RI_B_05_22_clippedtrimmed.fastq,RI_B_06_14_clippedtrimmed.fastq,RI_B_06_22_clippedtrimmed.fastq,RI_W_05_18_clippedtrimmed.fastq,RI_W_05_22_clippedtrimmed.fastq,RI_W_06_14_clippedtrimmed.fastq,RI_W_06_22_clippedtrimmed.fastq,VA_B_05_18_clippedtrimmed.fastq,VA_B_05_22_clippedtrimmed.fastq,VA_B_06_14_clippedtrimmed.fastq,VA_B_06_22_clippedtrimmed.fastq,VA_W_05_18_clippedtrimmed.fastq,VA_W_05_22_clippedtrimmed.fastq,VA_W_06_14_clippedtrimmed.fastq,VA_W_06_22_clippedtrimmed.fastq,RI_B_02_14_clippedtrimmed.fastq,RI_B_02_18_clippedtrimmed.fastq,RI_B_02_22_clippedtrimmed.fastq,RI_B_09_SNP_clippedtrimmed.fastq,RI_W_02_14_clippedtrimmed.fastq,RI_W_02_18_clippedtrimmed.fastq,RI_W_02_22_clippedtrimmed.fastq,RI_W_09_SNP_clippedtrimmed.fastq,VA_B_02_14_clippedtrimmed.fastq,VA_B_02_18_clippedtrimmed.fastq,VA_B_02_22_clippedtrimmed.fastq,VA_B_08_SNP_clippedtrimmed.fastq,VA_W_02_14_clippedtrimmed.fastq,VA_W_02_18_clippedtrimmed.fastq,VA_W_02_22_clippedtrimmed.fastq,VA_W_09_SNP_clippedtrimmed.fastq --CPU 32

```
4-Check https://trinityrnaseq.github.io/ for usage info
5-Submit your trinity script
```
[jwhal002@coreV3-23-002 QCFastqs]$ sbatch jcw_trinity.sh
```

## Day 06 Homework 05-Feb-2021

1- start an interactive session via salloc and run the /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl script on your Trinity.fasta output from your assembly
```
[jwhal002@coreV2-22-028 djbtestassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs/djbtestassembly
[jwhal002@coreV2-22-028 djbtestassembly]$ ls
Trinity.fasta
[jwhal002@coreV2-22-028 djbtestassembly]$ /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl Trinity.fasta


################################
## Counts of transcripts, etc.
################################
Total trinity 'genes':  20980
Total trinity transcripts:      21992
Percent GC: 46.21

########################################
Stats based on ALL transcript contigs:
########################################

        Contig N10: 1178
        Contig N20: 694
        Contig N30: 514
        Contig N40: 414
        Contig N50: 347

        Median contig length: 273
        Average contig: 356.95
        Total assembled bases: 7850006


#####################################################
## Stats based on ONLY LONGEST ISOFORM per 'GENE':
#####################################################

        Contig N10: 1027
        Contig N20: 643
        Contig N30: 486
        Contig N40: 397
        Contig N50: 336

        Median contig length: 271
        Average contig: 347.72
        Total assembled bases: 7295061
```
2- compare this with the output from avg_cov_len_fasta_advbioinf.py on our class reference assembly (/cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta) and add both to your logfile
```
[jwhal002@turing1 fastq]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta
The total number of sequences is 15079
The average sequence length is 876
The total number of bases is 13210470
The minimum sequence length is 500
The maximum sequence length is 10795
The N50 is 881
Median Length = 578
contigs < 150bp = 0
contigs >= 500bp = 15079
contigs >= 1000bp = 3660
contigs >= 2000bp = 536
```
3- less or head your bowtie2 job output file to look at your alignment statistics and calculate the following from the information:
```
[jwhal002@turing1 QCFastqs]$ tail jcwbowtie2.txt
    1228 (8.21%) aligned 0 times
    367 (2.45%) aligned exactly 1 time
    13363 (89.34%) aligned >1 times
91.79% overall alignment rate
167481650 reads; of these:
  167481650 (100.00%) were unpaired; of these:
    12023876 (7.18%) aligned 0 times
    7634379 (4.56%) aligned exactly 1 time
    147823395 (88.26%) aligned >1 times
92.82% overall alignment rate

```
	a-the mean percent "overall alignment rate"
```
[jwhal002@coreV3-23-024 QCFastqs]$ grep "overall alignment rate" jcwbowtie2.txt | cut -d "%" -f 1
88.89
86.95
87.36
88.24
88.26
92.55
92.92
93.67
93.68
93.18
93.16
92.46
92.54
93.20
91.79
92.82
```
	b-the mean percent reads "aligned exactly 1 time"
```
[jwhal002@coreV3-23-024 QCFastqs]$ grep "aligned exactly 1 time" jcwbowtie2.txt | cut -d "%" -f 1 | cut -d "(" -f 2
5.91
6.39
6.00
6.36
5.47
4.88
4.47
4.36
5.18
4.48
4.73
4.60
4.49
4.48
2.45
4.56
```
	c-the mean number of reads "aligned exactly 1 time"
```
[jwhal002@coreV3-23-024 QCFastqs]$ grep "aligned exactly 1 time" jcwbowtie2.txt | cut -d " " -f 5
350917
668166
830829
861858
206921
708047
627497
600014
436715
659303
356357
429609
566691
1045508
367
7634379
```
	d-the mean percent reads "aligned >1 times"
```
[jwhal002@coreV3-23-024 QCFastqs]$ grep "aligned >1 time" jcwbowtie2.txt | cut -d "%" -f 1 | cut -d "(" -f 2
82.99
80.56
81.35
81.88
82.79
87.68
88.44
89.31
88.50
88.71
88.43
87.86
88.05
88.72
89.34
88.26
```
	hint use grep and paste into excel

4- add your statistics as single rows to the shared table /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt as tab-delimited text in the following order:
LaneX_yourinitials	b-the mean percent "overall alignment rate"	c-the mean percent reads "aligned exactly 1 time"	d-the mean number of reads "aligned exactly 1 time"	e-the mean percent reads "aligned >1 times"
```
[jwhal002@coreV3-23-024 QCFastqs]$ pwd                                                                                                 /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs                                                           [jwhal002@coreV3-23-024 QCFastqs]$ nano alignstatsjcw2.txt
[jwhal002@coreV3-23-024 QCFastqs]$ cat alignstatsjcw2.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt
```

5- Data cleanup and archiving:
	a-mv your Trinity.fasta file from your trinity_out_dir to a folder called testassembly in your data directory
```
[jwhal002@coreV3-23-024 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs
[jwhal002@coreV3-23-024 QCFastqs]$ mkdir testassembly ../../
[jwhal002@coreV3-23-024 QCFastqs]$ mv djbtestassembly/Trinity.fasta ../../testassembly/
```
	b-set up a sbatch script to:
		rm -r YOURtrinity_out_dir
		rm -r YOURoriginalfastqs
		rm -r YOURfilteringstats # as long as you've already appended your filteringstats output to the class table as part of homework_day04.txt
```
[jwhal002@coreV3-23-024 QCFastqs]$ nano rmfiles.sh
[jwhal002@coreV3-23-024 fastq]$ cat rmfiles.sh
#!/bin/bash -l

#SBATCH -o rmfiles.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=rming

rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs/21sampleassembly_trinity_out_dir
rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/originalfastqs
rm -r /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/filteringstats
[jwhal002@coreV3-23-024 fastq]$ sbatch rmfiles.sh
Submitted batch job 9272889
```

6- submit a blast against sprot from your testassembly folder using the following command
```
[jwhal002@coreV3-23-024 testassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/testassembly
[jwhal002@coreV3-23-024 testassembly]$ nano jcw_blast2sprot.sh
[jwhal002@coreV3-23-024 testassembly]$ cat jcw_blast2sprot.sh
#!/bin/bash -l

#SBATCH -o jcw_blast2prot.txt
#SBATCH -n 6
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=b2p

enable_lmod
module load container_env blast
blastx -query Trinity.fasta -db /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018 -out blastx.outfmt6 \
        -evalue 1e-20 -num_threads 6 -max_target_seqs 1 -outfmt 6
[jwhal002@coreV3-23-024 testassembly]$ sbatch jcw_blast2sprot.sh
Submitted batch job 9272890
```

7- head one of your .sam files to look at the header
```
[jwhal002@coreV3-23-024 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs
[jwhal002@coreV3-23-024 QCFastqs]$ head RI_B_02_14_clippedtrimmed.fastq.sam
@HD     VN:1.0  SO:unsorted
@SQ     SN:AstrangiaT1FW_1      LN:4823
@SQ     SN:AstrangiaT1FW_10     LN:1096
@SQ     SN:AstrangiaT1FW_11     LN:2560
@SQ     SN:AstrangiaT1FW_12     LN:2686
@SQ     SN:AstrangiaT1FW_13     LN:629
@SQ     SN:AstrangiaT1FW_15     LN:582
@SQ     SN:AstrangiaT1FW_16     LN:502
@SQ     SN:AstrangiaT1FW_17     LN:1492
@SQ     SN:AstrangiaT1FW_18     LN:1197
```
8- grep -v '@' your.sam | head to look at the sequence read lines, why does this work to exclude the header lines?
```
[jwhal002@coreV3-23-024 QCFastqs]$ grep -v "@" RI_B_02_14_clippedtrimmed.fastq.sam | head
K00188:59:HMTFHBBXX:3:1101:4888:1666    0       AstrangiaT1FW_65674     800     1       51M     *       0       0       GGCTAGTTGATTCGGCAGGTGAGTTGTTACACACTCCTTAGCGGATTCCGA    AAFFFFJJJJJJJFFJJAJJJJFFJJJJJJJJJJ<JJJJJFJJJJJJJJJJ     AS:i:0  XS:i:0  XN:i:0  XM:i:0  XO:i:0XG:i:0   NM:i:0  MD:Z:51 YT:Z:UU RG:Z:RI_B_02_14
K00188:59:HMTFHBBXX:3:1101:5964:1666    0       AstrangiaT1FW_65554     517     30      51M     *       0       0       AAAGACTAATCGAACTGTCTAGTAGCTGGTTCCCTCCGAAGTTTCCCTCAG    AAFFFFFJJJJFJJJFJJJJJFAJJJJJFJJJJJJJJJJJFJJJJJJFJJJ     AS:i:0  XS:i:-5 XN:i:0  XM:i:0  XO:i:0XG:i:0   NM:i:0  MD:Z:51 YT:Z:UU RG:Z:RI_B_02_14
```

9- in an interactive session run /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py on 2-3 of your .sam files using * to select 2-3 at the same time.
```
[jwhal002@coreV3-23-024 QCFastqs]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py *2_14*.sam
RI_B_02_14_clippedtrimmed.fastq.sam
['0', '4', '16']
0 :
4 :
        read unmapped
16 :
        read reverse strand
RI_W_02_14_clippedtrimmed.fastq.sam
['0', '4', '16']
0 :
4 :
        read unmapped
16 :
        read reverse strand
VA_B_02_14_clippedtrimmed.fastq.sam
['0', '4', '16']
0 :
4 :
        read unmapped
16 :
        read reverse strand
VA_W_02_14_clippedtrimmed.fastq.sam
['0', '4', '16']
0 :
4 :
        read unmapped
16 :
        read reverse strand
```

10- we need to run the read sorting step required for SNP calling, so if you have time, set up and run the following script on your .sam files to finish before Wednesday:
```
[jwhal002@coreV1-22-001 QCFastqs]$ pwd                         
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs                                                        
[jwhal002@coreV1-22-001 QCFastqs]$ nano bamandsort.sh             
[jwhal002@coreV1-22-001 QCFastqs]$ cat bamandsort.sh
#!/bin/bash -l

#SBATCH -o jcwbamandsort.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=jcwbambam

enable_lmod
module load samtools/1
for i in *.sam; do `samtools view -bS $i > ${i%.sam}_UNSORTED.bam`; done

for i in *UNSORTED.bam; do samtools sort $i > ${i%_UNSORTED.bam}.bam
samtools index ${i%_UNSORTED.bam}.bam
done
[jwhal002@coreV1-22-001 QCFastqs]$ sbatch bamandsort.sh
Submitted batch job 9273039
```

## Day 07 Homework 10-Feb-2021
assess the quality of your assembly, cleanup data, start genotyping:

1- Run the following command on your sprot output file to process into the contig length/match format that trinity examines
```
[jwhal002@coreV3-23-040 testassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/testassembly
[jwhal002@coreV3-23-040 testassembly]$ nano blastparse.sh
[jwhal002@coreV3-23-040 testassembly]$ cat blastparse.sh
#!/bin/bash -l

#SBATCH -o jcw_blastx.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002.odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=jcwblastx

/cm/shared/apps/trinity/2.0.6/util/analyze_blastPlus_topHit_coverage.pl djbblastx.outfmt6 Trinity.fasta /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018.fasta

[jwhal002@coreV3-23-040 testassembly]$ sbatch blastparse.sh
[jwhal002@coreV3-23-040 testassembly]$ cat jcw_blastx.txt
Error: Couldn't open 15079_Apoc_hostsym.fasta
#hit_pct_cov_bin        count_in_bin    >bin_below
100     143     143
90      52      195
80      77      272
70      87      359
60      110     469
50      133     602
40      219     821
30      395     1216
20      726     1942
10      674     2616
```

2- Rm UNSORTED.bam
```
[jwhal002@coreV3-23-040 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/fastq/QCFastqs
[jwhal002@coreV3-23-040 QCFastqs]$ nano rmunsortbam.sh
[jwhal002@coreV3-23-040 QCFastqs]$ sbatch rmunsortbam.sh
Submitted batch job 9276498
```
3- Run the following to start genotyping your SNPs for filtering next class
```
[jwhal002@coreV3-23-040 QCFastqs]$ nano freebayessubref.sh                                                        [jwhal002@coreV3-23-040 QCFastqs]$ cat freebayessubref.sh
#!/bin/bash -l

#SBATCH -o freebayessubref.txt
#SBATCH -n 1
#SBATCH --mail-user=jwhal002@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=freeb

enable_lmod
module load dDocent
freebayes --genotype-qualities -f /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/john/data/testassembly/Trinty.fasta *.fastq.bam > jcwmergedfastqs.vcf
[jwhal002@coreV3-23-040 QCFastqs]$ sbatch freebayessubref.sh
Submitted batch job 9276575
```
