FROM rockylinux:8.5

## update the container and install core utils as root
RUN dnf update --no-cache -y

## add epel repo first
RUN dnf install -y epel-release
RUN dnf install -y git unzip tree sudo awscli wget

## enable passwordless sudo for different users in the container
RUN echo "ALL            ALL = (ALL) NOPASSWD: ALL" >> /etc/sudoers

## create the non-root user and configure to use the correct directory 
RUN useradd -ms /bin/bash docker-user
RUN usermod -aG docker-user wheel
USER docker-user
WORKDIR /home/docker-user

##install the appropriate tools to the container as docker-user
RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
RUN echo 'eval "$(rbenv init -)"' >> ~/.bash_profile

RUN git clone https://github.com/tfutils/tfenv.git ~/.tfenv
RUN echo 'export PATH="$HOME/.tfenv/bin:$PATH"' >> ~/.bash_profile

RUN git clone https://github.com/pyenv/pyenv.git ~/.pyenv
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
RUN echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
RUN echo 'eval "$(pyenv init -)"' >> ~/.bash_profile

## initialize the new .bash_profile file
RUN source ~/.bash_profile
