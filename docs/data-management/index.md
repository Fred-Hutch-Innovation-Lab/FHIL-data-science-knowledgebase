---
title: Data Management
children: true
---

{:toc}

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


## Data lifecycle

Raw data should be uploaded to Cirro as early as possible. Raw data can be removed from the fast drive one it has been processed and/or transferred (see [Data science workflow](docs/data-science-workflow/index.md) for more info)

Processed data for any non-failed run should be uploaded to Cirro (TBD if we should retain failed runs too).

Analysis snapshots and processed data for active analyses can be kept on the fast drive as needed until the project is complete, after which point they should be deleted.

Figure data should be kept upto/through publication. It should be relatively small and interoperable (CSV), so you should upload it to a cloud storage home at the end of a project. 

Logs should be kept/distributed with processed data whenever possible, even if it seems unnecessary. You never know what future questions may be asked of a process. Receipts are key. Logs of failed runs should be retained even if the processed data is not work saving. 

