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
# <a name="deploy-tooazure-container-instances-from-hello-azure-container-registry"></a><span data-ttu-id="b0269-103">Déployer des Instances conteneur tooAzure hello Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="b0269-103">Deploy tooAzure Container Instances from hello Azure Container Registry</span></span>

<span data-ttu-id="b0269-104">Hello Registre de conteneur Azure est un registre basé sur Azure, privé, pour les images de conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="b0269-104">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="b0269-105">Cet article décrit comment les images de conteneur toodeploy stocké dans hello Registre de conteneur Azure tooAzure les Instances du conteneur.</span><span class="sxs-lookup"><span data-stu-id="b0269-105">This article covers how toodeploy container images stored in hello Azure Container Registry tooAzure Container Instances.</span></span>

## <a name="using-hello-azure-cli"></a><span data-ttu-id="b0269-106">À l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="b0269-106">Using hello Azure CLI</span></span>

<span data-ttu-id="b0269-107">Hello CLI d’Azure inclut des commandes pour la création et la gestion des conteneurs dans les Instances du conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="b0269-107">hello Azure CLI includes commands for creating and managing containers in Azure Container Instances.</span></span> <span data-ttu-id="b0269-108">Si vous spécifiez une image privée Bonjour `create` de commande, vous pouvez également spécifier tooauthenticate de mot de passe requis hello image Registre avec le Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="b0269-108">If you specify a private image in hello `create` command, you can also specify hello image registry password required tooauthenticate with hello container registry.</span></span>

```azurecli-interactive
az container create --name myprivatecontainer --image mycontainerregistry.azurecr.io/mycontainerimage:v1 --registry-password myRegistryPassword --resource-group myresourcegroup
```

<span data-ttu-id="b0269-109">Hello `create` commande aussi prend en charge la spécification hello `registry-login-server` et `registry-username`.</span><span class="sxs-lookup"><span data-stu-id="b0269-109">hello `create` command also supports specifying hello `registry-login-server` and `registry-username`.</span></span> <span data-ttu-id="b0269-110">Toutefois, le serveur de connexion hello pour hello Registre de conteneur Azure est toujours *registryname*. azurecr.io et hello nom d’utilisateur de valeur par défaut est *registryname*, de sorte que ces valeurs sont déduits à partir du nom de l’image hello si ne sont pas explicitement fourni.</span><span class="sxs-lookup"><span data-stu-id="b0269-110">However, hello login server for hello Azure Container Registry is always *registryname*.azurecr.io and hello default username is *registryname*, so these values are inferred from hello image name if not explicitly provided.</span></span>

## <a name="using-an-azure-resource-manager-template"></a><span data-ttu-id="b0269-111">Utilisation d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b0269-111">Using an Azure Resource Manager template</span></span>

<span data-ttu-id="b0269-112">Vous pouvez spécifier des propriétés de hello de votre Registre de conteneur Azure dans un modèle Azure Resource Manager en insérant hello `imageRegistryCredentials` propriété dans la définition de groupe conteneur hello :</span><span class="sxs-lookup"><span data-stu-id="b0269-112">You can specify hello properties of your Azure Container Registry in an Azure Resource Manager template by including hello `imageRegistryCredentials` property in hello container group definition:</span></span>

```json
"imageRegistryCredentials": [
  {
    "server": "imageRegistryLoginServer",
    "username": "imageRegistryUsername",
    "password": "imageRegistryPassword"
  }
]
```

<span data-ttu-id="b0269-113">tooavoid le stockage de votre mot de passe de Registre de conteneur directement dans le modèle de hello, nous vous recommandons de stocker en tant que secret dans [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) et y fait référence dans le modèle hello à l’aide de hello [intégration native entre Bonjour Azure Resource Manager et le coffre de clés](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="b0269-113">tooavoid storing your container registry password directly in hello template, we recommend that you store it as a secret in [Azure Key Vault](../key-vault/key-vault-manage-with-cli2.md) and reference it in hello template using hello [native integration between hello Azure Resource Manager and Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="b0269-114">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0269-114">Using hello Azure portal</span></span>

<span data-ttu-id="b0269-115">Si vous gérez des images de conteneur Bonjour Azure conteneur de Registre, vous pouvez facilement créer un conteneur dans les Instances de conteneurs Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0269-115">If you maintain container images in hello Azure Container Registry, you can easily create a container in Azure Container Instances using hello Azure portal.</span></span>

1. <span data-ttu-id="b0269-116">Bonjour portail Azure, accédez à Registre de conteneur tooyour.</span><span class="sxs-lookup"><span data-stu-id="b0269-116">In hello Azure portal, navigate tooyour container registry.</span></span>

2. <span data-ttu-id="b0269-117">Choisissez les référentiels.</span><span class="sxs-lookup"><span data-stu-id="b0269-117">Choose Repositories.</span></span>

    ![menu de Registre de conteneur Azure Hello Bonjour portail Azure][acr-menu]

3. <span data-ttu-id="b0269-119">Choisissez le référentiel hello que vous souhaitez toodeploy à partir de.</span><span class="sxs-lookup"><span data-stu-id="b0269-119">Choose hello repository that you want toodeploy from.</span></span>

4. <span data-ttu-id="b0269-120">Cliquez sur la balise de hello pour l’image de conteneur hello souhaité toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b0269-120">Right-click hello tag for hello container image you want toodeploy.</span></span>

    ![Menu contextuel pour le lancement de conteneurs avec Azure Container Instances][acr-runinstance-contextmenu]

5. <span data-ttu-id="b0269-122">Entrez un nom pour le conteneur de hello et un nom pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b0269-122">Enter a name for hello container and a name for hello resource group.</span></span> <span data-ttu-id="b0269-123">Vous pouvez également modifier les valeurs par défaut de hello si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b0269-123">You can also change hello default values if you wish.</span></span>

    ![Créer un menu pour Azure Container Instances][acr-create-deeplink]

6. <span data-ttu-id="b0269-125">Une fois le déploiement de hello terminé, vous pouvez naviguer toohello groupes des conteneurs de hello notifications volet toofind son adresse IP et autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="b0269-125">Once hello deployment completes, you can navigate toohello container group from hello notifications pane toofind its IP address and other properties.</span></span>

    ![Affichage des détails pour le groupe de conteneurs d’Azure Container Instances][aci-detailsview]

## <a name="next-steps"></a><span data-ttu-id="b0269-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0269-127">Next steps</span></span>

<span data-ttu-id="b0269-128">Découvrez comment toobuild conteneurs, les push de Registre de conteneur privé tooa et déployer les Instances de conteneurs tooAzure par [hello didacticiel terminé](container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="b0269-128">Learn how toobuild containers, push them tooa private container registry, and deploy them tooAzure Container Instances by [completing hello tutorial](container-instances-tutorial-prepare-app.md).</span></span>

<!-- IMAGES -->
[acr-menu]: ./media/container-instances-using-azure-container-registry/acr-menu.png

[acr-runinstance-contextmenu]: ./media/container-instances-using-azure-container-registry/acr-runinstance-contextmenu.png

[acr-create-deeplink]: ./media/container-instances-using-azure-container-registry/acr-create-deeplink.png

[aci-detailsview]: ./media/container-instances-using-azure-container-registry/aci-detailsview.png
