### Building the Docker Image for PCGR and CPSR
```bash
# See listing of images on computer
docker image ls

# Build from Dockerfile
docker build --tag=ccbr_cpsr:v0.0.1 .

# Peak around the container: verify things run correctly
docker run -ti ccbr_cpsr:v0.0.1 /bin/bash

# Updating Tag  before pushing to DockerHub
docker tag ccbr_cpsr:v0.0.1 skchronicles/ccbr_cpsr:v0.0.1
docker tag ccbr_cpsr:v0.0.1 skchronicles/ccbr_cpsr         # latest
docker tag ccbr_cpsr:v0.0.1 nciccbr/ccbr_cpsr:v0.0.1
docker tag ccbr_cpsr:v0.0.1 nciccbr/ccbr_cpsr              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_cpsr:v0.0.1
docker push skchronicles/ccbr_cpsr:latest
docker push nciccbr/ccbr_cpsr:v0.0.1
docker push nciccbr/ccbr_cpsr:latest 
```

### Download reference files for PCGR
```bash
# Create a python virtual env to install `gdown` and then download reference files for GRCh37 and GRCh38
python3.5 -m venv vENV
source vENV/bin/activate

pip install --upgrade pip
pip install gdown

# Getting Resource files to run CPSR and PCGR

# Option 1) Download as tar ball
gdown https://drive.google.com/uc?id=1vIESS8NxiITUnrqZoWOdNk1YsklH8f1C -O pcgr_databundle_grch37.tar.gz # 15GB
gdown https://drive.google.com/uc?id=1eoMgc2AzK1w1jrX2LSLEas4YJPiQJx1B -O pcgr_databundle_grch38.tar.gz # 16GB

# Option 2) Download and extract
gdown https://drive.google.com/uc?id=1vIESS8NxiITUnrqZoWOdNk1YsklH8f1C -O - | tar xvzf - # grch37
gdown https://drive.google.com/uc?id=1eoMgc2AzK1w1jrX2LSLEas4YJPiQJx1B -O - | tar xvzf - # grch38

deactivate
```
