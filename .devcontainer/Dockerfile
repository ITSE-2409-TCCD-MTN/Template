FROM mcr.microsoft.com/devcontainers/base:ubuntu

RUN <<EOT
sudo apt-get update && apt-get upgrade -y
sudo apt-get -y install --no-install-recommends postgresql postgresql-contrib
sudo apt-get clean -y && rm -rf /var/lib/apt/lists/*
EOT
