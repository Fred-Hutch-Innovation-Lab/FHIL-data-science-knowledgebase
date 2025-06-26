---
title: Workflow Managers
parent: Data science workflow
---

# Workflow Managers

Workflow managers stich together multiple steps to create a more seemless and reproducible pipeline for data manipulation. If you find yourself regularily running certain programs/files in tandem, or you have a large number of files you want to process in a similar manner, you should consider finding or developing a pipeline for your efforts. 

Common workflow management languages include Nextflow, Snakemake, and Cromwell.

## Nextflow

Nextflow is available on Rhino as a module

```
module spider Nextflow
```

If the pipeline uses containerization, you should also load an `Apptainer` module.

execute the pipeline with 

```
nextflow run ./main.nf -c nextflow.config --profile [local,slurm]
```

### Nf-core

Nf-core is an open-source community repository of bioinformatic workflows written in nextflow. There are many modules, subworkflows, and full workflows for many types of bioinformatic experiments. Before creating a nextflow workflow from scratch, you should see if you can leverage existing code, or find a workflow that does what you need. There is also an institutional profile available for Fred Hutch to run nf-core workflows on Rhino. See [here](https://github.com/nf-core/configs/blob/master/docs/fred_hutch.md) for more details.

# Resources

- [Nextflow documentation](https://www.nextflow.io/docs/latest/index.html)
- [nf-core](https://nf-co.re/)