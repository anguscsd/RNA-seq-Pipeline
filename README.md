# RNA-Seq Data Processing and Analysis Pipeline

This repository contains scripts and documentation for processing and analyzing RNA-seq data.  
The workflow demonstrates key steps in a typical next-generation sequencing (NGS) analysis pipeline, from raw FASTQ processing through alignment, duplicate marking, and preparation for downstream transcriptomic analysis.

---

## Project Overview
This project focuses on building a **reproducible RNA-seq pipeline** using publicly available datasets and widely adopted bioinformatics tools.  
The pipeline processes paired-end reads, performs quality control, aligns reads to a reference genome, marks duplicates, and prepares the data for downstream analyses such as **gene expression quantification** and **splicing detection**.

---

## 📂 Dataset
- **Sample:** ERR2704713 (12 weeks, sample 5)  
- **Data Source:** [ENA](https://www.ebi.ac.uk/ena/browser/view/ERR2704713)  
- **Sequencing Type:** Paired-end RNA-seq
- **Reference Genome:** Chromosome 21 from **UCSC hg38** (unmasked)
- **Gene Annotations:** **GENCODE v44** GTF filtered for **chr21**

---

## Software & Tools Used

| Tool / Software      | Version   | Purpose |
|----------------------|-----------|----------------------------------------------|
| **Trimmomatic**      | v0.38    | Adapter removal & quality trimming |
| **FastQC**          | v0.11.8  | Read quality assessment (pre- & post-trimming) |
| **STAR**            | v2.7.0e  | Splice-aware genome indexing & alignment |
| **Picard**          | v2.20.2  | Marking and removing duplicate reads |
| **Samtools**        | v1.9     | BAM file indexing & manipulation |
| **wget**            | latest   | Downloading datasets & references |
| **SLURM**           | N/A      | Job scheduling on HPC cluster |

---

## Running on Cardiff University's HAWK Supercomputer

This project was executed on **Cardiff University's HAWK supercomputer**, a high-performance computing (HPC) cluster that uses the **SLURM** workload manager.  
The HAWK system provides the **memory, CPUs, and parallel processing capabilities** required for handling large-scale RNA-seq datasets.

### **Why HAWK Was Used**
- **High memory requirements**: STAR genome indexing and alignment require **20–40 GB RAM**, which can exceed local machine capacity.
- **Parallelisation**: By allocating multiple CPU cores, STAR and Picard can complete tasks significantly faster.
- **Reproducibility**: SLURM job scripts ensure that each stage of the pipeline is well-documented and repeatable.
- **Shared environment**: Cardiff provides pre-installed bioinformatics modules (e.g., STAR, Trimmomatic, Picard, FastQC), avoiding complex manual setups.

Each script in the repository contains `#SBATCH` directives to request resources from the SLURM scheduler, for example:
```bash
#SBATCH --mem=40G
#SBATCH --ntasks=4
#SBATCH --time=00:25:00
#SBATCH --job-name=ADmap
