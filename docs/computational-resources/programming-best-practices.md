---
title: Best practices in programming
children: false
parent: Computational resources
last_modified_date: 2024-06-06
---

# Best practices in programming

This document records best practices and useful tools for various programming langauges.

## Reproducible compute environments

Anaconda changed it's licensing for large institutions, making it less accessible. FH now has it's own mirror of some conda channels: https://conda-forge.fredhutch.org/

Modules used on the HPC can be bundled as a container for publication purposes. I don't know the exact details of this, but consider asking scicomp if you used modules to process some data and want to publish the image with your findings.

## HTML reports

TODO: details about quarto and RMD html report generation.

## Language-specific

### Nextflow

- [nf-core fred-hutch profile](https://github.com/nf-core/configs/blob/master/docs/fred_hutch.md): fred-hutch specific nf-core profile that should allow easier use of nf-core pipelines on Fred Hutch HPC 
- [nf-core](https://nf-co.re/docs/): Writing modules and workflows in compliance with nf-core guidelines allows for easier interpolation between users
- [Nextflow patterns](https://nextflow-io.github.io/patterns/): Examples of common workflows in NF
- [nf-test](https://www.nf-test.com/): Testing workflow recommended by nf-core
- [Seqera AI](https://seqera.io/ask-ai/chat): Decent chatbot for NF 

### R

- [here](https://here.r-lib.org/): Better path resolution in R projects
- [R for Data Science](https://r4ds.hadley.nz/): Good detail of all fundamentals.
- [Tidy models](https://www.tidymodels.org/start/models/) A standardized approach to modeling in R

#### Separating report rendering from interactive analysis

While RMD natively supports rendering to reports, it requires the whole script to be ran again to render, which can be time-consuming or undesirable. While you should be able to re-run your script without concern for results integrity, rerunning the script each time you want to make an aesthetic tweak can be annoying. Consider using external "report" markdown files that rely on the environment created by the "analysis" workbook (see below). This allows you to separate the markdown code for creating a pretty report from the actual generation of the results. 

```{r}
## This only works if all the variables called in the format file 
## are in the current environment. Check the format file to tweak
## aesthetics 
rmarkdown::render(here('analysis_scripts/02_processing_template.format.Rmd'),
                  output_file = '02_processing_report.html',
                  output_dir = here('reports'))
```
