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
kubectl delete svc nginx
# on recré le service en mode loadbalancer
kubectl expose deployment nginx --type=LoadBalancer
# on affiche les services
kubectl get svc 


# pour retrouver le dashboard dans les service caché (différent namespace)
kubectl get svc -A
# récupérer le token pour la connexion au dashboard
kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep admin-user | awk '{print $1}' )
```

#### Quand on delete un deployment le pod est delete mais pas les service et le endpoints qu'il faut supprimer à la main

## CPU an Limits
```shell script
 k create deployment hog --image vish/stress
```

## Namespace
```shell script
# crée un namespace nomé low-usage-limit
kubectl create namespace low-usage-limit
# Affiche les namespace
kubectl get namespace
# crée un namespace avec le fichier
kubectl --namespace=low-usage-limit create -f low-ressources-range.yaml
# affiche limit des ressources configuré
kubectl get limitrange -A
# crée dans le namespace low-usage-limit un deploiment "limited-hog" avec l'image vish-stress
kubectl -n low-usage-limit create deployment limited-hog --image vish/stress
# filtre l'affichage des pods sur notre namespace
kubectl get pods -n low-usage-limit
# affiche la conf du pod limited-hog de notre namespace (on voix notre conf precedente
kubectl get  -n low-usage-limit pod limited-hog-5c8d494fc5-gvzsd --export -o yaml
```

## Replicaset
```shell script
# affiche tout les replicaset
kubectl get replicasets -A (ou -n Nom_Namespace)
# crée un replicaset a partir de notre fichier
k create -f rs-one.yaml 
# décris le replicaset
k describe replicasets.apps rs-one
# edit un pod
k edit pod rs-one-bs96s
# affiche et ajoute la colonne system (on voix replicaOne et Isolated
k get pod -L system
# editer le tag labels system et mettre isolated
# au delete du replica le pod isolé survis et ne redémarre pas en cas de suprression du pod
# supprime tout les pod isolé
k delete po -l system=IsolatedPod
```

## DaemonSet
```shell script
# les daemon sont repartis sur tout les noeud (ex application supervision)
k create -f ds.yaml
```