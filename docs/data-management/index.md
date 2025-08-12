---
title: Data management
children: true
---

# Data Management

## Data organization

Most active data is stored on the `X://smb/fh/` drive under `fast` or `secure`. [See details for mounting the drives here](https://centernet.fredhutch.org/u/it/help-desk/mapping-network-drives/network-drive-paths-mac.html). Wet-lab folks tend to work more in `shared` for more human-utilized files, while larger computational files are stored in `fast`. In practice, I almost exclusively work in `fast`, occasionally outputting images or reports to `secure`. I think in theory there is slightly more cost associated with `fast`, but it hasn't been an issue.

`X: smb://center/fh` 

Key directories on the X drive are listed below. While there are many more than these, they are generally less actively used. I tried to organize things where I can, but people have different workflows, so you may work with other directories or see changes to this over time. 

```
fh
└─ secure
    | 
    └─ newell_e   // Evan Newell lab folder, ocassionally used with collaborators
    | 
    └─ _IRC 
        |
        └─ grp   // main data science working directory
            |
            └─ analyses                        // main directory for active analyses
            └─ bioinfo_tools                   // software for bioinformatics. E.g. cellranger
            └─ inhouse_computational_resources // FHIL specific resources, such as the knowledgebase repo, template repo, etc. 
            └─ NextSeq_SteamPlant              // Usual landing space for sequencing data
            └─ Xenium_Rundata                  // General landing space for Xenium run data
        └─ pub                                 // Apparently a public/shared dir, but I haven't used it
        └─ user                                // Side projects etc. here
|
└─ fast
    |
    └─ _IRC
        |
        └─ FHIL
            |
            └─ Database                // meeting notes and efforts to standardize the sample database
            └─ FHIL Proj_Figs          // Anna's preferred location for sharing figures / reports
            └─ Lab Protocol Documents  // Wetlab SOPs including some data management details (naming files etc.)
            └─ Lab Meetings            // Weekly standing meeting material. Put slideshows here

```

## Types of data 

Data can be thought of in these categories:

- **Raw**: Immutable data recovered from an instrument or observation.
    - BCLs and/or FASTQs
- **Intermediate**: Files produced during data processing that are used to produce the final output
    - BAMs, molecule_info.h5s
- **Processed**: The process of some transformation performed on raw data to produce new data. 
    - Counts matrices, AIRRs, VCFs
- **Analysis snapshots:** Saved data and objects representing checkpoints in computationally expensive workflows.
    - RDS files, model predictions
- **Figure:** Values or summary statistics used to create an image for publication. 
    - CSV
- **Logs:** Records of parameters, errors, and outcomes from computationally intense workflows.  

## Data lifecycle

Raw data should be uploaded to Cirro as early as possible. Raw data can be removed from the fast drive one it has been processed and/or transferred (see [Data science workflow](docs/data-science-workflow/index.md) for more info)

Intermediate files do not need to be retained long-term, as they are often large. Delete them when no long actively utilized. 

Processed data for any non-failed run should be uploaded to Cirro. Failed runs do not need to be kept. Processed data should be removed from the fast drive it is no longer being actively used for analysis.

Analysis snapshots and processed data for active analyses can be kept on the fast drive as needed until the project is complete, after which point they should be deleted.

Figure data should be kept upto/through publication. It should be relatively small and interoperable (CSV), so you should upload it to a cloud storage home at the end of a project. 

Logs should be kept/distributed with processed data whenever possible, even if it seems unnecessary. You never know what future questions may be asked of a process. Receipts are key. Logs of failed runs should be retained even if the processed data is not work saving. 
