### Building Docker Image for LibreOffice
```bash
# See listing of images on computer
docker image ls

# Build from Dockerfile
docker build --tag=libreoffice:v0.0.1 .

# Testing
docker run -ti nciccbr/libreoffice:v0.0.1 /bin/bash

# Updating tag(s) before pushing to DockerHub
docker tag libreoffice:v0.0.1 skchronicles/libreoffice:v0.0.1
docker tag libreoffice:v0.0.1 skchronicles/libreoffice         # latest
docker tag libreoffice:v0.0.1 nciccbr/libreoffice:v0.0.1
docker tag libreoffice:v0.0.1 nciccbr/libreoffice              # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/libreoffice:v0.0.1
docker push skchronicles/libreoffice:latest
docker push nciccbr/libreoffice:v0.0.1
docker push nciccbr/libreoffice:latest 
```
