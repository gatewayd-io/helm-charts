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

## Configuration
The following table lists the configurable parameters of the GatewayD Helm chart and their default values:

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `autoscaling.enabled`                       | Determines whether autoscaling is enabled for the deployment. If not enabled, the `replicaCount` value is used to set the number of replicas.                    | `false`                     |
| `replicaCount`                              | The number of replicas to create for the deployment                                                  | `1`                         |
| `podAnnotations`                            | Annotations to add to the pod                                                                         | `{}`                        |
| `podLabels`                                 | Labels to add to the pod                                                                              | `{}`                        |
| `imagePullSecrets`                          | Image pull secrets for the Docker registry                                                            | `[]`                        |
| `serviceAccountName`                       | The name of the service account to use for the deployment                                             | `""`                        |
| `podSecurityContext`                        | Security context for the pod                                                                          | `{}`                        |
| `securityContext`                           | Security context for the container                                                                    | `{}`                        |
| `image.repository`                          | The Docker image repository                                                                           | `gatewaydio/gatewayd`       |
| `image.tag`                                 | The Docker image tag. If not set, the app version from the chart is used                              | `""`                        |
| `image.pullPolicy`                          | The image pull policy                                                                                 | `IfNotPresent`              |
| `service.port`                              | The port that the service listens on                                                                  | `15432`                     |
| `resources`                                 | Resource requests and limits for the container                                                        | `{}`                        |
| `gatewaydPluginsConfig.enabled`             | Determines whether the `gatewayd_plugins.yaml` ConfigMap is mounted to the container. If enabled, a volume and volumeMount are added to the deployment. | `false`                     |
| `nodeSelector`                              | Node selector for the pod                                                                             | `{}`                        |
| `affinity`                                  | Affinity for the pod                                                                                  | `{}`                        |
| `tolerations`                               | Tolerations for the pod                                                                               | `[]`                        |
| `ingress.enabled`                           | Determines whether an Ingress resource should be created                                               | `false`                     |
| `gatewayd.fullname`                         | The full name of the deployment, used as part of the Ingress resource name                             |                             |
| `service.port`                              | The port that the service listens on, used as the service port in the Ingress rules                    |                             |
| `ingress.className`                         | The Ingress class to assign to the Ingress resource. This is only used for Kubernetes versions less than 1.18.                                                     |                             |
| `ingress.annotations`                       | Annotations to add to the Ingress resource. If `ingress.className` is set and the Kubernetes version is less than 1.18, the `kubernetes.io/ingress.class` annotation is added with the value of `ingress.className`. | `{}`                        |
| `Capabilities.KubeVersion.GitVersion`       | The Kubernetes version running in the cluster. This is used to determine the API version of the Ingress resource to create.                                       |                             |
| `gatewayd.fullname`                         | The full name of the deployment, used as the target of the Horizontal Pod Autoscaler.                                                                             |                             |
| `autoscaling.minReplicas`                   | The minimum number of replicas that the Horizontal Pod Autoscaler should maintain                      |                             |
| `autoscaling.maxReplicas`                   | The maximum number of replicas that the Horizontal Pod Autoscaler can scale out to                    |                             |
| `autoscaling.targetCPUUtilizationPercentage`| The target percentage of CPU utilization across all replicas that the Horizontal Pod Autoscaler should maintain. If set, a CPU utilization metric is added to the Horizontal Pod Autoscaler. |                             |
| `autoscaling.targetMemoryUtilizationPercentage`| The target percentage of memory utilization across all replicas that the Horizontal Pod Autoscaler should maintain. If set, a memory utilization metric is added to the Horizontal Pod Autoscaler. |                             |
| `gatewayd.fullname`                         | The full name of the deployment, used as the name of the Service.                                      |                             |
| `gatewayd.labels`                           | The labels to apply to the Service.                                                                    |                             |
| `service.type`                              | The type of the Service. Common types include `ClusterIP`, `NodePort`, and `LoadBalancer`.             |                             |
| `service.port`                              | The port that the Service listens on. This is the port that other services in the cluster use to communicate with this Service.                                  |                             |
| `gatewayd.selectorLabels`                   | The selector for the Service. This should match the labels of the Pods that the Service should route traffic to.                                                   |                             |
| `serviceAccount.create`                     | Determines whether a ServiceAccount should be created                                                  |                             |
| `gatewayd.serviceAccountName`               | The name of the ServiceAccount. This is used as the name of the ServiceAccount resource.                |                             |
| `gatewayd.labels`                           | The labels to apply to the ServiceAccount.                                                             |                             |
| `serviceAccount.annotations`                | Annotations to add to the ServiceAccount.                                                              |                             |
| `serviceAccount.automount`                  | Determines whether the ServiceAccount token should be automatically mounted to the pods. This is set as the `automountServiceAccountToken` field in the ServiceAccount resource. |                             |
| `gatewayd.fullname`                         | The full name of the deployment, used as the name of the ConfigMap.                                    |                             |
| `gatewayd.clients.default.address`          | The default address for the gatewayd clients. This is set as the `GATEWAYD_CLIENTS_DEFAULT_ADDRESS` data in the ConfigMap.                                        |                             |
| `gatewayd.loggers.default.level`            | The default level for the gatewayd loggers. This is set as the `GATEWAYD_LOGGERS_DEFAULT_LEVEL` data in the ConfigMap.                                              |                             |
| `gatewaydPluginsConfig.enabled`             | Determines whether the `gatewayd_plugins.yaml` ConfigMap should be created.                             |                             |
| `.Release.Name`                             | The release name, used as part of the ConfigMap name.                                                  |                             |
| `gatewaydPluginsConfig.content`             | The content of the `gatewayd_plugins.yaml` file. This is set as the `gatewayd_plugins.yaml` data in the ConfigMap.                                                  |                             |

## Usage

Modify the [values.yaml](values.yaml) file to customize the deployment according to your requirements. You can override any default values as needed.

## Contributing

Feel free to contribute to the development of this Helm chart by submitting issues or pull requests to the GitHub repository.
