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

# Allow any user on the local system to connect to any database with
# any database user name using Unix-domain sockets (the default for local
# connections).
#
# TYPE  DATABASE        USER            ADDRESS                 METHOD
RUN echo "local   all             all                                     trust" > $PGDATA/pg_hba.conf \

# The same using local loopback TCP/IP connections.
#
# TYPE  DATABASE        USER            ADDRESS                 METHOD
    && echo "host    all             all             127.0.0.1/32            trust" >> $PGDATA/pg_hba.conf \

# The same as the previous line, but using a separate netmask column
#
# TYPE  DATABASE        USER            IP-ADDRESS      IP-MASK             METHOD
    && echo "host    all             all             127.0.0.1       255.255.255.255     trust" >> $PGDATA/pg_hba.conf \

# The same over IPv6.
#
# TYPE  DATABASE        USER            ADDRESS                 METHOD
    && echo "host    all             all             ::1/128                 trust" >> $PGDATA/pg_hba.conf \

# The same using a host name (would typically cover both IPv4 and IPv6).
#
# TYPE  DATABASE        USER            ADDRESS                 METHOD
    && echo "host    all             all             localhost               trust" >> $PGDATA/pg_hba.conf

RUN mv /workspace/*/.devcontainer/pg_hba.conf $PGDATA/