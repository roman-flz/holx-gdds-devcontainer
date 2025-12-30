# Base Image
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Avoid Prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install cert tooling first
RUN apt-get update && apt-get install -y \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

#Add ZSCALER cert
COPY .devcontainer/certs/zscaler-ca.crt /usr/local/share/ca-certificates/zscaler-ca.crt
RUN chmod 644 /usr/local/share/ca-certificates/zscaler-ca.crt && \
    update-ca-certificates

# Core tools
RUN apt-get update && apt-get install -y \
    curl \
    git \
    ca-certificates \
    build-essential \
    unzip \
    sudo \
    zsh \
    && rm -rf /var/lib/apt/lists/*

# Node (LTS)
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
    && rm -rf /var/lib/apt/lists/*

# Optional: Bun
USER vscode

RUN curl -fsSL https://bun.sh/install | bash

# Set PATH for Bun
ENV PATH="/home/vscode/.bun/bin:$PATH"

# Default shell
SHELL ["/bin/zsh", "-c"]