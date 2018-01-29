---
title: Protection des applications Azure Service Bus contre les pannes et les sinistres | Microsoft Docs
description: "Techniques permettant de protéger les applications contre une panne Service Bus potentielle."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/06/2017
ms.author: sethm
ms.openlocfilehash: 6dd9045d7aa8d4dc8b3a1acbe6f927e232d9b505
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Bonnes pratiques pour protéger les applications contre les pannes de Service Bus et les sinistres

Les applications stratégiques doivent fonctionner en permanence, même en cas de pannes non planifiées ou de sinistres. Cette rubrique décrit les techniques que vous pouvez utiliser pour protéger les applications Service Bus contre une panne ou un sinistre potentiel.

Une panne est définie comme l'indisponibilité temporaire d'Azure Service Bus. La panne peut affecter certains composants de Service Bus, comme une banque de messagerie ou même le centre de données entier. Une fois le problème résolu, Service Bus redevient disponible. En règle générale, une panne n'entraîne pas la perte de messages ou autres données. L'indisponibilité d'une banque de messagerie spécifique constitue un exemple de défaillance d'un composant. Une panne d'alimentation ou un commutateur réseau défaillant constituent des exemples de panne au niveau du centre de données. Une panne peut durer de quelques minutes à plusieurs jours.

Un sinistre est défini comme la perte définitive d'une unité d'échelle ou d'un centre de données Service Bus. Le centre de données peut devenir disponible à nouveau ou pas. En général, un sinistre provoque la perte d'une partie ou de l'ensemble des messages ou autres données. Les incendies, les inondations ou les tremblements de terre sont des exemples de sinistres.

## <a name="current-architecture"></a>Architecture actuelle
Service Bus utilise plusieurs banques de messagerie pour stocker les messages sont envoyés à des files d’attente ou des rubriques. Une file d’attente ou une rubrique non partitionnée est affectée à une banque de messagerie. Si cette banque de messagerie n’est pas disponible, toutes les opérations sur cette file d’attente ou rubrique échoueront.

Toutes les entités de messagerie Service Bus (files d’attente, rubriques, relais) résident dans un espace de noms de service, qui est affilié à un centre de données. Service Bus ne permet pas la géo-réplication automatique des données et ne permet pas non plus qu’un espace de noms couvre plusieurs centres de données.

## <a name="protecting-against-acs-outages"></a>Protection contre les pannes ACS
Si vous utilisez des informations d'identification ACS et si ACS devient indisponible, les clients ne peuvent plus obtenir de jetons. Les clients qui ont un jeton au moment où ACS tombe en panne peuvent continuer à utiliser Service Bus jusqu'à ce que les jetons expirent. La durée de vie par défaut d'un jeton est de 3 heures.

