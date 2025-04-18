---
title: Analysis project structure
parent: Data science workflow
---

# General analysis project direcetory structure

```
project
└─── checkpoints                          # Saved objects reflecting a checkpoint after computationally expensive portions of an analysis
│   │   01-objects_post_filtering.Rds
│
└─── config                               # Project level definitions that affect multiple scripts. E.g. sample names, directories, etc.
│
│                               
└─── data                                 # Data generated as *inputs* to this project (not outputs)
│
└─── docs                                 # Documentation relevant to the project
│
└─── figures
│   └─── figure data                      # Tables of values to accomapny generated figures, for reference & publication
│       │   qc_pics.txt
│   └─── figure scripts                   # Isolated script to iterate on figures for publication
│       │   qc_pics.R
│   └─── figures
│       │   qc_pics.svg
│
└─── notebooks
│   └─── primary analyses                 # Main workflow notebooks
│       │   01_first-script.rmd/ipynb/etc
│       │   02...
│   └─── secondary analyses               # Separate lines of inquiry that may not continue
│       │   02.1_spinoff.rmd/ipynb/etc
│
└─── results                              # Tables, models, etc that represent outputs of an analysis for publication, other inputs, etc.
│
└─── reports                              # More comprehensive outputs from notebooks summarizing the work done
│   
└─── src                                  # Source files for code & helper functions that can be called in other scripts and notebooks
│   │   figure_labeller.R
│   │   file_extractor.py
│
│   README.md
│   .gitignore
│   renv.lock/uv.lock                     # Lockfiles for recording software versions
```

Additional reading:

https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424

https://github.com/KentonWhite/ProjectTemplate
