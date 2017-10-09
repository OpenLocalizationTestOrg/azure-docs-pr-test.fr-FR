---
title: "didacticiel d’Instances de conteneurs aaaAzure - déploiement d’une application | Documents Microsoft"
description: "Didacticiel Azure Container Instances - Déployer des applications"
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
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="47d71-103">Déployer un conteneur de tooAzure Instances de conteneurs</span><span class="sxs-lookup"><span data-stu-id="47d71-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="47d71-104">Il s’agit de hello dernière d’un didacticiel en trois parties.</span><span class="sxs-lookup"><span data-stu-id="47d71-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="47d71-105">Dans les sections précédentes, [une image de conteneur a été créée](container-instances-tutorial-prepare-app.md) et [envoyées tooan Registre de conteneur Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="47d71-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="47d71-106">Cette section termine didacticiel de hello en déployant hello conteneur tooAzure les Instances du conteneur.</span><span class="sxs-lookup"><span data-stu-id="47d71-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="47d71-107">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="47d71-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47d71-108">Définition d’un groupe de conteneurs à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="47d71-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="47d71-109">Déploiement de groupe de conteneur hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="47d71-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="47d71-110">Affichage des journaux de conteneurs</span><span class="sxs-lookup"><span data-stu-id="47d71-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="47d71-111">Déployer le conteneur de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="47d71-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="47d71-112">Hello CLI d’Azure permet le déploiement d’un conteneur de tooAzure les Instances du conteneur dans une seule commande.</span><span class="sxs-lookup"><span data-stu-id="47d71-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="47d71-113">Étant donné que l’image de conteneur hello est hébergé dans hello Registre de conteneur Azure privée, vous devez inclure des tooaccess requis des informations d’identification de hello il.</span><span class="sxs-lookup"><span data-stu-id="47d71-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="47d71-114">Si nécessaire, vous pouvez les interroger comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47d71-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="47d71-115">Serveur de connexion au Registre de conteneurs (mettez-le à jour avec le nom de votre Registre) :</span><span class="sxs-lookup"><span data-stu-id="47d71-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="47d71-116">Mot de passe du Registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="47d71-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="47d71-117">toodeploy votre image de conteneur à partir du Registre de conteneur hello avec une ressource de demande de 1 cœur d’UC et 1 Go de mémoire, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47d71-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="47d71-118">Après quelques secondes, vous recevrez une réponse initiale de la part d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47d71-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="47d71-119">état de hello tooview de déploiement hello, utilisez :</span><span class="sxs-lookup"><span data-stu-id="47d71-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="47d71-120">Nous pouvons continuer à exécuter cette commande jusqu'à ce que l’état hello passe de *en attente* trop*en cours d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="47d71-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="47d71-121">Nous pouvons ensuite continuer.</span><span class="sxs-lookup"><span data-stu-id="47d71-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="47d71-122">Afficher les journaux d’application et de conteneur hello</span><span class="sxs-lookup"><span data-stu-id="47d71-122">View hello application and container logs</span></span>

<span data-ttu-id="47d71-123">Une fois que la réussite du déploiement de hello, ouvrez votre adresse IP du navigateur toohello indiqué dans la sortie de hello Hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47d71-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Hello world application navigateur de hello][aci-app-browser]

<span data-ttu-id="47d71-125">Vous pouvez également afficher la sortie du journal hello de conteneur de hello :</span><span class="sxs-lookup"><span data-stu-id="47d71-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="47d71-126">Output:</span><span class="sxs-lookup"><span data-stu-id="47d71-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="47d71-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47d71-127">Next steps</span></span>

<span data-ttu-id="47d71-128">Dans ce didacticiel, vous terminé processus hello du déploiement de vos Instances de conteneurs de tooAzure conteneurs.</span><span class="sxs-lookup"><span data-stu-id="47d71-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="47d71-129">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="47d71-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="47d71-130">Déploiement de conteneur hello d’à l’aide du Registre de conteneur Azure hello hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="47d71-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="47d71-131">Afficher l’application hello dans le navigateur de hello</span><span class="sxs-lookup"><span data-stu-id="47d71-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="47d71-132">Affichage des journaux de conteneur hello</span><span class="sxs-lookup"><span data-stu-id="47d71-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
