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

Create a namespace, in this case called 'pub':

```
kubectl create namespace pub
```

## Local testing, restart:

```
helm -n pub uninstall publisher
```

```
eval $(minikube -p minikube docker-env)
```

```
sbt docker:publishLocal
```

```
helm -n pub upgrade --install publisher ./helm/gpd-publisher --values ./helm/gpd-publisher/dev-values.yaml
```
