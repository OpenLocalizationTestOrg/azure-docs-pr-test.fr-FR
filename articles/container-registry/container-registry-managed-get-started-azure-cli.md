---
title: "Registre de conteneur de Docker privé aaaCreate - CLI d’Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a>Créer un Registre de conteneur gérés à l’aide de hello CLI d’Azure

Azure Container Registry est un service de registre de conteneurs Docker géré utilisé pour stocker des images de conteneurs Docker privés. Ce guide décrit en détail la création d’une instance managée de Registre de conteneur Azure à l’aide de hello CLI d’Azure.

Les registres de conteneurs Azure gérés sont en préversion et non disponibles dans toutes les régions.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westcentralus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a>Créer un registre de conteneur

Créez une instance de l’ACR à l’aide de hello [az acr créer](/cli/azure/acr#create) commande.

> [!NOTE]
> Lorsque vous créez un registre, spécifiez un nom de domaine global unique de niveau supérieur, contenant uniquement des chiffres et des lettres.

 nom de Registre Hello dans l’exemple de hello est *myContainerRegistry1*, remplacer par un nom unique de votre choix.

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

Lors de la création de Registre de hello, sortie de hello est similaire toohello suivantes :

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a>Ouvrez une session dans l’instance de tooACR

Avant de poussées et les images de conteneur, vous devez vous connecter dans l’instance ACR toohello. toodo utilisez donc hello [connexion d’acr az](/cli/azure/acr#login) commande.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

commande Hello renvoie un message de succès de la connexion une fois terminé.

## <a name="use-azure-container-registry"></a>Utilisation d’Azure Container Registry

### <a name="list-container-images"></a>Répertorier les images conteneur

Hello d’utilisation `az acr` commandes CLI de balises dans un référentiel et des images de hello tooquery.

> [!NOTE]
> Actuellement, Registre de conteneur ne prend pas en charge hello `docker search` tooquery de commande pour les images et les balises.

### <a name="list-repositories"></a>Répertorier les référentiels

Hello exemple suivant répertorie les référentiels hello dans un Registre, au format JSON (JavaScript Object Notation) :

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a>Répertorier les balises

Hello exemple suivant répertorie les balises hello sur hello **exemples/nginx** référentiel, au format JSON :

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez créé une instance managée de Registre de conteneur Azure à l’aide de hello CLI d’Azure.

> [!div class="nextstepaction"]
> [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
