# Workshop Industrialisation des déploiements dans Azure avec Terraform 

tags: #workshop #aks #github #terraform

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/logoworkshop.jpg'/> 

## Jour 1 

### Matin
- Introduction à Terraform (jusqu'à output et datasources)
- [Lab 1 : création d'un compte de stockage + containers](/Terraform/Lab1_Compte_de_Stockage/README.md) </a>
- [Lab 2 :  création d'une VM   + utilisation du Storage Backend + utilisation](/Terraform/Lab2_VM/README.md)
- Question / Réponses : automatisation principe généraux CI/CD, Terraform Cloud...

### Après midi
- Introduction à GitHub (Repo + Workflow)
- [Lab 3 : simple pipeline](/Pipelines/Lab3_Simple_Pipeline/README.md)
- [Lab 4 : pipeline CI-CD terraform](/Terraform/Lab4_Pipeline_CI_CD_Terraform/README.md)


<img width='800' src='/images/Workshop-aks-day-1.png'/> 

---

## Jour 2
### Matin
- Introduction aux micro services
- Introduction ou rappels sur Kubernetes
- Introduction à Azure Kubernetes Services
- [Lab 5 : Déploiement Azure Container Registry](/Terraform/Lab5_Azure_Container_Registry/README.md)
- [Lab 6 : Déploiement Azure Kubernetes Service](/Terraform/Lab6_Azure_Kubernetes_Service/README.md)

### Après midi
- Rappels sur les déploiements Kubernetes : (YAML, Helm) et pipelines
- Focus/explication sur les Pipelines de Build 
- [Lab 7 : Pipeline de build (CI) d'une application conteneurisée](/Pipelines/Lab7_Pipeline_de_Build/README.md)
- Focus/explication Pipeline de release
- [Lab 8 : Pipeline de release d'une application dans Kubernetes](/Pipelines/Lab8_Pipeline_de_Release/README.md)
- [Lab 9 : Pipeline de release d'une application dans Kubernetes Advanced (analyse manifest YML...)](/Pipelines/Lab9_Pipeline_de_Release_Advanced)
- [Lab 10 : Déploiement dans Kubernetes avec Terraform](/Terraform/Lab10_Kubernetes_avec_Terraform/README.md)

---
## Pré requis

### Avoir un abonnement (subscription Azure) et les privilèges administrator

**/!\ L'ensemble des Labs peuvent être faits en utilisant Azure Cloud Shell.**

Informations complémentaires sur Azure Cloud Shell : https://docs.microsoft.com/en-us/azure/cloud-shell/overview 

## Créer une clé SSH (si vous n'en avez pas déjà)

Ouvrir un Azure Cloud Shell. Si c'est la première utilisation d'Azure Cloud Shell, valider la création d'un compte de stockage (qui contiendra les données du profil).

se placer sur le répertoire home :    cd

ssh-keygen -t rsa 


### Créer un Service Principal dans Azure

az login

az account list -o table

Récupérer l'ID de la subscription Azure puis exécuter la commande suivante :

az ad sp create-for-rbac --name "votrenom-demo-githubaction2022" --role "Contributor" --sdk-auth true --scopes /subscriptions/METTRE_ICI_L_ID_DE_LA_SUBSCRIPTION -o jsonc

cf. https://learn.microsoft.com/en-us/cli/azure/ad/sp?view=azure-cli-latest#az-ad-sp-create-for-rbac

Récupérer le output de la commande et le sauvegarder temporairement dans un fichier 

---

## Forker le repo du workshop

Ouvrir un navigateur Web et se connecter sur github.com avec un identifiant

Ouvrir un nouvel onglet web et aller sur ce repo : https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days

Cliquer le bouton Fork

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-fork.jpg'/> 

le repo est forké dans votre environnement github

Mettre la clé SSH (la partie publique dans le fichier id_rsa.pub) dans les paramètres du compte github

<img width='300' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-ssh1.jpg'/> 

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-ssh2.jpg'/> 

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-ssh3.jpg'/> 

## Cloner votre fork sur votre poste local

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-gitclone1.jpg'/> 

<img width='800' src='https://github.com/FrenchBarbusCorp/Workshop-Terraform-AKS-2days/blob/main/images/lab0-gitclone2.jpg'/>



## Installation des composants nécessaires pour travailler sur un poste local

### Avoir un environnement Bash 
- Pour ceux sous Windows 10/11 : Installation WSL2 https://docs.microsoft.com/en-us/windows/wsl/install

### Avoir les outils suivants installés dans WSL : 
- git -> https://git-scm.com/book/en/v2/Getting-Started-Installing-Git 
- Azure CLI -> https://docs.microsoft.com/fr-fr/cli/azure/install-azure-cli-linux?pivots=apt (test: ~$  az Login)
- terraform -> https://learn.hashicorp.com/tutorials/terraform/install-cli (test : ~$ terraform)

Procédure d'installation de la CLI Terraform pour Linux (WSL Ubuntu 20.04)
```
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install terraform
```

- kubectl -> https://kubernetes.io/docs/tasks/tools/#kubectl
- Visual Studio Code -> https://code.visualstudio.com
- Extension Terraform pour VSCode -> Depuis le bash, exécuter « code . » et aller chercher l’extension « Hashicorp Terraform »
- Extension WSL pour VSCode -> https://code.visualstudio.com/docs/remote/wsl-tutorial

