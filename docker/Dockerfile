FROM grababyte/ubuntu-base:0.5.0

LABEL devops.grababyte.image.authors="GrabAByte"

ENV ANSIBLE_VERSION 2.14.2
ENV CONTAINERD_VERSION 1.6.18-1
ENV ISTIO_VERSION 1.17.0
ENV K8S_VERSION 1.26.1-00
ENV PACKER_VERSION 1.8.6-1
ENV TERRAFORM_VERSION 1.3.9
ENV USER ubuntu23
ENV PATH "${PATH}:/istio-${ISTIO_VERSION}/bin"

USER root

RUN \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    gnupg=2.2.40-1ubuntu2 && \
  curl -s https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg -o /etc/apt/trusted.gpg.d/kubernetes-apt-key.gpg && \
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key --keyring /usr/share/keyrings/cloud.google.gpg add - && \
  curl -s https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
  echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" > /etc/apt/sources.list.d/docker-ce.list && \
  echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] http://packages.cloud.google.com/apt cloud-sdk main" > /etc/apt/sources.list.d/gcloud.list && \
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list && \
  echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com focal main" >/etc/apt/sources.list.d/hasicorp.list && \
  gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint && \
  apt-get update -y && \
  apt-get install --no-install-recommends -y \
    containerd.io=${CONTAINERD_VERSION} \
    kubectl=${K8S_VERSION} \
    packer=${PACKER_VERSION} \
    terraform=${TERRAFORM_VERSION} \
    yq=3.1.0-3 && \
  pip3 install --no-cache-dir --upgrade \
    ansible-core==${ANSIBLE_VERSION} \
    awscliv2==2.2.0 \
    azure-cli==2.45.0 \
    yamllint==1.29.0 && \
  curl -L https://istio.io/downloadIstio | ISTIO_VERSION=${ISTIO_VERSION} TARGET_ARCH=amd64 sh -

USER "${USER}"
