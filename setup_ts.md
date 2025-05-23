### Set Up GPDTS Environment

```
eval $(minikube -p minikube docker-env)
```
### Create Namespace
```
kubetctl create ns jmeter
```
### Configure Kubernetes Namespace

```
kubectl config set-context --current --namespace=jmeter
```
### Uninstall Existing Helm Release
```
helm -n jmeter uninstall <release-name>
```
### Install/Upgrade Helm Chart
```
helm -n jmeter upgrade --install gpdts-jmeter /Users/nikolett.palyi/Documents/DEV/gpdts-configrepo-aws-ppb/cdk/resources/gpdts --values /Users/nikolett.palyi/Documents/DEV/gpdts-configrepo-aws-ppb/cdk/resources/gpdts/values.yaml
```
### Copy JMeter Test Plans to Master Pod
```
kubectl cp <local-path-to-baseline-test-plan> <namespace>/<master-pod-name>:/tmp/
kubectl cp <local-path-to-stress-test-plan> <namespace>/<master-pod-name>:/tmp/
```
### Configure Keystore in Master Pod
```
kubectl exec -n <your-namespace> -it <master-pod-name> -- sh -c 'echo "server.rmi.ssl.disable=true" >> /opt/apache-jmeter-5.6.3/bin/user.properties'
```
### Verify Files in /tmp Directory
```
kubectl exec -n <your-namespace> <master-pod-name> -- ls -l /tmp/
```
### Test Connectivity to Worker Pods
```
kubectl exec -n <your-namespace> <master-pod-name> -- ping -c 4 <worker-pod-ip>
```
### Run JMeter Tests
Baseline Test Plan:
```
kubectl exec -n <your-namespace> <master-pod-name> -- jmeter -n -t "/tmp/GPDCS Baseline Test Plan.jmx" -R <worker-service-name> -l /tmp/result.jtl -j /tmp/jmeter.log
```
Stress Test Plan:
```
kubectl exec -n <your-namespace> <master-pod-name> -- jmeter -n -t "/tmp/GPDCS Stress Test Plan.jmx" -R <worker-service-name> -l /tmp/result.jtl -j /tmp/jmeter.log
```
### Copy Results to Local Machine
```
kubectl cp <namespace>/<master-pod-name>:/tmp/result.jtl <local-results-path>/result.jtl
kubectl cp <namespace>/<master-pod-name>:/tmp/jmeter.log <local-results-path>/jmeter.log
```
