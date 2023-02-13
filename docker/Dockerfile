FROM docker.io/ubuntu:23.04

LABEL devops.grababyte.image.authors="GrabAByte"

ENV USER ubuntu

RUN \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    curl=7.87.0-1ubuntu1 \
    gcc=4:12.2.0-1ubuntu1 \
    git=1:2.38.1-1ubuntu2 \
    jq=1.6-2.1ubuntu3 \
    openssh-server=1:9.0p1-1ubuntu8 \
    python3-dev=3.11.1-3 \
    python3-setuptools=65.5.0-1 \
    python3-pip=22.3.1+dfsg-2 \
    python3-yaml=6.0-3 \
    sshpass=1.09-1 \
    sudo=1.9.11p3-1ubuntu3 \
    tar=1.34+dfsg-1.1 \
    unzip=6.0-27ubuntu1 \
    zip=3.0-12build2 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  echo "${USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER ubuntu
