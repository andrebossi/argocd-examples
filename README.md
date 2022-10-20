# Instalação ArgoCD

[ArgoCD Helm](https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd)

### Instalação ArgoCD HA - CRDs
```bash
helm install -n argocd \
    --create-namespace \
    argo-ha argo-cd \
    --repo https://argoproj.github.io/argo-helm \
    -f argo-scale-values.yml
```

### Map port Kind (Kubernetes in Docker)
```bash
kubectl port-forward services/argo-ha-argocd-server -n argocd 8080:80
```

### Obter primeira senha
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

# Install ArgoCD Resources

Os recursos do Argo sempre devem ser instalados no namespace do Argo ou usar a label **app.kubernetes.io/part-of: argocd**

```bash
kubectl apply -f application-deploy.yml
```