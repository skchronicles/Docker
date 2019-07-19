# PCGR and CPSR
FROM continuumio/miniconda:4.6.14

# Personal Cancer Genome Reporter 
# https://github.com/sigven/pcgr#personal-cancer-genome-reporter-pcgr--variant-interpretation-report-for-precision-oncology

# Cancer Predisposition Seqeuencing Reporter 
# https://github.com/sigven/cpsr#cancer-predisposition-sequencing-reporter-cpsr

RUN mkdir -p /data
RUN mkdir -p /opt

WORKDIR /opt

# Setting language environment variable
ENV LANG en_US.UTF-8 

# Add Non-default channels
RUN conda config --add channels conda-forge && \
    conda config --add channels bioconda && \
    conda config --add channels pcgr

# Install Personal Cancer Genome Reporter
RUN conda install -y -c pcgr pcgr && \
    conda install -y r-upsetr && \
    conda install -y r-ggpubr

# Install Cancer Predisposition Seqeuencing Reporter
RUN conda install -y -c pcgr cpsr  

# Install VEP version 96: CPSR needs this version of VEP
RUN conda install -y -c bioconda ensembl-vep=96

COPY Dockerfile /opt
WORKDIR /data
