# Baski - Build And Scan Kubernetes Images

[//]: # ([![Known Vulnerabilities]&#40;https://snyk.io/test/github/drewbernetes/baski/badge.svg&#41;]&#40;https://snyk.io/test/github/drewbernetes/baski&#41;)
[![Build on Tag](https://github.com/drewbernetes/baski/actions/workflows/tag.yml/badge.svg?branch=main&event=release)](https://github.com/drewbernetes/baski/actions/workflows/tag.yml)

A binary for building and scanning (with [Trivy](https://github.com/aquasecurity/trivy)) a Kubernetes image using
the [kubernetes-sigs/image-builder](https://github.com/kubernetes-sigs/image-builder) repo or
the [drew-viles-image-builder](https://github.com/drew-viles/image-builder) repo where new functionality is required
but not yet merged upstream.

Baski also supports signing images and will tag the image with a digest so that a verification can be done against
images.

The scanning and signing functionality are separate from the build meaning these can be used on none Kubernetes images.

# Scope

✅ Stable

_However, no responsibility is held for anything that may go wrong with your images - it's been tested to the best of my
ability, but you know, hidden bugs exist in all projects_

# Supported clouds

| Cloud Provider                 |
|--------------------------------|
| [OpenStack](docs/openstack.md) |
| [Kubevirt](docs/kubevirt.md)   |

*More clouds could be supported but may not be maintained directly by Drewbernetes.*

# Usage

Run the binary with a config file or see the help for a list of flags.
In the [example config](baski-example.yaml), not all fields are required and any fields that are not required are left
blank - unless the fields are enabled by a bool, for example in the Nvidia options where none are required
if `enable-nvidia-support` is set to false,

The following are valid locations for the `baski.yaml` config file are:

```shell
/tmp/
/etc/baski/
$HOME/.baski/
```

### More info

For more flags and info, run `baski --help`

### Running locally

If you wish to run it locally then you can either build the binary and run it, or you can run it in docker by doing the
following example for OpenStack:

```shell
docker build -t baski:v0.0.0 -f docker/baski/Dockerfile .

docker run --name baski -it --rm --env OS_CLOUD=some-cloud -v /path/to/openstack/clouds.yaml:/home/baski/.config/openstack/clouds.yaml -v /path/to/baski.yaml:/tmp/baski.yaml baski:v0.0.0

#Then from in here
baski build / scan / sign
```
# TODO

* Automatically clear up resources when ctrl-c is pressed.
* Make this work for more than just Openstack so that it's more useful to the community around the Kubernetes Image
  Builder?
* Add metrics/telemetry to the process.
* Create all option to allow whole process?

# License

The scripts and documentation in this project are released under the [Apache v2 License](LICENSE).
