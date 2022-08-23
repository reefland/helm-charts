# Helm charts overview

While you can use these charts directly, they are not intended to be used directly.  These charts are not updated for version information.

These charts are for used as templates for an ArgoCD Application deployment.  That deployment maintains the hints needed for Renovate to update image versions.

---

| Chart | Description | ArgoCD Manifest |
| ----- | ----------- |-----------------|
| [mosquitto](apps/mosquitto) | Eclipse Mosquitto - An open source MQTT broker | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/mosquitto-argocd-helm) |
| [zigbee2mqtt](stable/zigbee2mqtt) | Bridges events and allows you to control your Zigbee devices via MQTT | [Link](https://github.com/reefland/ansible-k3s-argocd-renovate/tree/master/_extra_apps/zigbee2mqtt-argocd-helm) |