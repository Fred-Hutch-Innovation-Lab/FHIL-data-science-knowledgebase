---
title: Cell annotation
parent: bioinformatic-workflows
last_modified_date: 2025-08-12
---

# Cell annotation

"""
The most challenging task in scRNA-seq data analysis is arguably the interpretation of the results. Obtaining clusters of cells is fairly straightforward, but it is more difficult to determine what biological state is represented by each of those clusters. Doing so requires us to bridge the gap between the current dataset and prior biological knowledge, and the latter is not always available in a consistent and quantitative manner. Indeed, even the concept of a “cell type” is not clearly defined, with most practitioners possessing a “I’ll know it when I see it” intuition that is not amenable to computational analysis. As such, interpretation of scRNA-seq data is often manual and a common bottleneck in the analysis workflow.
"""
- [Basics of Single-Cell Analysis with Bioconductor](https://github.com/OSCA-source/OSCA.basic)

In general, your best options are (somewhat arranged in order of ease & quality):
1. Map a well annotated reference dataset onto yours
2. Quantify expression signatures of cannonical marker genes
3. Manually review specific marker genes in cluster markers

This workflow mostly pertains to single-cell RNA seq and spatial transcriptomics. While the data types and biases are different, the fundamental goal is similar, and in practice the tools/workflows are also the same (for now). 

## Reference mapping

Many packages exist to leverage annotated query data onto your unknown data. I have had success using [Azimuth](https://azimuth.hubmapconsortium.org/) and [celltypist](https://www.celltypist.org/), but benchmarking studies [1](https://doi.org/10.1093/bib/bbae392)[2](https://doi.org/10.1186/s13059-019-1795-z)[3](https://doi.org/10.1093/bib/bbac561) show popular packages being outperformed by simple support vector machine classifiers. The flexibility, low dependency, and transparency of making your own classifier makes this my preferred means for annotation.

### SVM classifier

Support vector machines (SVM) are general purpose classifiers that take (sparse) matrices of input features to determine optimal distinguishing boundaries in high-dimensional space. Then by plugging in new data with the same input features, you can quickly assign each data point to a group from the training data. You can even use a sampling method to get classification probabilities. Since the input features are just genes, you can easily interpret the feature weights as "gene importance for distinguishing celltypes", allowing you to check unsupervised outcomes against biological knowledge. You can train your own classifier in a couple hours with [scikit-learn](https://scikit-learn.org/stable/). 

Briefly, you should ensure that your reference/training data and query data are subset to the same features (and in the same order). For ease of training, select a subset of highly variable/informative features. Normalize and log-transform the data in a consistent manner. The data should also be scaled, which you can do in the pipeline or prior to inputing data (I'm partial to the former to avoid lugging around the dense matrix). From there, you should select a good value for the C parameter of SVM, though it's [probably not too impactful](https://scikit-learn.org/stable/auto_examples/svm/plot_svm_scale_c.html#sphx-glr-auto-examples-svm-plot-svm-scale-c-py), so you can choose '1' or you can do a grid search to find a better value. Then just train your data with `kernel="linear"` and `probability=True`, then you are good to use your model to predict celltypes in your query data!

There is a more verbose workflow as a jupyter notebook (to be determined where this will live). 

## Marker genes

1. Aggregate cells into clusters
2. Find differentially expressed genes between clusters
3. Search for known celltype marker genes in top cluster markers

[See the biology section]]({% link docs/biology/celltypes.md %}) for more details on markers and celltypes.


## Further reading

https://bioconductor.org/books/3.13/OSCA.basic/cell-type-annotation.html
