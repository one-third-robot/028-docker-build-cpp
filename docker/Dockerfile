# syntax=docker/dockerfile:experimental

# prepare the docker   -----------------
FROM ubuntu:20.04 AS build
ARG DEBIAN_FRONTEND=noninteractive
# By default, ubuntu docker images include code to remove downloaded packages.
# Use the invocation from examples to avoid this and make the apt cache effective.
RUN rm -f /etc/apt/apt.conf.d/docker-clean \
    && echo 'Binary::apt::APT::Keep-Downloaded-Packages "true";' \
    > /etc/apt/apt.conf.d/keep-cache

# make sure the command add-apt-repository exists in the next step
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    apt-get update && apt-get --no-install-recommends install -y \
    software-properties-common

# gcc-11 & g++-11
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test

# run export DOCKER_BUILDKIT=1 to enable BuildKit
RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
    --mount=type=cache,target=/var/lib/apt,sharing=locked \
    apt-get update && apt-get --no-install-recommends install -y \
    build-essential \
    gcc-11 \
    g++-11 \
    cmake \
    libtool \
    autoconf \
    pkg-config
