FROM alpine:3.21.3@sha256:a8560b36e8b8210634f77d9f7f9efd7ffa463e380b75e2e74aff4511df3ef88c

HEALTHCHECK NONE

ENTRYPOINT []

ARG USER_NAME=default
ARG USER_HOME=/home/default
ARG USER_ID=1000
ARG USER_GECOS=Default

SHELL ["/bin/ash", "-euo", "pipefail", "-c"]

# hadolint ignore=DL3019
RUN apk -U upgrade \
    && apk add \
    audiofile=0.3.6-r3 \
    blind=1.1-r5 \
    darkice=1.5-r0 \
    ffmpeg=6.1.2-r1 \
    ffmpegthumbnailer=2.2.2-r7 \
    ffmpegthumbs=24.08.3-r0 \
    flac=1.4.3-r1 \
    freac=1.1.7-r0 \
    mkvtoolnix=88.0-r0 \
    mlt=7.28.0-r0 \
    mp3splt=2.6.2-r1 \
    py3-pip=24.3.1-r0 \
    python3=3.12.9-r0 \
    pipewire=1.2.7-r0 \
    soundtouch=2.3.3-r0 \
    v4l-utils=1.28.1-r1 \
    wavpack=5.7.0-r0 \
    x265=3.6-r0 \
    yt-dlp=2025.03.21-r0 \
    && if apk -u list | grep -q -e . ; then \
      apk -u list ; \
      exit 1 ; \
    fi \
    && apk cache clean \
    && rm -rf /var/cache/apk/*

RUN adduser \
  --home "${USER_HOME}" \
  --uid "${USER_ID}" \
  --gecos "${USER_GECOS}" \
  --disabled-password \
  "${USER_NAME}"

ENV HOME="${USER_HOME}"

USER "${USER_NAME}"

WORKDIR "${HOME}"
