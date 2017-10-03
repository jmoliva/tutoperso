
### Installer VTiger sur Bluemix avec Docker/Kubernetes
Déploiement d'une image VTiger sur l'environnement Bluemix

1. Se connecter à Bluemix
1. Créer un cluster kubernetes :
```
bx cs cluster-create --name JMOcluster
```
Output:
```
OK
Name         ID                                 State       Created          Workers   Datacenter   Version
JMOcluster   ab68df3d7c8045e097651e33fd544731   deploying   11 seconds ago   0         hou02        1.7.4_1502
```
Attendre que le cluster soit provisionné. La commande permet de lister l'état du cluster et des workers nodes :
```
bx cs workers JMOcluster
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

```
