FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Set up environment variables
ENV PGDATA=/var/lib/postgresql/data
ENV PGHOST=localhost
ENV PGUSER=postgres

# Install PostgreSQL
RUN apt-get update && apt-get upgrade -y \
    && export DEBIAN_FRONTEND=noninteractive

RUN apt-get -y install --no-install-recommends postgresql postgresql-contrib \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/lib/postgresql/data

COPY <<EOF /etc/postgresql/16/main/postgresql.conf
listen_addresses = '*'
data_directory = '/var/lib/postgresql/data'
EOF

COPY <<EOF /etc/postgresql/16/main/pg_hba.conf
local   all all trust
host    all all 127.0.0.1/32    trust
host    all all localhost   trust
EOF

RUN <<EOT
chown -R postgres:postgres "${PGDATA}"
chmod 0750 $PGDATA
chown -R postgres:postgres /etc/postgresql/16/main
sudo -H -u postgres sh -c "/usr/lib/postgresql/16/bin/initdb -D ${PGDATA} --auth trust --auth-local trust --auth-host trust"
sudo -H -u postgres sh -c "/usr/lib/postgresql/16/bin/pg_ctl -D /var/lib/postgresql/data start"
EOT

# RUN sudo cat /etc/postgresql/16/main/pg_hba.conf
# RUN pg_isready

# RUN <<EOT
# su postgres
# /usr/lib/postgresql/16/bin/pg_ctl -D /var/lib/postgresql/data -l logfile start
# EOT