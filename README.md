# MetaSUB-Inter-City-Challenge
The MetaSUB Inter-City Challenge presents the urban microbiomes of three cities. Compare organism fingerprints from public places across cities. Investigate organism sequences and biodiversity vs location.

http://camda.info/

# Data
Data is here


```
/u/home/n/ngcrawfo/project-zarlab/igor/METASUB/CAMDA/ala.boku.ac.at/camda2017/MetaSUB/*/data
```

* Boston 141 samples
* NY 1572 samples
* Sacramento 18 samples 


# Alligment based profiling

Run our tool

### Convert from dsrc to fastq

```
$PWD/../bin/dsrc d Sample_1A.fastq.dsrc Sample_1A.fastq
```

```
while read line ; do echo ". /u/local/Modules/default/init/modules.sh">run_${line}.sh; echo "module load bwa" >>run_${line}.sh; echo "module load bowtie2" >>run_${line}.sh; echo "../bin/dsrc d ../data/${line}.fastq.dsrc ${line}.fastq">>run_${line}.sh;echo "bwa mem /u/home/s/serghei/project/Viruses/bwaIndex/viruses.fa ${line}.fastq | samtools view -bS - | samtools view -b -F 4 - >${line}.bam">>run_${line}.sh;done<../samples.txt```
Running virus here
```
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/virus
```


# Alligment free profiling 
David





