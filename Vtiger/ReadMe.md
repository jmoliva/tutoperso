
### Installer VTiger sur Bluemix avec Docker/Kubernetes
Déploiement d'une image VTiger sur l'environnement Bluemix

1. Se connecter à Bluemix
1. Créer un cluster kubernetes :
bx cs cluster-create --name JMOcluster
```
bx cs clusters
```
Output:
```
OK
Name         ID                                 State       Created          Workers   Datacenter   Version
JMOcluster   ab68df3d7c8045e097651e33fd544731   deploying   11 seconds ago   0         hou02        1.7.4_1502
```

