# Dockerfile for ClustalO (version 1.2.4)
FROM ubuntu:18.04

RUN mkdir -p /data
RUN mkdir -p /opt


# Package information for ClustalO: "https://packages.ubuntu.com/search?keywords=clustalo&searchon=names"
RUN apt-get update && \
  apt-get install -y \
  clustalo=1.2.4-1 curl && \
  apt-get clean && \
  apt-get purge && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data

# Download latest covid-19 data for MSA: https://www.ncbi.nlm.nih.gov/labs/virus/vssi/#/virus?SeqType_s=Nucleotide&VirusLineage_ss=SARS-CoV-2,%20taxid:2697049
RUN curl --retry 5 --verbose -L 'https://www.ncbi.nlm.nih.gov/genomes/VirusVariation/vvsearch2/?q=*:*&fq=%7B!tag=SeqType_s%7DSeqType_s:(%22Nucleotide%22)&fq=VirusLineageId_ss:(2697049)&cmd=download&sort=SourceDB_s%20desc,CreateDate_dt%20desc&dlfmt=fasta&fl=id,Definition_s,Nucleotide_seq' > sequences.fa 

COPY Dockerfile /opt
COPY README /opt
