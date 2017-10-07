---
title: "Présentation de l’API de concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des API Azure Event Hubs disponibles"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3f221a0c-182d-4e39-9f3d-3a3c16c5c6ed
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 46dfcc544ff92642cfd7a967f9ec38a0d8e2bd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="available-event-hubs-apis"></a>API Event Hubs disponibles

## <a name="runtime-apis"></a>API de runtime

Hello Voici une description de tous les clients de runtime Azure Event Hubs actuellement disponibles. Alors que certaines de ces bibliothèques incluent également des fonctionnalités de gestion est limitée, il existe également [bibliothèques spécifiques](#management-apis) dédié toomanagement operations. ACCENT Hello de ces bibliothèques est toosend et recevoir des messages à partir d’un concentrateur d’événements.

Consultez [des informations supplémentaires](#additional-information) pour plus d’informations sur l’état actuel de hello de chaque bibliothèque runtime.

| Langue/plateforme | Package client | Package EventProcessorHost | Référentiel |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) | [GitHub](https://github.com/azure/azure-event-hubs-dotnet) |
| .NET Framework | [NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/) | N/A |
| Java | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22) | [Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22) | [GitHub](https://github.com/Azure/azure-event-hubs-java) |
| Nœud | [NPM](https://www.npmjs.com/package/azure-event-hubs) | N/A | [GitHub](https://github.com/Azure/azure-event-hubs-node) |
| C | N/A | N/A | [GitHub](https://github.com/Azure/azure-event-hubs-c) |

### <a name="additional-information"></a>Informations supplémentaires

#### <a name="net"></a>.NET
écosystème de .NET Hello a plusieurs runtimes, par conséquent, il existe plusieurs bibliothèques .NET pour les concentrateurs d’événements. bibliothèque .NET Standard de Hello peut être exécuté à l’aide de .NET Core ou hello .NET Framework, tandis que la bibliothèque du .NET Framework hello ne peut être exécuté dans un environnement .NET Framework. Pour plus d’informations sur .NET Framework, consultez les [versions d’infrastructure](https://docs.microsoft.com/dotnet/articles/standard/frameworks#framework-versions).

#### <a name="node"></a>Nœud

bibliothèque de Node.js Hello est actuellement en version préliminaire et est conservée par les employés de Microsoft et des collaborateurs externes à un projet de côté. Toutes les contributions, y compris le code source sont les bienvenues et seront examinées.

## <a name="management-apis"></a>API de gestion

Hello Voici la liste de toutes les bibliothèques spécifiques de gestion actuellement disponibles. Aucun de ces bibliothèques contiennent des opérations d’exécution et pour hello seul but de la gestion des entités de concentrateurs d’événements.

| Langue/plateforme | Gestion des packages | Référentiel |
| --- | --- | --- | --- |
| .NET Standard | [NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) | [GitHub](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/ResourceManagement/EventHub) |

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)