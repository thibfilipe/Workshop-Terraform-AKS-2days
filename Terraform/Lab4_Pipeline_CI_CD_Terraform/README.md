# Lab 4 : Pipeline GitHub Action avec Terraform

Objectif : Déploiement d'un resource group Azure depuis un GitHub Workflow traitant du code Terraform

Pré requis : avoir un Service Principal Azure 

## Préparer les secrets  GitHub

Générer un token SAS sur le **container tfstate** du compte de stockage créé dans le Lab 1. Donner les permissions suivantes au token : read, add, create, write, List

Procédure : https://docs.microsoft.com/en-us/azure/cognitive-services/translator/document-translation/create-sas-tokens?tabs=Containers#create-your-tokens

Le token SAS doit ressembler à ce genre de chaine :  __sp=racwl&st=2022-03-11T14:00:27Z&se=2022-03-11T22:22:27Z&spr=https&sv=2020-08-04&sr=c&sig=vHXCwdRCoLpiRsLPURDd%2F2t3g8vQRiKCBM8qFrGsML0%3D__

Copier le token SAS dans un secret GITHUB appelé **BACKENDSTORAGESASTOKEN**

Procédure pour créer un secret GitHub : https://github.com/Azure/actions-workflow-samples/blob/master/assets/create-secrets-for-GitHub-workflows.md

De la même manière, créer 4 autres secrets GitHub représentant les 4 chaines de caractères d'un Service Principal
- **CLIENTID**
- **CLIENTSECRET**
- **SUBSCRIPTIONID**
- **TENANTID**

## Quand vont être utilisées ces informations d'authentification ?

<img width='1024' src='../images/terraformworkflow-et-authentification.jpg'/>

## Déclencher manuellement le workflow GiHub 

Le Pipeline est dans le répertoire : **.github/workflows/Lab4_Pipeline_CI_CD_Terraform.yml**

Aller dans GitHub dans votre
Cliquer sur Actions (entre Pull Request et Projets)
Sélectionner le workflow **2 - CI/CD Terraform**
Cliquer sur le menu déroulant Run Workflow
Cliquer sur le bouton Run workflow

Procédure associée : https://docs.github.com/en/actions/managing-workflow-runs/manually-running-a-workflow

Le Workflow va prendre quelques secondes à démarrer avec un indicateur orange

Cliquer sur le nom du workflow à côté du point orange pour voir le déroulé du workflow

Si le pipeline s'exécute correctement, une coche verte doit apparaitre.

Si c'est le cas, vérifier la création du resource group via le workflow Github avec la commande suivante : **az group list | grep Demo**
