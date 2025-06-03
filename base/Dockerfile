FROM mikefarah/yq as yq
FROM debian:unstable-slim

LABEL maintainer="damyan+dev@0x4711.org"

ARG USERNAME=damyan
ARG USER_UID=1000
ARG USER_GID=$USER_UID


# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get install -y sudo \
  && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME


# needed for tzdata
ARG DEBIAN_FRONEND=noninteractive

RUN apt-get update \
  && apt-get install -y --no-install-recommends --ignore-missing \
    apt-transport-https bash-completion ca-certificates curl \
    debian-keyring debian-archive-keyring git gnupg htop iputils-ping iproute2 jq less \
    linux-sysctl-defaults ncdu net-tools openssh-client socat strace telnet tcpdump tzdata tmux vim wget \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts

ENV TZ=Europe/Berlin

RUN curl -sS https://starship.rs/install.sh > install.sh
RUN sh install.sh -y

# install dot tools
WORKDIR "/home/damyan"

USER damyan

RUN git clone https://github.com/damyan/dotfiles.git .dotfiles && cd .dotfiles && ./install_dot_files.sh

# install yq
WORKDIR "/root"

USER root

RUN setcap cap_net_raw+p /usr/bin/ping

COPY --from=yq /usr/bin/yq /usr/local/bin/yq

RUN chmod a+x /usr/local/bin/yq
