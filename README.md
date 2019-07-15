# Docker

A collection of commonly used bioinformatics tools used for analyzing RNA-seq, ChIP-seq, and DNA-seq data.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

What things you need to install the software and how to install them:
- `docker`:  https://docs.docker.com/install/  
- `git`:     https://git-scm.com/book/en/v2/Getting-Started-Installing-Git  

If you are unsure if you have `git` or `docker` installed, please type `which docker` or `which git`.

### Installation

A step by step series of examples that tell you how to get a development environment up and running

Let's start off by cloning this repository
```
$ git clone https://github.com/skchronicles/Docker.git
$ cd Docker
```

Let's take a peak
```
$ tree .
.
├── ccbr_meme_suite
│   ├── Dockerfile
│   ├── README
│   └── meme-5.0.4.tar.gz
├── ccbr_python
│   ├── Dockerfile
│   └── README
└── ccbr_rsem_merge
    ├── Dockerfile
    └── README

```

Each of the listed `ccbr` directories represents a _dockerized_ tool.  
Within each directory you will find a `REAME` and a `dockerfile`. The `README` contains instructions for how to `build`, `tag`, and `push` the docker images.

## README: ccbr_meme_suite
```
# See listing of images on computer
docker image ls

# Build Dockerfile (assumes you are in the directory with the Dockerfile)
docker build --tag=ccbr_meme_suite:v0.0.1 .

# Peak around the container: verify things run correctly (similiar to `singularity shell`)
docker run -ti ccbr_meme_suite:v0.0.1 /bin/bash
echo $PATH
ls -larth /data/
ls -larth /opt/
# Check out what ever you want
exit

# Updating Tag(s) before pushing to DockerHub: create a version tag and `latest` tag 
## Creating Tags for `skchronicles` account 
docker tag ccbr_meme_suite:v0.0.1 skchronicles/ccbr_meme_suite:v0.0.1
docker tag ccbr_meme_suite:v0.0.1 skchronicles/ccbr_meme_suite         # latest
## Creating Tags for `nciccbr` account
docker tag ccbr_meme_suite:v0.0.1 nciccbr/ccbr_meme_suite:v0.0.1
docker tag ccbr_meme_suite:v0.0.1 nciccbr/ccbr_meme_suite              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_meme_suite:v0.0.1
docker push skchronicles/ccbr_meme_suite:latest
docker push nciccbr/ccbr_meme_suite:v0.0.1
docker push nciccbr/ccbr_meme_suite:latest 

# To pull the image we created using docker:
docker pull nciccbr/ccbr_meme_suite

# To pull the image we created using singularity:
singularity pull docker://nciccbr/ccbr_meme_suite

````

## Versioning

We use `git`, `GitHub`, and `DockerHub` for versioning. For the versions available on GitHub, please see the [tags on this repository](https://github.com/skchronicles/Docker/tags).
For more information about available container images, please visit: 
- https://hub.docker.com/u/skchronicles     
- https://hub.docker.com/u/nciccbr   

<hr>

<p align="center">
	<a href="#Docker">Back to Top</a>
</p>




