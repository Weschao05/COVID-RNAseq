## RNAseq Pipeline Guide
This guide outlines a basic RNA-seq pipeline including trimming, alignment, and quantification.

# Trimming
1. Enter your trimming environment, go to ```scripts/```, and create a ```<trim>.sh``` file
2. We will use the tool Trimgalore to cut our low quality bases, short reads and adapters on one of our sample (SRR11517726.fastq or HealthyLung_1.fastq)
```bash
# Default Trimgalore Code
trim_galore <input_fastq> -o <output>
```
3. Exit our of your script and run it
```bash
nohup bash <trim>.sh > ../logs/<run_trim>.log 2>&1 &
```
4. After trimming, go to ```trimmed/``` and run fastqc and see quality report
   
# Alignment
1. Enter your alignment environment, go to ```scripts/```, and create an ```<alignment>.sh``` file
We will use hisat2 to align our trimmed read to reference genome
```bash
#Default hisat2 alignment code
hisat2 -x <index> -U <reads.fq> -S <output.sam>
```
2. Exit out of your script and run:
```bash
nohup bash <alignment>.sh > ../logs/<alignment>.log 2>&1 &
```
3. Once complete check your ```alignment/``` and you should ```sorted.bam``` file and ```summary.txt```

# Quantification (Counting)
1. Enter your counting environment, go to your ```scripts/```, and create a ```<count>.sh``` file
2. We will use htseq to quantify our reads by counting
```bash
#Default code
htseq-count input.bam annotation.gtf > output.bam
```
3. Run the script
```bash
nohup bash <count>.sh > ../logs/<count>.log 2>&1 &
```
4. Check for results in ```counts/```
5. Download counts to your local computer using ```scp```

