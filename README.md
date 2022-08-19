# CNVkit CNV Calling Snakemake Pipeline

This repo is my implementation of [CNVkit](https://cnvkit.readthedocs.io/en/stable/) as a [Snakemake](https://snakemake.readthedocs.io/en/stable/) pipeline. My hope is this repo will help make cnv calling quick and easy for anyone.

## Install

If you haven't already, install (conda)[https://conda.io/projects/conda/en/latest/user-guide/install/index.html].

To install all necessary tools simply run

`conda env create -n cnvkit_snakemake -f environment.yml`

## Usage

Start the conda enviroment

`conda activate cnvkit_snakemake`

Example command

`snakemake -s cnvkit.snake --cores 64 --config ref_samples="ref_samples.example.txt" samples="samples.example.txt" bait="SureSelect_All_Exon_V2.bed" ref_genome="human_g1k_v37.fasta" access="access-5k-mappable.grch37.bed"`

`ref_samples` : the file for this parameter should be a list of the **absolute** file paths for the bam files you want to use as the reference panel for SavvyCNV. Each `.bam` file should have an accompanying `.bai` in the same location.

Example:

```
/the/absolute/path/ref_sample_1.bam
/the/absolute/path/ref_sample_2.bam
/the/absolute/path/ref_sample_3.bam
```

`samples` : the file for this parameter should be a list of the **absolute** file paths for the bam files you want to call CNVs on. Each `.bam` file should have an accompanying `.bai` in the same location.

Example:
```
/the/absolute/path/sample_A.bam
/the/absolute/path/sample_B.bam
/the/absolute/path/sample_C.bam
```

`reference`: reference genome `.fasta` file

`bait` : bait file in `.bed` format corresponding with the capture technology used in sample prep.

`access` : the sequence-accessible coordinates in chromosomes from the given reference genome, output as a BED file.

### Notes:

All file paths need to be absolute, not relative, as the pipeline will be symlinking the files.

Each sample's `.bam` must have a unique name and an accompanying `.bai`. 

The the final output calls will be saved in `result.cnn`.

