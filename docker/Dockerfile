FROM docker.io/ubuntu:23.04

LABEL devops.grababyte.image.authors="GrabAByte"

ARG USER=ubuntu23
ENV ID=1001

RUN \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    curl=7.87.0-1ubuntu1 \
    gcc=4:12.2.0-1ubuntu1 \
    git=1:2.38.1-1ubuntu2 \
    jq=1.6-2.1ubuntu3 \
    nodejs=18.13.0+dfsg1-1ubuntu1 \
    npm=9.2.0~ds1-1 \
    openssh-server=1:9.0p1-1ubuntu8 \
    python3-dev=3.11.1-3 \
    python3-setuptools=65.5.0-1 \
    python3-pip=22.3.1+dfsg-2 \
    python3-yaml=6.0-3 \
    ruby=1:3.0+3.1ubuntu1 \
    sshpass=1.09-1 \
    sudo=1.9.11p3-1ubuntu3 \
    tar=1.34+dfsg-1.1 \
    unzip=6.0-27ubuntu1 \
    zip=3.0-12build2 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  pip3 install --no-cache-dir --upgrade \
    pip==23.0.1 \
    setuptools==67.3.3 && \
  groupadd -g "${ID}" "${USER}" && \
  useradd -l -m -u "${ID}" -g "${USER}" "${USER}" && \
  echo "${USER} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER "${USER}"
