---
title: "aaaTroubleshooting avec le suivi d’événements | Documents Microsoft"
description: "problèmes courants de Hello rencontrés lors du déploiement des services sur Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Résoudre les problèmes courants rencontrés pendant le déploiement de services dans Azure Service Fabric
Lorsque vous exécutez des services sur votre ordinateur de développement, il est facile toouse [outils de débogage de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Pour les clusters à distance, [rapports d’intégrité](service-fabric-view-entities-aggregated-health.md) sont toujours un toostart parfait. Hello plus simple tooaccess façons ces rapports sont via PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md). Cet article suppose que vous déboguez un cluster distant et que vous avez une connaissance de base toouse une de ces outils.

## <a name="application-crash"></a>Blocage d'application
Hello » Partition est inférieure à cibler le nombre de réplica ou l’instance « rapport est une bonne indication que votre service est en panne. toofind out où votre service est en panne prend un examen peu plus approfondi. Lors d’une exécution de votre service à grande l'échelle, votre meilleur ami est un ensemble de traces bien planifiées.  Nous vous suggérons d’essayer de [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) pour collecter les traces et à l’aide d’une solution comme [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) pour l’affichage et recherche les traces hello.

![Intégrité de la partition SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Au cours de l’initialisation du service ou de l’acteur
Toutes les exceptions avant l’initialisation du type de service hello entraîne hello processus toocrash. Pour ces types de pannes, journal des événements application hello affiche erreur hello à partir de votre service.
Il s’agit de hello courants exceptions toosee avant l’initialisation du service de hello.

***System.IO.FileNotFoundException***

Cette erreur est souvent en raison des dépendances d’assembly toomissing. Vérifiez la propriété CopyLocal hello dans Visual Studio ou hello global assembly cache pour le nœud de hello.

***System.Runtime.InteropServices.COMException*** *à System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Cela indique que ce nom de type hello service inscrit ne correspond pas au manifeste de service hello.

[Diagnostics Azure](service-fabric-diagnostics-how-to-setup-wad.md) peut être un journal des événements application hello tooupload configuré pour tous les nœuds de votre automatiquement.

### <a name="runasync-or-onactivateasync"></a>RunAsync() or OnActivateAsync()
Si l’incident de hello se produit lors de l’initialisation de hello ou en cours d’exécution de votre type de service inscrit ou un acteur, hello exception sera interceptée par Azure Service Fabric. Vous pouvez afficher à partir des fournisseurs de EventSource hello détaillées dans la section « Étapes suivantes » de hello.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les diagnostics existants fournis par Service Fabric :

* [Diagnostics Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Diagnostics Reliable Services](service-fabric-reliable-services-diagnostics.md)

