---
title: aaaTroubleshooting les Instances du conteneur Azure
description: "Découvrez comment tootroubleshoot problèmes avec les Instances du conteneur Azure"
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
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="9d7c1-103">Résoudre les problèmes de déploiement liés à Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="9d7c1-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="9d7c1-104">Cet article explique comment tootroubleshoot problèmes lors du déploiement de conteneurs tooAzure les Instances du conteneur.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="9d7c1-105">Elle décrit également les problèmes courants de hello que vous risquez de rencontrer.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="9d7c1-106">Récupération des événements de diagnostic</span><span class="sxs-lookup"><span data-stu-id="9d7c1-106">Getting diagnostic events</span></span>

<span data-ttu-id="9d7c1-107">journaux tooview à partir de votre code d’application dans un conteneur, vous pouvez utiliser hello [az conteneur journaux](/cli/azure/container#logs) commande.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="9d7c1-108">Mais si votre conteneur ne déploie pas correctement, vous devez tooreview hello des informations de diagnostic fournies par le fournisseur de ressources des Instances de conteneurs Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="9d7c1-109">événements de hello tooview pour votre conteneur, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9d7c1-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="9d7c1-110">sortie de Hello inclut des propriétés principales de hello de votre conteneur, ainsi que les événements de déploiement :</span><span class="sxs-lookup"><span data-stu-id="9d7c1-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="9d7c1-111">Problèmes de déploiement courants</span><span class="sxs-lookup"><span data-stu-id="9d7c1-111">Common deployment issues</span></span>

<span data-ttu-id="9d7c1-112">La plupart des erreurs de déploiement sont liées à quelques problèmes courants.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="9d7c1-113">Impossible de toopull image</span><span class="sxs-lookup"><span data-stu-id="9d7c1-113">Unable toopull image</span></span>

<span data-ttu-id="9d7c1-114">Si les Instances du conteneur Azure est impossible toopull votre image au départ, il effectue une nouvelle tentative pendant une certaine période avant l’échec par la suite.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="9d7c1-115">Si l’image de hello ne peut pas être extraite, événements comme hello suivantes sont affichées :</span><span class="sxs-lookup"><span data-stu-id="9d7c1-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

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
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
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

<span data-ttu-id="9d7c1-116">tooresolve, supprimer le conteneur de hello et réessayez votre déploiement, qui paient attention particulière que vous avez tapé un nom de l’image hello correctement.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="9d7c1-117">Le conteneur s’arrête et redémarre en permanence</span><span class="sxs-lookup"><span data-stu-id="9d7c1-117">Container continually exits and restarts</span></span>

<span data-ttu-id="9d7c1-118">Azure Container Instances prend uniquement en charge les services de longue durée.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="9d7c1-119">Si votre conteneur s’exécute toocompletion et s’arrête, il automatiquement redémarre et s’exécute à nouveau.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="9d7c1-120">Si cela se produit, les événements tels que ceux qui suivent sont affichés.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="9d7c1-121">Notez que le conteneur de hello démarre correctement, puis redémarre rapidement.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="9d7c1-122">Hello API des Instances de conteneur inclut un `retryCount` propriété qui indique combien de fois un conteneur particulier a redémarré.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="9d7c1-123">La plupart des images de conteneur pour les distributions Linux définir un interpréteur de commandes, tels que bash, comme la commande hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="9d7c1-124">Un interpréteur de commandes n’étant pas en soi un service de longue durée, ces conteneurs quittent la procédure immédiatement et entrent dans une boucle de redémarrage.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="9d7c1-125">Conteneur prend un toostart beaucoup de temps</span><span class="sxs-lookup"><span data-stu-id="9d7c1-125">Container takes a long time toostart</span></span>

<span data-ttu-id="9d7c1-126">Si votre conteneur prend un toostart beaucoup de temps, mais finit par aboutit, commencez par examiner de taille hello de votre image de conteneur.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="9d7c1-127">Étant donné que les Instances du conteneur Azure extrait l’image de conteneur à la demande, le temps de démarrage de hello vous rencontrez est directement lié tooits taille.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="9d7c1-128">Vous pouvez afficher la taille de hello de votre image de conteneur à l’aide de hello Docker CLI :</span><span class="sxs-lookup"><span data-stu-id="9d7c1-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="9d7c1-129">Output:</span><span class="sxs-lookup"><span data-stu-id="9d7c1-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="9d7c1-130">tailles d’image clé tookeeping Hello small est de vous assurer que votre image finale ne contienne pas tout ce qui n’est pas nécessaire lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="9d7c1-131">Une façon toodo avec [en plusieurs builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="9d7c1-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="9d7c1-132">En plusieurs builds rendent tooensure facile qu’image finale de hello contient des artefacts hello uniquement vous avez besoin pour votre application, et pas les hello supplémentaire de contenu qui a été requis au moment de la génération.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="9d7c1-133">Hello autre impact n’hello tooreduce moyen de l’extraction d’image hello dans les temps de démarrage de votre conteneur est image de conteneur hello toohost à l’aide de hello Registre de conteneur Azure Bonjour même région où vous prévoyez d’Instances de conteneurs toouse Azure.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="9d7c1-134">Cela réduit le chemin d’accès réseau hello qui hello tootravel de besoins image conteneur, raccourcir considérablement les temps de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="9d7c1-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
