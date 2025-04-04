# Install metal lb

```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.14.5/config/manifests/metallb-native.yaml
```

Apply the config
```
kubectl apply -f metallb-config.yaml
```

--- 

# Install cert-manager

Add Helm Repo

```
helm repo add jetstack https://charts.jetstack.io
helm repo update
```

Install cert-manager
```
helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.14.4 \
  --set installCRDs=true
```

# Apply ClusterIssuer
```
kubectl apply -f letsencrypt-clusterissuer.yaml
```

# Install Traefik
Add Helm Repo
```
helm repo add traefik https://traefik.github.io/charts
helm repo update
```
Install Traefik with values
```
helm install traefik traefik/traefik --namespace traefik --create-namespace -f traefik-values.yaml
```

# Install Demo Web Service (nginx)
```
kubectl apply -f nginx.yaml
```
Create Ingress
```
kubectl apply -f nginx-ingress.yaml
```