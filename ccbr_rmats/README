# See listing of images on computer
docker image ls

# Build Dockerfile
docker build --tag=rmats:v0.0.1 .

# Testing
docker run -ti nciccbr/rmats:v0.0.1 /bin/bash

# Updating Tag  before pushing to DockerHub
docker tag rmats:v0.0.1 skchronicles/rmats:v0.0.1
docker tag rmats:v0.0.1 skchronicles/rmats         # latest
docker tag rmats:v0.0.1 nciccbr/rmats:v0.0.1
docker tag rmats:v0.0.1 nciccbr/rmats              # latest




# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/rmats:v0.0.1
docker push skchronicles/rmats:latest
docker push nciccbr/rmats:v0.0.1
docker push nciccbr/rmats:latest 
