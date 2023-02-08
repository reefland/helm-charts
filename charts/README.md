# Helm charts overview

While you can use these charts directly, they are not intended to be used directly.  These charts are not updated for per application version.

NOTE: These charts are used as templates for an ArgoCD Application deployment.  The ArgoCD deployment maintains the hints needed for RenovateBot to update application image versions (see application *Link* for details)

---

| Chart | Description | ArgoCD Manifest |
| ----- | ----------- |-----------------|
| [apt-cacher-ng](apps/apt-cacher-ng/) | Apt-Cacher NG - A caching proxy. Specialized for package files from Linux distributors, primarily for Debian (and Debian based) distributions but not limited to those. | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/apt-cacher-ng-argocd-helm) |
| [home-assistant](apps/home-assistant) | Home Assistant - Open source home automation that puts local control and privacy first.| [Link](https://github.com/reefland/extra_k8s_apps/tree/master/home-assistant-argocd-helm) |
| [mosquitto](apps/mosquitto) | Eclipse Mosquitto - An open source MQTT broker | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/mosquitto-argocd-helm) |
| [pod-restart-info-collector](apps/pod-restart-info-collector/)| Controller to Monitor for and alert (Slack) on Kubernetes Pod Restarts | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/pod-restart-info-collector) |
| [Syncthing](apps/syncthing/)| Syncthing synchronizes files between two or more computers in real time, safely protected from prying eyes. | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/syncthing-argocd-helm) |
| [trilium-notes](apps/trilium-notes/)|Trilium Notes is a hierarchical note taking application with focus on building large personal knowledge bases.| [Link](https://github.com/reefland/extra_k8s_apps/tree/master/trilium-notes-argocd-helm) |
| [unifi](apps/unifi) | Ubiquiti Network's Unifi Controller | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/unifi-controller-argocd-helm) |
| [zigbee2mqtt](apps/zigbee2mqtt) | Bridges events and allows you to control your Zigbee devices via MQTT | [Link](https://github.com/reefland/extra_k8s_apps/tree/master/zigbee2mqtt-argocd-helm) |
