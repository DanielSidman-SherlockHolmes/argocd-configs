# kube-configs
This repo contains my Kube configurations to demo ArgoCD


## Command

```sh
kubectl apply -f .\webapp.yaml
```

### To make the service IP externally accessible
```sh
minikube service webapp-service
```

### Load local docker image in minikube
```sh
# setup docker-env
minikube docker-env

# load your local image with tag 
minikube image load <docker-image>:<tag>

#Listout Images
minikube image ls --format table

# Apply your Deployment on k8s
kubectl apply -f webapp.yaml
```

### Install ArgoCD in MINIKUBE
```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Access ArgoCD UI
```sh
# we can use minikube command
minikube service argocd-server -n argocd

or
# kubectl port forward
# get all running services
kubectl get svc -n argocd
# forward port to 8080
kubectl port-forward -n argocd svc argocd-server 8080:443
```

- In UI we have username/password.
> - username will be 'admin'.
> - password will be found in kubernetes secret. you have to convert base64 encoded string to decoded string.

```sh
# Get all the secrets
kubectl get secret -n argocd

# Get password in argocd-initial-admin-secret secret with Base64.
kubectl get secret -n argocd argocd-initial-admin-secret -o yaml
```