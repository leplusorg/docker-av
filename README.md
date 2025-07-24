# Audiovisual

Multi-platform Docker container with utilities to process audiovisual media (`ffmpeg`, `mkvtoolnix`, `mlt`, `flac`, `mp3splt`...).

[![Dockerfile](https://img.shields.io/badge/GitHub-Dockerfile-blue)](av/Dockerfile)
[![Docker Build](https://github.com/leplusorg/docker-av/workflows/Docker/badge.svg)](https://github.com/leplusorg/docker-av/actions?query=workflow:"Docker")
[![Docker Stars](https://img.shields.io/docker/stars/leplusorg/av)](https://hub.docker.com/r/leplusorg/av)
[![Docker Pulls](https://img.shields.io/docker/pulls/leplusorg/av)](https://hub.docker.com/r/leplusorg/av)
[![Docker Version](https://img.shields.io/docker/v/leplusorg/av?sort=semver)](https://hub.docker.com/r/leplusorg/av)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/10081/badge)](https://bestpractices.coreinfrastructure.org/projects/10081)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/leplusorg/docker-av/badge)](https://securityscorecards.dev/viewer/?uri=github.com/leplusorg/docker-av)

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

## Software Bill of Materials (SBOM)

To get the SBOM for the latest image (in SPDX JSON format), use the
following command:

```bash
docker buildx imagetools inspect leplusorg/av --format '{{ json (index .SBOM "linux/amd64").SPDX }}'
```

Replace `linux/amd64` by the desired platform (`linux/amd64`, `linux/arm64` etc.).

### Sigstore

[Sigstore](https://docs.sigstore.dev) is trying to improve supply
chain security by allowing you to verify the origin of an
artifcat. You can verify that the jar that you use was actually
produced by this repository. This means that if you verify the
signature of the ristretto jar, you can trust the integrity of the
whole supply chain from code source, to CI/CD build, to distribution
on Maven Central or whever you got the jar from.

You can use the following command to verify the latest image using its
sigstore signature attestation:

```bash
cosign verify leplusorg/av --certificate-identity-regexp 'https://github\.com/leplusorg/docker-av/\.github/workflows/.+' --certificate-oidc-issuer 'https://token.actions.githubusercontent.com'
```

The output should look something like this:

```text
Verification for index.docker.io/leplusorg/xml:main --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - The code-signing certificate was verified using trusted certificate authority certificates

[{"critical":...
```

For instructions on how to install `cosign`, please read this [documentation](https://docs.sigstore.dev/cosign/system_config/installation/).

## Request new tool

Please use [this link](https://github.com/leplusorg/docker-av/issues/new?assignees=thomasleplus&labels=enhancement&template=feature_request.md&title=%5BFEAT%5D) (GitHub account required) to request that a new tool be added to the image. I am always interested in adding new capabilities to these images.
