# polysolver

## About 
POLYSOLVER is a tool for HLA typing based on whole exome sequencing (WES) data and infers alleles for the three major MHC class I  (HLA-A, -B, -C) genes.
The latest docker image of polysolver does not have R bundled, and this causes an issue when running the positional argument `-insertCalc` is set to 1. This argument indicates whether empirical insert size distribution should be used in the model (0 or 1). Under the hood, it internally calls `picard CollectInsertSizeMetrics` which needs R to be installed.
This patch includes the latest version of polysolver (as the base image) with R installed: https://software.broadinstitute.org/cancer/cga/polysolver

## Building the Docker Image for polysolver
``` bash
# See listing of images on computer
docker image ls

# Build Dockerfile
docker build --tag=ccbr_polysolver:v0.0.1 .

# Peak around the container: verify things run correctly
docker run -ti ccbr_polysolver:v0.0.1 /bin/bash

# Updating tag(s) before pushing to DockerHub
docker tag ccbr_polysolver:v0.0.1 skchronicles/ccbr_polysolver:v0.0.1
docker tag ccbr_polysolver:v0.0.1 skchronicles/ccbr_polysolver         # latest
docker tag ccbr_polysolver:v0.0.1 nciccbr/ccbr_polysolver:v0.0.1
docker tag ccbr_polysolver:v0.0.1 nciccbr/ccbr_polysolver              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_polysolver:v0.0.1
docker push skchronicles/ccbr_polysolver:latest
docker push nciccbr/ccbr_polysolver:v0.0.1
docker push nciccbr/ccbr_polysolver:latest 
```

## Run `polysolvers` with its included test data
``` bash
docker run -v $PWD:/data2 ccbr_polysolver:v0.0.1 bash /home/polysolver/scripts/shell_call_hla_type_test /home/polysolver/test/test.bam Unknown 1 hg19 STDFQ 1 test_docker 
```
