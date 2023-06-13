FROM ghcr.io/damyan/sak-base

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    bind9-dnsutils mtr-tiny net-tools \
    psmisc procps iperf3 tshark \
  && rm -rf /var/lib/apt/lists/*

