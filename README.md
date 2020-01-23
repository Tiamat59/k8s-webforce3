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
```shell script
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
  kubectl get ep nginx
## renvoi le node sur lequel tourne notre pod
    kubectl get po -o wide

## scale sur 3 serveur
kubectl scale deployment nginx --replicas=3
kubectl get pod -o wide
kubectl get deployment nginx
## arrete les pod
kubectl scale deployment nginx --replicas=0

kubectl exec nginx-85ff79dd56-jtp8m -- printenv | grep KUBERNETES

# delete le service
k delete svc nginx
# on recré le service en mode loadbalancer
k expose deployment nginx --type=LoadBalancer
# on affiche les services
k get svc 


# pour retrouver le dashboard dans les service caché (différent namespace)
k get svc -A
# récupérer le token pour la connexion au dashboard
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}' )
```

#### Quand on delete un deployment le pod est delete mais pas les service et le endpoints qu'il faut supprimer à la main

## CPU an Limits
```shell script
 k create deployment hog --image vish/stress
```