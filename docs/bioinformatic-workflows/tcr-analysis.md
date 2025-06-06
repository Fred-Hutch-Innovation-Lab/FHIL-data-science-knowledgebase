---
title: BCR/TCR Analysis
parent: Bioinformatic workflows
---

# T cell repertoire sequencing

[MixCR](https://mixcr.com/mixcr/reference/overview-analysis-overview/)
[Immunarch](https://immunarch.com/)

MixCR is one of the most popular tools for BCR/TCR analysis. 
It extracts repertores from target amplicon sequencing protocols with and without molecular barcodes,
shotgun and RNA-Seq libraries, various single cell technologies and is flexible to be tuned for any custom protocol.

## Data preparation

Table from https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9369427/
<img width="993" alt="image" src="https://github.com/user-attachments/assets/d5948016-4b33-4ba6-992d-bb9076ce6e18">


## Processing

UMIs are commonly employed in repertoire sequencing to improve the fidelity in detection of rare clonotypes. 
You'll have to refer to the library preparation method to find how the UMIs were designed. Your workflow should
incorporate some UMI correction such as consensus sequence building.

Different libraries and experimental questions focus on different regions of the repertoire genes, so how you define
clones may vary by experiment. In general, the hyper-variable CDR3 region is one of the most unique, clonotype defining regions. 

### Running MixCR

MixCR is installed as modules on FH servers, but those are older versions. To run a more current MixCR version, you
can set up a container/apptainer. MixCR publishes an official image. To create an apptainer, `module load Apptainer` 
and pull the image from a public repository.

`apptainer pull ./mixcr_<name_the_version> docker://ghcr.io/milaboratory/mixcr/mixcr`

MixCR requires a license to opperate, which can be aquired for free as a non-profit. You can then pass the license file
to MixCR commands at runtime. For containerized versions, you can mount the file at `/opt/mixcr/mi.license` for automatic detection.

MixCR provides a wrapper command to run all parts of the pipeline automatically, or you can run individual steps manually for more 
granular control. See the documentation for full details.

#### Example scripts

<details><summary>Sbatch script</summary>

```
#!/bin/bash

# Job Options- must be before *any* executable lines

#SBATCH --job-name="mixcr"
#SBATCH --output=mixcr.out
#SBATCH --error=mixcr.err
#SBATCH --nodes=1                # node count
#SBATCH --ntasks=1               # total number of tasks across all nodes
#SBATCH --cpus-per-task=1        # cpu-cores per task (>1 if multi-threaded tasks)
#SBATCH --mem-per-cpu=80G        # memory per cpu-core
#SBATCH --time=48:48:00          # total run time limit (HH:MM:SS)
#SBATCH --mail-type=begin        # send email when job begins
#SBATCH --mail-type=end          # send email when job ends
#SBATCH --mail-type=fail         # send email if job fails
#SBATCH --mail-user=dgratz@fredhutch.org

module load Apptainer
cd /fh/fast/_IRC/FHIL/grp/BM03/processing/mixcr

# R1 = 1, R2 = 2
# 3 = sample name
# 4 = outdir
# 5 tagpattern

apptainer exec --bind ./mixcr_license.txt:/opt/mixcr/mi.license:ro \
        --bind /fh/fast/_IRC/FHIL/grp/BM03/processing/mixcr/:/home/dgratz/mixcr \
        --bind /fh/fast/_IRC/FHIL/grp/NextSeq_SteamPlant/240614_VH00738_246_AAFVY2MM5/FHIL_06142024_2024-06-14T19_50_58_68f53f1-421632874/BCLConvert_06_15_2024_16_53_29Z-740072376/:/home/dgratz/data \
        mixcr_4.6.0-226-devel.sif \
        ./mixcr/qiaseq/mixcr_qiaseq_1.sh
```

</details>

<details><summary>MixCR script</summary>

```
#!/bin/bash

# R1 = 1, R2 = 2
# 3 = sample name
# 4 = outdir
# 5 tagpattern

function run_mixcr {
    mixcr align \
        -p generic-amplicon-with-umi \
        --species hsa \
        --rna \
        --rigid-left-alignment-boundary \
        --floating-right-alignment-boundary C\
        --tag-pattern "^(R1:*) \ ^(UMI:N{12})N{12}(R2:*)" \
        --report $4/$3.report.txt \
        --json-report $4/$3.report.json \
        $1 \
        $2 \
        $4/$3ƒ.vdjca -f

    mixcr refineTagsAndSort \
        --report $4/$3.refineTags.report.txt \
        --json-report $4/$3.refineTags.report.json \
        $4/$3.vdjca \
        $4/$3.refined.vdjca -f

    mixcr assemble \
        -OassemblingFeatures="CDR3" \
        -OseparateByJ=true \
        -OseparateByV=true \
        --report $4/$3.report.txt \
        --json-report $4/$3.report.json \
        $4/$3.refined.vdjca \
        $4/$3.clns -f

    mixcr exportClones \
        -uniqueTagCount UMI \
        $4/$3.clns \
        $4/$3.txt -f 
}

function loop_files {
    # datadir='/fh/fast/_IRC/FHIL/grp/NextSeq_SteamPlant/240614_VH00738_246_AAFVY2MM5/FHIL_06142024_2024-06-14T19_50_58_68f53f1-421632874/BCLConvert_06_15_2024_16_53_29Z-740072376/'
    datadir='/home/dgratz/data'
    for file in $datadir/**/*R1*.fastq.gz; 
        do r1="$file"; 
        r2="$(echo $r1 | sed -E "s/(.+Q-F.+R).+/\1/")2_001.fastq.gz";
        samplename="$(echo $r1 | sed -E "s/.+(Q-F[^_]+).+/\1/")";
        # tagpattern="^(R1:*) \ ^(UMI:N{12})N{12}(R2:*)";
        outdir="mixcr/qiaseq";
        # echo $r1; echo $r2; echo $samplename; 
        mkdir $samplename;
        run_mixcr $r1 $r2 $samplename $outdir;
        done
}

loop_files 
```
  
</details>

## Analysis

[Immunarch](https://immunarch.com/) is a CRAN ready R package for exploring repertoire sequencing data. It's compatible with outputs
from MixCR and 10x pipelines. You can load data from multiple samples and quickly calculate comparisons and visualizations. Analysis
options include clontype tracking across samples, diversity estimations, gene usage, etc. Other possibly relevant metrics include
V(D)J segment use; nucleotide insertions and deletions; CDR lengths; and amino acid distributions along the CDRs.

## Terms

**Clonal evenness**: Distribution of TCR to see if there is clonal expansion
**Clonal richness**: Measurement of the number of clones with unique TCRs
**Clonal diversity**: Distribution of TCR, taking into account both evenness and richness
**TCR convergence**: Different clones with the same TCR due to degeneracy of codons
