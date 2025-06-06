---
title: Open data science
children: false
parent: Data science workflow
last_modified_date: 2024-06-06
---

# Open data science

1. TOC
{:toc}

## Openness

**Open** science implies it can be seen by others. This usually means publishing code and data online. Github is used for code management, while Zenodo is useful for general digital storage.Gene Expression Omnibus or Sequence Read Archive are more domain specific resources for storing genomic/transcriptomic data for publications. If you intend to publish an analysis, you will likely have to make your data public through one of these resources.

## Accessibility

**Accessibility** deals with how understandable your code and workflows are. Well defined project structures, lab notebooks, ample READMEs, and modularized & documented code will make your work more accessible. 

See the [github template repo](https://github.com/Fred-Hutch-Innovation-Lab/analysis_project_template) for the preferred project structure. The structure is inspired by the [gin-tonic](https://gin-tonic.netlify.app/standard/) project and the file naming conventions of [The Turing Way](https://book.the-turing-way.org/reproducible-research/rdm/rdm-storage#rr-rdm-storage-organisation).

### Version Control

Version control is essential for tracking changes, collaborating with others, and maintaining reproducible workflows. You should develop a habit of regularily commiting updates to analyses. All scripts used to produce an analysis should be version tracked and ideally cloud-backed in GitHub or something similar. This will allow you to revert to:

* Revert to previous versions of an analysis
* Record failed analyses
* Test different analyses in parallel with branching
* Publish code with papers

- [Git branching workflows](https://nvie.com/posts/a-successful-git-branching-model/)
- [Git with RStudio](https://happygitwithr.com/usage-intro)

### Dry lab notebooks

### Data/research compendia


## Reproducibility

**Reproducibility** determines how reliable your results are. If it can't be reproduced, it isn't real. Container systems like Docker and Apptainer help manage system level consistency such as system libraries, operating systems, and language versions. Programming-language-specific dependency managers like Renv (R) and UV or poetry (Python) record versions. Random seed control ensure non-deterministic processes will output the same results when reran. 

Further reading: 

- https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/

### Containerization

Containers allow you to package an application with all of its dependencies into a standardized unit for software development. This is useful for developing robust workflows and publishing reproducible analyses. Docker is the most common containerization platform. Singularity (now called Apptainer) is a container platform designed for HPC environments. It is similar to Docker and can use docker images without root permissions.

- [Docker Documentation](https://docs.docker.com/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Security Best Practices](https://docs.docker.com/engine/security/)

#### Apptainer

Apptainer (formerly Singularity) is a docker-like solution for shared computing environments (such as high-performance computing clusters). When working with Rhino/Gizmo/Slurm, you will need to use Apptainer instead of docker to skirt permissions issues. See the [wiki](https://sciwiki.fredhutch.org/compdemos/Apptainer/) for more info.

- [Apptainer Documentation](https://apptainer.org/docs/)

### Dependency management

#### Renv (R)

Renv operates within an R console. [renv Documentation](https://rstudio.github.io/renv/)

```{r}
## Install Renv if needed
if (!require('renv')) {
  install.packages('renv')
}

## Initialize Renv
renv::init()

## Run this when installing new programs
renv::snapshot()
```

#### UV (Python)

UV operates outside of Python and will be invoked at the command line. On Gizmo/Rhino (FH HPCs), there is a module with UV installed. [UV Documentation](https://github.com/astral-sh/uv)

```{bash}
module load UV

## initialize a project with UV
uv init

## install a dependency
uv add <>
```
