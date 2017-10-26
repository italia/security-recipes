FROM debian:jessie

###
# Dependencies
###

ENV DEBIAN_FRONTEND=noninteractive

RUN \
    apt-get update \
    && apt-get install \
        -y \
        --no-install-recommends \
        --no-install-suggests \
      build-essential \
      curl \
      git \
      libc6-dev \
      libfontconfig1 \
      libreadline-dev \
      libssl-dev \
      libssl-doc \
      libxml2-dev \
      libxslt1-dev \
      libyaml-dev \
      make \
      unzip \
      wget \
      zlib1g-dev \
      autoconf \
      automake \
      bison \
      gawk \
      libffi-dev \
      libgdbm-dev \
      libncurses5-dev \
      libsqlite3-dev \
      libtool \
      pkg-config \
      sqlite3 \
      libbz2-dev \
      llvm \
      libncursesw5-dev\
      nodejs \
      npm \
      python3-dev \
      python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc/ \
    && rm -rf /usr/share/man \
    && rm -rf /usr/share/locale


###
## Python
###

ENV PYENV_RELEASE 1.1.1
ENV PYENV_PYTHON_VERSION 3.6.1
ENV PYENV_ROOT /opt/pyenv
ENV PYENV_REPO https://github.com/pyenv/pyenv

RUN wget ${PYENV_REPO}/archive/v${PYENV_RELEASE}.zip \
      --no-verbose \
  && unzip v$PYENV_RELEASE.zip -d $PYENV_ROOT \
  && mv $PYENV_ROOT/pyenv-$PYENV_RELEASE/* $PYENV_ROOT/ \
  && rm -r $PYENV_ROOT/pyenv-$PYENV_RELEASE

ENV PATH $PYENV_ROOT/bin:$PATH

RUN echo 'eval "$(pyenv init -)"' >> /etc/profile \
    && eval "$(pyenv init -)" \
    && pyenv install $PYENV_PYTHON_VERSION \
    && pyenv local $PYENV_PYTHON_VERSION

COPY requirements.txt requirements.txt
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools
RUN pip3 install -r requirements.txt

###
# pshtt
###

RUN pip3 install pshtt==0.2.1 \
  && pip install six --upgrade


###
# Create unprivileged User
###

ENV SCANNER_HOME /home/scanner
RUN mkdir $SCANNER_HOME

RUN groupadd -r scanner \
  && useradd -r -c "Scanner user" -g scanner scanner \
  && chown -R scanner:scanner ${SCANNER_HOME}

###
# Prepare to Run
###

WORKDIR $SCANNER_HOME

# Volume mount for use with the 'data' option.
VOLUME /data

ENTRYPOINT ["./scan_wrap.sh"]
