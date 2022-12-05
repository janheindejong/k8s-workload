# Kubernetes workload 

This is a mock project, to play a bit with deploying workloads to k8s. 

## Grafana & Loki 

Add Grafana repository for Helm: 

```powershell 
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update 
``` 

Install Grafana and Loki:

``` 
helm install loki --namespace=loki-stack grafana/loki-stack --create-namespace -f .\loki-stack\values.yml
helm install grafana --namespace=grafana grafana/grafana --create-namespace -f .\grafana\values.yml
```

Now, you can log into Grafana, and add Loki as a datasource. Since it runs in the `loki-stack` namespace, you can access it from within the cluster at `http://loki.loki-stack.svc.cluster.local`. 
