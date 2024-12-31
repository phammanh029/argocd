# argocd

# Setup

## Setup k8s
1. `minikube start`
2. `kubectl create namespace argocd`
3. `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
4. export service of argo cd:
`kubectl port-forward svc/argocd-server -n argocd 8080:443`
5. Add gitea
```
helm repo add gitea-charts https://dl.gitea.io/charts/
helm repo update
kubectl create namespace gitea
helm install gitea gitea-charts/gitea --namespace gitea -f gitea/values.yaml
kubectl port-forward svc/gitea-http -n gitea 3000:3000

```
6. Get password for argocd
`kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d`
7. Forward port: `kubectl port-forward svc/argocd-server -n argocd 8080:443` then we can login at http://localhost:8080 with user `admin` and password that you've get from step 6