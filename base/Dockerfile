FROM mikefarah/yq AS yq
FROM debian:unstable-slim

LABEL maintainer="damyan+dev@0x4711.org"

ARG USERNAME=damyan
ARG USER_UID=1000
ARG USER_GID=$USER_UID


# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get update \
  && apt-get install -y --no-install-recommends sudo \
  && rm -rf /var/lib/apt/lists/* \
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

# set keys
RUN mkdir -p ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts

# set timezone
ENV TZ=Europe/Berlin

# install starship
RUN curl -sS https://starship.rs/install.sh > install.sh \
  && sh install.sh -y

# fix ping
RUN setcap cap_net_raw+p /usr/bin/ping

# install yq
COPY --from=yq /usr/bin/yq /usr/local/bin/yq
RUN chmod a+x /usr/local/bin/yq

# install dot tools
WORKDIR "/home/damyan"
USER damyan
RUN git clone https://github.com/damyan/dotfiles.git .dotfiles \
  && cd .dotfiles \
  && ./install_dot_files.sh
