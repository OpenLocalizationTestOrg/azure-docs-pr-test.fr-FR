---
title: aaaStateful diagnostics de Services fiables | Documents Microsoft
description: "Fonctionnalité de diagnostic pour Reliable Services avec état"
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
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>Fonctionnalité de diagnostic pour Reliable Services avec état
Hello StatefulServiceBase de Services fiables avec état classe émet [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) les événements qui peuvent être utilisé toodebug hello service, fournissent des informations sur comment hello runtime est d’exploitation et vous aider à résoudre.

## <a name="eventsource-events"></a>Événements EventSource
Hello EventSource nom hello classe de StatefulServiceBase de Services fiables avec état est « Microsoft-ServiceFabric-Services ». Événements à partir de cette source d’événements s’affichent dans le [événements de diagnostic](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) fenêtre hello service est en cours [de débogage dans Visual Studio](service-fabric-debugging-your-application.md).

[PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Diagnostics Microsoft Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) et [Microsoft TraceEvent Library](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent) sont des exemples d’outils et de technologies permettant de collecter et/ou d’afficher des événements EventSource.

## <a name="events"></a>Événements
| Nom de l'événement | ID de l’événement | Level | Description de l’événement |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |Informations |Émis lorsque la tâche de service RunAsync est démarrée |
| StatefulRunAsyncCancellation |2 |Informations |Émis lorsque la tâche de service RunAsync est annulée |
| StatefulRunAsyncCompletion |3 |Informations |Émis lorsque la tâche de service RunAsync est terminée |
| StatefulRunAsyncSlowCancellation |4 |Avertissement |Émis lorsque la tâche du service de RunAsync prend trop de temps toocomplete d’annulation |
| StatefulRunAsyncFailure |5 |Erreur |Émis lorsque la tâche de service RunAsync renvoie une exception |

## <a name="interpret-events"></a>Interprétation des événements
Événements StatefulRunAsyncInvocation, StatefulRunAsyncCompletion et StatefulRunAsyncCancellation sont utiles toohello service Enregistreur toounderstand hello cycle de vie d’un service--ainsi que de minutage hello lorsqu’un service est démarré, annulé ou terminé . Cela peut être utile lors du débogage des problèmes de service ou de présentation hello cycle de vie du service.

Rédacteurs du service prêtez attention particulière tooStatefulRunAsyncSlowCancellation et les événements de StatefulRunAsyncFailure, car elles indiquent des problèmes avec le service de hello.

StatefulRunAsyncFailure est émis chaque fois que la tâche de RunAsync() hello service lève une exception. En règle générale, une exception indique une erreur ou un bogue dans le service hello. En outre, hello cas hello service toofail, afin qu’il soit déplacé tooa autre nœud. Cela peut être une opération coûteuse et peut retarder les demandes entrantes pendant que le service de hello est déplacé. Rédacteurs du service doivent déterminer la cause de hello d’exception de hello et, si possible, limiter ce risque.

StatefulRunAsyncSlowCancellation est émise chaque fois qu’une demande d’annulation de tâche de RunAsync hello prend plue de quatre secondes. Lorsqu’un service prend trop de temps toocomplete d’annulation, il affecte la capacité hello pour toobe de service hello rapidement redémarré sur un autre nœud. Cela peut avoir un impact sur la disponibilité globale du service de hello de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Fournisseurs EventSource dans PerfView](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
