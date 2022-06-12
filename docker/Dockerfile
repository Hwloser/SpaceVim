FROM debian:stable

MAINTAINER Hwloser <hwloser@163.com>

# ENV http_proxy=http://192.168.2.106:7890
# ENV https_proxy=http://192.168.2.106:7890

RUN apt-get update && \
    apt-get install -y \
    neovim \
    curl \
    python3 \
    python3-pip \
    lua5.3 \
    git \
    exuberant-ctags \
    silversearcher-ag && \
    apt-get clean

ENV HOME /home/spacevim

RUN groupdel users                                              \
  && groupadd -r spacevim                                       \
  && useradd --create-home --home-dir $HOME                     \
             -r -g spacevim                                     \
             spacevim

USER spacevim

WORKDIR $HOME

ENV PYTHON3_HOST_PROG "/usr/bin/python3"

RUN mkdir -p $HOME/.config $HOME/.SpaceVim.d

RUN pip install --user pynvim

RUN curl https://raw.githubusercontent.com/Hwloser/SpaceVim/master/docker/init.toml > $HOME/.SpaceVim.d/init.toml

RUN curl -sLf https://raw.githubusercontent.com/Hwloser/SpaceVim/master/docs/install.sh | bash

RUN nvim --headless +'call dein#install#_update([], "install", v:false)' +qall

RUN rm $HOME/.SpaceVim.d/init.toml

# ENTRYPOINT nvim
