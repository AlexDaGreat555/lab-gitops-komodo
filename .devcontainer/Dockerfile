FROM docker.io/library/docker:29.0.2-cli@sha256:4715cbd5a462b91d956ee9f9fc06d3f111e9c9e0a204f5ae712b928c4c7fba73 AS docker_cli

FROM mcr.microsoft.com/devcontainers/base:1-bookworm@sha256:ce2e9e611939e611b737362c045bb6d3449bb3efb84898525d724aace1737b90

USER root

# Copy the pinned Docker 29.0.2 client and Compose 2.40.3 plugin. The
# docker-outside-of-docker feature only supplies access to the host socket.
COPY --from=docker_cli /usr/local/bin/docker /usr/local/bin/docker
COPY --from=docker_cli /usr/local/libexec/docker/cli-plugins/docker-compose /usr/local/libexec/docker/cli-plugins/docker-compose

RUN apt-get update \
    && apt-get install --yes --no-install-recommends python3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER vscode

