# See listing of images on computer
docker image ls

# Build Dockerfile
docker build --tag=ccbr_rsem_merge:v0.0.1 .


# Updating Tag  before pushing to DockerHub
docker tag ccbr_rsem_merge:v0.0.1 skchronicles/ccbr_rsem_merge:v0.0.1
docker tag ccbr_rsem_merge:v0.0.1 skchronicles/ccbr_rsem_merge         # latest
docker tag ccbr_rsem_merge:v0.0.1 nciccbr/ccbr_rsem_merge:v0.0.1
docker tag ccbr_rsem_merge:v0.0.1 nciccbr/ccbr_rsem_merge              # latest




# Check out new tag(s)
docker image ls

# Push new tagged image to DockerHub
docker push skchronicles/ccbr_rsem_merge:v0.0.1
docker push skchronicles/ccbr_rsem_merge:latest
docker push nciccbr/ccbr_rsem_merge:v0.0.1
docker push nciccbr/ccbr_rsem_merge:latest 
