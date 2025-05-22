# Fixing ArgoCD Repository Error

If you're seeing this error in ArgoCD:

```
Unable to sync: error resolving repo revision: rpc error: code = Unknown desc = failed to list refs: Get "https://your-git-repo-url/yolo-detection.git/info/refs?service=git-upload-pack": dial tcp: lookup your-git-repo-url on 10.96.0.10:53: no such host
```

You need to update the repository URL to point to your actual Git repository. Here are two ways to fix this:

## Option 1: Update values.yaml and use the Helm template

1. Update the `gitRepo.url` in `values.yaml`:

```yaml
gitRepo:
  url: "https://github.com/yourusername/yolo-detection.git"  # Your actual repository URL
  branch: "main"  # Your branch name
```

2. Install with Helm:

```bash
helm install yolo-detection ./prod
```

## Option 2: Use the direct Application manifest

1. Edit the `yolo-detection-argocd-app.yaml` file and update the repository URL:

```yaml
spec:
  source:
    repoURL: https://github.com/yourusername/yolo-detection.git  # Your actual repository URL
```

2. Apply directly to your cluster:

```bash
kubectl apply -f prod/yolo-detection-argocd-app.yaml
```

## Creating a Git Repository

If you don't have a Git repository set up yet:

1. Create a new repository on GitHub, GitLab, or your preferred Git hosting service
2. Push your Helm chart to this repository:

```bash
git init
git add .
git commit -m "Initial commit for YOLO detection Helm chart"
git remote add origin https://github.com/yourusername/yolo-detection.git
git push -u origin main
```

After updating the repository URL and applying the changes, ArgoCD should be able to sync your application successfully. 