# QualiMap from Conda
FROM conda/miniconda2

# R Packages: seurat (>3)

RUN mkdir -p /data
RUN mkdir -p /opt

WORKDIR /opt

# Setting language environment variable
ENV LANG en_US.UTF-8 

# Install Seurat
RUN conda config --add channels bioconda && \
    conda config --add channels r && \
    conda config --add channels conda-forge && \
    conda update --all -y && \
    conda install -y -c bioconda r-seurat && \ 
    conda install -y -c bioconda/label/gcc7 r-seurat && \ 
    conda install -y -c bioconda/label/cf201901 r-seurat 

# Install UMAP
RUN conda install -c conda-forge umap-learn && \
    conda install -c conda-forge/label/cf201901 umap-learn 

ENV LC_ALL=C
COPY Dockerfile /opt
WORKDIR /data
