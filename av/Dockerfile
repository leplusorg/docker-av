FROM alpine:3.24.1@sha256:28bd5fe8b56d1bd048e5babf5b10710ebe0bae67db86916198a6eec434943f8b

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

RUN apk upgrade --no-cache \
    && apk add --no-cache \
    audiofile=0.3.6-r3 \
    blind=1.1-r6 \
    coreutils=9.11-r0 \
    curl=8.20.0-r1 \
    darkice=1.6-r0 \
    ffmpeg=8.1.2-r0 \
    ffmpegthumbnailer=2.2.4-r0 \
    ffmpegthumbs=26.04.2-r0 \
    flac=1.4.3-r2 \
    git=2.54.0-r0 \
    mkvtoolnix=99.0-r0 \
    mlt=7.36.1-r1 \
    mp3splt=2.6.2-r1 \
    pipx=1.14.0-r0 \
    py3-pip=26.1.2-r0 \
    python3=3.14.5-r0 \
    pipewire=1.6.6-r0 \
    soundtouch=2.4.1-r0 \
    v4l-utils=1.32.0-r1 \
    wavpack=5.9.0-r0 \
    x265=4.1-r0 \
    && apk cache --no-cache clean \
    && rm -rf /var/cache/apk/*

COPY requirements.txt /tmp/requirements.txt

RUN pipx ensurepath --global \
    && xargs -a /tmp/requirements.txt -n 1 pipx install --global \
    && rm -f /tmp/requirements.txt

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

USER "${USER_NAME}"

ENV HOME="${USER_HOME}"

WORKDIR "${HOME}"
