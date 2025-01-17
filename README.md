# Quality-Assessment-and-Preprocessing-of-E.-coli-K-12-MG1655-DNA-Seq-Data

```bash
trimmomatic PE -threads 4 \
  SRR13921545_1.fastq SRR13921545_2.fastq \
  SRR13921545_1_paired.fastq SRR13921545_1_unpaired.fastq \
  SRR13921545_2_paired.fastq SRR13921545_2_unpaired.fastq \
  ILLUMINACLIP:adapters.fa:2:30:10 SLIDINGWINDOW:4:20 MINLEN:36
```
PE: Indicates paired-end data.
- threads 4: Specifies 4 threads for faster processing.
- SRR13921545_1.fastq SRR13921545_2.fastq: Input files for paired-end reads.
- SRR13921545_1_paired.fastq SRR13921545_1_unpaired.fastq: Output for read 1 (paired and unpaired).
- SRR13921545_2_paired.fastq SRR13921545_2_unpaired.fastq: Output for read 2 (paired and unpaired).
- ILLUMINACLIP:adapters.fa:2:30:10: Adapter trimming with parameters:
- 2: Maximum mismatches.
- 30: Palindrome clip threshold.
- 10: Simple clip threshold.
SLIDINGWINDOW:4:20: Trims reads with an average quality below 20 in a sliding window of 4 bases.
MINLEN:36: Removes reads shorter than 36 bases after trimming.
