# SDTD
# Projet SDTD Ensimag
Apres installation du kops et kubectl
Dans l'exemple on considére que le nom du domaine est "ensimag.com"
**Etape 1: création du nom de domaine**
creation d’un nom de domaine public et configuration des dns en ajoutant les sous services  fournis par le route53 du aws
**Etape 2: creation S3 bucket pour stocker l’état du cluster**
'''aws s3 mb s3://clusters.sdtd.ensimag.com'''
//afin de ne pas la modifier à chaque fois
'''export KOPS_STATE_STORE=s3://clusters.sdtd.ensimag.com'''
**Etape3:creation du cluster**
//création d'un cluster de base avec 3 noeuds dont un est le master
'''kops create cluster --zones=us-east-1c –-name ensimag.com –yes'''
une fois les instances sont lancées il faut valider par 
validating cluster ensimag.com
pour vérifier les nodes 
kubectl get nodes 
**Etape 4:déploiment des images** 

**Etapes 4: déploiment de Flink**
//les ressources sont disponibles
*creation des services:*
'''kubectl create -f flink-configuration-configmap.yaml'''
'''kubectl create -f jobmanager-deployment.yaml'''
'''kubectl create -f taskmanager-deployment.yaml'''
'''kubectl create -f jobmanager-service.yaml'''
