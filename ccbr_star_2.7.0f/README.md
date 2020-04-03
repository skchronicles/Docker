# See listing of images on computer
docker image ls

# Build Dockerfile
docker build --tag=ccbr_star_2.7.0f:v0.0.1 .

# Testing
docker run -ti nciccbr/ccbr_star_2.7.0f:v0.0.1 /bin/bash

# Updating Tag  before pushing to DockerHub
docker tag ccbr_star_2.7.0f:v0.0.1 skchronicles/ccbr_star_2.7.0f:v0.0.1
docker tag ccbr_star_2.7.0f:v0.0.1 skchronicles/ccbr_star_2.7.0f         # latest
docker tag ccbr_star_2.7.0f:v0.0.1 nciccbr/ccbr_star_2.7.0f:v0.0.1
docker tag ccbr_star_2.7.0f:v0.0.1 nciccbr/ccbr_star_2.7.0f              # latest




# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_star_2.7.0f:v0.0.1
docker push skchronicles/ccbr_star_2.7.0f:latest
docker push nciccbr/ccbr_star_2.7.0f:v0.0.1
docker push nciccbr/ccbr_star_2.7.0f:latest 
