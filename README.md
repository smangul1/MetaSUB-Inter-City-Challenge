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
running here
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/fungi

```

run ameoba

```
while read line ; do echo ". /u/local/Modules/default/init/modules.sh">run_${line}.sh; echo "module load bwa" >>run_${line}.sh; echo "module load bowtie2" >>run_${line}.sh; echo "bwa mem -a /u/home/s/serghei/project/eupathdb/bwa/ameoba.fa ../data/${line}.fastq | samtools view -bS - | samtools view -b -F 4 - >${line}.bam">>run_${line}.sh;done<../samples.txt
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/ameoba
```



# Run imrep

```
qsub -cwd -V -N imrep -l h_data=16G,time=24:00:00 run.sh 
/u/home/s/serghei/collab/MetaSUB-Inter-City-Challenge/imrep
```



# Preliminary results

Mapping to fungi using BWA we detect Malassezia supported by 516826 (2.5% abundance) reads
in one sample SRR3545919 . Total number of reads 20466091. 

This fungus also reported in ths study here : Urban Transit System Microbial Communities Differ by Surface Type and Interaction with Humans and the Environment

- http://msystems.asm.org/content/1/3/e00018-16

Another fungus supported by 
is Cryptococcus Gattii  (maybe FP?) 
was not reported in urban microbiome

### Ameoba
samtools view SRR3545919.bam | awk '{print $3}' | sort  | uniq -c >../SRR3545919.ameoba_genomes 

The most abundant - Entamoeba. 290511 reads 

- Entamoeba rise to symptoms that usually include diarrhea related to damage in the wall of the bowel.

### Virus

Looking at one sample nothing shows up

```
for f in *bam ; do samtools view ${f} | awk '{print $3}' | sort | uniq -c >${f}.profile;done
```


# FP

```
sort -k 1n SRR3545948.bam.profile
 9584 gi|531034792|ref|NC_022098.1| - FP?
  14849 gi|9628932|ref|NC_001731.1| - TP, confirmed by SURPI
  ```

# CAMDA 2017 abstract 

## Viruses

```
grep "" *profile | awk '{if($2>1000) print}' | awk '{print $3}' | sort | uniq -c | wc -l
129

```
