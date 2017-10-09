---
title: "Registre Docker privé aaaCreate - portail Azure | Documents Microsoft"
description: "Commencer à créer et gérer des registres de conteneur Docker privés avec hello portail Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a>Créer un Registre de conteneur gérés à l’aide de hello portail Azure

Azure Container Registry est un service de registre de conteneurs Docker géré utilisé pour stocker des images de conteneurs Docker privés. Ce guide décrit en détail création d’une instance managée de Registre de conteneur Azure à l’aide de hello portail Azure.

Les registres de conteneurs Azure gérés sont en préversion et non disponibles dans toutes les régions.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez une session dans toohello portail Azure à http://portal.azure.com.

## <a name="create-a-container-registry"></a>Créer un registre de conteneur

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Marketplace hello de recherche pour **Registre de conteneur Azure** et sélectionnez-le.

3. Cliquez sur **créer** Panneau de création de hello ACR s’affichera.

    ![Paramètres de Container Registry](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. Bonjour **Registre de conteneur Azure** panneau, entrez hello informations suivantes. Une fois ces opérations effectuées, cliquez sur **Créer**.

    a. **Nom du registre** : Un nom de domaine global unique et de niveau supérieur pour votre registre spécifique. Dans cet exemple, le nom de Registre hello est *myAzureContainerRegistry1*, mais remplacer par un nom unique de votre choix. nom de Hello peut contenir que des lettres et des chiffres.

    b. **Groupe de ressources**: sélectionnez un existant [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.

    c. **Emplacement**: sélectionnez un emplacement de centre de données Azure où le service de hello est [disponible](https://azure.microsoft.com/regions/services/), tel que **Amérique du Sud**.

    d. **L’utilisateur Admin**: Si vous le souhaitez, activer un Registre de hello tooaccess admin utilisateur. Vous pouvez modifier ce paramètre après avoir créé le Registre de hello.

    e. **Registre de managé utilisation**: sélectionnez Oui toohave ACR automatiquement gérer le stockage de Registre hello, des webhooks et l’authentification AAD.

    f. **Niveau tarifaire** : sélectionnez un niveau tarifaire. Consultez ici les prix ACR pour plus d’informations.

## <a name="log-in-tooacr-instance"></a>Ouvrez une session dans l’instance de tooACR

Avant de poussées et les images de conteneur, vous devez vous connecter dans l’instance ACR toohello. 

toodo utilisez donc hello Azure CLI 2.0. Tout d’abord, si nécessaire, ouvrez une session dans Azure à l’aide de hello [ouverture de session az](/cli/azure/#login) commande. 

```azurecli
az login
```

Ensuite, utilisez hello [connexion d’acr az](/cli/azure/acr#login) toolog de commande dans toohello Registre de conteneur Azure.

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

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

Dans ce guide de démarrage rapide, vous avez créé une instance managée de Registre de conteneur Azure à l’aide de hello portail Azure.

> [!div class="nextstepaction"]
> [Push de votre première image à l’aide de hello Docker CLI](container-registry-get-started-docker-cli.md)
