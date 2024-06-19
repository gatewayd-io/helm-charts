# Kubernetes Helm Charts for GatewayD

This Helm charts installs GatewayD on your Kubernetes cluster.

## How to use the charts

1. Clone this repository
2. Install the chart
3. (Optionally) Uninstall the chart

```bash
git clone https://github.com/gatewayd-io/helm-charts.git
cd helm-charts/charts/gatewayd/
helm install gatewayd-release -f values.yaml ./
# Optionally, if you want to remove GatewayD from your cluster
# helm uninstall gatewayd-release
```

## Configurations

### Deployment Configuration

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
| `resources`                                 | Resource requests and limits for the container                                                        | `{}`                        |
| `gatewaydPluginsConfig.enabled`             | Determines whether the `gatewayd_plugins.yaml` ConfigMap is mounted to the container. If enabled, a volume and volumeMount are added to the deployment. | `false`                     |
| `gatewaydConfig.enabled`             | Determines whether the `gatewayd.yaml` ConfigMap is mounted to the container. If enabled, a volume and volumeMount are added to the deployment. | `false`                     |
| `nodeSelector`                              | Node selector for the pod                                                                             | `{}`                        |
| `affinity`                                  | Affinity for the pod                                                                                  | `{}`                        |
| `tolerations`                               | Tolerations for the pod                                                                               | `[]`                        |

### Service Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `service.port`                              | The port that the service listens on                                                                  | `15432`                     |
| `ingress.enabled`                           | Determines whether an Ingress resource should be created                                               | `false`                     |

### Ingress Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `gatewayd.fullname`                         | The full name of the deployment, used as part of the Ingress resource name                             |                             |
| `service.port`                              | The port that the service listens on, used as the service port in the Ingress rules                    |                             |
| `ingress.className`                         | The Ingress class to assign to the Ingress resource. This is only used for Kubernetes versions less than 1.18.                                                     |                             |
| `ingress.annotations`                       | Annotations to add to the Ingress resource. If `ingress.className` is set and the Kubernetes version is less than 1.18, the `kubernetes.io/ingress.class` annotation is added with the value of `ingress.className`. | `{}`                        |
| `Capabilities.KubeVersion.GitVersion`       | The Kubernetes version running in the cluster. This is used to determine the API version of the Ingress resource to create.                                       |                             |

### Autoscaling Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `gatewayd.fullname`                         | The full name of the deployment, used as the target of the Horizontal Pod Autoscaler.                                                                             |                             |
| `autoscaling.minReplicas`                   | The minimum number of replicas that the Horizontal Pod Autoscaler should maintain                      |                             |
| `autoscaling.maxReplicas`                   | The maximum number of replicas that the Horizontal Pod Autoscaler can scale out to                    |                             |
| `autoscaling.targetCPUUtilizationPercentage`| The target percentage of CPU utilization across all replicas that the Horizontal Pod Autoscaler should maintain. If set, a CPU utilization metric is added to the Horizontal Pod Autoscaler. |                             |
| `autoscaling.targetMemoryUtilizationPercentage`| The target percentage of memory utilization across all replicas that the Horizontal Pod Autoscaler should maintain. If set, a memory utilization metric is added to the Horizontal Pod Autoscaler. |                             |

### Service Account Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `serviceAccount.create`                     | Determines whether a ServiceAccount should be created                                                  |                             |
| `gatewayd.serviceAccountName`               | The name of the ServiceAccount. This is used as the name of the ServiceAccount resource.                |                             |
| `gatewayd.labels`                           | The labels to apply to the ServiceAccount.                                                             |                             |
| `serviceAccount.annotations`                | Annotations to add to the ServiceAccount.                                                              |                             |
| `serviceAccount.automount`                  | Determines whether the ServiceAccount token should be automatically mounted to the pods. This is set as the `automountServiceAccountToken` field in the ServiceAccount resource. |                             |

### Pod Disruption Budgets Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `podDisruptionBudget.minAvailable`                   | Specifies the minimum number of pods from the set that must still be available after the eviction, even in the absence of the evicted pod.                      |        `1`                   |
| `podDisruptionBudget.maxUnavailable`                   | Specifies the maximum number of pods from the set that can be unavailable after the eviction. It can be either an absolute number or a percentage.                    |                             |

### ConfigMap Configuration

| Parameter                                   | Description                                                                                           | Default Value               |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|-----------------------------|
| `gatewayd.fullname`                         | The full name of the deployment, used as the name of the ConfigMap.                                    |                             |
| `.Release.Name`                             | The release name, used as part of the ConfigMap name.                                                  |                             |
| `files/gatewayd_plugins.yaml`             | The content of the `gatewayd_plugins.yaml` file. This is set as the `gatewayd_plugins.yaml` data in the ConfigMap.                                                  |                             |
| `files/gatewayd.yaml`             | The content of the `gatewayd.yaml` file. This is set as the `gatewayd.yaml` data in the ConfigMap.                                                  |                             |

## Usage

Modify the [values.yaml](values.yaml) file to customize the deployment according to your requirements. You can override any default values as needed. Please refer to GatewayD [documentation](https://docs.gatewayd.io/getting-started/welcome) for more information.

## Contributing

We welcome contributions from everyone. Just open an [issue](https://github.com/gatewayd-io/helm-charts/issues) or send us a [pull request](https://github.com/gatewayd-io/helm-charts/pulls).

## License

GatewayD Helm Charts is licensed under the [Apache 2.0 License](https://github.com/gatewayd-io/helm-charts/blob/main/LICENSE).
