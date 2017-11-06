FROM python:3.4-slim

RUN \
  apt-get update \
  && apt-get install \
      -y \
      --no-install-recommends \
      --no-install-suggests \
    gcc \
    libpq-dev \
    paxctl \
    git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /usr/share/doc/ \
  && rm -rf /usr/share/man \
  && rm -rf /usr/share/locale

RUN adduser gcorn
COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

EXPOSE 8000
USER gcorn
