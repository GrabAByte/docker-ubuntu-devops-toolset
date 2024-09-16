FROM grababyte/ubuntu-base:0.7.2

LABEL devops.grababyte.image.authors="GrabAByte"

ENV ARCH amd64
ENV ANSIBLE_VERSION 2.16.11-1ppa~noble
ENV CONTAINERD_VERSION 1.7.22-1
ENV K8S_VERSION 1:492.0.0-0
ENV HELM_VERSION 3.15.4-1
ENV PACKER_VERSION 1.11.2-1
ENV TERRAFORM_VERSION 1.9.5-1
ENV USER ubuntu24

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN \
  curl -s https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
  curl -s https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
  curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | tee /usr/share/keyrings/helm.gpg > /dev/null && \
  echo "deb [arch=${ARCH}] https://download.docker.com/linux/ubuntu focal stable" > /etc/apt/sources.list.d/docker-ce.list && \
  echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" > /etc/apt/sources.list.d/gcloud.list && \
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | tee /etc/apt/sources.list.d/helm-stable-debian.list && \
  gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint && \
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com focal main" >/etc/apt/sources.list.d/hasicorp.list && \
  apt-add-repository ppa:ansible/ansible && \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    ansible-core="${ANSIBLE_VERSION}" \
    containerd.io="${CONTAINERD_VERSION}" \
    kubectl="${K8S_VERSION}" \
    helm="${HELM_VERSION}" \
    packer="${PACKER_VERSION}" \
    terraform="${TERRAFORM_VERSION}" \
    yq=3.1.0-3 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

USER "${USER}"
