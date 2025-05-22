---
title: BaseSpace
parent: Data management
---

# BaseSpace

Basespace is Illumina's cloud server where sequencing run data can be backed up or processed. Raw sequencing data is in the form of BCL files which have to be extracted and converted to FASTQs for most applications. This can be done at the command line via tools like `bcl2fastq`, or through BaseSpace with the sample sheet provided for the sequencing run. The later is the current preferred method for extractions at FHIL, as it is familiar and accessible without the CLI. FASTQs can manually be downloaded from BaseSpace (see the SOP at ), or they can be downloaded on the HPC via the `BaseSpaceCLI` module. 

## CLI

The first time you use the basespace CLI, you will need to cache your credentials. Run `bs auth` and follow the prompts. The credentials should then be cached in your home directory for future use. 

`bs download` will allow you to retrieve files from sequencing runs. 