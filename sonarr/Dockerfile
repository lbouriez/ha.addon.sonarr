ARG BUILD_FROM=ghcr.io/linuxserver/sonarr:amd64-0.6.1397

# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Environment variables
ENV \
    LANG="C.UTF-8" \
    S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \
    S6_CMD_WAIT_FOR_SERVICES=1

# Copy root filesystem
COPY rootfs /

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base system
RUN \
    set -o pipefail \
    \
    && curl -J -L -o /tmp/bashio.tar.gz \
        "https://github.com/hassio-addons/bashio/archive/v0.13.0.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf \
        /tmp/bashio.tar.gz \
        --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -s /usr/lib/bashio/bashio /usr/bin/bashio \
    && chmod -R 555 /usr/lib/bashio \
    \
    && rm -f -r \
        /tmp/*