
# Installer VTiger sur Bluemix avec Docker/Kubernetes
Déploiement d'une image VTiger sur l'environnement Bluemix

## Création du cluster kubernetes
### Connexion à Bluemix
Se connecter à Bluemix en ligne de commande (sous windows dans le ```Docker QuickStart Terminal```) et sélectionner une organisation et un espace
### Création du Cluster Kubernetes
Créer le cluster kubernetes
```
bx cs cluster-create --name <cluster-name>
```
Output:
```
OK
Name         ID                                 State       Created          Workers   Datacenter   Version
<cluster-name>   ab68df3d7c8045e097651e33fd544731   deploying   11 seconds ago   0         hou02        1.7.4_1502
```
Attendre que le cluster soit provisionné. La commande `bs workers` permet de lister l'état du cluster et des workers nodes :
```
bx cs workers <cluster-name>
```
Les différentes sorties sont:
```
ID                                                 Public IP   Private IP   Machine Type   State               Status                              Version
kube-hou02-paab68df3d7c8045e097651e33fd544731-w1   -           -            free           provision_pending   Waiting for master to be deployed   1.7.4_1502

ID                                                 Public IP   Private IP   Machine Type   State          Status                     Version
kube-hou02-paab68df3d7c8045e097651e33fd544731-w1   -           -            free           provisioning   Provisioning in progress   1.7.4_1502

ID                                                 Public IP         Private IP     Machine Type   State           Status                    Version
kube-hou02-paab68df3d7c8045e097651e33fd544731-w1   184.172.214.129   10.76.92.206   free           bootstrapping   Configuring Kubectl CLI   1.7.4_1502

ID                                                 Public IP         Private IP     Machine Type   State      Status                         Version
kube-hou02-paab68df3d7c8045e097651e33fd544731-w1   184.172.214.129   10.76.92.206   free           deployed   Deploy Automation Successful   1.7.4_1502

ID                                                 Public IP         Private IP     Machine Type   State    Status   Version
kube-hou02-paab68df3d7c8045e097651e33fd544731-w1   184.172.214.129   10.76.92.206   free           normal   Ready    1.7.4_1502
```
### Récupération de la configuration Kubernetes
Mettre à jour la configuration Kubernetes pour utiliser la commande ```kubectl``` sur le cluster
```
bx cs cluster-config <cluster-name>
```
### Vérification ou création de votre namespace dans la registry Bluemix
Vérifier si vous avez déjà défini un namespace dans la registry Bluemix
```
bx cr namespace-list
```
Si vous n'aviez pas déjà créé un namespace (la liste est vide), définissez le maintenant
```
bx cr namespace-add <your-namespace>
```
## Récupération de l'image
On récupère l'image docker de la dernière version de VTiger 7.0.1 sur DockerHub <a href="https://hub.docker.com/r/ldavid/vtiger7/" target="_blank"></a>
```
docker pull ldavid/vtiger7
```

## Création des volumes persistants de stockage pour la base et pour Vtiger
