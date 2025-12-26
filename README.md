# Grafana OTEL LGTM Helm Chart

This Helm chart deploys the Grafana OTEL LGTM stack using the `grafana/otel-lgtm` Docker image.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+

## Installation

```bash
helm install grafana-otel-lgtm ./helm/grafana-otel-lgtm
```

## Configuration

The following table lists the configurable parameters and their default values:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Docker image repository | `grafana/otel-lgtm` |
| `image.tag` | Docker image tag | `latest` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Kubernetes service type | `ClusterIP` |
| `service.ports` | Service ports configuration | See values.yaml |
| `ingress.enabled` | Enable ingress | `false` |
| `resources.limits` | Resource limits | See values.yaml |
| `resources.requests` | Resource requests | See values.yaml |
| `autoscaling.enabled` | Enable horizontal pod autoscaling | `false` |

## Ports

The chart exposes the following ports:

- **3000**: Grafana web interface
- **4317**: OTLP gRPC endpoint
- **4318**: OTLP HTTP endpoint

## Accessing Grafana

### Port Forwarding

```bash
kubectl port-forward service/grafana-otel-lgtm 3000:3000
```

Then access Grafana at `http://localhost:3000`

### Using Ingress

Enable ingress in `values.yaml`:

```yaml
ingress:
  enabled: true
  className: "nginx"
  hosts:
    - host: grafana.example.com
      paths:
        - path: /
          pathType: Prefix
```

## Uninstallation

```bash
helm uninstall grafana-otel-lgtm
```

