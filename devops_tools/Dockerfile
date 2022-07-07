FROM rockylinux:8.5

## update the container and install epel-release
RUN dnf clean all
RUN dnf update -y
RUN dnf install -y epel-release

## install core cli utils
RUN dnf install -y git unzip tree sudo awscli wget ansible

## enable passwordless sudo for different users in the container
RUN echo "ALL            ALL = (ALL) NOPASSWD: ALL" >> /etc/sudoers

## create the non-root user and configure to use the correct directory 
RUN useradd -ms /bin/bash docker-user && usermod -aG wheel docker-user
USER docker-user
WORKDIR /home/docker-user

## install rbenv to manage ruby version for development
RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc

## install tfenv terraform tool
RUN git clone https://github.com/tfutils/tfenv.git ~/.tfenv
RUN echo 'export PATH="$HOME/.tfenv/bin:$PATH"' >> ~/.bashrc

## install pyenv to manage python version
RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
RUN echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(pyenv init -)"' >> ~/.bashrc

