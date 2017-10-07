---
title: "aaaAzure Premium de Bus de Service de messagerie Standard tarification niveaux présentation et | Documents Microsoft"
description: Couches messagerie Service Bus Premium et Standard
services: service-bus-messaging
documentationcenter: .net
author: djrosanova
manager: timlt
editor: 
ms.assetid: e211774d-821c-4d79-8563-57472d746c58
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: darosa;sethm
ms.openlocfilehash: 4eea5d86d342e858f50450308fb3d96a7a80b49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-premium-and-standard-messaging-tiers"></a>Couches messagerie Service Bus Premium et Standard

La messagerie Service Bus, qui comprend des entités telles que les files d’attente et les rubriques, associe des fonctionnalités de messagerie d’entreprise à une sémantique riche de publication et d’abonnement à l’échelle du cloud. Messagerie Service Bus est utilisée en tant que principal de communication hello pour de nombreuses solutions de cloud sophistiquées.

Hello *Premium* couche de messagerie Service Bus traite les demandes de client courantes autour de l’échelle, les performances et disponibilité pour les applications critiques. Bien que les ensembles de fonctionnalités hello sont presque identiques, ces deux niveaux de messagerie Service Bus est conçus tooserve différents cas d’usage.

Des différences de haut niveau sont mis en surbrillance dans hello tableau suivant.

| Premium | Standard |
| --- | --- |
| Débit élevé |Débit variable |
| Performances prévisibles |Latence variable |
| Prix fixe |Tarification à l’utilisation variable |
| Charge de travail tooscale capacité haut et bas |N/A |
| Taille de message too1 Mo |Taille de message des too256 Ko |

**La messagerie Service Bus Premium** fournit une isolation de ressource au niveau de l’UC et mémoire hello afin que chaque charge de travail du client s’exécute de manière isolée. Ce conteneur de ressources est appelé *unité de messagerie*. Au moins une unité de messagerie est allouée à chaque espace de noms premium. Vous pouvez acheter une, deux ou quatre unités de messagerie pour chaque espace de noms Service Bus Premium. Une charge de travail unique ou une entité peut s’étendre sur plusieurs unités de messagerie et nombre de hello d’unités de messagerie peut être modifiée à volonté, bien que la facturation est frais de taux de 24 heures ou tous les jours. Hello résulte des performances prévisibles et reproductibles pour votre solution basée sur le Bus de Service.

Au final, les performances de votre solution Service Bus sont non seulement prévisibles et répétables, mais aussi supérieures. Service Bus Premium-Messaging s’appuie sur le moteur de stockage hello introduit dans [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/). Premium-Messaging, les performances de pointe sont beaucoup plus rapidement qu’avec le niveau Standard de hello.

## <a name="premium-messaging-technical-differences"></a>Différences techniques de la messagerie Premium

Hello sections suivantes présentent quelques différences entre les éditions Premium et les niveaux de messagerie Standard.

### <a name="partitioned-queues-and-topics"></a>Files d’attente et rubriques partitionnées

Les files d’attente et rubriques partitionnées sont prises en charge dans la messagerie Premium ; en fait ces entités sont toujours partitionnées (et ne peut pas être désactivées). Toutefois, Premium partitionnée files d’attente et rubriques ne fonctionnent pas hello même façon que dans hello Basic Standard et les niveaux de messagerie Service Bus. Ne de messagerie Premium utilise pas SQL comme magasin de données et ne plus a hello concurrence ressources possibles associée à une plateforme partagée. Par conséquent, le partitionnement n’est pas nécessaire tooimprove performances. En outre, le nombre de partitions hello a été modifié de 16 partitions dans les partitions de too2 de messagerie Standard dans Premium. Avoir deux partitions garantit la disponibilité et une valeur plus appropriée pour l’environnement d’exécution hello Premium. 

Avec la messagerie Premium, lorsque vous spécifiez la taille de hello d’une entité avec [MaxSizeInMegabytes](/dotnet/api/microsoft.servicebus.messaging.queuedescription.maxsizeinmegabytes#Microsoft_ServiceBus_Messaging_QueueDescription_MaxSizeInMegabytes), que taille est répartie de manière égale entre les partitions hello 2, contrairement aux [Standard partitionnée entités](service-bus-partitioning.md#standard) les Bonjour taille totale est de 16 heures hello de taille spécifiée. 

Pour plus d’informations sur le partitionnement, voir [Files d’attentes et rubriques partitionnées](service-bus-partitioning.md).

### <a name="express-entities"></a>Entités Express

La messagerie Premium s’exécutant dans un environnement d’exécution complètement isolé, les entités express ne sont pas prises en charge dans les espaces de noms Premium. Pour plus d’informations sur la fonctionnalité d’express hello, consultez hello [QueueDescription.EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propriété.

Si vous avez le code exécuté sous tooport de messagerie et que vous souhaitez Standard de niveau Premium de toohello, vérifiez que hello [EnableExpress](/dotnet/api/microsoft.servicebus.messaging.queuedescription.enableexpress#Microsoft_ServiceBus_Messaging_QueueDescription_EnableExpress) propriété a la valeur trop**false** (valeur par défaut de hello).

## <a name="get-started-with-premium-messaging"></a>Prise en main de Premium Messaging

Mise en route avec la messagerie Premium est simple et les processus hello sont similaire toothat de messagerie Standard. Commencez par [créer un espace de noms](service-bus-create-namespace-portal.md). Veillez à sélectionner **Premium** sous **Niveau de tarification**.

![create-premium-namespace][create-premium-namespace]

Vous pouvez également créer des [espaces de noms Premium à l’aide de modèles Azure Resource Manager](https://azure.microsoft.com/en-us/resources/templates/101-servicebus-pn-ar/).


## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur la messagerie Service Bus, consultez hello rubriques suivantes.

* [Introducing Azure Service Bus Premium Messaging (Présentation de la messagerie Azure Service Bus Premium (billet de blog))](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducing Azure Service Bus Premium Messaging (Présentation de la messagerie Azure Service Bus Premium (Channel9))](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Service Bus messaging: flexible data delivery in the cloud (Messagerie Service Bus : service flexible de distribution de données dans le cloud)](service-bus-messaging-overview.md)
* [Comment les files d’attente de toouse Service Bus](service-bus-dotnet-get-started-with-queues.md)

<!--Image references-->

[create-premium-namespace]: ./media/service-bus-premium-messaging/select-premium-tier.png
