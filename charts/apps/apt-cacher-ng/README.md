# Apt-Cacher NG

![Version: 0.0.1](https://img.shields.io/badge/Version-0.0.1-informational?style=flat-square) ![AppVersion: 3.7.4-20220421](https://img.shields.io/badge/AppVersion-3.7.4-informational?style=flat-square)

Apt-Cacher NG is a caching proxy, specialized for package files from Linux distributors, primarily for Debian (and Debian based) distributions but not limited to those.

## Source Code

* <https://www.unix-ag.uni-kl.de/~bloch/acng/>
* <https://github.com/sameersbn/docker-apt-cacher-ng>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://library-charts.k8s-at-home.com | common | 4.5.2 |

## TL;DR

```console
helm repo add reefland https://reefland.github.io/helm-charts
helm repo update
helm install apt-cacher-ng reefland/apt-cacher-ng
```

## Installing the Chart

To install the chart with the release name `apt-cacher-ng`

```console
helm install apt-cacher-ng reefland/apt-cacher-ng
```

## Uninstalling the Chart

To uninstall the `apt-cacher-ng` deployment

```console
helm uninstall apt-cacher-ng
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install apt-cacher-ng \
  --set env.TZ="America/New York" \
    reefland/apt-cacher-ng
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install apt-cacher-ng reefland/apt-cacher-ng -f values.yaml
```

## Custom Configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"zadam/trilium"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |

## Changelog

### Version 0.0.1

#### Added

N/A

#### Changed

* Initial Chart Release

#### Fixed

N/A
