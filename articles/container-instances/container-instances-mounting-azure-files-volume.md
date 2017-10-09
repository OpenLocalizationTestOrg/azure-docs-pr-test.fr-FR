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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="b0a03-103">Montage d’un partage de fichiers Azure avec Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b0a03-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="b0a03-104">Par défaut, les conteneurs Azure Container Instances sont sans état.</span><span class="sxs-lookup"><span data-stu-id="b0a03-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="b0a03-105">Si le conteneur de hello tombe en panne ou s’arrête, ensemble de son état est perdue.</span><span class="sxs-lookup"><span data-stu-id="b0a03-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="b0a03-106">l’état toopersist au-delà de la durée de vie hello hello du conteneur de, vous devez monter un volume à partir d’un magasin externe.</span><span class="sxs-lookup"><span data-stu-id="b0a03-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="b0a03-107">Cet article explique comment toomount un Azure de partage de fichiers pour une utilisation avec les Instances du conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a03-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="b0a03-108">Crée un partage de fichiers Azure</span><span class="sxs-lookup"><span data-stu-id="b0a03-108">Create an Azure file share</span></span>

<span data-ttu-id="b0a03-109">Avant d’utiliser un partage de fichiers Azure avec Azure Container Instances, vous devez le créer.</span><span class="sxs-lookup"><span data-stu-id="b0a03-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="b0a03-110">Exécutez hello suivant script toocreate un partage de fichiers de stockage compte toohost hello et hello partagent lui-même.</span><span class="sxs-lookup"><span data-stu-id="b0a03-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="b0a03-111">Notez que ce nom de compte de stockage hello doit être globalement unique, afin de script de hello ajoute une chaîne en base toohello valeur aléatoire.</span><span class="sxs-lookup"><span data-stu-id="b0a03-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

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

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="b0a03-112">Obtenir les détails d’accès au compte de stockage</span><span class="sxs-lookup"><span data-stu-id="b0a03-112">Acquire storage account access details</span></span>

<span data-ttu-id="b0a03-113">toomount un fichier Azure partagent un volume dans les Instances du conteneur Azure, vous devez les trois valeurs : hello nom de compte de stockage, nom de partage hello et clé d’accès de stockage de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a03-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="b0a03-114">Si vous avez utilisé le script hello ci-dessus, le nom de compte de stockage hello a été créé avec une valeur aléatoire à fin de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a03-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="b0a03-115">tooquery hello final chaîne (y compris hello aléatoire partie) utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="b0a03-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="b0a03-116">Hello nom de partage est déjà connu (il s’agit de *acishare* dans le script hello ci-dessus), de sorte que tout ce qui reste est la clé de compte de stockage hello, qui se trouve à l’aide de hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b0a03-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="b0a03-117">Stocker les détails de l’accès au compte de stockage avec un coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="b0a03-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="b0a03-118">Clés de compte de stockage protègent des données de tooyour d’accès, nous vous recommandons de les stocker dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a03-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="b0a03-119">Créer un coffre de clés avec hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="b0a03-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="b0a03-120">Hello `enabled-for-template-deployment` commutateur permet des secrets à partir de votre coffre de clés Azure toopull du Gestionnaire de ressources au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="b0a03-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="b0a03-121">Stocker la clé de compte de stockage hello en tant que nouveau secret hello coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="b0a03-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="b0a03-122">Monter le volume de hello</span><span class="sxs-lookup"><span data-stu-id="b0a03-122">Mount hello volume</span></span>

<span data-ttu-id="b0a03-123">Le montage d’un partage de fichiers Azure en tant que volume dans un conteneur est un processus en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="b0a03-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="b0a03-124">Tout d’abord, vous fournir les détails de hello du partage hello en tant que partie de la définition de groupe du conteneur hello, puis vous indiquez comment vous souhaitez que le volume de hello monté dans un ou plusieurs des conteneurs hello dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a03-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="b0a03-125">ajouter des volumes de hello toodefine souhaité toomake disponible pour le chargement, un `volumes` toohello définition de groupe conteneur dans le modèle de gestionnaire de ressources Azure hello de tableau, puis de les référencer dans la définition de hello des conteneurs individuels de hello.</span><span class="sxs-lookup"><span data-stu-id="b0a03-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="b0a03-126">modèle de Hello inclut les nom de compte de stockage hello et la clé en tant que paramètres, qui peuvent être fournis dans un fichier de paramètres distincts.</span><span class="sxs-lookup"><span data-stu-id="b0a03-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="b0a03-127">fichier de paramètres toopopulate hello, vous devez trois valeurs : hello nom de compte de stockage et hello ID de ressource de votre coffre de clés Azure hello nom secret de coffre de clés que vous avez utilisé la clé toostore hello.</span><span class="sxs-lookup"><span data-stu-id="b0a03-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="b0a03-128">Si vous avez suivi les étapes précédentes, vous pouvez obtenir ces valeurs avec hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="b0a03-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="b0a03-129">Insérez les valeurs hello dans le fichier de paramètres hello :</span><span class="sxs-lookup"><span data-stu-id="b0a03-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="b0a03-130">Conteneur de hello de déployer et gérer des fichiers</span><span class="sxs-lookup"><span data-stu-id="b0a03-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="b0a03-131">Avec modèle hello défini, vous pouvez créer un conteneur de hello et monter son volume à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a03-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="b0a03-132">En supposant que hello fichier modèle nommé *azuredeploy.json* et ce fichier de paramètres hello est nommé *azuredeploy.parameters.json*, puis de la ligne de commande hello est :</span><span class="sxs-lookup"><span data-stu-id="b0a03-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="b0a03-133">Une fois le conteneur de hello démarre, vous pouvez utiliser l’application web simple hello déployée via hello **aci/seanmckenna-hellofiles** toohello image, gérer les fichiers dans le partage de fichiers Azure hello au chemin d’accès de montage hello que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="b0a03-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="b0a03-134">Obtenir une adresse ip de hello pour l’application web de hello via les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="b0a03-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="b0a03-135">Vous pouvez utiliser un outil tel que hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve et inspecter le partage de fichiers toohello hello fichier écrits.</span><span class="sxs-lookup"><span data-stu-id="b0a03-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="b0a03-136">toolearn en savoir plus sur l’utilisation des modèles Azure Resource Manager, les fichiers de paramètres et le déploiement avec hello CLI d’Azure, consultez [déployer des ressources avec des modèles de gestionnaire de ressources et CLI d’Azure](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0a03-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0a03-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0a03-137">Next steps</span></span>

- <span data-ttu-id="b0a03-138">Déployer pour votre premier conteneur à l’aide d’Instances de conteneurs Azure hello [démarrage rapide](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="b0a03-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="b0a03-139">En savoir plus sur hello [relation entre les Instances du conteneur Azure et orchestrators de conteneur](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="b0a03-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
