FROM alpine:3.22.0@sha256:8a1f59ffb675680d47db6337b49d22281a139e9d709335b492be023728e11715

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
    blind=1.1-r6 \
    darkice=1.5-r1 \
    ffmpeg=6.1.2-r2 \
    ffmpegthumbnailer=2.2.3-r0 \
    ffmpegthumbs=25.04.0-r0 \
    flac=1.4.3-r1 \
    freac=1.1.7-r0 \
    mkvtoolnix=92.0-r0 \
    mlt=7.30.0-r2 \
    mp3splt=2.6.2-r1 \
    py3-pip=25.1.1-r0 \
    python3=3.12.10-r1 \
    pipewire=1.4.4-r0 \
    soundtouch=2.3.3-r0 \
    v4l-utils=1.28.1-r1 \
    wavpack=5.8.0-r0 \
    x265=3.6-r0 \
    yt-dlp=2025.05.22-r0 \
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

USER "${USER_NAME}"

ENV HOME="${USER_HOME}"

WORKDIR "${HOME}"
