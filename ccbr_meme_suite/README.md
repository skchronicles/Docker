### Building Docker Image for MEME Suite 
```bash
# See listing of images on computer
docker image ls

# Build from Dockerfile
docker build --tag=ccbr_meme_suite:v0.0.1 .

# Peak around the container: verify things run correctly
docker run -ti ccbr_meme_suite:v0.0.1 /bin/bash

# Updating tag(s) before pushing to DockerHub
docker tag ccbr_meme_suite:v0.0.1 skchronicles/ccbr_meme_suite:v0.0.1
docker tag ccbr_meme_suite:v0.0.1 skchronicles/ccbr_meme_suite         # latest
docker tag ccbr_meme_suite:v0.0.1 nciccbr/ccbr_meme_suite:v0.0.1
docker tag ccbr_meme_suite:v0.0.1 nciccbr/ccbr_meme_suite              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_meme_suite:v0.0.1
docker push skchronicles/ccbr_meme_suite:latest
docker push nciccbr/ccbr_meme_suite:v0.0.1
docker push nciccbr/ccbr_meme_suite:latest 
```
