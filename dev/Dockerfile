FROM ghcr.io/damyan/sak-base

USER root

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    build-essential delve gdb golang-1.20-go golang-1.21-go make python3 python3-pip \
  && rm -rf /var/lib/apt/lists/*

WORKDIR "/home/damyan"

USER damyan
