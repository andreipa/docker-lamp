FROM mysql:8

# Update and upgrade the system
RUN apt-get update && apt-get upgrade -y --no-install-recommends apt-utils

# Additional utilities
RUN apt-get update && apt-get install -y \
    nano \
    vim \
 && rm -rf /var/lib/apt/lists/*

# Cleanup
RUN rm -rf /usr/src/*

# Init db schema
# You can setup a db entry point by default if you want
#COPY ./init.sql /docker-entrypoint-initdb.d/