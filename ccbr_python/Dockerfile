FROM ubuntu:16.04
MAINTAINER Skyler Kuhn <kuhnsa3@gmail.com>

RUN mkdir -p /data
RUN mkdir -p /opt

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install --yes \
 build-essential \
 apt-utils \
 git-all \
 python \ 
 python-pip \
 wget

# pip install: numpy, pandas, matplotlib, argparse
RUN pip install --upgrade pip
RUN pip install numpy pandas matplotlib argparse

# pip install snakemake
RUN DEBIAN_FRONTEND=noninteractive apt-get install --yes \
  python3 \
  python3-pip && pip3 install snakemake

# Set environment variable
ENV LANG en_US.UTF-8 

WORKDIR /opt
COPY Dockerfile /opt

WORKDIR /data

