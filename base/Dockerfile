FROM mikefarah/yq as yq
FROM debian:unstable-slim

LABEL maintainer="damyan+dev@0x4711.org"

# needed for tzdata
ARG DEBIAN_FRONEND=noninteractive

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    apt-transport-https ca-certificates bash-completion curl \
    debian-keyring debian-archive-keyring git gnupg iputils-ping iproute2 htop jq less \
    net-tools openssh-client strace tcpdump tzdata tmux vim wget \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts

ENV TZ=Europe/Berlin

RUN git clone https://github.com/damyan/dotfiles.git .dotfiles && cd .dotfiles && ./install_dot_files.sh

COPY --from=yq /usr/bin/yq /usr/local/bin/yq

RUN chmod a+x /usr/local/bin/yq
