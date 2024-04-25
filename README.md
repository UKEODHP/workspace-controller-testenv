# Workspace Controller Test Environment

## Installation

The test environment assumes that the workspace controller is either being run locally or has been manually deployed to the test cluster. See the [workspace controller readme](https://github.com/UKEODHP/workspace-controller.git/README.md) for details.

### Minikube

```bash
minikube start -p workspaces --addons ingress
```

### Test Environment

```bash
kubectl apply -k apps/argocd  # install argocd
kubectl apply -f platform/    # install argocd applications
```

Access the ArgoCD UI with:

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
kubectl port-forward service/argocd-server -n argocd 8080:443
```

### Delete the Environment

```bash
kubectl delete -f platform/
minikube delete -p workspaces
```
