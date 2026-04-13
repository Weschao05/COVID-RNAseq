# Installing Miniconda3 and Setting Up RNA-seq Environment

## 1. Install Miniconda3

1. Log in to Kepler and ensure you are in your home directory.

2. Download and install Miniconda3:

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-py39_4.12.0-Linux-x86_64.sh
bash Miniconda3-py39_4.12.0-Linux-x86_64.sh

#Reload Shell Configuration and verify installation
source .bashrc
conda --version
```

## 2. Configure Conda Channels
1. Check current channels:
```bash
conda config --show channels
```
You should see ```defaults```.

2. Add required bioinformatics channels:
```bash
conda config --add channels conda-forge
conda config --add channels bioconda
```

## 3. Create Conda Environments
1. Set up separate environments for each step of the workflow:
```bash
#Trimming and QC
conda create -n trimming -c bioconda -c conda-forge trim-galore fastqc

#Alignment
conda create -n alignment -c bioconda -c conda-forge hisat2 samtools

#Read Counting
conda create -n counting -c bioconda -c conda-forge htseq
```
2. Activate Conda Environments. Type:
```bash
conda activate <environment_name>
```
(Optional)
For faster environment switching, you can add aliases to your .bashrc or .bash_profile:

## 4. Downloading Raw FASTQ Files and Reference Genome
1. Create Project Directory Structure
```bash
mkdir raw_reads trimmed_reads ref_genome fastqc hisat2 alignments counts scripts logs
```
2. Copy Raw FASTQ Files
```bash
cp /full/path/to/raw_reads/*.fastq .
```
3. Copy Reference Genome
```bash
cp /full/path/to/ref_genome/*.ht2 .
```
