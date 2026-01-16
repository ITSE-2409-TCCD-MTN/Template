FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Set up environment variables
ENV PGDATA=/var/lib/postgresql/data
ENV PGHOST=localhost
ENV PGUSER=postgres

# Install PostgreSQL
RUN apt-get update && apt-get upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends postgresql postgresql-contrib \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Configure the database
RUN mkdir -p $PGDATA \
    && chown -R postgres:postgres $PGDATA \
    && chmod 750 $PGDATA

RUN mv /workspace/*/.devcontainer/pg_hba.conf $PGDATA/