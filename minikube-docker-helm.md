# Deploy Your Programs onto Minikube with Docker and Helm

command for local testing an app with docker image , helm


```
minikube start
```

In different terminal window/tab:
```
minikube tunnel
```

At the code repository's folder:

```
eval $(minikube -p minikube docker-env)
```
```
sbt docker:publishLocal
```

Create a namespace, in this case called 'pub':

```
kubectl create namespace gpdcs
```
```
kubectl config set-context minikube --namespace=gpdcs
```

## Local testing, uninstall, deploy, reinstall GPDCS:

```
helm -n gpdcs uninstall gpd-configuration-service
```

```
helm -n gpdcs upgrade --install gpd-configuration-service ./helm/gpdcs --values ./helm/gpdcs/values.yaml
```

## For SGX(EPS):
Create a namespace, in this case called 'pub':

```
kubectl create namespace gpdeps
```
```
kubectl config set-context minikube --namespace=gpdeps
```
```
helm -n gpdeps uninstall gpd-pricing-service
```

```
helm -n gpdeps upgrade --install gpd-pricing-service ./helm/gpdcs --values ./helm/gpdeps/values.yaml
```
