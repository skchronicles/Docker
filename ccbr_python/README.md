### Build from Dockerfile
```bash
# See listing of images on computer
docker image ls

# Build
docker build --tag=ccbr_python:v0.0.1 .

# Updating tag(s) before pushing to DockerHub
docker tag ccbr_python:v0.0.1 skchronicles/ccbr_python:v0.0.1
docker tag ccbr_python:v0.0.1 skchronicles/ccbr_python        # latest
docker tag ccbr_python:v0.0.1 nciccbr/ccbr_python:v0.0.1
docker tag ccbr_python:v0.0.1 nciccbr/ccbr_python             # latest

# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_python:v0.0.1
docker push skchronicles/ccbr_python:latest
docker push nciccbr/ccbr_python:v0.0.1
docker push nciccbr/ccbr_python:latest
```
