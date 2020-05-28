# Dockerfile for polysolver (v4): 
FROM sachet/polysolver:v4

RUN mkdir -p /data2/
RUN mkdir -p /opt2/

ENV DEBIAN_FRONTEND noninteractive

# Package information for polysolver: https://software.broadinstitute.org/cancer/cga/polysolver 
# Install r-base 
RUN apt-get update && \
    apt-get install -y r-base && \
    apt-get clean && \
    apt-get purge && \
  rm -rf /var/lib/apt/lists/*


WORKDIR /data2/

# Copy Dockerfile and README into /opt2
COPY Dockerfile /opt2
COPY README.md /opt2
