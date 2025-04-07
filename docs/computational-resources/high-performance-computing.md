---
title: High performance computing
parent: Computational resources
---

# High performance computing 

High performance computing/computers (HPCs) are networks of computing servers (often called 'clusters') designed to provide a shared resource for computationally intensive programs that users can borrow as needed. Where an individual may be limited by the hardware of their laptop or the budget of their lab, the HPC is free to use and users can request very large amounts of RAM, CPUs, GPUs, disk space, etc. HPCs use job handling software such as SLURM or Sun Grid Engine (SGE) to manage user's requests and allocate resources. Compute jobs are submitted to the cluster using an `.sbatch` script to register the job with SLURM.

HPCs are great for running expensive processing scripts, but you can also run interactive sessions and GUI notebook servers like RStudio and Jupyter. 

See 'Further reading' for more details.

## Getting access to the HPC

Users can use the [Sci-comp self-service portal](https://scicomp-self-service.fredhutch.org/) to request access to the cluster. 

# Further reading

[Fred Hutch cluster 101](https://hutchdatascience.org/FH_Cluster_101/)

[Fred Hutch scientific computing wiki](https://sciwiki.fredhutch.org/)

[Rstudio server launcher](https://rstudio-launcher.fredhutch.org/)