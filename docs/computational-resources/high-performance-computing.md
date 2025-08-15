---
title: High performance computing
parent: Computational resources
last_modified_date: 2024-06-06
---

# High performance computing 

High performance computing/computers (HPCs) are networks of computing servers (often called 'clusters') designed to provide a shared resource for computationally intensive programs that users can borrow as needed. Where an individual may be limited by the hardware of their laptop or the budget of their lab, the HPC is free to use and users can request very large amounts of RAM, CPUs, GPUs, disk space, etc. HPCs use job handling software such as SLURM or Sun Grid Engine (SGE) to manage user's requests and allocate resources. Compute jobs are submitted to the cluster using an `.sbatch` script to register the job with SLURM. HPCs are great for running expensive processing scripts, but you can also run interactive sessions and GUI notebook servers like RStudio and Jupyter with high RAM and quick file access. 

- [Fred Hutch cluster 101](https://hutchdatascience.org/FH_Cluster_101/)
- [Slurm examples at FH](https://github.com/FredHutch/slurm-examples/tree/main)
- [Software modules on FH HPC](https://sciwiki.fredhutch.org/scicomputing/compute_environments/) 

## Getting access to the HPC

Users can use the [Sci-comp self-service portal](https://scicomp-self-service.fredhutch.org/) to request access to the cluster. 

## Interactive sessions on HPC

Screen + grabnode allows a persistent, long-term interactive session.

```bash
## use screen or something similar to avoid crashing your session on disconnect
screen

## grab a node for interactive use. Follow the interactive prompts
grabnode
```

Both RStudio and JupyterLab can be run on the HPC and accessed from your local computer browser, allowing you to leverage the HPC resources and connect to the shared drives.

### Jupyter

**Recommended: Use the FHIL Jupyter Lab Launcher**

The [FHIL Jupyter Lab Launcher](https://github.com/Fred-Hutch-Innovation-Lab/jupyter-lab-launcher) provides a streamlined way to run Jupyter Lab on the HPC. This allows you to configure your own resource allocation and control the system libraries with greater permissions (by editing the image definition).

```bash
# Clone the repository
git clone https://github.com/Fred-Hutch-Innovation-Lab/jupyter-lab-launcher.git
cd jupyter-lab-launcher

# Submit the job (automatically pulls container and sets up networking)
sbatch launch_jupyter_lab.sh
```

**Alternative: Traditional module-based approach**

You can also use Rhino modules with Jupyter installed, or set up your own environment with UV. This is fine but a little sloppier for recording the environment used, managing screen sessions, etc.

```bash
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

### RStudio

**Recommended: Use the FHIL RStudio Server Launcher**

The [FHIL RStudio Server Launcher](https://github.com/Fred-Hutch-Innovation-Lab/rstudio-server-launcher) provides a streamlined way to run RStudio Server on the HPC. This allows you to configure your own resource allocation and control the system libraries with greater permissions (by editing the image definition).

```bash
# Clone the repository
git clone https://github.com/Fred-Hutch-Innovation-Lab/rstudio-server-launcher.git
cd rstudio-server-launcher

# Submit the job (automatically pulls container and sets up networking)
sbatch launch_rstudio_server.sh
```


**Alternative: FH rstudio launcher**

This will be faster, but has more limits on the system libraries you can install. Also, if you want to get a reproducible compute environment for publishing, you'll have to contact scicomp and ask them for the details (probably not that hard, but I prefer to just build it myself). 

- [Rstudio server launcher](https://rstudio-launcher.fredhutch.org/) (legacy)
