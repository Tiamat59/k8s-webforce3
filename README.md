# k8s-webforce3

## Check
```shell script
  kubectl get nodes
  kubectl get node
  kubectl get node -o wide

## Deployment example
  kubectl create deployment nginx --image=nginx
  kubectl get deployments
  kubectl describe deployment nginx
  kubectl get events
  kubectl get deployment nginx -o yaml 
  kubectl get deployment nginx -o yaml > first.yaml
```

## les lignes grises ont été supprimé

## Delete le deployment
```
 kubectl delete deployments.apps nginx

## crée un nouveau deployment par rapport au fichier modifié

k create -f first.yaml

  kubectl create deployment two --image=nginx --dry-run -o yaml
  kubectl get deployment nginx --export -o yaml


### aprés modification du yaml pour réimporter la conf si le deployment existe

kubectl replace -f first.yaml
kubectl get deploy,pod
## expose le port configuré dans first.yaml
kubectl expose deployment/nginx
## services
kubectl get svc nginx
```