FROM alpine:3.23.2@sha256:865b95f46d98cf867a156fe4a135ad3fe50d2056aa3f25ed31662dff6da4eb62

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
    coreutils=9.8-r1 \
    curl=8.17.0-r1 \
    darkice=1.5-r1 \
    ffmpeg=8.0.1-r0 \
    ffmpegthumbnailer=2.2.4-r0 \
    ffmpegthumbs=25.08.3-r0 \
    flac=1.4.3-r2 \
    git=2.52.0-r0 \
    mkvtoolnix=96.0-r0 \
    mlt=7.34.0-r0 \
    mp3splt=2.6.2-r1 \
    pipx=1.8.0-r0 \
    py3-pip=25.1.1-r1 \
    python3=3.12.12-r0 \
    pipewire=1.4.9-r4 \
    soundtouch=2.3.3-r0 \
    v4l-utils=1.32.0-r0 \
    wavpack=5.8.1-r0 \
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
