# ArgoCD Test Repo

## Deploy ArgoCD
```bash
# install argocd
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
k create namespace argocd
helm install argocd argo/argo-cd --namespace argocd
k get all -n argocd
k port-forward svc/argocd-server -n argocd 8080:443
# username: admin
# password
k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Test Deploy Helm
```bash
helm install helloworld-release ./helm-chart
k get pod helloworld-pod
k logs helloworld-pod
helm uninstall helloworld-release
```