Pour vous protéger contre les pannes ACS, utilisez des jetons SAS (Signature d'accès partagé). Dans ce cas, le client s'authentifie directement auprès de Service Bus en signant un jeton auto-émis avec une clé secrète. Les appels aux services ACS ne sont plus nécessaires. Pour plus d’informations sur les jetons SAS, consultez [Authentification Service Bus][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Protection des files d’attente et des rubriques contre les défaillances de la banque de messagerie
Une file d’attente ou une rubrique non partitionnée est affectée à une banque de messagerie. Si cette banque de messagerie n’est pas disponible, toutes les opérations sur cette file d’attente ou rubrique échoueront. D'autre part, une file d'attente partitionnée est constituée de plusieurs fragments. Chaque fragment est stocké dans une banque de messagerie différente. Lorsqu’un message est envoyé à une file d’attente ou une rubrique partitionnée, Service Bus affecte le message à l’un des fragments. Si la banque de messagerie correspondante n'est pas disponible, Service Bus écrit le message dans un fragment différent, si possible. Pour plus d’informations sur les entités partitionnées, consultez [Files d’attente et rubriques partitionnées][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Protection contre les pannes ou les sinistres du centre de données
Pour permettre un basculement entre deux centres de données, vous pouvez créer un espace de noms de service Service Bus dans chaque centre de données. Par exemple, l’espace de noms de service Service Bus **contosoPrimary.servicebus.windows.net** peut se trouver dans la région États-Unis (Nord/Centre) et **contosoSecondary.servicebus.windows.net** peut se trouver dans la région États-Unis (Sud/Centre). Si une entité de messagerie Service Bus doit rester accessible en cas de panne du centre de données, vous pouvez créer cette entité dans les deux espaces de noms.

Pour plus d’informations, consultez la section « Échec de Service Bus dans un centre de données Azure » sous [Modèles de messagerie asynchrone et haute disponibilité][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Protection des points de terminaison de relais contre les pannes ou les sinistres du centre de données
La géo-réplication des points de terminaison de relais permet à un service qui expose un point de terminaison de relais d'être accessible en cas de pannes de Service Bus. Pour obtenir la géo-réplication, le service doit créer deux points de terminaison de relais dans des espaces de noms différents. Les espaces de noms doivent résider dans des centres de données différents et les deux points de terminaison doivent avoir des noms différents. Par exemple, un point de terminaison principal peut être accessible sous **contosoPrimary.servicebus.windows.net/myPrimaryService**, alors que son homologue secondaire peut être accessible sous **contosoSecondary.servicebus.windows.net/mySecondaryService**.

Le service écoute alors sur les deux points de terminaison et un client peut appeler le service par le biais de n'importe quel point de terminaison. Une application cliente choisit de façon aléatoire l'un des relais en tant que point de terminaison principal et envoie sa requête au point de terminaison actif. Si l'opération échoue avec un code d'erreur, cette défaillance indique que le point de terminaison de relais n'est pas disponible. L'application ouvre un canal vers le point de terminaison de sauvegarde et soumet la requête à nouveau. À ce stade, les points de terminaison actif et de sauvegarde permutent leurs rôles : l'application cliente considère l'ancien point de terminaison actif comme nouveau point de terminaison de sauvegarde, et l'ancien point de terminaison de sauvegarde comme nouveau point de terminaison actif. Si les deux opérations d'envoi échouent, les rôles des deux entités restent inchangés et une erreur est renvoyée.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Protection des files d’attente et des rubriques contre les pannes ou les sinistres du centre de données
Pour obtenir une résilience contre les pannes du centre de données lors de l’utilisation de la messagerie répartie, Service Bus prend en charge deux approches : la réplication *active* et *passive*. Pour chaque approche, si une file d’attente ou une rubrique donnée doit rester accessible en cas de panne du centre de données, vous pouvez la créer dans les deux espaces de noms. Les deux entités peuvent avoir le même nom. Par exemple, une file d’attente principale peut être accessible sous **contosoPrimary.servicebus.windows.net/myQueue**, alors que son homologue secondaire peut être accessible sous **contosoSecondary.servicebus.windows.net/myQueue**.

Si l'application ne nécessite pas une communication permanente entre l'expéditeur et le destinataire, l'application peut implémenter une file d'attente côté client durable pour empêcher la perte de messages et protéger l'expéditeur contre toute erreur Service Bus temporaire.

## <a name="active-replication"></a>Réplication active
La réplication active utilise des entités dans les deux espaces de noms pour chaque opération. Tout client qui envoie un message envoie deux copies du même message. La première copie est envoyée à l’entité principale (par exemple, **contosoPrimary.servicebus.windows.net/sales**) et la deuxième copie du message est envoyée à l’entité secondaire (par exemple, **contosoSecondary.servicebus.windows.net/sales**).

Un client reçoit des messages des deux files d'attente. Le destinataire traite la première copie d'un message et la deuxième copie est supprimée. Pour supprimer les messages en double, l'expéditeur doit attribuer un identificateur unique à chaque message. Les deux copies du message doivent avoir le même identificateur. Vous pouvez utiliser les propriétés [BrokeredMessage.MessageId][BrokeredMessage.MessageId] ou [BrokeredMessage.Label][BrokeredMessage.Label] ou une propriété personnalisée, pour baliser le message. Le destinataire doit conserver une liste des messages qu'il a déjà reçus.

L’exemple [Géo-réplication avec la messagerie répartie de Service Bus][Geo-replication with Service Bus Brokered Messages] illustre la réplication active des entités de messagerie.

> [!NOTE]
> L'approche de réplication active double le nombre d'opérations ; par conséquent, cette approche peut mener à un coût plus élevé.
> 
> 

## <a name="passive-replication"></a>Réplication passive
En cas d'absence de panne, la réplication passive n'utilise qu'une seule des deux entités de messagerie. Un client envoie le message à l'entité active. Si l'opération sur l'entité active échoue avec un code d'erreur qui indique que le centre de données qui héberge l'entité active n'est pas disponible, le client envoie une copie du message à l'entité de sauvegarde. À ce stade, les entités active et de sauvegarde permutent leurs rôles : le client en charge de l'envoi considère l'ancienne entité active comme nouvelle entité de sauvegarde, et l'ancienne entité de sauvegarde comme nouvelle entité active. Si les deux opérations d'envoi échouent, les rôles des deux entités restent inchangés et une erreur est renvoyée.

Un client reçoit des messages des deux files d'attente. Étant donné qu'il est possible que le destinataire reçoive deux copies du même message, le destinataire doit supprimer les messages en double. Vous pouvez supprimer les doublons de la même façon que celle décrite pour la réplication active.

En général, la réplication passive est moins onéreuse que la réplication active, car dans la plupart des cas, une seule opération est effectuée. La latence, le débit et le coût monétaire sont identiques au scénario de la non réplication.

Lorsque vous utilisez la réplication passive, les messages peuvent être perdus ou reçus deux fois, dans les scénarios suivants :

* **Retard ou perte de message**: supposons que l'expéditeur a envoyé avec succès un message m1 à la file d'attente principale, et qu'ensuite la file d'attente devient indisponible avant que le destinataire ne reçoive m1. L'expéditeur envoie un message ultérieur m2 à la file d'attente secondaire. Si la file d'attente principale est temporairement indisponible, le destinataire reçoit m1 lorsque la file d'attente est à nouveau disponible. En cas de sinistre, le destinataire peut ne jamais recevoir m1.
* **Réception de doublons**: supposons que l'expéditeur envoie un message m à la file d'attente principale. Service Bus traite m avec succès mais ne parvient pas à envoyer une réponse. Après expiration de l'opération d'envoi, l'expéditeur envoie une copie identique de m à la file d'attente secondaire. Si le destinataire peut recevoir la première copie de m avant que la file d'attente principale ne devienne indisponible, le destinataire reçoit les deux copies de m approximativement au même moment. Si le destinataire ne peut pas recevoir la première copie de m avant que la file d'attente principale ne devienne indisponible, le destinataire ne reçoit initialement que la deuxième copie de m, mais reçoit ensuite une deuxième copie de m lorsque la file d'attente principale devient disponible.

L’exemple [Géo-réplication avec la messagerie répartie de Service Bus][Geo-replication with Service Bus Brokered Messages] illustre la réplication passive des entités de messagerie.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur la récupération d'urgence, consultez les articles suivants :

* [Continuité de l’activité Azure SQL Database][Azure SQL Database Business Continuity]
* [Conception d’applications résilientes pour Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoReplication
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
