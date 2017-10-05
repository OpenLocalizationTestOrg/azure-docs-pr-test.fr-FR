---
title: "Résolution des problèmes liés à Azure Container Instances"
description: "Découvrez comment résoudre les problèmes liés à Azure Container Instances"
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
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="924ee-103">Résoudre les problèmes de déploiement liés à Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="924ee-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="924ee-104">Cet article explique comment résoudre les problèmes de déploiement de conteneurs sur Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="924ee-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="924ee-105">Il décrit également les problèmes courants que vous risquez de rencontrer.</span><span class="sxs-lookup"><span data-stu-id="924ee-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="924ee-106">Récupération des événements de diagnostic</span><span class="sxs-lookup"><span data-stu-id="924ee-106">Getting diagnostic events</span></span>

<span data-ttu-id="924ee-107">Pour afficher les journaux à partir de votre code d’application dans un conteneur, vous pouvez utiliser la commande [az container logs](/cli/azure/container#logs).</span><span class="sxs-lookup"><span data-stu-id="924ee-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="924ee-108">Toutefois, si votre conteneur ne se déploie pas correctement, vous devez examiner les informations de diagnostic fournies par le fournisseur de ressources Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="924ee-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="924ee-109">Pour afficher les événements liés à votre conteneur, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="924ee-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="924ee-110">La sortie inclut les propriétés principales de votre conteneur, ainsi que les événements de déploiement :</span><span class="sxs-lookup"><span data-stu-id="924ee-110">The output includes the core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="924ee-111">Problèmes de déploiement courants</span><span class="sxs-lookup"><span data-stu-id="924ee-111">Common deployment issues</span></span>

<span data-ttu-id="924ee-112">La plupart des erreurs de déploiement sont liées à quelques problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="924ee-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="924ee-113">Impossible d’extraire l’image</span><span class="sxs-lookup"><span data-stu-id="924ee-113">Unable to pull image</span></span>

<span data-ttu-id="924ee-114">Si Azure Container Instances ne parvient pas à extraire votre image initialement, il réessaie pendant une certaine période, sans succès.</span><span class="sxs-lookup"><span data-stu-id="924ee-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="924ee-115">Des événements tels que les suivants sont alors affichés :</span><span class="sxs-lookup"><span data-stu-id="924ee-115">If the image cannot be pulled, events like the following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="924ee-116">Pour résoudre cette situation, supprimez le conteneur et essayez de le redéployer, en veillant à taper correctement le nom de l’image.</span><span class="sxs-lookup"><span data-stu-id="924ee-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="924ee-117">Le conteneur s’arrête et redémarre en permanence</span><span class="sxs-lookup"><span data-stu-id="924ee-117">Container continually exits and restarts</span></span>

<span data-ttu-id="924ee-118">Azure Container Instances prend uniquement en charge les services de longue durée.</span><span class="sxs-lookup"><span data-stu-id="924ee-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="924ee-119">Si votre conteneur s’exécute jusqu’au bout et s’arrête, il redémarre et se réexécute automatiquement.</span><span class="sxs-lookup"><span data-stu-id="924ee-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="924ee-120">Si cela se produit, les événements tels que ceux qui suivent sont affichés.</span><span class="sxs-lookup"><span data-stu-id="924ee-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="924ee-121">Notez que le conteneur démarre correctement, puis redémarre rapidement.</span><span class="sxs-lookup"><span data-stu-id="924ee-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="924ee-122">L’API Container Instances inclut une propriété `retryCount` qui indique combien de fois un conteneur particulier a redémarré.</span><span class="sxs-lookup"><span data-stu-id="924ee-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="924ee-123">La plupart des images conteneur pour les distributions Linux définissent un interpréteur de commandes, tel que bash, comme commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="924ee-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="924ee-124">Un interpréteur de commandes n’étant pas en soi un service de longue durée, ces conteneurs quittent la procédure immédiatement et entrent dans une boucle de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="924ee-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="924ee-125">Le démarrage du conteneur prend beaucoup de temps</span><span class="sxs-lookup"><span data-stu-id="924ee-125">Container takes a long time to start</span></span>

<span data-ttu-id="924ee-126">Si le démarrage de votre conteneur prend beaucoup de temps, commencez par examiner la taille de votre image conteneur.</span><span class="sxs-lookup"><span data-stu-id="924ee-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="924ee-127">Étant donné qu’Azure Container Instances extrait l’image conteneur à la demande, le temps de démarrage est directement lié à la taille de cette image.</span><span class="sxs-lookup"><span data-stu-id="924ee-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="924ee-128">Vous pouvez afficher la taille de votre image conteneur à l’aide de l’interface CLI Docker :</span><span class="sxs-lookup"><span data-stu-id="924ee-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="924ee-129">Output:</span><span class="sxs-lookup"><span data-stu-id="924ee-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="924ee-130">Pour que l’image conserve une petite taille, faites en sorte que l’image finale ne contienne aucun élément qui soit superflu au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="924ee-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="924ee-131">Pour ce faire, vous pouvez utiliser des [builds à plusieurs étapes](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="924ee-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="924ee-132">Grâce aux builds à plusieurs étapes, vous pouvez facilement faire en sorte que l’image finale ne contienne que les artefacts nécessaires à votre application, à l’exclusion de tout contenu supplémentaire qui était requis au moment de la génération.</span><span class="sxs-lookup"><span data-stu-id="924ee-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="924ee-133">Une autre façon de réduire l’impact de l’extraction de l’image sur le temps de démarrage de votre conteneur consiste à héberger l’image conteneur à l’aide d’Azure Container Registry dans la région où vous envisagez d’utiliser Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="924ee-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="924ee-134">Cette opération raccourcit le chemin réseau que l’image conteneur doit parcourir, réduisant considérablement le temps de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="924ee-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>