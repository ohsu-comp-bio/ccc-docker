FROM phusion/baseimage

ENV GALAXY_EGGS_PATH /data/galaxy/eggs
ENV GALAXY_ROOT /opt/galaxy

RUN mkdir $GALAXY_ROOT

WORKDIR $GALAXY_ROOT

RUN apt-get update
RUN apt-get install -y \
  build-essential \
  git \
  libbz2-dev \
  libreadline-dev \
  libsqlite3-dev \
  libssl-dev \
  make \
  python-pip \
  sqlite3 \
  zlib1g-dev

# Install pyenv
ENV PYENV_ROOT /opt/pyenv
RUN git clone https://github.com/yyuu/pyenv.git $PYENV_ROOT
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH

# Install Python 2.7.10 and set as pyenv global version
RUN pyenv install 2.7.10
RUN pyenv global 2.7.10

# Create a virtual environment
RUN pip install virtualenv && virtualenv .venv

ADD . /

# Copy our config over
RUN cp /etc/galaxy/galaxy.ini $GALAXY_ROOT/config/galaxy.ini
RUN cp /usr/local/bin/galaxy_environment.sh $GALAXY_ROOT/contrib/intel_env.sh

# Use Bash as our shell.
RUN update-alternatives --install /bin/sh bash /bin/bash 1

EXPOSE 8080
