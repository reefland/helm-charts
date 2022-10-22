# Helm charts overview

While you can use these charts directly, they are not intended to be used directly.  These charts are not updated for version information.

These charts are for used as templates for an ArgoCD Application deployment.  That deployment maintains the hints needed for Renovate to update image versions.

---

| Chart | Description | ArgoCD Manifest |
| ----- | ----------- |-----------------|
| [home-assistant](apps/home-assistant) | Home Assistant | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/home-assistant-argocd-helm) |
| [mosquitto](apps/mosquitto) | Eclipse Mosquitto - An open source MQTT broker | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/mosquitto-argocd-helm) |
| [k8s-pod-restart-info-collector](apps/pod-restart-info-collector/)| Controller to Monitor for and alert on Kubernetes Pod Restarts | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/pod-restart-info-collector) |
| [trilium-notes](apps/trilium-notes/)|Trilium Notes is a hierarchical note taking application with focus on building large personal knowledge bases.| [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/trilium-notes-argocd-helm) |
| [unifi](apps/unifi) | Ubiquiti Network's Unifi Controller | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/unifi-controller-argocd-helm) |
| [zigbee2mqtt](apps/zigbee2mqtt) | Bridges events and allows you to control your Zigbee devices via MQTT | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/zigbee2mqtt-argocd-helm) |
