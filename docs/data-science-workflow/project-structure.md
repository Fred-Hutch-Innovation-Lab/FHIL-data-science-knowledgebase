---
title: Analysis project structure
parent: Data science workflow
---

# General analysis project direcetory structure

```
project
│   README.md
│   .gitignore
│   renv.lock/uv.lock                     # Lockfiles for recording software versions
│                               
└─── data                                 # Data generated as *inputs* to this project (not outputs)
│
└─── figures
│   └─── figure scripts                   # Isolated script to iterate on figures for publication
│       │   qc_pics.R
│   └─── figures
│       │   qc_pics.svg
│   └─── figure data                      # Tables of values to accomapny generated figures
│       │   qc_pics.txt
│
└─── notebooks
│   └─── primary analyses                 # Main workflow notebooks
│       │   01_first-script.rmd/ipynb/etc
│       │   02...
│   └─── secondary analyses               # Separate lines of inquiry that may not continue
│       │   02.1_spinoff.rmd/ipynb/etc
│   
└─── src                                  # Source files for code & helper functions that can be called in other scripts and notebooks
│   │   figure_labeller.R
│   │   file_extractor.py
│
└─── reports                              # More comprehensive outputs from notebooks summarizing the work done
│
└─── analysis_snapshots                   # Saved objects reflecting a checkpoint after computationally expensive portions of an analysis
│   │   01-objects_post_filtering.Rds
│
└─── docs                                 # Documentation relevant to the project

```

Additional reading:

https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424

https://github.com/KentonWhite/ProjectTemplate
