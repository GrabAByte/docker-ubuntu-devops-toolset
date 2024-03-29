FROM grababyte/ubuntu-base:0.5.2

LABEL devops.grababyte.image.authors="GrabAByte"

ENV ARCH amd64
ENV ANSIBLE_VERSION 2.14.2
ENV CONTAINERD_VERSION 1.6.18-1
ENV ISTIO_VERSION 1.17.0
ENV K8S_VERSION 1.26.1-00
ENV PACKER_VERSION 1.8.6-1
ENV TERRAFORM_VERSION 1.3.9
ENV USER ubuntu23
ENV PATH "${PATH}:/istio-${ISTIO_VERSION}/bin"

USER root

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN \
  curl -s https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
  curl -s https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
  echo "deb [arch=${ARCH}] https://download.docker.com/linux/ubuntu focal stable" > /etc/apt/sources.list.d/docker-ce.list && \
  echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" > /etc/apt/sources.list.d/gcloud.list && \
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com focal main" >/etc/apt/sources.list.d/hasicorp.list && \
  gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint && \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    containerd.io=${CONTAINERD_VERSION} \
    kubectl=${K8S_VERSION} \
    packer=${PACKER_VERSION} \
    terraform=${TERRAFORM_VERSION} \
    yq=3.1.0-3 && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  curl -L https://istio.io/downloadIstio | ISTIO_VERSION=${ISTIO_VERSION} TARGET_ARCH=${ARCH} sh -

USER "${USER}"

RUN  \
    pip3 install --no-cache-dir --upgrade \
      ansible-core==${ANSIBLE_VERSION} \
      awscliv2==2.2.0 \
      azure-cli==2.45.0 \
      yamllint==1.29.0
