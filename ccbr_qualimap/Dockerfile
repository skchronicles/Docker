# QualiMap from Conda
FROM conda/miniconda2

# Here is QualiMap's installation documentation needs: http://qualimap.bioinfo.cipf.es/doc_html/intro.html#installation
# 1. JAVA runtime > 6
# 2. R enviroment > 3.1
# 3. R Packages: optparse (CRAN), NOISeq (Bioconductor), Repitools (Bioconductor), Rsamtools (Bioconductor), GenomicFeatures (Bioconductor), rtracklayer (Bioconductor) 

RUN mkdir -p /data
RUN mkdir -p /opt

WORKDIR /opt

# Setting language environment variable
ENV LANG en_US.UTF-8 

RUN conda config --add channels bioconda && \
    conda config --add channels r && \
    conda config --add channels conda-forge && \
    conda update --all -y &&\
    conda install -y qualimap=2.2.2a

COPY Dockerfile /opt
WORKDIR /data
