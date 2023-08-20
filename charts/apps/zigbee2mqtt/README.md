# ⚠️ Deprecated Notice

This `k8s@home` forked chart has been replaced by an updated chart based on `app-template`.  Please see my [other repository](https://github.com/reefland/extra_k8s_apps/tree/master/apps/zigbee2mqtt-argocd-helm) for reference instructions.

---

## zigbee2mqtt

![Version: 9.4.5](https://img.shields.io/badge/Version-9.4.5-informational?style=flat-square) ![AppVersion: 1.32.2](https://img.shields.io/badge/AppVersion-1.32.2-informational?style=flat-square)

Bridges events and allows you to control your Zigbee devices via MQTT

## Source Code

* <https://github.com/Koenkk/zigbee2mqtt>

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
helm install zigbee2mqtt reefland/zigbee2mqtt
```

## Installing the Chart

To install the chart with the release name `zigbee2mqtt`

```console
helm install zigbee2mqtt reefland/zigbee2mqtt
```

## Uninstalling the Chart

To uninstall the `zigbee2mqtt` deployment

```console
helm uninstall zigbee2mqtt
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/reefland/helm-charts/blob/main/charts/library/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install zigbee2mqtt \
  --set env.TZ="America/New York" \
    reefland/zigbee2mqtt
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install zigbee2mqtt reefland/zigbee2mqtt -f values.yaml
```

## Custom configuration

**IMPORTANT NOTE:** a zigbee controller device must be accessible on the node where this pod runs, in order for this chart to function properly.

First, you will need to mount your zigbee device into the pod, you can do so by adding the following to your values:

```yaml
additionalVolumeMounts:
  - name: usb
    mountPath: /path/to/device

additionalVolumes:
  - name: usb
    hostPath:
      path: /path/to/device
```

Second you will need to set a nodeAffinity rule, for example:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: app
          operator: In
          values:
          - zigbee-controller
```

... where a node with an attached zigbee controller USB device is labeled with `app: zigbee-controller`

If you are getting errors, that the device cannot be opened when starting Zigbee2Mqtt, try uncommenting the privileged flag:

```yaml
securityContext:
  privileged: true
```

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/reefland/helm-charts/tree/main/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity constraint rules to place the Pod on a specific node. [[ref]](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) |
| config | object | See values.yaml | zigbee2mqtt configuration settings. This will be copied into the container's persistent storage at first run only. Further configuration should be done in the application itself! See [project documentation](https://www.zigbee2mqtt.io/information/configuration.html) for more information. |
| config.advanced | object | `{"homeassistant_discovery_topic":"homeassistant","homeassistant_status_topic":"homeassistant/status","last_seen":"ISO_8601","log_level":"info","log_output":["console"],"network_key":"GENERATE"}` |  port: /dev/serial/by-id/usb-dresden_elektronik_ingenieurtechnik_GmbH_ConBee_II_DE2400981-if00 Optional: adapter type, not needed unless you are experiencing problems (options: zstack, deconz) adapter: deconz |
| config.advanced.last_seen | string | `"ISO_8601"` |  default: 11 channel: 11 Optional: Baudrate for serial port (default: 115200 for Z-Stack, 38400 for Deconz) baudrate: 38400 Optional: RTS / CTS Hardware Flow Control for serial port (default: false) rtscts: true Optional: Add a last_seen attribute to MQTT messages, contains date/time of last Zigbee message possible values are: disable (default), ISO_8601, ISO_8601_local, epoch (default: disable) |
| config.homeassistant | bool | `false` |  Home Assistant integration (MQTT discovery) |
| config.permit_join | bool | `true` |  WARNING: Disable this after all devices have been paired! (default: false) Note: this will be controllable in the UI |
| env | object | See below | environment variables. See [image docs](https://www.zigbee2mqtt.io/information/configuration.html#override-via-environment-variables) for more details. |
| env.ZIGBEE2MQTT_DATA | string | `"/data"` | Set the data folder for Zigbee2MQTT. |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"koenkk/zigbee2mqtt"` | image repository |
| image.tag | string | `"1.19.1"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| persistence.usb | object | See values.yaml | Configure a hostPathMount to mount a USB device in the container. |
| securityContext.privileged | bool | `nil` | Privileged securityContext may be required if USB controller is accessed directly through the host machine |
| service | object | See values.yaml | Configures service settings for the chart. Normally this does not need to be modified. |

## Changelog

### Version 9.4.5

#### Added

N/A

#### Changed

* Added deprecated warning notice.

#### Fixed

* Fix broken links
* Bump application version
