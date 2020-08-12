# BagFootR

**About**  
In response to activating signals, transcription factors (TFs) bind DNA and regulate gene expression. TF binding can be measured by protection of the bound sequence from DNase digestion (i.e., footprint). Here, we report that 80% of TF binding motifs do not show a measurable footprint, partly because of a variable cleavage pattern within the motif sequence. To more faithfully portray the effect of TFs on chromatin, we developed an algorithm that captures two TF-dependent effects on chromatin accessibility: footprinting and motif-flanking accessibility. The algorithm, termed bivariate genomic footprinting (BaGFoot), efficiently detects TF activity. BaGFoot is robust to different accessibility assays (DNase-seq, ATAC-seq), all examined peak-calling programs, and a variety of cut bias correction approaches. BaGFoot reliably predicts TF binding and provides valuable information regarding the TFs affecting chromatin accessibility in various biological systems and following various biological events, including in cases where an absolute footprint cannot be determined.

Alternative program: http://centipede.uchicago.edu/  

## General Installation

**Pre-requistes**  

```R
# Dependencies
install.packages("hash")
install.packages("digest")
install.packages("data.table")
install.packages("Cairo")
install.packages("aplpack")
source("https://bioconductor.org/biocLite.R")
biocLite("BSgenome.Hsapiens.UCSC.hg19")
biocLite("BSgenome.Mmusculus.UCSC.mm9")
```

> Please Note: It is assumed that the following dependencies are installed on the target system. 

**Install BagFootR from source and generate reference files**  
```bash
# Get from R package from SourceForge
curl -L https://sourceforge.net/projects/bagfootr/files/bagfoot_0.9.7.02.tar.gz/download > bagfoot_0.9.7.02.tar.gz

# tar -xvzf bagfoot_0.9.7.02.tar.gz  # OPTIONAL STEP: Extracting the tarball so I can peek around

# Install as a local installation
module load R/3.5
mkdir -p local_install
R CMD INSTALL -l $PWD/local_install bagfoot_0.9.7.02.tar.gz

# Get the example dataset and rscripts on sourceforge
curl -L https://sourceforge.net/projects/bagfootr/files/example_bagfoot_scripts_and_data.zip/download > bagfoot.zip
unzip bagfoot.zip

# Generate Mappability reference files using code from PeakSeq: http://archive.gersteinlab.org/proj/PeakSeq/Mappability_Map/Code/
mkdir -p mappability
curl -L 'http://archive.gersteinlab.org/proj/PeakSeq/Mappability_Map/Code/Mappability_Map.tar.gz' > mappability/Mappability_Map.tar.gz
tar -xvzf mappability/Mappability_Map.tar.gz -C mappability/

# Location to hold mappability files for each supported reference genome
mkdir -p mappability/mm9 mappability/mm10 mappability/hg19 mappability/hg38

# Steps to create your own mappability files
# Download the fa files you want (one per chromosome)
for ref in "mm9" "mm10" "hg19" "hg38"; do echo "cp /data/CCBR_Pipeliner/db/PipeDB/Indices/${ref}_basic/Chromsomes/chr*.fa mappability/${ref}/" ; done | bash

# Make the 3 executables (chr2hash, oligoFindPLFFile, mergeOligoCounts) using the Makefile
cd mappability/ && make && cd ..


# Adding python scripts to a location relative to inputs
for ref in "mm9" "mm10" "hg19" "hg38"; do echo "cp mappability/compile.py mappability/CountMap.py mappability/${ref}/"; done | bash

# Adding executables to PATH
export PATH=$PATH:$PWD/mappability

# In the directory containing the fa files, run: python compile.py (takes several hours to run better off submitting as swarm job)
# Method 1: If you do submit as a swarm job don't forget to add the executables to your PATH before running compile.py
for ref in "mm9" "hg19"; do echo "cd mappability/${ref}/ && python2.7 compile.py 35 && cd ../.."; done | bash
for ref in "mm10" "hg38"; do echo "cd mappability/${ref}/ && python2.7 compile.py 50 && cd ../.."; done | bash

# Method 2: Swarm job to run "python compile.py" in the directory containing the fa files
cat << EOF
!/bin/bash

echo "mm9"; export PATH=$PATH:$PWD/mappability; cd mappability/mm9/ && python2.7 compile.py 35
echo "hg19"; export PATH=$PATH:$PWD/mappability; cd mappability/hg19/ && python2.7 compile.py 35
echo "mm10"; export PATH=$PATH:$PWD/mappability; cd mappability/mm10/ && python2.7 compile.py 50
echo "hg38"; export PATH=$PATH:$PWD/mappability; cd mappability/hg38/ && python2.7 compile.py 50
EOF > compile_mappability.swarm

swarm -g 8 -t 4 --time=72:00:00 -f compile_mappability.swarm

# You'll end up with pairs of files for each <chrname>.fa.HashOffsetTable, <chrname>.fa.HashPosTable
# Then, use CountMap.py in the usual way to access the data
```

### Importing BagFootR
**Import the local package**
```R
library("bagfoot", lib.loc="/scratch/Testing/forVishal/local_install/")
```
> **Please Note:** The installation method used above will not install bagfoot as a site package. You will need to modify your Rscripts and/or the example Rscripts so they point to our local installation of bagfoot (see example above). 

Try running with the example datasets and rscripts located here:
`/scratch/Testing/forVishal/example_bagfoot_scripts_and_data/`

### Run BagFootR with example dataset
```bash
module load samtools/0.1.19
module load R/3.5

# make sure to edit your library() import statement for bagfoot
cd example_bagfoot_scripts_and_data/
Rscript Rscript bagfoot_prep_example.R
```

**Please don't forget to add** `lib.loc` **PATH to the import statements** before running the scripts.

---

## Building the Docker Image for bagfootr
``` bash
# See listing of images on computer
docker image ls

# Build Dockerfile
docker build --tag=ccbr_bagfootr:v0.0.1 .

# Peak around the container: verify things run correctly
docker run -ti ccbr_bagfootr:v0.0.1 /bin/bash

# Updating tag(s) before pushing to DockerHub
docker tag ccbr_bagfootr:v0.0.1 skchronicles/ccbr_bagfootr:v0.0.1-beta
docker tag ccbr_bagfootr:v0.0.1 skchronicles/ccbr_bagfootr         # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_bagfootr:v0.0.1-beta
docker push skchronicles/ccbr_bagfootr:latest
```

### Run `bagfootr` with included test data
``` bash
# Docker
docker run -v $PWD:/data2 ccbr_bagfootr:v0.0.1 bash /home/bagfootr/scripts/shell_call_hla_type_test /home/bagfootr/test/test.bam Unknown 1 hg19 STDFQ 1 test_docker_dir 

# Singularity
singularity pull docker://skchronicles/ccbr_bagfootr:v0.0.1-beta
singularity exec -B "$PWD:/data2/" ccbr_bagfootr_v0.0.1-beta.sif bash /home/bagfootr/scripts/shell_call_hla_type_test /home/bagfootr/test/test.bam Unknown 0 hg19 STDFQ 0 test_singularity_dir
```
