# Dockerfile
# rMATS: 4.0.2 and STAR:2.7.0f
FROM ubuntu:16.04

RUN mkdir -p /data /opt

RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen

RUN apt-get update && \
	apt-get upgrade -y 

RUN apt-get install -y software-properties-common && \
	add-apt-repository universe

RUN apt-get install -y python-dev build-essential git wget bzip2 zlib1g-dev

# Install pip and numpy
RUN wget https://bootstrap.pypa.io/get-pip.py && \
	python get-pip.py && \
	pip install --upgrade pip

RUN pip install numpy

# Install Dependencies
RUN apt-get -y install libblas-dev liblapack-dev zlibc zlib1g libgsl-dev gfortran make  gcc g++

WORKDIR /usr/lib/x86_64-linux-gnu
RUN ln -s libgsl.so.19.0.0 libgsl.so.0

WORKDIR /opt

# Install STAR:2.7.0f
RUN wget https://github.com/alexdobin/STAR/archive/2.7.0f.tar.gz
RUN tar -xzf 2.7.0f.tar.gz
WORKDIR /opt/STAR-2.7.0f/source
RUN make STAR
WORKDIR /opt
RUN rm 2.7.0f.tar.gz

# Install rMATS:4.0.2
RUN wget https://sourceforge.net/projects/rnaseq-mats/files/MATS/rMATS.4.0.2.tgz
RUN tar -xzf rMATS.4.0.2.tgz
RUN rm rMATS.4.0.2.tgz

RUN apt-get clean

# Updating $PATH 
ENV PATH=/opt/rMATS.4.0.2/rMATS-turbo-Linux-UCS4:/opt/STAR-2.7.0f/bin/Linux_x86_64:$PATH
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib/x86_64-linux-gnu

# Creating Biowulf-specific filesystem bind PATHS
RUN mkdir -p /gpfs /spin1 /scratch /lscratch /data /fdb
RUN for i in $(seq 1 30); do mkdir -p /gs$i; ln -s /gpfs/gsfs$i /gs$i; done

# Updating Permissions
RUN chmod 775 /opt/rMATS.4.0.2/rMATS-turbo-Linux-UCS4/rmats.py

WORKDIR /data
COPY Dockerfile /opt
