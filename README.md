# ShortCut
Adapter trimming and length distributions from small RNA-seq data

# Introduction
Small RNA sequencing usually produces reads that are longer than the biological RNAs. The extra sequence derives from adapters and is present at the 3' end of each read. Before analysis, these residual adapter sequences need to be identified and removed. After trimming, the size distribution of the trimmed reads is informative to assess sample quality. High rates of RNA degradation in the input are often reflected in the size profile of the trimmed reads. 

ShortCut automates adapter discovery, trimming, and provides an easy to use report on the results. The trimmed reads are output in a condensed FASTA format (see below) and are ready for further analysis.

## Input
One or more FASTQ files (can be .gz compressed) containing untrimmed small RNA seq data.

## Output
- Three condensed FASTA files per input FASTQ file. The three files contained properly trimmed sequences, sequences that were too short to be acceptable after trimming, and sequences where no adapter was identified, respectively.
- A csv-formatted file containing summary data on the output.
- An html report file giving an overview of the results.

# Install
1. Install `pixi` on your system <https://pixi.prefix.dev/latest/installation/>
2. Configure `pixi` to use BioConda per <https://bioconda.github.io/>
3. ```
   mkdir myShortCut
   cd myShortCut
   pixi init
   pixi add pandas cutadapt plotly
   pixi shell
   ```
4. Download the `ShortCut` file, `chmod +x ShortCut`, and run using `./ShortCut`. Or install to your path as you see fit.

(Mike to do - place this version of ShortCut on BioConda to simplify installation)

# Usage
With `pixi shell` activated as described above:
```
usage: ShortCut [-h] --fastq FASTQ [FASTQ ...] [--min_read_size MIN_READ_SIZE] [--out_dir OUT_DIR] [--threads THREADS] [--dicermin DICERMIN] [--dicermax DICERMAX]
                [--trim_key TRIM_KEY | --adapter ADAPTER]

options:
  -h, --help            show this help message and exit
  --fastq FASTQ [FASTQ ...]
                        One or more FASTQ alignment files
  --min_read_size MIN_READ_SIZE
                        Minimum length of trimmed reads to retain
  --out_dir OUT_DIR     output directory
  --threads THREADS     Number of threads to use. Default=1
  --dicermin DICERMIN   Minimum trimmed read length for true regulatory small RNA. Default=21
  --dicermax DICERMAX   Minimum trimmed read length for true regulatory small RNA. Default=24
  --trim_key TRIM_KEY   Trim key to use to infer adapter sequence (default: UCGGACCAGGCUUCAUUCCCC)
  --adapter ADAPTER     Adapter sequence to use for trimming
```

# Test / Example
Get some example small RNA-seq files from SRA. (Assumes installation of `fasterq-dump` from `sra-tools`).
`fasterq-dump SRR3222443 SRR3222444 SRR3222445`

Then, using four threads:
`ShortCut --fastq *.fastq --threads 4`






