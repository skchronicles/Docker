FROM python:2.7
MAINTAINER Skyler Kuhn <kuhnsa3@gmail.com>

RUN mkdir -p /data
RUN mkdir -p /opt

# pip install: numpy, pandas, matplotlib, argparse
RUN pip install --upgrade pip --no-cache-dir
RUN pip install --no-cache-dir numpy pandas matplotlib argparse

# Set environment variable
ENV LANG en_US.UTF-8

WORKDIR /opt
COPY Dockerfile /opt

WORKDIR /data
