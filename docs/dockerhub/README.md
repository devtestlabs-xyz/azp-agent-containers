# Supported tags and respective Dockerfile links
Tags are grouped by image variant.

All images are tagged using the following convention:
* {{ BASE_IMAGE }}-{{ BASE_IMAGE_VERSION }}-{{ CALVER }}


If you want to guarantee consistency through space and time use the long image tag!

*NOTE: Tag specifications are linked to the image variant path within the [Github: devtestlabs-xyz/azp-agent-containers project](https://github.com/devtestlabs-xyz/azp-agent-containers)*

## Debian Stretch Slim
* [debian-stretch-slim-20200313.1]((https://github.com/devtestlabs-xyz/azp-agent-containers/tree/master/dockerfiles/debian-stretch-slim))


## Debian Buster Slim
...TODO...

# How to use this image

Read https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#start-the-image-1

*docker run example*
```
docker run \
  -e AZP_URL="https://dev.azure.com/{{ ORGANIZATION }}/" 
  -e AZP_TOKEN="{{ AZP_TOKEN }}" 
  -e AZP_AGENT_NAME="{{ AZP_AGENT_NAME }}" 
  -e AZP_POOL="{{ AZP_POOL_NAME }}" 
  azp:{{ IMAGE_VERSION }}
```

*podman run example*
```
podman run \
  -e AZP_URL="https://dev.azure.com/{{ ORGANIZATION }}/" 
  -e AZP_TOKEN="{{ AZP_TOKEN }}" 
  -e AZP_AGENT_NAME="{{ AZP_AGENT_NAME }}" 
  -e AZP_POOL="{{ AZP_POOL_NAME }}" 
  azp:{{ IMAGE_VERSION }}
```

*NOTE: Replace `{{ ... }}` with actual value or better yet, use a secured `.env` file or host environment variables for improved security.*

# Image variants
The DevTestLabs/azp-agent image is a lighter weight [Azure Pipelin Agent](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-linux?view=azure-devops) [OCI compliant](https://www.opencontainers.org/) container image that run on [Docker](https://www.docker.com/), [Podman](https://podman.io/), and [Kubernetes](https://kubernetes.io/). 

All images variants managed by this project have the following commonalities:

* The official [Debian Linux image](https://hub.docker.com/_/debian) is employed as the base image

* Run as Docker containers, Podman containers, and in K8s


# GitHub Project
https://github.com/devtestlabs-xyz/azp-agent-containers

