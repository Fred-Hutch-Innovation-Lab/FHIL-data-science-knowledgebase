---
title: Open data science
children: false
parent: Data science workflow
last_modified_date: 2025-08-15
---

# Open data science

1. TOC
{:toc}

**Reproducibility** determines how reliable your results are. If it can't be reproduced, it isn't real. The reproducibility stack consists of multiple layers that work together to ensure your analysis can be exactly reproduced by others (or yourself on different machines).

To create a fully reproducible analysis:

1. **Start with a structured project**
   - [FHIL analysis template](https://github.com/Fred-Hutch-Innovation-Lab/analysis_project_template)
2. **Use containers** for system-level consistency (Docker/Apptainer) 
   - [R/Rstudio](https://github.com/Fred-Hutch-Innovation-Lab/rstudio-server-launcher)
   - [Python/Jupyter (with R and Julia)](https://github.com/Fred-Hutch-Innovation-Lab/jupyter-lab-launcher)
3. **Manage packages** with language-specific tools (renv/UV)
4. **Version control** all code and configuration
5. **Set random seeds** for deterministic results
6. **Document everything** in READMEs and lab notebooks
7. **Test reproducibility** on clean environments
8. **Publish** code, data, and environment specifications

- [An expanded version](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/)

## 1. Containerization (System Level)

Containers package your application with all its system dependencies into a standardized unit. This ensures consistency across different operating systems, system libraries, and computing environments. Docker is the most common containerization platform. Singularity (now called Apptainer) is a container platform designed for HPC environments. It is similar to Docker and can use docker images without root permissions.

Further reading: 
- [Docker Documentation](https://docs.docker.com/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Security Best Practices](https://docs.docker.com/engine/security/)
- [Apptainer at FH wiki](https://sciwiki.fredhutch.org/compdemos/Apptainer/)


### FHIL Compute Environment Launchers

FHIL provides streamlined launchers that automatically manage containers for interactive compute environments. These handle container setup and hosting for interactive analysis sessions on Fred Hutch HPCs

- [JupyterLab Launcher](https://github.com/Fred-Hutch-Innovation-Lab/jupyter-lab-launcher)
- [RStudio Server Launcher](https://github.com/Fred-Hutch-Innovation-Lab/rstudio-server-launcher)

## 2. Project Structure & Documentation (project level)

Well-defined project structures, lab notebooks, ample READMEs, and modularized & documented code make your work more accessible and reproducible. The [FHIL analysis template](https://github.com/Fred-Hutch-Innovation-Lab/analysis_project_template) provides a preferred project structure inspired by the [gin-tonic](https://gin-tonic.netlify.app/standard/) project and the file naming conventions of [The Turing Way](https://book.the-turing-way.org/reproducible-research/rdm/rdm-storage#rr-rdm-storage-organisation).

## 3. Package Management (Language Level)

Package managers track exact versions of language-specific dependencies, ensuring the same packages are used across different environments. The [FHIL project template](https://github.com/Fred-Hutch-Innovation-Lab/analysis_project_template) comes with some startup scripts to initialize these project workflows.

- [R: renv](https://rstudio.github.io/renv/)
- [Python: UV](https://github.com/astral-sh/uv)

## 4. Version Control (Code Level)

Version control tracks changes to your analysis code, allowing you to:
- Revert to previous versions
- Track what changed and when
- Collaborate with others
- Publish code with papers

**Resources:**
- [Git branching workflows](https://nvie.com/posts/a-successful-git-branching-model/)
- [Git with RStudio](https://happygitwithr.com/usage-intro)

## 5. Random Seed Control (Algorithm Level)

Set random seeds to ensure non-deterministic processes produce the same results when rerun.

```r
# R
set.seed(42)

# Python
import numpy as np
np.random.seed(42)

# Set seeds at the beginning of your analysis
# Document the seed value used
```

## 6. Data Versioning (Data Level)

Track versions of input data and intermediate results:
- Use data versioning tools (DVC, Git LFS)
- Document data sources and processing steps
- Include data checksums for verification
- When possible, store data in human-readable/non-proprietary formats

# Further Reading

- [The Turing Way](https://book.the-turing-way.org/)
- [Reproducible and Trustworthy Workflows for Data Science](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/)
