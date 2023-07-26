# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.245.0/containers/ubuntu/.devcontainer/base.Dockerfile

# [Choice] Ubuntu version (use ubuntu-22.04 or ubuntu-18.04 on local arm64/Apple Silicon): ubuntu-22.04, ubuntu-20.04, ubuntu-18.04
ARG VARIANT="jammy"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-${VARIANT}

LABEL maintainer="Khanh Nguyen <khanhnv.uit@gmail.com>"

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  apt-utils \
  software-properties-common \
  build-essential \
  jq \
  git \
  vim \
  python3 \
  python3-dev \
  python3-pip && \
  rm -rf /var/lib/apt/lists/*

RUN add-apt-repository universe \
  && add-apt-repository multiverse \
  && apt update

RUN pip3 install --upgrade \
  setuptools \
  pip

ADD requirements.txt /requirements.txt

RUN pip3 install --upgrade -r /requirements.txt

RUN apt-get install sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
  && chmod 0440 /etc/sudoers.d/$USERNAME \
  #
  # Clean up
  && apt-get autoremove \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*