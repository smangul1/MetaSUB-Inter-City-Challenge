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


I selected all Sacramento, Boston and 65 NY samples. Total n=224. Fastq files are here
```
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/data
```

# Alligment based profiling

Run our tool

### Convert from dsrc to fastq

```
download release from here
https://github.com/lrog/dsrc/releases
$PWD/../bin/dsrc d Sample_1A.fastq.dsrc Sample_1A.fastq
```

```
while read line ; do echo ". /u/local/Modules/default/init/modules.sh">run_${line}.sh; echo "module load bwa" >>run_${line}.sh; echo "module load bowtie2" >>run_${line}.sh; echo "../bin/dsrc d ../data/${line}.fastq.dsrc ${line}.fastq">>run_${line}.sh;echo "bwa mem /u/home/s/serghei/project/Viruses/bwaIndex/viruses.fa ${line}.fastq | samtools view -bS - | samtools view -b -F 4 - >${line}.bam">>run_${line}.sh;done<../samples.txt
```

```
while read line ; do echo ". /u/local/Modules/default/init/modules.sh">run_${line}.sh; echo "module load bwa" >>run_${line}.sh; echo "module load bowtie2" >>run_${line}.sh; echo "bwa mem /u/home/s/serghei/project/Viruses/bwaIndex/viruses.fa ../data/${line}.fastq | samtools view -bS - | samtools view -b -F 4 - >${line}.bam">>run_${line}.sh;done<../samples.txt
ls run*sh | awk '{i+=1;print "qsub -cwd -V -N bwa"i" -l h_data=12G,time=12:00:00 "$1}' > ALL.SH
here
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/virus2

```

Running virus here
```
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/virus
```

run fungi

```
while read line ; do echo ". /u/local/Modules/default/init/modules.sh">run_${line}.sh; echo "module load bwa" >>run_${line}.sh; echo "module load bowtie2" >>run_${line}.sh; echo "bwa mem -a /u/home/s/serghei/project/eupathdb/bwa/fungi.fa ../data/${line}.fastq | samtools view -bS - | samtools view -b -F 4 - >${line}.bam">>run_${line}.sh;done<../samples.txt 
```


# Alligment free profiling 
David





