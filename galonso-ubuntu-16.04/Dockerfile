#docker build -t galonso/ubuntu:16.04 .

FROM       ubuntu:16.04
MAINTAINER Gabriel Alonso <gbr.alonso@gmail.com>

RUN apt-get upgrade
RUN apt-get update -qq -y
RUN apt-get update --fix-missing
RUN apt-get install -qq -y \
    sudo                   \
    git                    \
    curl                   \
    build-essential        \
    autoconf               \
    man                    \
    libreadline-dev        \
    libssl-dev             \
    libxml2-dev            \
    libxslt-dev            \
    zlib1g-dev             \
    libbz2-dev             \
    wget                   \
    nano                   \
    supervisor             \
    vim

RUN useradd -m -s /bin/bash default
RUN chgrp -R default /usr/local
RUN find /usr/local -type d | xargs chmod g+w

RUN echo "default ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/default
RUN chmod 0440 /etc/sudoers.d/default

RUN echo "export TERM=xterm" >> /home/default/.bashrc

ENV     HOME /home/default
WORKDIR /home/default
USER    default
