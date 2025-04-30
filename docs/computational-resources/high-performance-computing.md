---
title: High performance computing
parent: Computational resources
---

# High performance computing 

High performance computing/computers (HPCs) are networks of computing servers (often called 'clusters') designed to provide a shared resource for computationally intensive programs that users can borrow as needed. Where an individual may be limited by the hardware of their laptop or the budget of their lab, the HPC is free to use and users can request very large amounts of RAM, CPUs, GPUs, disk space, etc. HPCs use job handling software such as SLURM or Sun Grid Engine (SGE) to manage user's requests and allocate resources. Compute jobs are submitted to the cluster using an `.sbatch` script to register the job with SLURM.

HPCs are great for running expensive processing scripts, but you can also run interactive sessions and GUI notebook servers like RStudio and Jupyter. 

## Getting access to the HPC

Users can use the [Sci-comp self-service portal](https://scicomp-self-service.fredhutch.org/) to request access to the cluster. 

## Interactive sessions on HPC

Both Rstudio and JupyterLab can be ran on the HPC and accessed from your local computer browser, allowing you to leverage the HPC resources and connect to the shared drives.

### Jupyter

You can use Rhino modules with Jupyter installed, or you can use UV to set up your own environment for python. See 

```{bash}
## use screen or something similar to avoid crashing your session on disconnect
screen

## grab a node for interactive use. Follow the interactive prompts
grabnode

## with UV
uv add jupyter
uv run --with jupyter jupyter lab --ip=$(hostname) --port=$(fhfreeport) --no-browser

## with modules
ml JupyterLab/4.0.3-GCCcore-12.2.0  Seaborn/0.12.2-foss-2022b scikit-learn/1.2.1-gfbf-2022b
jupyter lab --ip=$(hostname) --port=$(fhfreeport) --no-browser

```

### Rstudio

[Rstudio server launcher](https://rstudio-launcher.fredhutch.org/)

# Further reading

- [Fred Hutch cluster 101](https://hutchdatascience.org/FH_Cluster_101/)
- [Fred Hutch scientific computing wiki](https://sciwiki.fredhutch.org/)