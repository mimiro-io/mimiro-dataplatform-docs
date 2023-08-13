# Usage

## Get Started

Being a Golang application, the DataHub is compliled to a single binary file and can be run by executing said binary.

However, for a production environment with sizable datasets and many jobs, DataHub has better performance
when using [jemalloc](https://jemalloc.net/) as the memory allocator for storage operations.

Precompiled binaries using jemalloc are provided in form of docker images on [dockerhub](https://hub.docker.com/r/mimiro/datahub).

To run the DataHub using docker, execute the following command:

```bash
docker run -p 8080:8080 mimiro/datahub:latest
```

If you wish to run a binary file directly, it must be built from source.
See the [build instructions](https://github.com/mimiro-io/datahub#building) on github.

There is also a go-only version of the DataHub included in the published docker images. This version does not use
jemalloc. In some cases, the Go garbage collector is better suited to keep storage operations within given memory limits.

To use the go-only version, run the following command:

```bash
docker run -p 8080:8080 mimiro/datahub:latest ./server-gogc
```

To use the go-only version, with a memory limit of 8Gb and less frequent garbage collection, run the following command:

```bash
docker run -e GOGC=1000 -e GOMEMLIMIT=8GiB -p 8080:8080 mimiro/datahub:latest ./server-gogc
```

Read more about tuning the Go garbage collector using ENV variables [here](https://pkg.go.dev/runtime#hdr-Environment_Variables).

Also check out the [getting started](https://github.com/mimiro-io/datahub#getting-started) section on github.

## The DataHub CLI

The DataHub itself is operated through an HTTP API. For convenience, we recommend getting and installing, `mim`, the
MIMIRO DataHub CLI.

`mim` can be downloaded for any platform: linux, macos, and windows. Check out the [releases](https://github.com/mimiro-io/datahub-cli/releases) on github.

The DataHub cli `mim` is written in Go and compiled into a single binary. Download the right version for your
operating systems, unpack it and add the `mim` binary to your path.
