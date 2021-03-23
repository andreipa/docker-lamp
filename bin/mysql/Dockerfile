FROM mysql:8.0

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Additional utilities
RUN apt-get update && apt-get install -y \
    nano \
    vim \
 && rm -rf /var/lib/apt/lists/*

#Init db schema
#COPY ./init.sql /docker-entrypoint-initdb.d/