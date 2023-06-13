FROM ghcr.io/damyan/sak-base

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    build-essential golang-1.19-go golang-1.20-go make \
  && rm -rf /var/lib/apt/lists/*
