---
title: aaaMounting un volume de fichiers Azure dans les Instances du conteneur Azure
description: "Découvrez comment toomount fichiers Azure état toopersist de volume avec les Instances du conteneur Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Montage d’un partage de fichiers Azure avec Azure Container Instances

Par défaut, les conteneurs Azure Container Instances sont sans état. Si le conteneur de hello tombe en panne ou s’arrête, ensemble de son état est perdue. l’état toopersist au-delà de la durée de vie hello hello du conteneur de, vous devez monter un volume à partir d’un magasin externe. Cet article explique comment toomount un Azure de partage de fichiers pour une utilisation avec les Instances du conteneur Azure.

## <a name="create-an-azure-file-share"></a>Crée un partage de fichiers Azure

Avant d’utiliser un partage de fichiers Azure avec Azure Container Instances, vous devez le créer. Exécutez hello suivant script toocreate un partage de fichiers de stockage compte toohost hello et hello partagent lui-même. Notez que ce nom de compte de stockage hello doit être globalement unique, afin de script de hello ajoute une chaîne en base toohello valeur aléatoire.

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>Obtenir les détails d’accès au compte de stockage

toomount un fichier Azure partagent un volume dans les Instances du conteneur Azure, vous devez les trois valeurs : hello nom de compte de stockage, nom de partage hello et clé d’accès de stockage de hello. 

Si vous avez utilisé le script hello ci-dessus, le nom de compte de stockage hello a été créé avec une valeur aléatoire à fin de hello. tooquery hello final chaîne (y compris hello aléatoire partie) utilisez hello suivant de commandes :

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Hello nom de partage est déjà connu (il s’agit de *acishare* dans le script hello ci-dessus), de sorte que tout ce qui reste est la clé de compte de stockage hello, qui se trouve à l’aide de hello la commande suivante :

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Stocker les détails de l’accès au compte de stockage avec un coffre de clés Azure

Clés de compte de stockage protègent des données de tooyour d’accès, nous vous recommandons de les stocker dans un coffre de clés Azure. 

Créer un coffre de clés avec hello CLI d’Azure :

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Hello `enabled-for-template-deployment` commutateur permet des secrets à partir de votre coffre de clés Azure toopull du Gestionnaire de ressources au moment du déploiement.

Stocker la clé de compte de stockage hello en tant que nouveau secret hello coffre de clés :

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Monter le volume de hello

Le montage d’un partage de fichiers Azure en tant que volume dans un conteneur est un processus en deux étapes. Tout d’abord, vous fournir les détails de hello du partage hello en tant que partie de la définition de groupe du conteneur hello, puis vous indiquez comment vous souhaitez que le volume de hello monté dans un ou plusieurs des conteneurs hello dans le groupe de hello.

ajouter des volumes de hello toodefine souhaité toomake disponible pour le chargement, un `volumes` toohello définition de groupe conteneur dans le modèle de gestionnaire de ressources Azure hello de tableau, puis de les référencer dans la définition de hello des conteneurs individuels de hello.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

modèle de Hello inclut les nom de compte de stockage hello et la clé en tant que paramètres, qui peuvent être fournis dans un fichier de paramètres distincts. fichier de paramètres toopopulate hello, vous devez trois valeurs : hello nom de compte de stockage et hello ID de ressource de votre coffre de clés Azure hello nom secret de coffre de clés que vous avez utilisé la clé toostore hello. Si vous avez suivi les étapes précédentes, vous pouvez obtenir ces valeurs avec hello script suivant :

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Insérez les valeurs hello dans le fichier de paramètres hello :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>Conteneur de hello de déployer et gérer des fichiers

Avec modèle hello défini, vous pouvez créer un conteneur de hello et monter son volume à l’aide de hello CLI d’Azure. En supposant que hello fichier modèle nommé *azuredeploy.json* et ce fichier de paramètres hello est nommé *azuredeploy.parameters.json*, puis de la ligne de commande hello est :

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Une fois le conteneur de hello démarre, vous pouvez utiliser l’application web simple hello déployée via hello **aci/seanmckenna-hellofiles** toohello image, gérer les fichiers dans le partage de fichiers Azure hello au chemin d’accès de montage hello que vous avez spécifié. Obtenir une adresse ip de hello pour l’application web de hello via les éléments suivants de hello :

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Vous pouvez utiliser un outil tel que hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve et inspecter le partage de fichiers toohello hello fichier écrits.

>[!NOTE]
> toolearn en savoir plus sur l’utilisation des modèles Azure Resource Manager, les fichiers de paramètres et le déploiement avec hello CLI d’Azure, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Étapes suivantes

- Déployer pour votre premier conteneur à l’aide d’Instances de conteneurs Azure hello [démarrage rapide](container-instances-quickstart.md)
- En savoir plus sur hello [relation entre les Instances du conteneur Azure et orchestrators de conteneur](container-instances-orchestrator-relationship.md)
