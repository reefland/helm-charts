# Apt-Cacher NG

![Version: 0.0.5](https://img.shields.io/badge/Version-0.0.5-informational?style=flat-square) ![AppVersion: 3.7.4-20220421](https://img.shields.io/badge/AppVersion-3.7.4-informational?style=flat-square)

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

**IMPORTANT NOTE:**  The service type of LoadBalancer with a specified IP address should be used.  This will allow easy mapping to the pod for external clients who will use the Apt-Cacher NG proxy.

```yaml

service:
  main:
    enabled: true
    primary: true
    type: LoadBalancer
    loadBalancerIP: 192.168.0.240
    ports:
      http:
        enabled: true
        port: 3142
        protocol: TCP
        targetPort: 3142
```

The Apt-Cacher NG comes with a predefined configuration file which is not editable.  This helm chart allows you to define a replacement file (they are not merged, it will be replaced).  You would need to specify a full conf file with any modification you need (if any at all).

```yaml
configmap:
  acng-conf-file:
    enabled: true
    data:
      acng.conf: |
        # Storage directory for downloaded data and related maintenance activity.
        #
        # Note: When the value for CacheDir is changed, change the file
        # /lib/systemd/system/apt-cacher-ng.service too
        #
        CacheDir: /var/cache/apt-cacher-ng

        ...
```

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
|configmap.acng-conf-file| object | See values.yaml | Configuration file replacement of one provided within container |
| env | object | See below | environment variables. |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"sameersbn/apt-cacher-ng"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence.acng-conf-file | object | See values.yaml | Configure configMap mounting under this key. |
| persistence.cache-vol | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service | object | See values.yaml | Configures service settings for the chart. Need to set LoadBalancer IP address here. |

## Changelog

### Version 0.0.5

#### Added

N/A

#### Changed

* Removed incorrect application icon

#### Fixed

N/A
