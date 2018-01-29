---
title: "Diagnostic pour Reliable Services avec état dans Azure Service Fabric | Microsoft Docs"
description: "Fonctionnalité de diagnostic pour Reliable Services avec état dans Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/15/2017
ms.author: dekapur
ms.openlocfilehash: edcaaaf8f1619082b33195aedf1fb1abf32e85b1
ms.sourcegitcommit: 804db51744e24dca10f06a89fe950ddad8b6a22d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Fonctionnalité de diagnostic pour Reliable Services avec état
La classe StatefulServiceBase de Reliable Services avec état dans Azure Service Fabric émet des événements [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) qui peuvent être utilisés pour déboguer le service, fournir des informations sur le fonctionnement du runtime et vous aider lors du dépannage.

## <a name="eventsource-events"></a>Événements EventSource
Le nom EventSource de la classe StatefulServiceBase de Reliable Services avec état est « Microsoft-ServiceFabric-Services ». Les événements issus de cette source d’événements s’affichent dans la fenêtre [Événements de diagnostics](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) lorsque le service est en cours de [débogage dans Visual Studio](service-fabric-debugging-your-application.md).

[PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Diagnostics Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) et [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent) sont des exemples d’outils et de technologies permettant de collecter et/ou d’afficher des événements EventSource.

## <a name="events"></a>Événements
| Nom de l'événement | ID de l’événement | Level | Description de l’événement |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informations |Émis lorsque la tâche de service RunAsync est démarrée |
| StatefulRunAsyncCancellation |2 |Informations |Émis lorsque la tâche de service RunAsync est annulée |
| StatefulRunAsyncCompletion |3 |Informations |Émis lorsque la tâche de service RunAsync est terminée |
| StatefulRunAsyncSlowCancellation |4 |Avertissement |Émis lorsque la tâche de service RunAsync prend trop de temps pour terminer l'annulation |
| StatefulRunAsyncFailure |5 |Error |Émis lorsque la tâche de service RunAsync renvoie une exception |

## <a name="interpret-events"></a>Interprétation des événements
Les événements StatefulRunAsyncInvocation, StatefulRunAsyncCompletion et StatefulRunAsyncCancellation sont utiles à l’enregistreur du service pour comprendre le cycle de vie d’un service, ainsi que le minutage lorsqu’un service démarre, est annulé ou se termine. Cette information peut être utile lors du débogage de problèmes du service ou pour comprendre le cycle de vie du service.

Les enregistreurs de service doivent prêter attention aux événements StatefulRunAsyncSlowCancellation et StatefulRunAsyncFailure qui indiquent des problèmes liés au service.

StatefulRunAsyncFailure est émis à chaque fois que la tâche RunAsync() du service lève une exception. En général, une exception levée indique une erreur ou un bogue dans le service. En outre, l’exception entraîne l’échec du service, qui est alors déplacé vers un autre nœud. Cette opération peut s’avérer coûteuse et peut retarder les requêtes entrantes pendant le déplacement du service. Les enregistreurs de service doivent déterminer la cause de l’exception et, si possible, la résoudre.

StatefulRunAsyncSlowCancellation est émis à chaque fois qu’une requête d’annulation de la tâche RunAsync prend plus de quatre secondes. Lorsqu’un service prend trop de temps pour terminer l’annulation, cela a un impact sur la capacité du service à être redémarré rapidement sur un autre nœud. Ce scénario peut avoir un impact sur la disponibilité globale du service.

## <a name="next-steps"></a>Étapes suivantes
[Fournisseurs EventSource dans PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
