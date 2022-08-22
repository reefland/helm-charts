# helm-charts

A collection of Helm charts.

## Goal

This repo contains Helm charts based on previous work from [k8s@home project](https://github.com/k8s-at-home/charts) for [applications](https://github.com/reefland/helm-charts/tree/main/charts) I've deploy to my [Home Kubernetes](https://github.com/reefland/ansible-k3s-argocd-renovate) Cluster.

## Installation

The Helm repository can be installed as follows:

```console
helm repo add reefland https://reefland.github.io/helm-charts
```

You can then search the application charts:

```console
helm search repo reefland
```

## Documentation

Documentation can be found [here](https://github.com/reefland/helm-charts/tree/main/docs).

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md)

## License

[Apache 2.0 License](./LICENSE)

