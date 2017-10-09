---
title: "Présentation de l’API de relais aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des API Azure Relay disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fdaa1d2b-bd80-4e75-abb9-0c3d0773af2d
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: 3c4d737d5fee9a8babce094fa6dfddb28910834b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="available-relay-apis"></a>API Relay disponibles

## <a name="runtime-apis"></a>API de runtime

Hello tableau suivant répertorie tous les clients de runtime de relais actuellement disponibles.

Hello [des informations supplémentaires](#additional-information) section contient plus d’informations sur l’état de hello de chaque bibliothèque runtime.

| Langue/plateforme | Fonctionnalité disponible | Package client | Référentiel |
| --- | --- | --- | --- |
| .NET Standard | les connexions hybrides | [Microsoft.Azure.Relay](https://www.nuget.org/packages/Microsoft.Azure.Relay/) | [GitHub](https://github.com/azure/azure-relay-dotnet) |
| .NET Framework | Relais WCF | [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | N/A |
| Nœud | les connexions hybrides | [`hyco-ws`](https://www.npmjs.com/package/hyco-ws)<br/>[`hyco-websocket`](https://www.npmjs.com/package/hyco-websocket) | [GitHub](https://github.com/Azure/azure-relay-node) |

### <a name="additional-information"></a>Informations supplémentaires

#### <a name="net"></a>.NET
écosystème de .NET Hello a plusieurs runtimes, par conséquent, il existe plusieurs bibliothèques .NET pour les concentrateurs d’événements. bibliothèque .NET Standard de Hello peut être exécuté à l’aide de .NET Core ou hello .NET Framework, tandis que la bibliothèque du .NET Framework hello ne peut être exécuté dans un environnement .NET Framework. Pour plus d’informations sur .NET Framework, consultez les [versions d’infrastructure](/dotnet/articles/standard/frameworks#framework-versions).

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur Azure relais, consultez ces liens :
* [Qu’est-ce qu’Azure Relay ?](relay-what-is-it.md)
* [FAQ Relay](relay-faq.md)