---
title: "aaaUsing ACR avec un cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: Utiliser un Azure Container Registry avec un cluster DC/OS dans Azure Container Service
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, conteneurs, micro-services, Mesos, Azure, FileShare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Utiliser ACR avec un toodeploy de cluster de contrôleur de domaine/système d’exploitation de votre application

Dans cet article, nous explorons comment toouse Registre de conteneur Azure avec un cluster de contrôleur de domaine/système d’exploitation. À l’aide de ACR vous permet de tooprivately store et gérer les images de conteneur. Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Déployer Azure Container Registry (le cas échéant)
> * Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation
> * Télécharger une image de toohello Registre de conteneur Azure
> * Exécuter une image de conteneur à partir de hello Registre de conteneur Azure

Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel. Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Déployer Azure Container Registry

Si nécessaire, créez un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande. 

Hello exemple suivant crée un Registre avec une générer de façon aléatoire nom. Registre de Hello est également configuré avec un compte d’administrateur à l’aide de hello `--admin-enabled` argument.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Une fois que le Registre de hello a été créé, hello CLI d’Azure génère des données similaires toohello suit. Prenez note de hello `name` et `loginServer`, ils sont utilisés dans les étapes ultérieures.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Obtenir des informations d’identification du Registre hello conteneur à l’aide de hello [afficher d’informations d’identification az acr](/cli/azure/acr/credential) commande. Hello de substitution `--name` avec hello une indication dans la dernière étape de hello. Notez un mot de passe, nécessaire pour une étape ultérieure.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Pour plus d’informations sur le Registre de conteneur Azure, consultez [registres de conteneur Docker Introduction tooprivate](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Gérer l’authentification ACR

façon conventionnelle de Hello image toopush et par extraction à partir d’un Registre privé est toofirst s’authentifier auprès du Registre de hello. toodo ainsi, vous devez utiliser hello `docker login` commande sur n’importe quel client qui a besoin des registres privés de tooaccess hello. Un cluster de contrôleur de domaine/système d’exploitation peut contenir plusieurs nœuds, tous doivent toobe authentifié avec hello ACR, il est utile tooautomate ce processus sur chaque nœud. 

### <a name="create-shared-storage"></a>Créer un stockage partagé

Ce processus utilise un partage de fichiers Azure qui a été monté sur chaque nœud de cluster de hello. Si vous n’avez pas déjà configuré de stockage partagé, consultez [Configurer un partage de fichier dans un cluster de contrôleur de domaine/système d’exploitation](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Configurer une authentification ACR

Tout d’abord, obtenez hello hello DC/OS maître et le stocker dans une variable de nom de domaine complet.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Créez une connexion SSH avec hello masque (ou de hello première) de votre cluster basé sur le système d’exploitation contrôleur de domaine. Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello.

```azurecli-interactive
ssh azureuser@$FQDN
```

Exécutez hello suivant commande toologin toohello Registre de conteneur Azure. Remplacez hello `--username` avec nom hello du Registre de conteneur hello et hello `--password` avec l’un des mots de passe hello fourni. Remplacez le dernier argument de hello *mycontainerregistry.azurecr.io* dans l’exemple hello avec le nom de loginServer hello du Registre de conteneur hello. 

Cette commande stocke les valeurs de l’authentification de hello localement sous hello `~/.docker` chemin d’accès.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Créer un fichier compressé qui contient des valeurs de l’authentification de Registre de conteneur hello.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Copiez ce stockage partagé de cluster toohello des fichiers. Cette étape rend hello disponible sur tous les nœuds du cluster de contrôleur de domaine/système d’exploitation hello.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Télécharger l’image tooACR

Maintenant à partir d’un ordinateur de développement, ou tout autre système avec Docker installé, créez une image et téléchargez-le toohello Registre de conteneur Azure.

Créer un conteneur à partir de l’image d’Ubuntu hello.

```azurecli-interactive
docker run ubunut --name base-image
```

Prêt à capturer les conteneur hello dans une nouvelle image. nom de l’image Hello doit tooinclude hello `loginServer` nom de registrywith de conteneur hello un format de `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Connexion en hello Registre de conteneur Azure. Remplacez hello par nom de loginServer hello, hello--nom d’utilisateur avec le nom hello du Registre de conteneur hello et hello--mot de passe avec l’un des mots de passe hello fourni.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Enfin, téléchargez Registre d’ACR toohello hello images. Cet exemple permet de télécharger une image nommée dcos-demo.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Exécuter une image à partir de l’ACR

toouse une image à partir du Registre ACR hello, créez un fichier de noms *acrDemo.json* et hello de copie après le texte dans celle-ci. Remplacez nom de l’image hello avec le nom de loginServer de Registre de conteneur hello et le nom de l’image, par exemple `loginServer/imageName`. Prenez note de hello `uris` propriété. Cette propriété contient l’emplacement de hello du fichier de l’authentification Registre hello conteneur, dans ce cas est le partage de fichiers Azure hello est monté sur chaque nœud de cluster de contrôleur de domaine/système d’exploitation hello.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Déployer l’application hello avec hello DC/OC CLI.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel vous avez configurer toouse de contrôleur de domaine/système d’exploitation registre de conteneur Azure notamment hello suivant de tâches :

> [!div class="checklist"]
> * Déployer Azure Container Registry (le cas échéant)
> * Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation
> * Télécharger une image de toohello Registre de conteneur Azure
> * Exécuter une image de conteneur à partir de hello Registre de conteneur Azure
