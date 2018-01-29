---
title: "Basculer et mettre à l’échelle une application de conteneurs Azure Service Fabric | Microsoft Docs"
description: "Découvrez comment le basculement est géré dans une application de conteneurs Azure Service Fabric.  Sachez également mettre à l’échelle les conteneurs et les services qui s’exécutent dans un cluster."
services: service-fabric
documentationcenter: 
author: suhuruli
manager: timlt
editor: suhuruli
tags: servicefabric
keywords: Docker, Containers, Conteneurs, Microservices, Service Fabric, Azure
ms.assetid: 
ms.service: service-fabric
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/12/2017
ms.author: suhuruli
ms.custom: mvc
ms.openlocfilehash: 21dd9dfbc90c26236c43e2c334305ca97f63d361
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="demonstrate-fail-over-and-scaling-of-container-services-with-service-fabric"></a>Présenter le basculement et la mise à l’échelle de services de conteneur avec Service Fabric

Ce didacticiel est le troisième de la série. Dans ce didacticiel, vous découvrez la gestion du basculement au sein d’applications de conteneur dans Service Fabric. Vous apprenez également à mettre à l’échelle des conteneurs. Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]
> * En savoir plus sur le basculement de conteneur dans un cluster Service Fabric  
> * Mettre à l’échelle les conteneurs web frontaux dans une application

## <a name="prerequisites"></a>Composants requis
À partir de la [Partie 2](service-fabric-tutorial-package-containers.md), l’application s’exécute dans un cluster Service Fabric actif.

## <a name="fail-over-a-container-in-a-cluster"></a>Basculer un conteneur dans un cluster
Service Fabric s’assure que vos instances de conteneur se déplacent automatiquement vers d’autres nœuds du cluster en cas d’échec. Vous pouvez aussi manuellement drainer un nœud de conteneurs, puis déplacer normalement ces conteneurs vers d’autres nœuds du cluster. Il existe plusieurs façon de mettre à l’échelle vos services, dans cet exemple, nous utilisons Service Fabric Explorer.

Pour basculer le conteneur frontal, effectuez les étapes suivantes :

1. Ouvrez Service Fabric Explorer dans votre cluster. Par exemple, `http://lin4hjim3l4.westus.cloudapp.azure.com:19080`.
2. Cliquez sur le nœud **fabric:/TestContainer/azurevotefront** dans l’arborescence, puis développez le nœud de la partition (représenté par un GUID). Remarquez le nom du nœud dans l’arborescence qui vous renseigne sur les nœuds en cours d’exécution dans le conteneur, par exemple `_nodetype_1`.
3. Développez le nœud **Nœuds** dans l’arborescence. Cliquez sur les points de suspension (trois points) en regard du nœud qui exécute le conteneur.
1. Choisissez **Redémarrer** pour redémarrer ce nœud et confirmer l’action de redémarrage. Le redémarrage entraîne le basculement du conteneur vers un autre nœud du cluster.

![RedémarrageDuNœud][noderestart]

Remarquez comment le nom du nœud indiquant l’emplacement où les conteneurs frontaux s’exécutent est désormais remplacé par un autre nœud du cluster. Au bout de quelques instants, vous devez être en mesure d’accéder de nouveau à l’application et la voir s’exécuter sur un autre nœud.

## <a name="scale-containers-and-services-in-a-cluster"></a>Mettre à l’échelle les conteneurs et services dans un cluster
Les conteneurs Service Fabric peuvent être mis à l’échelle dans un cluster pour s’adapter à la charge sur les services. Pour mettre à l’échelle un conteneur, vous modifiez le nombre d’instances s’exécutant dans le cluster.

Pour mettre à l’échelle le service web frontal, effectuez les étapes suivantes :

1. Ouvrez Service Fabric Explorer dans votre cluster. Par exemple, `http://lin4hjim3l4.westus.cloudapp.azure.com:19080`.
2. Cliquez sur les points de suspension (trois points) en regard du nœud **fabric:/TestContainer/azurevotefront** dans l’arborescence, puis choisissez **Mettre à l’échelle le service**.

![MettreÀL’échelleSfx][sfxscale]

Vous pouvez maintenant choisir de mettre à l’échelle le nombre d’instances du service web frontal.

3. Définissez le nombre sur **2**, puis cliquez sur **Scale Service** (Mettre à l’échelle le service).
4. Cliquez sur le nœud **fabric:/TestContainer/azurevotefront** dans l’arborescence, puis développez le nœud de la partition (représenté par un GUID).

![MiseÀL’échelleDeSfxEffectuée][sfxscaledone]

Vous constatez désormais que le service possède deux instances. Dans l’arborescence, vous voyez quels sont les nœuds sur lesquels les instances s’exécutent.

Par cette tâche de gestion simple, nous avons doublé les ressources disponibles pour permettre à notre service frontal de traiter la charge utilisateur. Il est important de comprendre que vous n’avez pas besoin de plusieurs instances d’un service pour que celui-ci s’exécute de manière fiable. En cas de défaillance d’un service, Service Fabric veille à ce qu'une nouvelle instance du service s’exécute dans le cluster.

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous a présenté le basculement d’un conteneur ainsi que la mise à l’échelle d’une application. Les étapes suivantes ont été effectuées :

> [!div class="checklist"]
> * En savoir plus sur le basculement de conteneur dans un cluster Service Fabric  
> * Mettre à l’échelle les conteneurs web frontaux dans une application

Dans cette série de didacticiels, vous avez appris à : 
> [!div class="checklist"]
> * Créer des images de conteneur
> * Envoyer des images conteneur à Azure Container Registry
> * Créer des packages de conteneurs pour Service Fabric à l’aide de Yeoman
> * Créer et exécuter une application Service Fabric avec des conteneurs
> * En savoir plus sur la gestion du basculement et de la mise à l’échelle dans Service Fabric

[noderestart]: ./media/service-fabric-tutorial-containers-failover/containersfailovertutorialnoderestart.png
[sfxscale]: ./media/service-fabric-tutorial-containers-failover/containersfailovertutorialscale.png
[sfxscaledone]: ./media/service-fabric-tutorial-containers-failover/containersfailovertutorialscaledone.png
