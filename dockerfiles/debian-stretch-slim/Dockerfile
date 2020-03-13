# AZP Release Agent variant
# Official Debian minimal image
ARG  BASE_IMAGE_VERSION
FROM debian:${BASE_IMAGE_VERSION}

# Build arguments
ARG ANSIBLE_VERSION
ARG VCS_URL
ARG VCS_REF
# ARG BUILD_DATE
ARG IMAGE_LONG_VERSION

# Environment variables
ENV DEBIAN_FRONTEND=noninteractive

COPY ./start.sh /azp/start.sh

RUN set -x && \
    \
    env && \
    echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes && \
    apt-get update && \
    apt-get install -y \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
        libcurl3 \
        libicu57 \
        libunwind8 \
        netcat \
        ssh \
        openssl && \
   rm -rf /var/lib/apt/lists/* && \
   chmod +x start.sh

WORKDIR /azp

CMD ["./start.sh"]

# Labels
# http://label-schema.org/rc1/ namespace labels
LABEL maintainer="Ryan Craig"

LABEL org.label-schema.schema-version="1.0"
#LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.name="devtestlabs/azp-agent"
LABEL org.label-schema.description="Azure Pipeline Agent"
#LABEL org.label-schema.url=$ORG_WEB_URL
LABEL org.label-schema.vcs-url=$VCS_URL
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vendor="devtestlabs.xyz"
LABEL org.label-schema.version=$IMAGE_LONG_VERSION
LABEL org.label-schema.docker.cmd='docker run -e AZP_URL="https://dev.azure.com/{{ ORGANIZATION }}/" -e AZP_TOKEN="{{ AZP_TOKEN }}" -e AZP_AGENT_NAME="{{ AZP_AGENT_NAME }}" -e AZP_POOL="{{ AZP_POOL_NAME }}" azp-agent:{{ IMAGE_VERSION }}'
