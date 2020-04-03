### Building the Docker Image for ClustalO
```bash
# See listing of images on computer
docker image ls

# Build from Dockerfile
docker build --tag=ccbr_clustalo:v0.0.1 .

# Peak around the container: verify things run correctly
docker run -ti ccbr_clustalo:v0.0.1 /bin/bash

# Updating tag(s) before pushing to DockerHub
docker tag ccbr_clustalo:v0.0.1 skchronicles/ccbr_clustalo:v0.0.1
docker tag ccbr_clustalo:v0.0.1 skchronicles/ccbr_clustalo         # latest
docker tag ccbr_clustalo:v0.0.1 nciccbr/ccbr_clustalo:v0.0.1
docker tag ccbr_clustalo:v0.0.1 nciccbr/ccbr_clustalo              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_clustalo:v0.0.1
docker push skchronicles/ccbr_clustalo:latest
docker push nciccbr/ccbr_clustalo:v0.0.1
docker push nciccbr/ccbr_clustalo:latest 
```
