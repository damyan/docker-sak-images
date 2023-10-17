FROM ghcr.io/damyan/sak-base

USER root

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    build-essential golang-1.19-go golang-1.20-go golang-1.21-go make \
  && rm -rf /var/lib/apt/lists/*

WORKDIR "/home/damyan"

USER damyan
