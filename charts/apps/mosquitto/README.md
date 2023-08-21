# ⚠️ Deprecated Notice

This `k8s@home` forked chart has been replaced by an updated chart based on `app-template`.  Please see my [other repository](https://github.com/reefland/extra_k8s_apps/tree/master/apps/mosquitto-argocd-helm) for reference instructions.

---

## mosquitto

![Version: 4.8.4](https://img.shields.io/badge/Version-4.8.4-informational?style=flat-square) ![AppVersion: 2.0.15](https://img.shields.io/badge/AppVersion-2.0.15-informational?style=flat-square)

Eclipse Mosquitto - An open source MQTT broker

## Source Code

* <https://github.com/eclipse/mosquitto>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://library-charts.k8s-at-home.com> | common | 4.5.2 |

## TL;DR

```console
helm repo add reefland https://reefland.github.io/helm-charts/
helm repo update
helm install mosquitto reefland/mosquitto
```

## Installing the Chart

To install the chart with the release name `mosquitto`

```console
helm install mosquitto reefland/mosquitto
```

## Uninstalling the Chart

To uninstall the `mosquitto` deployment

```console
helm uninstall mosquitto
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install mosquitto \
  --set env.TZ="America/New York" \
    reefland/mosquitto
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install mosquitto reefland/mosquitto -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/reefland/helm-charts/tree/main/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| addListener | bool | `true` | When enabled, this adds the `listener` option to the mosquitto config. Change this to false when using TLS. |
| auth.enabled | bool | `false` | By enabling this, `allow_anonymous` gets set to `false` in the mosquitto config. |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"eclipse-mosquitto"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| perListenerSettings | bool | `false` | By enabling this, authentication and access control settings will be controlled on a per-listener basis |
| persistence.configinc | object | See values.yaml | Configure a persistent volume to place *.conf mosquitto-config-files in. When enabled, this gets set as `include_dir` in the mosquitto config. |
| persistence.data | object | See values.yaml | Configure a persistent volume to place mosquitto data in. When enabled, this enables `persistence` and `persistence_location` in the mosquitto config. |
| service | object | See values.yaml | Configures service settings for the chart. Normally this does not need to be modified. |

## Changelog

### Version 4.8.4

#### Added

N/A

#### Changed

N/A

#### Fixed

* Removed outdated repository links
* Added deprecated notice, [this chart has been replaced](https://github.com/reefland/extra_k8s_apps/tree/master/apps/mosquitto-argocd-helm).
