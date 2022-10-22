# Trilium Notes

![Version: 0.0.1](https://img.shields.io/badge/Version-0.0.1-informational?style=flat-square) ![AppVersion: 0.55.1](https://img.shields.io/badge/AppVersion-0.55.1-informational?style=flat-square)

Trilium Notes

## Source Code

* <https://github.com/zadam/trilium>

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
helm install trilium-notes reefland/trilium-notes
```

## Installing the Chart

To install the chart with the release name `trilium-notes`

```console
helm install trilium-notes reefland/trilium-notes
```

## Uninstalling the Chart

To uninstall the `trilium-notes` deployment

```console
helm uninstall trilium-notes
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install trilium-notes \
  --set env.TZ="America/New York" \
    reefland/trilium-notes
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install trilium-notes reefland/trilium-notes -f values.yaml
```

## Custom configuration

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
