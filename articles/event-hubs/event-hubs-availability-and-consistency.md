---
title: "aaaAvailability et la cohérence dans Azure Event Hubs | Documents Microsoft"
description: "Comment tooprovide hello maximum de disponibilité et la cohérence avec les concentrateurs d’événements Azure à l’aide de partitions."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Disponibilité et cohérence dans Event Hubs

## <a name="overview"></a>Vue d'ensemble
Azure Event Hubs utilise un [modèle de partitionnement](event-hubs-features.md#partitions) tooimprove disponibilité et la parallélisation au sein d’un concentrateur d’événements unique. Par exemple, si un concentrateur d’événements a quatre partitions, et l’une de ces partitions est déplacée à partir de tooanother d’un serveur dans une opération d’équilibrage de charge, vous pouvez toujours envoyer et recevoir des trois autres partitions. En outre, avoir davantage de partitions permet toohave lecteurs simultanés plus le traitement de vos données, améliorer le débit d’agrégation. Comprendre les implications en matière de hello de partitionnement et l’ordre dans un système distribué est un aspect essentiel de la conception de la solution.

toohelp expliquent les compromis de hello entre la commande et la disponibilité, consultez hello [théorème de CAP](https://en.wikipedia.org/wiki/CAP_theorem), également connue sous le théorème de Brewer. Cette théorème de traite des choix hello entre la cohérence, la disponibilité et la tolérance de partition.

Le théorème de Brewer définit la cohérence et la disponibilité de la façon suivante :
* La tolérance de panne de partition : hello la capacité d’un toocontinue de système de traitement des données du traitement des données même en cas d’une défaillance de la partition.
* Disponibilité : un nœud sans échec renvoie une réponse raisonnable dans un délai raisonnable (sans erreurs ou expirations de délai).
* Cohérence : une lecture est garantie tooreturn hello dernière inscription pour un client donné.

## <a name="partition-tolerance"></a>Tolérance de la partition
Event Hubs repose sur un modèle de données partitionné. Vous pouvez configurer le nombre hello de partitions dans votre concentrateur d’événements pendant l’installation, mais vous ne pouvez pas modifier cette valeur ultérieurement. Étant donné que vous devez utiliser des partitions avec des concentrateurs d’événements, vous devez toomake une décision sur la disponibilité et la cohérence de votre application.

## <a name="availability"></a>Disponibilité
Hello tooget de façon la plus simple en main de concentrateurs d’événements est le comportement par défaut de hello toouse. Si vous créez un nouveau `EventHubClient` de l’objet et utilisez hello `Send` (méthode), les événements sont automatiquement distribués entre des partitions dans votre concentrateur d’événements. Ce comportement permet hello plus grande partie du temps d’activité.

Pour les cas d’usage qui nécessitent maximum hello le temps, ce modèle est préféré.

## <a name="consistency"></a>Cohérence
Dans certains scénarios, hello classement d’événements peut être important. Par exemple, vous souhaiterez peut-être votre tooprocess système back-end une commande de mise à jour avant qu’une commande delete. Dans ce cas, vous pouvez définir la clé de partition hello sur un événement, ou utiliser un `PartitionSender` objet tooonly envoyer les événements tooa certaine partition. Cela garantit que lorsque ces événements sont lus à partir de la partition de hello, ils sont lus dans l’ordre.

Avec cette configuration, gardez à l’esprit que si toowhich de partition particulière hello que vous envoyez n’est pas disponible, vous recevrez une réponse d’erreur. En tant que point de comparaison, si vous ne disposez pas d’une partition unique tooa d’affinité, hello service Event Hubs envoie votre partition disponible suivante événement toohello.

Une solution possible tooensure classement, tout en optimisant également le temps, serait tooaggregate événements dans le cadre de votre application de traitement des événements. Hello tooaccomplish de façon plus simple de cela est toostamp votre événement avec une propriété de numéro de séquence personnalisée. Hello suivant de code illustre un exemple :

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

Cet exemple envoie votre tooone d’événement des partitions disponibles de hello dans votre concentrateur d’événements et définit le numéro de séquence hello correspondant à partir de votre application. Cette solution requiert toobe état conservé par votre application de traitement, mais il donne à votre expéditeurs un point de terminaison qui est plus probable toobe disponible.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Présentation du service Event Hubs](event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](event-hubs-create.md)
