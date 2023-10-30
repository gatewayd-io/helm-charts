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
