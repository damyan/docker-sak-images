FROM ghcr.io/damyan/sak-base

USER root

RUN apt-get update \
  && apt-get install -y --no-install-recommends --ignore-missing \
    build-essential delve gdb golang-1.23-go golang-1.24-go make python3 python3-pip \
  && rm -rf /var/lib/apt/lists/*

WORKDIR "/home/damyan"

USER damyan
