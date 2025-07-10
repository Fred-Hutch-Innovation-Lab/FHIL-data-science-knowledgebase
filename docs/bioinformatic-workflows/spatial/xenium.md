---
title: Xenium spatial RNA-seq
children: true
parent: Bioinformatic workflows
---

# Xenium spatial RNA-seq

# Processing steps

Xenium features negative control probes and codewords that can be used to assess the quality of algorithms. It's a good idea to check these periodically to see if they are driving anything such as clustering or differential expression.

## Cell segmentation

Xenium's default is often out-performed by 3rd party tools. FHIL prefers [Proseg](https://github.com/dcjones/proseg) as it was developed by our collaborator.

## Cell filtering

## Clustering

Focusing on highly SVF may help clustering algorithms perform better. Review the selcetion of SVFs to minimize negative control probes.

## Other processing steps

Log-transformation & normalization
Use all PCs in graph formation


# Reading

1. [Best practices in Xenium analysis](https://www.nature.com/articles/s41592-025-02617-2#Sec13)
