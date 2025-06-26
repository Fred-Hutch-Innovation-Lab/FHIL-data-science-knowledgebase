---
title: Data science workflow
---

# Data science workflow

The data science workflow at FHIL consists of the following steps. I relate more common domain verbage to the 'ETL' language used more generally in data science. Much like the central dogma of biology, there will likely be devations from this as a linear workflow. This is simply to provide common language and understanding of how I conceive of my workflow. 

1. Retrieve ('Extract')
    - Data is pulled from it's raw output form from instruments, web servers, etc.  
        - BCL data from an Illumina instrument
        - FASTQs from BaseSpace
2. Processes ('Transform')
    - Raw data is processed to produce some more meaningful quantification of biogical state. Examples include:
        - Extracting FASTQs from BCL files (bcl2fastq)
        - Aligning FASTQs to reference genomes (STAR)
        - cellranger, spaceranger, other vendor-specific software
3. Transfer ('Load')
    - Save the data to a stable cloud-storage location such as Cirro. Send to collaborators if no additional analysis is required. See [Data management]({% link docs/data-management/index.md %}) for more details.
4. Analyze
    - Analyze the processed data to discover insights. Not every dataset we handle will require analysis. See [Bioinformatic workflows]({% link docs/bioinformatic-workflows/index.md %}) for specific types of analyses. 
5. Publish
    - If analyses are to be published on, the raw data, processing workflows, and analysis code need to be made accessible. 


While specifics of implementation will vary, there are general principles that apply to all data science workflows: namely that they are **accessible**, **reproducible**, and **open**. See [open data science]({% link docs/data-science-workflow/open-data-science.md %}) for more dicussion on best practices in data science. 

# 1. Retrieval

Data retrieval may occur as database queries, external transfers, or newly generated data. Data retrieved from some source should be treated as the **only copy** of said data. **Do not make direct changes to raw retrieved data**.

## Sequencing runs

In most cases, this will be a sequencing run performed by FHIL or another team. The data will be in the form of sequencer outputs in the form of BCL files, or sometimes FASTQs, depending on if the demultiplexing and extraction has been performed by the data creator. 

1. Record the details of the data generation in the `Data collection runs` sheet of the sample database. 
    - Link the run back to processed samples and libraries if possible
    - Record as much metadata about the sequencing run as possible
2. Back the run up in a cloud storage repo (e.g. [Cirro]({% link docs/data-management/cirro/index.md %}))
3. Transfer the data to the designated storage location in the fast drive.
    - As of 2025-05-20, that is `/fh/fast/_IRC/FHIL/grp/NextSeq_SteamPlant`. This seems to be true regardless of whether we generated it or not. 

## FASTQs

FASTQs are produced by extracting/demultiplexing BCL data. In some cases, this is performed as part of the sequencing data generation process, e.g. through BaseSpace. In those instances, the FASTQs will be included with the sequencing data. Given that the extraction is a deterministic process with few parameters, we can treat these as 'raw' data similar to the BCL files.
1. Record the details of the FASTQs in the `FASTQs` table of the sample database. 
2. Backup the files in a cloud storage repo (e.g. [Cirro]({% link docs/data-management/cirro/index.md %})). 
    - For now, we are continuing to group FASTQs with the sequencing run from which they were derived. This is not the most normalized way to store this, so it may change, but it is convenient for now.

# 2. Processing

Raw data in the form of FASTQs are often processed to create some intermediate output such as alignment files, count matrices, VCFs, AIRRs, etc. 

1. Initialize a new directory in the data processing folder
    - `/fh/fast/_IRC/FHIL/grp/processed_data`
    - Use the project ID to name the folder. Refer to the sample database to associate Data collection runs with project IDs. 
2. Create a README describing the location and identifying information of the source material and the details of the processing performed.
    - E.g. 
    ```
    Cellranger processing for the BM03 study. Using Cellranger v8.0.0
    Raw data lives at these locations:
    local:
    cloud:
        cirro:
            takara: 240723_VH00738_256_AAFWG5MM5
            neb: 240730_VH00738_259_AAFWGHHM5
            cellecta_RNA: 
                unused:
                    v1: 240813_VH00738_265_AAG3G77M5
                    v1.2: 240924_VH00738_279_AAG5FY7M5
                active (v2): 241224_VH00738_305_AAG5CHHM5
            cellecta_DNA: 241023_VH00738_289_AAG5FYFM5
            qiaseq:
                v1: 240614_VH00738_246_AAFVY2MM5
                v1.2: 240823_VH00738_270_AAG3JWMM5
    DOI:
    ```
3. Record the processing run information in the `Data processing runs` sheet of the sample database. 
4. Upload processing run ouptuts to the cloud (e.g. Cirro)

# 3. Transfer

If the data is to be transferred, ensure that both the raw data and processed data are backed up in Cirro and recorded in the sample database. After transferring, the data can be removed from the local fast drive. It can always be re-downloaded from Cirro. 

# 4. Analysis

Depending on the analysis, you may not need to access the raw data anymore, but it may be convenient to keep it around for a while if iterating on processing steps. Use your judgment ot decide if it needs to be kept. 

1. Create a new folder in the analysis directory
    - `/fh/fast/_IRC/FHIL/grp/analyses`
    - Use the project ID to name the folder. Refer to the sample database to associate Data collection runs with project IDs. 
2. Use the [analysis project structure]({% link docs/data-science-workflow/project-structure.md %}) to initialize the repository.
3. Populate the raw and processed data folders in the project structure. You can copy the data or use symlinks. Be sure to record the locations and identifiers of the data.
4. Use Git tracking to backup analysis work on Github or a similar service. You do not need to backup intermediate objects used to produce results. 
5. When finished with the analysis, push the whole thing to Cirro. Try to remove large intermediate files if necessary, but prioritize reproducibility over simplicity. 

# 5. Publication

1. Submit raw data through the Gene Expression Omnibus(GEO) or Sequence Read Archive (SRA).
    - See [data publication]({% link docs/data-management/data-publication.md %})
2. (Optional) submit processed data (e.g. counts matrices) through GEO or Zenodo. This is preferred but not strictly necessary for most publications. 
3. Publicize the Git repo used for analysis. 
4. Remove local/fast drive copies of raw and processed data.

