# ArgoCD Test Repo
This repository demonstrates how to deploy a simple application using ArgoCD with dynamic parameters passed through Helm.

## Step 1: Deploy ArgoCD
```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
k create namespace argocd
helm install argocd argo/argo-cd --namespace argocd
k get all -n argocd
k port-forward svc/argocd-server -n argocd 8080:443

# Login to ArgoCD 
# username: admin
# password:
k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Step 2: Deploy the HelloWorld Application Using Helm
```bash
helm install helloworld-release ./helm-chart
k get pod helloworld-pod
k logs helloworld-pod
# Expected Output: Hello from helm values.yaml!
helm uninstall helloworld-release
```

## Step 3: Deploy the HelloWorld Application Using ArgoCD
```bash
k apply -f argocd-application.yaml
k get pod helloworld-pod
k logs helloworld-pod
# Expected Output: Hello from ArgoCD!
```