# kubectl-anoujean #

***ALIAS : jackwire***

# Création du pod redis #
1/ récupération de l'image
```
image: redis
```

2/ affectation au port 6379 (port par défaut)
```
ports:
    - containerPort: 6379
```

# Création du service du pod de redis #
Garder le même nom que le pod ainsi que le port (6379)
```
app: jackwire-redis
...
ports:
    - port: 6379
      targetPort: 6379
```

# Création du pod du serveur node #
1/ récupération de l'image 

```
image: cloud.canister.io:5000/arhturescriou/node-redis
```

2/ ne pas oublier la clé vu que c'est une image privée
```
imagePullSecrets:
    - name: regcred
```

3/récupération de l'ip
```
>> kubectl get services
jackwire-redis              LoadBalancer   10.3.27.122    <pending>         6379:32749/TCP   7s
```

# Les commandes pour créer, supprimmer et appliquer les modifications des pods et du service #

```
kubectl create -f pod-redis-anoujean.yaml
kubectl delete -f pod-redis-anoujean.yaml
kubectl apply -f pod-redis-anoujean.yaml

kubectl create -f service-redis-anoujean.yaml
kubectl delete -f service-redis-anoujean.yaml
kubectl apply -f service-redis-anoujean.yaml


kubectl create -f pod-node-anoujean.yaml
kubectl delete -f pod-node-anoujean.yaml
kubectl apply -f pod-node-anoujean.yaml
```

# Véfifier que le résultat est présent#

```
>> kubectl logs jackwire-node-redis
redis connected to redis://10.3.27.122:6379
listening at http://localhost:8080
```

