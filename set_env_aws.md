# Set ENV details

## Example: 
gpdes

NXT
Cluster

```
aws eks update-kubeconfig --name Rttk8sNxt-v2 --region eu-west-1
```

Namespace
```
kubectl config set-context --current --namespace=gpdes-nxt
```

PRD
Cluster

```
aws eks update-kubeconfig --name Rttk8sPrd-v2 --region eu-west-1
```
Namespace
```
kubectl config set-context --current --namespace=gpdes-prd
```
