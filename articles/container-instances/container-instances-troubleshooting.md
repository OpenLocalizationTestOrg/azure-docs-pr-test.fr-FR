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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Résoudre les problèmes de déploiement liés à Azure Container Instances

Cet article explique comment tootroubleshoot problèmes lors du déploiement de conteneurs tooAzure les Instances du conteneur. Elle décrit également les problèmes courants de hello que vous risquez de rencontrer.

## <a name="getting-diagnostic-events"></a>Récupération des événements de diagnostic

journaux tooview à partir de votre code d’application dans un conteneur, vous pouvez utiliser hello [az conteneur journaux](/cli/azure/container#logs) commande. Mais si votre conteneur ne déploie pas correctement, vous devez tooreview hello des informations de diagnostic fournies par le fournisseur de ressources des Instances de conteneurs Azure hello. événements de hello tooview pour votre conteneur, exécutez hello de commande suivante :

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

sortie de Hello inclut des propriétés principales de hello de votre conteneur, ainsi que les événements de déploiement :

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

## <a name="common-deployment-issues"></a>Problèmes de déploiement courants

La plupart des erreurs de déploiement sont liées à quelques problèmes courants.

### <a name="unable-toopull-image"></a>Impossible de toopull image

Si les Instances du conteneur Azure est impossible toopull votre image au départ, il effectue une nouvelle tentative pendant une certaine période avant l’échec par la suite. Si l’image de hello ne peut pas être extraite, événements comme hello suivantes sont affichées :

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

tooresolve, supprimer le conteneur de hello et réessayez votre déploiement, qui paient attention particulière que vous avez tapé un nom de l’image hello correctement.

### <a name="container-continually-exits-and-restarts"></a>Le conteneur s’arrête et redémarre en permanence

Azure Container Instances prend uniquement en charge les services de longue durée. Si votre conteneur s’exécute toocompletion et s’arrête, il automatiquement redémarre et s’exécute à nouveau. Si cela se produit, les événements tels que ceux qui suivent sont affichés. Notez que le conteneur de hello démarre correctement, puis redémarre rapidement. Hello API des Instances de conteneur inclut un `retryCount` propriété qui indique combien de fois un conteneur particulier a redémarré.

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
> La plupart des images de conteneur pour les distributions Linux définir un interpréteur de commandes, tels que bash, comme la commande hello par défaut. Un interpréteur de commandes n’étant pas en soi un service de longue durée, ces conteneurs quittent la procédure immédiatement et entrent dans une boucle de redémarrage.

### <a name="container-takes-a-long-time-toostart"></a>Conteneur prend un toostart beaucoup de temps

Si votre conteneur prend un toostart beaucoup de temps, mais finit par aboutit, commencez par examiner de taille hello de votre image de conteneur. Étant donné que les Instances du conteneur Azure extrait l’image de conteneur à la demande, le temps de démarrage de hello vous rencontrez est directement lié tooits taille.

Vous pouvez afficher la taille de hello de votre image de conteneur à l’aide de hello Docker CLI :

```bash
docker images
```

Output:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

tailles d’image clé tookeeping Hello small est de vous assurer que votre image finale ne contienne pas tout ce qui n’est pas nécessaire lors de l’exécution. Une façon toodo avec [en plusieurs builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). En plusieurs builds rendent tooensure facile qu’image finale de hello contient des artefacts hello uniquement vous avez besoin pour votre application, et pas les hello supplémentaire de contenu qui a été requis au moment de la génération.

Hello autre impact n’hello tooreduce moyen de l’extraction d’image hello dans les temps de démarrage de votre conteneur est image de conteneur hello toohost à l’aide de hello Registre de conteneur Azure Bonjour même région où vous prévoyez d’Instances de conteneurs toouse Azure. Cela réduit le chemin d’accès réseau hello qui hello tootravel de besoins image conteneur, raccourcir considérablement les temps de téléchargement hello.
