# Base image using microsoft's dotnet
# sdk, installs Pisces/5.2.10.49
FROM mcr.microsoft.com/dotnet/nightly/sdk:2.1-focal AS build

LABEL maintainer=kuhnsa@nih.gov

# Create Container filesystem specific 
# working directory and opt directories 
RUN mkdir -p /opt2 && mkdir -p /data2
WORKDIR /opt2 

# Set time zone to US east coast 
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone

# This section installs system packages 
# required for your project. If you need 
# extra system packages add them here.
RUN apt-get update \
    && apt-get -y upgrade \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \    
        build-essential \
        bzip2 \
        curl \
        git \
        locales \
        python3 \
        python3-pip \
        samtools \
        unzip \
        wget \
    && apt-get clean && apt-get purge \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set the locale
RUN localedef -i en_US -f UTF-8 en_US.UTF-8

# Install Pisces 5.2.10.49 and create env
# variables and a wrapper for ease of use 
RUN wget https://github.com/Illumina/Pisces/releases/download/v5.2.10.49/Pisces_5.2.10.49.tar.gz \
    && tar -xvf Pisces_5.2.10.49.tar.gz \
    && rm Pisces_5.2.10.49.tar.gz 
ENV PISCES_PATH="/opt2/Pisces_5.2.10.49/"
RUN echo '#!/bin/bash' > /opt2/Pisces5.2 \
    && echo 'dotnet ${PISCES_PATH}/Pisces.dll "$@"' >> /opt2/Pisces5.2 \
    && chmod a+rx /opt2/Pisces5.2

# Install Pisces 5.3.0.0 and create env
# variables for ease of use
RUN curl -OL https://github.com/tamsen/Pisces/raw/master/binaries/5.3.0.0/pisces_all_5.3.0.0.tar.gz \
    && tar -xvf pisces_all_5.3.0.0.tar.gz \
    && rm pisces_all_5.3.0.0.tar.gz \
    && ln -s /opt2/pisces_all/Pisces /opt2/ \
    && ln -s /opt2/pisces_all/Pisces /opt2/Pisces5.3

# Add Dockerfile and argparse.bash script
# and export environment variables
# and creating a backwards compatible
# wrapper for Biowulf's trimmomatic/0.39
# and set java8 as default with links
# to alternative versions
ADD Dockerfile /opt2/Dockerfile
RUN chmod -R a+rX /opt2 
ENV PATH="/opt2:$PATH"
WORKDIR /data2

