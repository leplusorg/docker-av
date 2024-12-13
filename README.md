# Images

Docker container to manipulate audiovisual media (ffmpeg, mkvtoolnix, mlt...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](https://github.com/leplusorg/docker-av/blob/main/av/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-av/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-av/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/av)](https://hub.docker.com/r/leplusorg/av)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/av)](https://hub.docker.com/r/leplusorg/av)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/av?sort=semver)](https://hub.docker.com/r/leplusorg/av)

## Example without using the filesystem

Let's say that you have a MP3 `foo.mp3` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
cat foo.mp3 | docker run --rm -i --net=none leplusorg/av ffprobe -v error -show_streams -
```

**Windows**

```batch
type foo.mp3 | docker run --rm -i --net=none leplusorg/av ffprobe -v error -show_streams -
```

## Example using the filesystem

Same thing, assuming that you have a MP3 `foo.mp3` in your current working directory that you want to extract its metadata:

**Mac/Linux**

```bash
docker run --rm -t --user="$(id -u):$(id -g)" --net=none -v "$(pwd):/tmp" leplusorg/av ffprobe -v error -show_streams /tmp/foo.mp3
```

**Windows**

In `cmd`:

```batch
docker run --rm -t --net=none -v "%cd%:/tmp" leplusorg/av ffprobe -v error -show_streams /tmp/foo.mp3
```

In PowerShell:

```pwsh
docker run --rm -t --net=none -v "${PWD}:/tmp" leplusorg/av ffprobe -v error -show_streams /tmp/foo.mp3
```

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-av/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
