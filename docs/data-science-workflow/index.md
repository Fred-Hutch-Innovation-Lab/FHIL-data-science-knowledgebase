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
    - Save the data to a stable cloud-storage location such as Cirro. Send to collaborators if no additional analysis is required. See [Data 
    management](docs/data-management/index.md) for more details.
4. Analyze
    - Analyze the processed data to discover insights. Not every dataset we handle will require analysis. See [Bioinformatic workflows](docs/bioinformatic-workflows/index.md) for specific types of analyses. 

# Data analysis workflow

While processing follows a more formulaic transformation of data from one state to another, analysis is a lot more fluid and poorly defined. The types of analyses will depend on the project goals. There are general principles that apply to all analyses: namely that they are **accessible**, **reproducible**, and **open**. 

