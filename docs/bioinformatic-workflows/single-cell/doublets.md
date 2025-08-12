---
title: Doublet removal
children: false
parent: single-cell
last_modified_date: 2024-06-26
---

## Doublet Removal

Most single-cell technologies are imperfect at isolating a single-cells. 
It is not impossible to have 2 or more cells in the same GEM or well, 
where each cell would be tagged with the same barcode. After sequencing, 
the shared barcode makes all reads appear to have come from one cell. 
This has various negative effects, including obscuring real signal. 
They should be removed when possible. 

Doublets are created during sample preparation and are partially a function
of batch effects. The expected doublet rate and distribution of normal values 
may vary between captures. Doublet correction should be performed at a capture level.

Some tools/papers distinguish between two types of doublets:
* Heterotypic doublets have reads from two transcriptionally distinct cells
(e.g. two different cell types)
* Homotypic doublets include transcriptionally similar cells (e.g. two B cells)
Some approaches to doublet removal are more tailored two resolving one or the other.  


### scDblFinder

[Github](https://github.com/plger/scDblFinder)

#### How it works

1. Artificial doublets are generated from existing data
2. Dimensional reduction and kNN
3. Train a classifier
4. Define a threshold based on expected doublet rate and classification error
    + Expected doublet rate is often described by the device manufacturer, but if it is not available, you can set an uninformative prior (`dbr.sd=1`)

#### Runtime considerations

Input data should **not** be pre-processed or filtered to remove low-quality GEMs based on metrics such as high UMI or gene count.
This may remove some doublets that could inform the classifier or contribute to the expected doublet count. 
However, the algorithm may fail to run if some input cells have too few data. If you encounter a 'size factors should be positive error', this 
may indicate you have GEMs with too few reads/genes to work with. For that reason, it is advised to remove cells with excessively low input
data prior to running scDblFinder.

scDblFinder can be fed clustered data or unclustered. Per their documentation, pre-clustered data is preferred for well-partitioned datasets, and unclustered is preferred for less well-partioned data, but the performance is not objectively better for either case.
I prefer using unclustered data to avoid additional decision points reliant on human input in the processing workflow.

### Doublet Finder

[Github](https://github.com/chris-mcginnis-ucsf/DoubletFinder)

This package had some major overhauls in a V3 release that broke some previous compatibility. Despite the overhaul, it didn't seem to be very actively maintained, so 
it's not my first choice package anymore.

#### How it works

1. Preprocess data, including removing low quality cells/clusters, normalizing, clustering, and possibly annotating cell types (for additional functionality).

1. Create simulated doublets in the dataset by averaging cells
2. Process mixed data using a constant Seurat pipeline
3. Cluster mixed data 
4. Predict doublets as cells with high number of artificial neighbors

DoubletFinder can also be supplied with 'Ground Truth' data: 
doublets in your dataset identified by conflicting sets of antibody 
tags in hashed studies (see cell hashing section). This can help seed
the expected doublet rate for your capture. 

DoubletFinder is incorporated in the gencoreSC package. See the 'using-gencoreSC' package for more details on using it in our standard workflow.

#### Runtime considerations

Doublet finder overestimates detectable doublets due to difficulty in identifying homotypic doublets.
This can be somewhat remedied by providing cell-type annotations and using them to calculate a lower-bound of doublet rate.
[More info](https://github.com/chris-mcginnis-ucsf/DoubletFinder#doublet-number-estimation)
