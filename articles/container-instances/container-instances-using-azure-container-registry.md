---
title: aaaDeploy tooAzure les Instances du conteneur de hello Registre de conteneur Azure | Documentation Azure
description: "Déployer des Instances conteneur tooAzure hello Registre de conteneur Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2667f91db8ed92a9ccc9ba722a2b1f5c5ea93886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a>Déployer des Instances conteneur tooAzure hello Registre de conteneur Azure

Hello Registre de conteneur Azure est un registre basé sur Azure, privé, pour les images de conteneur Docker. Cet article décrit comment les images de conteneur toodeploy stocké dans hello Registre de conteneur Azure tooAzure les Instances du conteneur.

## <a name="using-hello-azure-cli"></a>À l’aide de hello CLI d’Azure

Hello CLI d’Azure inclut des commandes pour la création et la gestion des conteneurs dans les Instances du conteneur Azure. Si vous spécifiez une image privée Bonjour `create` de commande, vous pouvez également spécifier tooauthenticate de mot de passe requis hello image Registre avec le Registre de conteneur hello.

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

Hello `create` commande aussi prend en charge la spécification hello `registry-login-server` et `registry-username`. Toutefois, le serveur de connexion hello pour hello Registre de conteneur Azure est toujours *registryname*. azurecr.io et hello nom d’utilisateur de valeur par défaut est *registryname*, de sorte que ces valeurs sont déduits à partir du nom de l’image hello si ne sont pas explicitement fourni.

## <a name="using-an-azure-resource-manager-template"></a>Utilisation d’un modèle Azure Resource Manager

Vous pouvez spécifier des propriétés de hello de votre Registre de conteneur Azure dans un modèle Azure Resource Manager en insérant hello `imageRegistryCredentials` propriété dans la définition de groupe conteneur hello :

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

tooavoid le stockage de votre mot de passe de Registre de conteneur directement dans le modèle de hello, nous vous recommandons de stocker en tant que secret dans [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) et y fait référence dans le modèle hello à l’aide de hello [intégration native entre Bonjour Azure Resource Manager et le coffre de clés](../azure-resource-manager/resource-manager-keyvault-parameter.md).

## <a name="using-hello-azure-portal"></a>À l’aide de hello portail Azure

Si vous gérez des images de conteneur Bonjour Azure conteneur de Registre, vous pouvez facilement créer un conteneur dans les Instances de conteneurs Azure à l’aide de hello portail Azure.

1. Bonjour portail Azure, accédez à Registre de conteneur tooyour.

2. Choisissez les référentiels.

    ![menu de Registre de conteneur Azure Hello Bonjour portail Azure][acr-menu]

3. Choisissez le référentiel hello que vous souhaitez toodeploy à partir de.

4. Cliquez sur la balise de hello pour l’image de conteneur hello souhaité toodeploy.

    ![Menu contextuel pour le lancement de conteneurs avec Azure Container Instances][acr-runinstance-contextmenu]

5. Entrez un nom pour le conteneur de hello et un nom pour le groupe de ressources hello. Vous pouvez également modifier les valeurs par défaut de hello si vous le souhaitez.

    ![Créer un menu pour Azure Container Instances][acr-create-deeplink]

6. Une fois le déploiement de hello terminé, vous pouvez naviguer toohello groupes des conteneurs de hello notifications volet toofind son adresse IP et autres propriétés.

    ![Affichage des détails pour le groupe de conteneurs d’Azure Container Instances][aci-detailsview]

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toobuild conteneurs, les push de Registre de conteneur privé tooa et déployer les Instances de conteneurs tooAzure par [hello didacticiel terminé](container-instances-tutorial-prepare-app.md).

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
