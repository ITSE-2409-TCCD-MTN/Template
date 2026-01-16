FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN apt-get update && apt-get upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql postgresql-contrib \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN chown -R postgres:postgres /var/lib/postgresql
