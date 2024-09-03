# kubernetes-sa-token-stress-test
Kubernetes Service Account renewal load test for renewal jitter value


[requirements posts](https://blog.hyunwoo.monster/kubernetes-kubelet-serviceaccounttoken-jiteo-gabs-gaeseon/)


## 1. Deploying Token Load Test
kubectl apply -f token-renewal-load-test.yaml

## 2. Deploying Monitoring(windows11 + wsl2)
```
# deploying monitoring tools
sudo apt-get install socat
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
# serving monitoring tools
kubectl port-forward --namespace monitoring svc/prometheus-grafana 3000:80
socat TCP-LISTEN:3001,fork TCP:localhost:3000
# get grafana password
kubectl get secret --namespace monitoring prometheus-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
