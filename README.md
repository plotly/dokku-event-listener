# dokku-event-listener [![CircleCI](https://circleci.com/gh/dokku/dokku-event-listener.svg?style=svg)](https://circleci.com/gh/dokku/dokku-event-listener)

Plotly Updates: Service that listens to docker events and runs workspace commands.

## Requirements

- golang 1.12+

## Background

This package tails the Docker event stream for container events and performs specific actions depending on those events.

- Container restarts that result in IP address changes will result in call to `dokku nginx:build-config` for the related app.
- Container restarts that exceed the maximum restart policy retry count for the given container will result in a call to `dokku ps:rebuild` for the related app.

Note that this is only performed for Dokku app containers with the label `com.dokku.app-name`. If the container is missing that label, then no action will be performed when that container emits events on the Docker event stream.

## Installation

Debian and RPM packages are available via [packagecloud](https://packagecloud.io/dokku/dokku)

For a prebuilt binaries, see the [github releases page](https://github.com/dokku/dokku-event-listener/releases).

## Building from source

A make target is provided for building the package from source.

```shell
make build
```

In addition, builds can be performed in an isolated Docker container:

```shell
make build-docker-image build-in-docker
```
