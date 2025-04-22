---
title: Data Management
children: true
---

# Data Management

This section covers various aspects of data management in research workflows.

## Types of data 

Data can be thought of in these categories

* **Raw**: Immutable data recovered from an instrument or observation.
    - BCLs and/or FASTQs

* **Processed**: The process of some transformation performed on raw data to produce new data. 
    - Counts matrices, AIRRs, VCFs

* **Intermediate**: Files produced during data processing that are used to produce the final output
    - BAMs, molecule_info.h5s

* **Analysis snapshots:** Saved data and objects representing checkpoints in computationally expensive workflows.
    - RDS files, model predictions

* **Figure:** Values or summary statistics used to create an image for publication. 
    - CSV

* **Logs:** Records of parameters, errors, and outcomes from computationally intense workflows.  

## File naming conventions

Data should have some reference to the library used to produce it. It must have a data collection run identifier. It doesn't have to include the sample or project identifier, but we will probably work to define naming conventions together.

ideas:

`<run-ID>_<project-ID>_<sample-ID>_<file-info>.fo`
e.g.
`SR0001_XE010_B1-5X-F1-WT_R1_001.fastq.gz`

### Project IDs

*	Xenium: = `XE00#`
*   Xenium Prime: `XP00#`
*	CosMx = `CM00#`
*	CytAssist = `CA00#`
*	FLEX = `FL00#`
*	Parse = `PA00#`
*	Scale = `SC00#`
*	Fluent = `FB00#`
*	10X 3' = `3P00#`
*	10X 5' = `5P00#`
*	Benchmark Platforms = `BM00#`

## Semantic versioning

Datasets that reflect new versions of old data (e.g. resequencing due to poor quality) or supplemental/additional data (e.g. sequencing for additional depth) can borrow semantic versioning guidelines to indicate the relationship between datasets. 

- Data intended to **replace** previous data can be indicated with a *version* suffix.
- Data intended to **supplement** previous data can be indicated with a *set* suffix **appended after** the version suffix. 
If no version or set is enumerated, it should be assumed to be the first, as this is the most common case and most datasets will not have additional versions or sets. 

`<dataset_name><.version><.set>.<extension>`

### Examples

Original sequencing run

`BM02-F1A_R1_001.fastq.gz`

Additional sequencing to bring the previous dataset to full depth. Here, we supply the version as well, to indicate the `.2` refers to the set. It will be implied that the original dataset will likely not have any versioning info as it was the first data generated for this project.

`BM02-F1A.1.2_R1_001.fastq.gz`

*New sequencing run intended to replace previous run due to poor quality*. 

Here we don't need to supply the set suffix yet. The absence of this value indicates this is the first sequencing run of the new replacement library.

`BM02-F1A.2_R1_001.fastq.gz`


## Data lifecycle

Raw data should be uploaded to Cirro as early as possible. Raw data can be removed from the fast drive one it has been processed and/or transferred (see [Data science workflow](docs/data-science-workflow/index.md) for more info)

Processed data for any non-failed run should be uploaded to Cirro (TBD if we should retain failed runs too). It should be removed when it is no longer being actively used for analysis.

Analysis snapshots and processed data for active analyses can be kept on the fast drive as needed until the project is complete, after which point they should be deleted.

Figure data should be kept upto/through publication. It should be relatively small and interoperable (CSV), so you should upload it to a cloud storage home at the end of a project. 

Logs should be kept/distributed with processed data whenever possible, even if it seems unnecessary. You never know what future questions may be asked of a process. Receipts are key. Logs of failed runs should be retained even if the processed data is not work saving. 

# GEO submissions

The Gene Expression Omnibus (GEO) is a genomics data repository. It used to store sequencing-based data such as FASTQs, counts matrices, RDS, etc. Many publication journals require data to be uploaded to GEO or something similar. You'll need and NCBI account to create a new submission. Follow their [instructions](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html) and use their metadata sheet template to complete submission. Files can be transfered efficiently using a file transfer protocol (FTP) on the HPC. 

Use the module `lftp: lftp/4.9.1-GCCcore-8.3.0` (or whatever the latest version is)

```
module load lftp

## you'll get a password and folder for your submission once you start
lftp ftp-private.ncbi.nlm.nih.gov -u geoftp,<your_password_here>
## if you connect successfully, your prompt will change

cd uploads/your@mail.com_yourfolder
mirror -R Folder_with_submission_files uploads/your@mail.com_yourfolder
```