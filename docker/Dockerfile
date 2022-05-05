FROM docker.io/ubuntu:22.04

LABEL devops.grababyte.image.authors="GrabAByte"

RUN \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    gcc=4:11.2.0-1ubuntu1 \
    curl=7.81.0-1ubuntu1.1 \
    git=1:2.34.1-1ubuntu1.2 \
    jq=1.6-2.1ubuntu3 \
    openssh-server=1:8.9p1-3 \
    python3-dev=3.10.4-0ubuntu2 \
    python3-setuptools=59.6.0-1.2 \
    python3-pip=22.0.2+dfsg-1 \
    python3-yaml=5.4.1-1ubuntu1 \
    sshpass=1.09-1 \
    sudo=1.9.9-1ubuntu2 \
    tar=1.34+dfsg-1build3 \
    unzip=6.0-26ubuntu3 \
    zip=3.0-12build2 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  pip3 install --no-cache-dir ansible==5.7.1 && \
  mkdir /etc/ansible && \
  printf "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts
