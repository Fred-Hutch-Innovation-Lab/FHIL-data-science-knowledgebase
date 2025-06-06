---
title: Best practices in programming
children: false
parent: Computational-resources
last_modified_date: 2024-06-06
---

# Best practices in programming

## Notebooks and reports

Notebooks such as quarto, jupyter, and R markdown allow interactive programming with nice GUIs to facilitate active analysis with data. They can be paired with static report rendering to produce deliverables.

- [Quarto](https://quarto.org/) A notebook solution that supports multiple languages. This seems to be the replacement for R markdown moving forward, as it is developed by Posit. 
- [Jupyter Book](https://jupyterbook.org/en/stable/intro.html) Seems to be a python-ic approach to the RMD style
- [R markdown](https://rmarkdown.rstudio.com/) 

## Data validation

Enforcing consistent data forms will make computational resources more utilizable and robust.

[Pointblank: Data validation in R](https://github.com/rstudio/pointblank)

## Language-specific

### Nextflow


- [Nextflow patterns](https://nextflow-io.github.io/patterns/): Examples of common workflows in NF
- [nf-test](https://www.nf-test.com/): Testing workflow recommended by nf-core
- [Seqera AI](https://seqera.io/ask-ai/chat): Decent chatbot for NF 

### R

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
