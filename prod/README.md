# YOLO Detection Helm Chart

This Helm chart deploys the YOLO Detection application using ArgoCD with auto-scaling capabilities.

## Configuration

The deployment uses the following configurations:

- Image: `luminoussg/yolo-detection:v1`
- LoadBalancer IP: `192.168.31.197` (MetalLB)
- Autoscaling enabled with min 1, max 5 replicas, targeting 80% CPU utilization

## Installation

### Direct Helm Installation

```bash
# Install the chart
helm install yolo-detection ./prod

# Upgrade existing installation
helm upgrade yolo-detection ./prod
```

### Using ArgoCD

1. Make sure ArgoCD is installed in your cluster
2. Update the `repoURL` in `application.yaml` to point to your git repository
3. Apply the ArgoCD Application:

```bash
kubectl apply -f prod/templates/application.yaml
```

## Configuration Parameters

To modify the default configuration, update the `values.yaml` file or provide overrides during installation:

```bash
helm install yolo-detection ./prod --set replicaCount=2 --set autoscaling.maxReplicas=10
```

## Uninstallation

```bash
helm uninstall yolo-detection
``` 