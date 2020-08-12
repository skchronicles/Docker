FROM rocker/verse:latest

MAINTAINER   Songjoon Baek <sojbaek@hotmail.com>

#Install TCL/TK
RUN apt-get update && apt-get -y install tcl8.6-dev tk8.6-dev 

#Samtools
RUN apt-get update && apt-get -y upgrade && \
	apt-get install -y build-essential wget \
		libncurses5-dev zlib1g-dev libbz2-dev liblzma-dev libcurl3-dev && \
	apt-get clean && apt-get purge && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
	
WORKDIR /usr/src
RUN wget https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2 && \
	tar jxf samtools-1.9.tar.bz2 && \
	rm samtools-1.9.tar.bz2 && \
	cd samtools-1.9 && \
	./configure --prefix $(pwd) && \
	make
ENV PATH=${PATH}:/usr/src/samtools-1.9 

# required R packages
RUN R -e "install.packages('hash')"
RUN R -e "install.packages('parallel')"
RUN R -e "install.packages('digest')"
RUN R -e "install.packages('data.table')"
RUN R -e "install.packages('Cairo')"
RUN R -e "install.packages('aplpack')"

RUN R -e "if (!requireNamespace('BiocManager', quietly = TRUE)) install.packages('BiocManager')"
RUN R -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm9')"
RUN R -e "BiocManager::install('BSgenome.Mmusculus.UCSC.mm10')"
RUN R -e "BiocManager::install('BSgenome.Hsapiens.UCSC.hg38')"
RUN R -e "BiocManager::install('BSgenome.Hsapiens.UCSC.hg19')"
RUN R -e "BiocManager::install('BSgenome.Rnorvegicus.UCSC.rn5')"
RUN R -e "BiocManager::install('BSgenome.Rnorvegicus.UCSC.rn6')"
RUN R -e "BiocManager::install('Rsamtools')"
RUN R -e "BiocManager::install('GenomeInfoDb')"
RUN R -e "BiocManager::install('GenomicRanges')"
RUN R -e "BiocManager::install('IRanges')"


# copy BagFoot related files

WORKDIR /home/bagfoot
RUN wget https://sourceforge.net/projects/bagfootr/files/example_data.tar.gz
RUN tar -xvf /home/bagfoot/example_data.tar.gz

RUN wget https://sourceforge.net/projects/bagfootr/files/bagfoot_0.9.7.06.tar.gz
RUN wget https://sourceforge.net/projects/bagfootr/files/bagfoot_prep_example.R
RUN wget https://sourceforge.net/projects/bagfootr/files/bagfoot_run_example.R


# bagfoot installation
RUN R -e "install.packages('bagfoot_0.9.7.06.tar.gz')"


RUN rm /home/bagfoot/example_data.tar.gz
COPY Dockerfile /opt
#  To build:
#   sudo docker build -t bagfoot .
#
#  To run:
#    sudo docker run -ti --rm  -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix   bagfoot bash
#    In R, type 'source("bagfoot_run_example.R")' to run the example program.

