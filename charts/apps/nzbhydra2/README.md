# NZBHydra 2

![Version: 0.0.4](https://img.shields.io/badge/Version-0.0.4-informational?style=flat-square) ![AppVersion: 5.1.1](https://img.shields.io/badge/AppVersion-5.1.1-informational?style=flat-square)

NZBHydra 2 is a meta search for newznab indexers and torznab trackers.

## Source Code

* <https://github.com/theotherp/nzbhydra2>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://library-charts.k8s-at-home.com> | common | 4.5.2 |

## TL;DR

```console
helm repo add reefland https://reefland.github.io/helm-charts
helm repo update
helm install nzbhydra2 reefland/nzbhydra2
```

## Installing the Chart

To install the chart with the release name `nzbhydra2`

```console
helm install nzbhydra2 reefland/nzbhydra2
```

## Uninstalling the Chart

To uninstall the `nzbhydra2` deployment

```console
helm uninstall nzbhydra2
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install nzbhydra2 \
  --set env.TZ="America/New York" \
    reefland/nzbhydra2
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install nzbhydra2 reefland/nzbhydra2 -f values.yaml
```

## Custom Configuration

The service type of ClusterIP should be all that is needed.

```yaml
service:
  main:
    enabled: true
    type: ClusterIP
    ports:
      http:
        enabled: true
        port: 5076
        protocol: TCP
        targetPort: http
```

The ingress within the chart can be enabled or an external ingress can be used.

```yaml
ingress:
  # -- Enable and configure ingress settings for the chart under this key.
  # @default -- See values.yaml
  main:
    enabled: false
    annotations:
      traefik.ingress.kubernetes.io/router.entrypoints: "websecure"
      traefik.ingress.kubernetes.io/router.middlewares: "traefik-x-forward-https-headers@kubernetescrd,traefik-compress@kubernetescrd"
    hosts:
      - host: hydra.example.com
        paths:
          - path: /
            pathType: Prefix
```

### PVC Storage

Two PVC storage entries are needed:

* One named `config` to hold the NZBHydra 2 configuration, log files, database.  This can be a storage class which only does `ReadWriteOnce` (ceph-block shown in example, adjust to your environment).

```yaml
    persistence:
      config:
        enabled: true
        mountPath: /config
        type: pvc
        accessMode: ReadWriteOnce
        size: 1Gi
        retain: true
        storageClass: ceph-block
```

* Second named `data` which is PVC storage for shared space among other NZB aware applications this is a working area for downloading, queues, watch directory, etc.  This MUST be a storage class which supports `ReadWriteMany` (ceph-filesystem shown in example, adjust to your environment).

```yaml
      data:
        enabled: true
        mountPath: /data/downloads
        type: pvc
        accessMode: ReadWriteMany
        size: 100Gi
        retain: true
        storageClass: ceph-filesystem
```

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. |
| env.TZ | string | `"UTC"` | Set the container timezone |
| env.PUID | integer | 1001 | Default process User ID |
| env.PGID | integer | 1001 | Default process Group ID |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"lscr.io/linuxserver/nzbhydra2"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence.config | object | See values.yaml | Configure persistence settings for configuration under this key. |
| persistence.data | object | See values.yaml | Configure persistence settings for data sharing  under this key. |
| service | object | See values.yaml | Configures service settings for the chart. |

## Changelog

### Version 0.0.4

#### Added

* Ingress example to docs.

#### Changed

* Increased initialDelaySeconds, startup probe delay.

#### Fixed

N/A
