FROM alpine:3.22.2@sha256:4b7ce07002c69e8f3d704a9c5d6fd3053be500b7f1c69fc0d80990c2ad8dd412

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
    coreutils=9.7-r1 \
    curl=8.14.1-r2 \
    darkice=1.5-r1 \
    ffmpeg=6.1.2-r2 \
    ffmpegthumbnailer=2.2.3-r0 \
    ffmpegthumbs=25.04.2-r0 \
    flac=1.4.3-r1 \
    git=2.49.1-r0 \
    mkvtoolnix=92.0-r0 \
    mlt=7.30.0-r2 \
    mp3splt=2.6.2-r1 \
    pipx=1.7.1-r0 \
    py3-pip=25.1.1-r0 \
    python3=3.12.12-r0 \
    pipewire=1.4.7-r0 \
    soundtouch=2.3.3-r0 \
    v4l-utils=1.28.1-r1 \
    wavpack=5.8.0-r0 \
    x265=3.6-r0 \
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
