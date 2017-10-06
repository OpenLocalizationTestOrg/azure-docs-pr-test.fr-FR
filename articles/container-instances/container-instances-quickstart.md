---
title: "aaaCreate votre premier conteneur d’Instances de conteneurs Azure | Documentation Azure"
description: "Déploiement et prise en main d’Azure Container Instances"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="d2486-103">Créer son premier conteneur dans Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d2486-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="d2486-104">Les Instances du conteneur Azure rend facile toocreate et gérer des conteneurs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d2486-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="d2486-105">Dans ce démarrage rapide, vous créez un conteneur dans Azure et l’exposer toohello internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d2486-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="d2486-106">Cette opération s’effectue en une seule commande.</span><span class="sxs-lookup"><span data-stu-id="d2486-106">This operation is completed in a single command.</span></span> <span data-ttu-id="d2486-107">En l’espace de quelques secondes, ceci s’affiche dans votre navigateur :</span><span class="sxs-lookup"><span data-stu-id="d2486-107">Within just a few seconds, you will see this in your browser:</span></span>

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

<span data-ttu-id="d2486-109">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="d2486-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d2486-110">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.12 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d2486-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="d2486-111">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="d2486-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d2486-112">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d2486-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="d2486-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d2486-113">Create a resource group</span></span>

<span data-ttu-id="d2486-114">Les instances Azure Container Instances sont des ressources Azure et doivent être placées dans un groupe de ressources Azure, un ensemble logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="d2486-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d2486-115">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="d2486-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="d2486-116">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="d2486-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="d2486-117">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="d2486-117">Create a container</span></span>

<span data-ttu-id="d2486-118">Vous pouvez créer un conteneur en attribuant un nom, une image Docker ainsi qu’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d2486-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="d2486-119">Vous pouvez éventuellement exposer hello conteneur toohello internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d2486-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="d2486-120">Dans ce cas, nous utilisons un conteneur qui héberge une application web basique écrite dans [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="d2486-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="d2486-121">Après quelques secondes, vous devez obtenir une demande de tooyour de réponse.</span><span class="sxs-lookup"><span data-stu-id="d2486-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="d2486-122">Au départ, hello conteneur soit dans un **création** état, mais elle doit démarrer dans quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="d2486-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="d2486-123">Vous pouvez vérifier le statut hello à l’aide de hello `show` commande :</span><span class="sxs-lookup"><span data-stu-id="d2486-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="d2486-124">Au bas de hello de sortie de hello, vous verrez l’état d’approvisionnement du conteneur hello et son adresse IP :</span><span class="sxs-lookup"><span data-stu-id="d2486-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

<span data-ttu-id="d2486-125">Une fois le conteneur de hello déplace toohello **Succeeded** d’état, vous pouvez l’atteindre dans le navigateur hello à l’aide de l’adresse IP hello fournie.</span><span class="sxs-lookup"><span data-stu-id="d2486-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="d2486-127">Collecteur de journaux du conteneur hello</span><span class="sxs-lookup"><span data-stu-id="d2486-127">Pull hello container logs</span></span>

<span data-ttu-id="d2486-128">Vous pouvez extraire des journaux de hello du conteneur de hello vous avez créé à l’aide de hello `logs` commande :</span><span class="sxs-lookup"><span data-stu-id="d2486-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="d2486-129">Output:</span><span class="sxs-lookup"><span data-stu-id="d2486-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="d2486-130">Supprimer le conteneur de hello</span><span class="sxs-lookup"><span data-stu-id="d2486-130">Delete hello container</span></span>

<span data-ttu-id="d2486-131">Lorsque vous avez terminé avec le conteneur de hello, vous pouvez le supprimer à l’aide de hello `delete` commande :</span><span class="sxs-lookup"><span data-stu-id="d2486-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d2486-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2486-132">Next steps</span></span>

<span data-ttu-id="d2486-133">Tous les Hello du code pour le conteneur de hello utilisé dans ce démarrage rapide est disponible [sur GitHub][app-github-repo], ainsi que son fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="d2486-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="d2486-134">Si vous souhaitez que tootry génération vous-même et déployer des Instances de conteneurs tooAzure à l’aide de hello Registre de conteneur Azure, continuer le didacticiel d’Instances de conteneurs Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="d2486-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d2486-135">Didacticiels Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d2486-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png