# GatewayD Community Kubernetes Helm Charts

The Helm charts in this repository can be used for deploying GatewayD on Kubernetes. For instructions on how to use these charts, see the [README.md](charts/gatewayd/README.md).

## Contributing

We welcome contributions from everyone. Just open an [issue](https://github.com/gatewayd-io/helm-charts/issues) or send us a [pull request](https://github.com/gatewayd-io/helm-charts/pulls).

## License

GatewayD Helm Charts is licensed under the [Apache 2.0 License](https://github.com/gatewayd-io/helm-charts/blob/main/LICENSE).

# GatewayD Community Kubernetes Helm Charts

This Helm charts installs GatewayD on your Kubernetes cluster.

## How to use the charts

1. Clone this repository
2. Install the chart
3. (Optionally) Uninstall the chart

```bash
git clone https://github.com/gatewayd-io/helm-charts.git
cd helm-charts/charts/gatewayd/
helm install gatewayd-release -f values.yaml ./
# helm uninstall gatewayd-release
```