---
title: BaseSpace
parent: Data management
---

# Principles

- Machine readable
    - Avoid special characters ()?\!@\*%{[<> and spaces
    - Hyphens - and underscores _ can be used to separate related and unrelated chunks, respectively
        - Underscore separates units of metadata, hyphen separates related words
    - Case-sensitive: use lowercase when possible
- Human readable
    - Descriptive identifiers (slugs) 
- Promotes useful default ordering
    - Dates in ISO 8601 format (YYYYMMDD)
    - Left padded numbers for cardinal ordering (01, 02)
    - Semantic versioning (vX.Y.Z)

# File naming conventions

Data should have some reference to the library used to produce it. It must have a data collection run identifier. It doesn't have to include the sample or project identifier, but we will probably work to define naming conventions together.

ideas:

`<run-ID>_<project-ID>_<sample-ID>_<file-info>.fo`
e.g.
`SR0001_XE010_B1-5X-F1-WT_R1_001.fastq.gz`

## Project IDs

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

# Examples

Original sequencing run

`BM02-F1A_R1_001.fastq.gz`

Additional sequencing to bring the previous dataset to full depth. Here, we supply the version as well, to indicate the `.2` refers to the set. It will be implied that the original dataset will likely not have any versioning info as it was the first data generated for this project.

`BM02-F1A.1.2_R1_001.fastq.gz`

*New sequencing run intended to replace previous run due to poor quality*. 

Here we don't need to supply the set suffix yet. The absence of this value indicates this is the first sequencing run of the new replacement library.

`BM02-F1A.2_R1_001.fastq.gz`



# Additional guidelines

- Use the researcher’s name/initials
- Do not make file names too long (this can complicate file transfers)
- Avoid personal data in file names

# Resources

[MIT file and folder naming guidelines](https://libraries.mit.edu/data-management/store/organize/)
[The Turing way for data organization](https://book.the-turing-way.org/reproducible-research/rdm/rdm-storage#rr-rdm-storage-organisation)