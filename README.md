# Kubernetes workload 

This is a mock project, to play a bit with deploying workloads to k8s. 

## ELK stack 

I'm trying to deploy ELK stack to minikube, but this is not very succesful thusfar. Perhaps I'm trying the wrong thing. 

Anyway, to deploy ELK-stack, use helm: 

```powershell
helm repo add elastic elastic.helm.io 
helm repo update 

helm install elasticsearch elastic/elasticsearch -n elastic --create-namespace -f values.yml 
helm install kibana elastic/kibana -n elastic
```

The valuefile for elasticsearch should contain an option for allowing it to run on a single node, otherwise they will keep pending. 



