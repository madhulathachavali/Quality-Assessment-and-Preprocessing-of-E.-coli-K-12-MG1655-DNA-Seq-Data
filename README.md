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

Alignment Summary
Reads Processed: 82,458 reads.
CPU Time: 378.175 seconds.
Real Time: 668.257 seconds.

Alignment Summary
Key Metrics
- Total Reads: 9,675,593
- Mapped Reads: 9,051,992 (93.55%)
- Properly Paired Reads: 8,901,678 (92.12%)
- Singletons: 36,187 (0.37%)
- Supplementary Alignments: 12,497 (e.g., chimeric reads)
- Reads with Mate Mapped to Different Chromosomes: 0
- High Mapping Efficiency:
Over 93.5% of reads aligned to the reference genome, reflecting good data quality and library preparation.
- Low Singletons:
Only 0.37% of reads had mates that failed to align, indicating high pairing accuracy.



Create a new file named fastqc_pipeline.nf in your Ecoli directory:
bash
cd /Users/madhuchavali/Desktop/Ecoli
touch fastqc_pipeline.nf
Open fastqc_pipeline.nf and write:
text
process FASTQC {
    publishDir "/Users/madhuchavali/Desktop/Ecoli/FastQC_output", mode: 'copy'

    input:
    tuple val(sample_id), path(reads)

    output:
    path "fastqc_${sample_id}_logs"

    script:
    """
    mkdir fastqc_${sample_id}_logs
    fastqc -o fastqc_${sample_id}_logs -f fastq -q ${reads}
    """
}

workflow {
    read_pairs_ch = Channel.fromFilePairs("/Users/madhuchavali/Desktop/Ecoli/FastQ/*_{1,2}.fastq.gz")
    FASTQC(read_pairs_ch)
}
Save the file and exit the text editor.
Install Nextflow:
bash
curl -s https://get.nextflow.io | bash
Make the Nextflow script executable:
bash
chmod +x nextflow
Run the Nextflow pipeline:
bash
./nextflow run fastqc_pipeline.nf





