# Use the official Ubuntu 22.04 image as a base
FROM ubuntu:22.04 AS ubuntu-base

ARG TARGETARCH

ARG NODE_TAG
ENV NODE_TAG ${NODE_TAG:-21.x}
ARG DENO_TAG
ENV DENO_TAG ${DENO_TAG:-v1.40.0}

ARG USER
ENV USER ${USER:-user}
ARG PUID
ENV PUID ${PUID:-1000}
ARG PGID
ENV PGID ${PGID:-1000}
ENV HOME /home/${USER}

# suppress interactive prompts during package installation.  
ENV DEBIAN_FRONTEND=noninteractive

# set work directory
WORKDIR /src/app

# Timezone
ENV TZ="Asia/Bangkok"
RUN apt clean 
RUN apt update && apt upgrade -y
# Set timezone
RUN apt install -y tzdata
RUN ln -snf /usr/share/zoneinfo/$CONTAINER_TIMEZONE /etc/localtime && echo $CONTAINER_TIMEZONE > /etc/timezone

# Set locales
# https://leimao.github.io/blog/Docker-Locale/
RUN apt-get install -y locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LC_ALL en_US.UTF-8 
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  

# Update the package lists
RUN apt update && apt upgrade -y

# Install additional packages (replace with your desired packages)
RUN apt install -y nginx
# vim openssh-server openssh-client \
# apache2 \
# postgresql postgresql-contrib

# Copy your application files (if any)
COPY . /app

# Set the working directory
WORKDIR /app

# Define the command to run when the container starts
CMD ["nginx", "-g", "daemon off;"]