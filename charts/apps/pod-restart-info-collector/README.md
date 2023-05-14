# Pod Restart Info Collector

![Version: 0.1.2](https://img.shields.io/badge/Version-0.1.2-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

k8s-pod-restart-info-collector is a simple K8s customer controller that watches for Pods changes and collects K8s Pod restart reasons, logs, and events to Slack channel when a Pod restarts.

## Source Code

The project did not offer a Helm Chart repository.  _This is being offered only until the project publishes an official Helm Repository._

* <https://github.com/airwallex/k8s-pod-restart-info-collector>

## Requirements

Slack Channel for WebHook notification.

## Dependencies

N/A

## TL;DR

```console
helm repo add reefland https://reefland.github.io/helm-charts
helm repo update
helm install pod-restart-info-collector reefland/k8s-pod-restart-info-collector
```

## Installing the Chart

To install the chart with the release name `pod-restart-info-collector`

```console
helm install pod-restart-info-collector reefland/k8s-pod-restart-info-collector
```

## Uninstalling the Chart

To uninstall the `pod-restart-info-collector` deployment

```console
helm uninstall pod-restart-info-collector
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install pod-restart-info-collector \
  --set slackWebhookUrl="https://hooks.slack.com/services/Change-Me" \
  --set clusterName="Change-Me" 
  --set slackChannel="Change-Me" \
  reefland/k8s-pod-restart-info-collector
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install pod-restart-info-collector reefland/k8s-pod-restart-info-collector -f values.yaml
```

Example Slack Notification Image from GitHub Project Page:

![Notification Image Example](https://camo.githubusercontent.com/b394a049d5d34f78e186ac8695c23611e1afb1fcf6ae9ada8b31bbd1f44fc905/68747470733a2f2f6d69726f2e6d656469756d2e636f6d2f6d61782f313230302f312a6d767a5868624e6551434a39426c68316f44483475772e706e67)

## Values

| Name                                | Description                                        | Value         |
| ------------------------------------| -------------------------------------------------- | ------------- |
| `clusterName`                       | K8s cluster name (Display on slack message)                        | required         |
| `slackUsername`                     | Slack username (Display on slack message) | default: `"k8s-pod-restart-info-collector"`          |
| `slackChannel`                      | Slack channel name | default: `"restart-info-nonprod"`          |
| `muteSeconds`                       | The time to mute duplicate pod alerts | default: `"600"`    
| `ignoreRestartCount`                | The number of pod restart count to ignore | default: `"30"`
| `ignoredNamespaces`                 | A comma-separated list of namespaces to ignore | default: `""`    
| `ignoredPodNamePrefixes`            | A comma-separated list of pod name prefixes to ignore | default: `""`   
| `watchedNamespaces`                 | A comma-separated list of namespaces to watch, default is all ("")| default: `""`    
| `watchedPodNamePrefixes`            | A comma-separated list of pod name prefixes to watch, default is all ("")| default: `""`   
| `ignoreRestartsWithExitCodeZero`    | Whether restart events with an exit code of 0 should be ignored | default: `false`
| `slackWebhookUrl`                   | Slack webhook URL | required if slackWebhooUrlSecretKeyRef is not present                       |
| `slackWebhookurlSecretKeyRef.key`   | Slack webhook URL SecretKeyRef.key                 | key within the secret which has webhook value |
| `slackWebhookurlSecretKeyRef.name`  | Slack webhook URL SecretKeyRef.name                | name of secret holding the Slack WebHook URL  |
## Changelog

### Version 0.1.2

#### Added

N/A

#### Changed

* Updated per upstream project.

#### Fixed

* Documentation references only
