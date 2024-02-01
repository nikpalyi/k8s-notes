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
minikube docker-env
```
or just:
```
eval $(minikube -p minikube docker-env)
```

Create a namespace, in this case called 'pub':

```
kubectl create namespace gpdcs
```
```
kubectl config get-contexts
```
```
kubectl config view
```
```
kubectl config set-context minikube --namespace=gpdcs
```

## Local testing, restart:

```
helm -n gpdcs uninstall gpd-configuration-service
```

```
eval $(minikube -p minikube docker-env)
```

```
sbt docker:publishLocal
```

```
helm -n gpdcs upgrade --install gpd-configuration-service ./helm/gpd-configuration-service --values ./helm/gpd-configuration-service/dev-values.yaml
```
