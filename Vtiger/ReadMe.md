
# Installer VTiger sur Bluemix avec Docker/Kubernetes
Déploiement d'une image VTiger sur l'environnement Bluemix

## Création du cluster kubernetes
1. Se connecter à Bluemix en ligne de commande (sous windows dans le ```Docker QuickStart Terminal```) et sélectionner une organisation et un espace
1. Créer le cluster kubernetes
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
1. Mettre à jour la configuration Kubernetes pour utiliser la commande ```kubectl``` sur le cluster
```
bx cs cluster-config <cluster-name>
```
## Création des volumes persistants de stockage pour la base et pour Vtiger
