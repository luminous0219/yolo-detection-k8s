# YOLO Detection Kustomize Setup

This is a Kustomize configuration for deploying the YOLO Detection Gradio application.

## Structure

- `base/`: Contains the base Kubernetes manifests
  - `deployment.yaml`: Deployment configuration with resource limits
  - `service.yaml`: Service configuration to expose the application
  - `hpa.yaml`: Horizontal Pod Autoscaler configuration
  - `kustomization.yaml`: Base kustomization file

- `overlays/prod/`: Production environment specific overlays
  - `service-patch.yaml`: Patch to use LoadBalancer with MetalLB IP
  - `kustomization.yaml`: Production kustomization file

## Key Details

- The application runs on port **7860** (Gradio default port)
- LoadBalancer IP: `192.168.31.197` (MetalLB)
- Auto-scaling is enabled (1-5 replicas based on 80% CPU utilization)

## Deployment Options

### Using kubectl directly

```bash
# Preview the resources
kubectl kustomize kustomize/overlays/prod

# Apply the resources
kubectl apply -k kustomize/overlays/prod
```

### Using ArgoCD

Apply the ArgoCD Application:

```bash
kubectl apply -f kustomize/yolo-detection-argocd-app.yaml
```

## Updating the Configuration

1. Make changes to the base or overlay files as needed
2. Commit and push your changes to the repository
3. ArgoCD will automatically detect and apply the changes 