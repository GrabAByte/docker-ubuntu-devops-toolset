FROM grababyte/ubuntu-base:0.8.0

LABEL devops.grababyte.image.authors="GrabAByte"

ENV ARCH=amd64
ENV CONTAINERD_VERSION=1.7.27-1
ENV K8S_VERSION=1:519.0.0-0
ENV HELM_VERSION=3.17.2-1
ENV PACKER_VERSION=1.12.0-1
ENV TERRAFORM_VERSION=1.11.4-1
ENV USER=ubuntu24

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN \
  curl https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor | tee /usr/share/keyrings/docker.gpg > /dev/null && \
  curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor | tee /usr/share/keyrings/google-cloud.gpg > /dev/null && \
  curl https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null  && \
  curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | tee /usr/share/keyrings/helm.gpg > /dev/null && \
  echo "deb [arch=${ARCH} signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu plucky stable" > /etc/apt/sources.list.d/docker-ce.list && \
  echo "deb [signed-by=/usr/share/keyrings/google-cloud.gpg] https://packages.cloud.google.com/apt cloud-sdk main" > /etc/apt/sources.list.d/gcloud.list && \
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | tee /etc/apt/sources.list.d/helm-stable-debian.list && \
  gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint && \
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com focal main" >/etc/apt/sources.list.d/hasicorp.list && \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    containerd.io="${CONTAINERD_VERSION}" \
    kubectl="${K8S_VERSION}" \
    helm="${HELM_VERSION}" \
    packer="${PACKER_VERSION}" \
    terraform="${TERRAFORM_VERSION}" && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

USER "${USER}"
