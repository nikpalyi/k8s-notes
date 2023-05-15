# eval-docker-helm
command for local testing docker image , helm

```
minikube docker-env
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
