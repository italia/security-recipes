FROM node:6.11.0-alpine

RUN \
  apk update \
  && apk add \
    paxctl \
    python \
    make \
    g++ \
  && paxctl -cm /usr/local/bin/node \
  && npm install --global gulp-cli
