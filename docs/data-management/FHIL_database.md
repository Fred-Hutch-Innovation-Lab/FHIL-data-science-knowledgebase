---
title: FHIL database
parent: Data management

---

# FHIL database

FHIL maintains a database of samples and their processing, sequencing, and analysis. Currently, the database lives as a cloud-hosted excel document. Request access if needed. The current structure is as follows:

<iframe width="560" height="315" src='https://dbdiagram.io/e/68476925579a5a75f793c6f8/68476ac5579a5a75f793e6d6'> </iframe>

The wet-lab team maintains the first three sheets for intake samples, processed samples, and libraries. Data science people manage the later sheets for data collection runs, raw sample data, and processing runs. We are currently undergoing efforts to normalize the database, so the structure may change. For data-scientist purposes, the database should serve as the ground truth record of 

- What samples (and versions of samples) are in a sequencing run
- Where sample-level data files are stored (e.g. cirro, fast drive)
- What samples and special parameters (if any) were used for a data processing run
- When a sequencing run or a data processing run was performed

To the last point, we should make an effort to update the samplesheet whenever a data-generating transformation is performed. E.g., FASTQ extraction, cellranger processing, etc. When the data is moved from local to cloud hosting, we should update the storage location accordingly.
