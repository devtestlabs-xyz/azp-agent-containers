# Azure Pipeline Agent Container
![](https://github.com/devtestlabs-xyz/azp-agent-containers/workflows/Build%20and%20publish%20AZP%20Agent%20Debian%20Stretch-Slim%20image/badge.svg)

The Microsoft Azure Pipelines (AZP) self-hosted agent can be run directly on a Windows host, Linux host, and inside a Docker container. Containerizing the AZP self-hosted agent allows for efficient horizontal scaling of AZP build and deployment processes. Moreover, containerization enforces immutable configuration, mitigating configuration drift. The primary goal of this project is to maintain a streamlined OCI compliant image.

# Linux Base Image
The official [Debian Linux image](https://hub.docker.com/_/debian) is used as the base Docker image for each AZP Agent Docker image.  The specific image variant used is `debian:stretch-slim`. For more detailed information see https://hub.docker.com/_/debian.

# Best Practices
A number of industry, community, and vendor best practices are injected into each Docker image definition. Read the following documentation to learn more about just a few well-documented best practices:

* [Label Schema](http://label-schema.org/rc1/) provides a recommended community-owned namespace for container labels that align with Docker and Project Atomic guidelines.
* [Docker Best Practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
* [Docker standards and compliance](https://docs.docker.com/compliance/)

# Getting Started
## Build Docker Image
On your development workstation or Linux Docker host, in `terminal` execute:

1. `cd` to path where the target Dockerfile lives
1. `docker build -t azp-agent:{{ TAG }} .` For example, execute `docker build -t azp-agent:local .`.

## Pulling the publicly available image on Dockerhub
If you don't want to build the image locally you may pull the image from Dockerhub instead.

```
docker pull devtestlabs/azp-agent:debian-stretch-slim
```

## Run Docker Image
On your development workstation or Linux Docker host, in `terminal` execute:
```
docker run \
  -e AZP_URL="https://dev.azure.com/{{ ORGANIZATION }}" 
  -e AZP_TOKEN="{{ AZP_TOKEN }}" 
  -e AZP_AGENT_NAME="{{ AZP_AGENT_NAME }}" 
  -e AZP_POOL="{{ AZP_POOL_NAME }}" 
  azp-agent:{{ TAG }}`
```
*example docker run*
```
docker run \
  -e AZP_URL="https://dev.azure.com/example-com" 
  -e AZP_TOKEN="123423fdfsfasdfsadfg23" 
  -e AZP_AGENT_NAME="my-local-vagrant-vnet" 
  -e AZP_POOL="devtest" azp-agent:local
```
See https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#start-the-image-1 for further details.

## Bind mount SSH key(s)
If you need to use the SSH client in the AZP Agent container you probably want to bind mount a path to one or more RSA keys. To accomplish this you need to use Docker bind mounts `--mount type=bind,source=/some/path/on/host/,target=/some/path/in/container/`

For example, if you want to bind mount a single RSA private key file on the host `$HOME/.ssh/vagrant_insecure_rsa` to the container path `azp/.ssh/vagrant_insecure_rsa` you would run the docker container as follows.

*example*
```
docker run \
-e AZP_URL="https://dev.azure.com/example-com" \
-e AZP_TOKEN="123423fdfsfasdfsadfg23" \
-e AZP_AGENT_NAME="my-local-vagrant-vnet" \
-e AZP_POOL="devtest" \
--mount type=bind,source="$(home)"/.ssh/vagrant_insecure_rsa,target=azp/.ssh/vagrant_insecure_rsa \ 
azure-pipeline-agent:local
```

*NOTE: Docker bind mounts can and should be used to mount any path or file you may need to use within the container but do not wish to copy into the Docker image due to security concerns. You can use more than one `--mount` switch within a `docker run` command.*

See https://docs.docker.com/storage/bind-mounts/ for further details.


# Contribute
Submit a PR. If it makes sense, I'll merge it. Or submit a Github issue to discuss what you want to do.

# Dockerhub Repository
https://hub.docker.com/repository/docker/devtestlabs/azp-agent

# External references

* https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#linux
* https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#start-the-image-1
* https://docs.docker.com/storage/bind-mounts/
* http://label-schema.org/rc1/
* https://hub.docker.com/repository/docker/devtestlabs/azp-agent

