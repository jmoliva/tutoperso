
# Installer VTiger sur Bluemix avec Docker/Kubernetes
Déploiement d'une image VTiger sur l'environnement Bluemix
- Les commandes `bx cs` font appel au plugin **Container Service** de Bluemix
- Les commandes `bx cr` font appel au plugin **Container Regitry** de Bluemix

## Pre-requis

+ Avoir un [Bluemix IBM id](https://bluemix.net)
+ Installer la [Bluemix CLI](http://clis.ng.bluemix.net)
+ Installer docker for [Mac](https://docs.docker.com/engine/installation/mac/) or [Windows](https://docs.docker.com/engine/installation/windows/)
+ Installer [Kubectl](https://kubernetes.io/docs/user-guide/prereqs/)

## 1. Création du cluster kubernetes
### 1.1 Connexion à Bluemix
Se connecter à Bluemix en ligne de commande et sélectionner une organisation et un espace.

_NB : sous Windows utiliser le ```Docker QuickStart Terminal``` de l'installation Docker_
### 1.2 Création du Cluster Kubernetes
Créer le cluster kubernetes si vous n'en avait pas déjà créé un (si la commande `bx cs clusters` ne vous retourne aucun cluster)
```
bx cs cluster-create --name <cluster-name>
```
Output:
```
OK
Name         ID                                 State       Created          Workers   Datacenter   Version
<cluster-name>   ab68df3d7c8045e097651e33fd544731   deploying   11 seconds ago   0         hou02        1.7.4_1502
```
Attendre que le cluster soit provisionné. La commande `bs cs workers` permet de lister l'état du cluster et des workers nodes :
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
### 1.3 Récupération de la configuration Kubernetes
Mettre à jour la configuration Kubernetes pour pouvoir utiliser la commande ```kubectl``` sur le cluster
```
bx cs cluster-config <cluster-name>
```
### 1.4 Vérification ou création de votre namespace dans la registry Bluemix
Se loguer sur le service de registry de Bluemix
```
bx cr login
```
Vérifier si vous avez déjà définie un namespace dans la registry Bluemix
```
bx cr namespace-list
```
Si vous n'aviez pas déjà (la liste est vide), créé un namespace maintenant
```
bx cr namespace-add <your-namespace>
```
## 2. Récupération et push de l'image Vtiger
On récupère une image docker de la dernière version de VTiger 7.0.1 sur DockerHub <https://hub.docker.com/r/ldavid/vtiger7/>
```
docker pull ldavid/vtiger7
```
Une fois l'image récupérée, on va la taguée dans la registry Bluemix
```
docker tag ldavid/vtiger7 registry.ng.bluemix.net/<your-namespace>/vtiger7:1
```
Une fois taguée, l'image peut être poussée dans la registry
```
docker push registry.ng.bluemix.net/<your-namespace>/vtiger7:1
```
à ce moment là l'image est disponible dans Bluemix
```
bx cr images
```
Output :
```
Liste des images...

REFERENTIEL                                   ESPACE DE NOM   ETIQUETTE   CONDENSE       CREE           TAILLE   STATUT DE VULNERABILITE
registry.ng.bluemix.net/<your-namespace>/vtiger7   <your-namespace>     1           dc6492210a9b   3 months ago   230 MB   Vulnérable
```
## 3. Création des volumes persistants de stockage pour la base et pour Vtiger

## 4. Création d'une base compose MySQL
Provisionner le service **Compose for MySQL** à partir de la page du catalogue de Bluemix ici : <https://console.bluemix.net/catalog/services/compose-for-mysql>

![](./images/Test.png)



