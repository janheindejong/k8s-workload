# Kubernetes workload 

This is a mock project, to play a bit with deploying workloads to k8s. 

## Grafana & Loki 

Loki is a log aggregation tool - like prometheus, but for logs - that can be added as a datasource in Grafana. 

Deploying it is really easy. Create a values file: 

```yaml 
loki: 
  commonConfig: 
    replicatio_factor: 1
  storage: 
    type: 'filesystem' 
``` 

Add Grafana repository for Helm: 

```powershell 
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update 
``` 

Install Grafana and Loki 
``` 
helm install loki --namespace=loki-stack loki/loki-stack --create-namespace
helm install grafana --namespace=grafana grafana/grafana --create-namespace
```

Now, you can log into Grafana, and add Loki as a datasource. Since it runs in the `loki-stack` namespace, you can access it from within the cluster at `http://loki.loki-stack.local`. 

## ELK stack 

I'm trying to deploy ELK stack to minikube, but this is not very succesful thusfar. Perhaps I'm trying the wrong thing. 

Anyway, to deploy ELK-stack, use helm: 

```powershell
helm repo add elastic elastic.helm.io 
helm repo update 

helm install elasticsearch elastic/elasticsearch -n elastic --create-namespace -f values.yml 
helm install kibana elastic/kibana -n elastic
```

I used a values file from the `/examples/minikube` directory in the repository. However, I had to increase the memory allocated to each elasticseach pod. 

Anyway, it doesn't seem to be the right tool for us, and Loki is a better alternative. 

