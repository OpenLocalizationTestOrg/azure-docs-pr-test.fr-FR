---
title: "Créer son premier conteneur Azure Container Instances | Azure Docs"
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
ms.openlocfilehash: 905f69e5e1e237a31d9bb1e326969ec83292c244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="d874a-103">Créer son premier conteneur dans Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d874a-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="d874a-104">Azure Container Instances simplifie la création et la gestion des conteneurs dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d874a-104">Azure Container Instances makes it easy to create and manage containers in Azure.</span></span> <span data-ttu-id="d874a-105">Dans ce guide de démarrage rapide, vous allez voir comment créer un conteneur dans Azure et comment l’exposer sur internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d874a-105">In this quick start, you will create a container in Azure and expose it to the internet with a public IP address.</span></span> <span data-ttu-id="d874a-106">Cette opération s’effectue en une seule commande.</span><span class="sxs-lookup"><span data-stu-id="d874a-106">This operation is completed in a single command.</span></span> <span data-ttu-id="d874a-107">En l’espace de quelques secondes, ceci s’affiche dans votre navigateur :</span><span class="sxs-lookup"><span data-stu-id="d874a-107">Within just a few seconds, you will see this in your browser:</span></span>

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

<span data-ttu-id="d874a-109">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="d874a-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d874a-110">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.12 ou une version ultérieure pour poursuivre la procédure décrite dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="d874a-110">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="d874a-111">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="d874a-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="d874a-112">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d874a-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="d874a-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d874a-113">Create a resource group</span></span>

<span data-ttu-id="d874a-114">Les instances Azure Container Instances sont des ressources Azure et doivent être placées dans un groupe de ressources Azure, un ensemble logique dans lequel des ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="d874a-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d874a-115">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d874a-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="d874a-116">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="d874a-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="d874a-117">Créer un conteneur</span><span class="sxs-lookup"><span data-stu-id="d874a-117">Create a container</span></span>

<span data-ttu-id="d874a-118">Vous pouvez créer un conteneur en attribuant un nom, une image Docker ainsi qu’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d874a-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="d874a-119">Si vous le souhaitez, vous pouvez exposer le conteneur sur internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d874a-119">You can optionally expose the container to the internet with a public IP address.</span></span> <span data-ttu-id="d874a-120">Dans ce cas, nous utilisons un conteneur qui héberge une application web basique écrite dans [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="d874a-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="d874a-121">Après quelques secondes, vous obtenez une réponse à votre requête.</span><span class="sxs-lookup"><span data-stu-id="d874a-121">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="d874a-122">Au début, le conteneur aura le statut **En cours de création**, mais démarrera après quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="d874a-122">Initially, the container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="d874a-123">Vous pouvez vérifier le statut à l’aide de la commande `show` :</span><span class="sxs-lookup"><span data-stu-id="d874a-123">You can check the status using the `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="d874a-124">En bas de la sortie, vous verrez le statut de la configuration et l’adresse IP du conteneur :</span><span class="sxs-lookup"><span data-stu-id="d874a-124">At the bottom of the output, you will see the container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="d874a-125">Une fois que le statut du conteneur passe à **Réussi**, vous pouvez l’atteindre dans le navigateur en utilisant l’adresse IP obtenue.</span><span class="sxs-lookup"><span data-stu-id="d874a-125">Once the container moves to the **Succeeded** state, you can reach it in the browser using the IP address provided.</span></span> 

![L’application déployée à l’aide d’Azure Container Instances est affichée dans le navigateur][aci-app-browser]

## <a name="pull-the-container-logs"></a><span data-ttu-id="d874a-127">Extraire les journaux de conteneur</span><span class="sxs-lookup"><span data-stu-id="d874a-127">Pull the container logs</span></span>

<span data-ttu-id="d874a-128">Vous pouvez extraire les journaux du conteneur que vous avez créé à l’aide de la commande `logs` :</span><span class="sxs-lookup"><span data-stu-id="d874a-128">You can pull the logs for the container you created using the `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="d874a-129">Output:</span><span class="sxs-lookup"><span data-stu-id="d874a-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-the-container"></a><span data-ttu-id="d874a-130">Supprimer un conteneur</span><span class="sxs-lookup"><span data-stu-id="d874a-130">Delete the container</span></span>

<span data-ttu-id="d874a-131">Lorsque vous avez fini d’utiliser le conteneur, vous pouvez le supprimer à l’aide de la commande `delete` :</span><span class="sxs-lookup"><span data-stu-id="d874a-131">When you are done with the container, you can remove it using the `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="d874a-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d874a-132">Next steps</span></span>

<span data-ttu-id="d874a-133">Les codes pour le conteneur et le fichier Dockerfile utilisés dans ce guide de démarrage rapide sont disponibles [sur GitHub][app-github-repo].</span><span class="sxs-lookup"><span data-stu-id="d874a-133">All of the code for the container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="d874a-134">Si vous voulez essayer de le créer et de le déployer dans Azure Container Instances à l’aide d’Azure Container Registry, veuillez vous référer au didacticiel sur Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="d874a-134">If you'd like to try building it yourself and deploying it to Azure Container Instances using the Azure Container Registry, continue to the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d874a-135">Didacticiels Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="d874a-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png