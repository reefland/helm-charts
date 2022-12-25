# syncthing

![Version: 3.5.3](https://img.shields.io/badge/Version-3.5.3-informational?style=flat-square) ![AppVersion: 1.22.2](https://img.shields.io/badge/AppVersion-1.22.2-informational?style=flat-square)

Open Source Continuous File Synchronization

## Source Code

* <https://syncthing.net/>
* <https://github.com/syncthing/syncthing>

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
helm install syncthing reefland/syncthing
```

## Installing the Chart

To install the chart with the release name `syncthing`

```console
helm install syncthing reefland/syncthing
```

## Uninstalling the Chart

To uninstall the `syncthing` deployment

```console
helm uninstall syncthing
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install syncthing \
  --set env.TZ="America/New York" \
    reefland/syncthing
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install syncthing reefland/syncthing -f values.yaml
```

## Custom configuration

**IMPORTANT NOTE:**  The service type of LoadBalancer with a specified IP address should be used.  This will allow easy mapping to the pod for external Syncthing clients.

```yaml
listen:
  enabled: true
  type: LoadBalancer
  # loadBalancerIP: 192.168.10.221
  externalTrafficPolicy: Local
  ports:
    listen:
      enabled: true
      port: 22000
      protocol: TCP
      targetPort: 22000
    discovery:
      enabled: true
      port: 21027
      protocol: UDP
      targetPort: 21027
discovery:
    enabled: false
```

* Modern kubernetes LoadBalancers support multi-protocol two different LoadBalancers are not needed.  Above shows both TCP and UDP on a single LoadBalancer with the Chart's default second one disabled. If you need two then set the type and IP, move the values and enable the 2nd one.

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"syncthing/syncthing"` | image repository |
| image.tag | string | `"1.22.2"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence.data | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service.listen | object | See values.yaml | Configures LoadBalancer service settings for the chart. |
| service.main | object | See values.yaml | Configures Ingress service settings for the chart. |

## Changelog

### Version 3.5.3

#### Added

N/A

#### Changed

* Updated README.md documentation.

#### Fixed

N/A

### Older versions

A historical overview of changes can be found on [ArtifactHUB](https://artifacthub.io/packages/helm/k8s-at-home/syncthing?modal=changelog)
