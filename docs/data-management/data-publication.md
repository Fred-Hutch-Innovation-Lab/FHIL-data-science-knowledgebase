---
title: Data publication
children: false
parent: Data management
last_modified_date: 2024-06-06
---

# Data publication

Data for any paper should be made publically available to support the publication. Common data publication resources include GEO, SRA, Zenodo, etc. 

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