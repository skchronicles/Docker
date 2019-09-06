# LibreOffice: 6.3.1 Dockerfile
FROM ubuntu:16.04

# LibreOffice
# Installation Notes:   https://wiki.documentfoundation.org/Documentation/Install/Linux
# Debian tarball:       https://download.documentfoundation.org/libreoffice/stable/6.3.1/deb/x86_64/LibreOffice_6.3.1_Linux_x86-64_deb.tar.gz

RUN mkdir -p /data/ && mkdir -p /opt/


RUN apt-get update && \
    apt-get upgrade -y 

RUN apt-get install -y --no-install-recommends wget \
                                               libdbus-glib-1-2 \
                                               libsm6 \
                                                openjdk-8-jre \
    && rm -rf /var/lib/apt/lists/*


WORKDIR /opt/

# Get tarball and install from source
RUN wget -q https://download.documentfoundation.org/libreoffice/stable/6.3.1/deb/x86_64/LibreOffice_6.3.1_Linux_x86-64_deb.tar.gz
RUN tar -xzf LibreOffice_6.3.1_Linux_x86-64_deb.tar.gz
WORKDIR /opt/LibreOffice_6.3.1.2_Linux_x86-64_deb/DEBS/
RUN dpkg -i *.deb

# Clean-up installation
RUN ln -s /opt/libreoffice6.3/program/soffice /usr/local/bin/
RUN rm /opt/LibreOffice_6.3.1_Linux_x86-64_deb.tar.gz
RUN rm -rf /opt/LibreOffice_6.3.1.2_Linux_x86-64_deb/


WORKDIR /data
COPY Dockerfile /opt
