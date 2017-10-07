---
title: applications de Service Bus de Azure aaaInsulating contre les pannes et sinistres | Documents Microsoft
description: "Décrit les techniques que vous pouvez utiliser les applications tooprotect d’une panne de Bus de Service potentielle."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: fd9fa8ab-f4c4-43f7-974f-c876df1614d4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2017
ms.author: sethm
ms.openlocfilehash: 349b4968456c9f15375753d83495246f5a3ddfdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-insulating-applications-against-service-bus-outages-and-disasters"></a>Meilleures pratiques pour protéger les applications contre les pannes de Service Bus et les sinistres
Les applications critiques doivent fonctionner en permanence, même en présence de hello d’arrêts ou de catastrophes naturelles. Cette rubrique décrit les techniques que vous pouvez utiliser des applications de Service Bus tooprotect par rapport à une interruption de service potentielle ou un incident.

Une panne est définie comme une indisponibilité temporaire de hello du Bus des services Azure. panne de Hello peut affecter certains composants de Service Bus, tel qu’une banque de messages, ou hello même centre de données entier. Après avoir réglé le problème de hello, Service Bus est à nouveau disponible. En règle générale, une panne n'entraîne pas la perte de messages ou autres données. Un exemple de défaillance d’un composant est indisponibilité hello d’une banque de messagerie particulier. Un exemple d’une panne à l’échelle du centre de données est une panne de courant de centre de données hello ou un commutateur de réseau de centre de données est défectueux. Une panne peut durer quelques minutes tooa quelques jours.

Un incident est défini comme la perte définitive de hello d’une unité d’échelle Service Bus ou d’un centre de données. Centre de données Hello peut ou ne peut pas devenir disponible à nouveau. En général, un sinistre provoque la perte d'une partie ou de l'ensemble des messages ou autres données. Les incendies, les inondations ou les tremblements de terre sont des exemples de sinistres.

## <a name="current-architecture"></a>Architecture actuelle
Service Bus utilise plusieurs magasins toostore des messages envoyés tooqueues ou rubriques. Une file d’attente de non partitionnée ou une rubrique est assigné tooone banque d’informations. Si cette banque de messagerie n’est pas disponible, toutes les opérations sur cette file d’attente ou rubrique échoueront.

Toutes les entités de messagerie Service Bus (files d’attente, rubriques, relais) résident dans un espace de noms de service, qui est affilié à un centre de données. Service Bus n’active pas la géo-réplication automatique des données, ni ne permet pas qu’un espace de noms toospan plusieurs centres de données.

## <a name="protecting-against-acs-outages"></a>Protection contre les pannes ACS
Si vous utilisez des informations d'identification ACS et si ACS devient indisponible, les clients ne peuvent plus obtenir de jetons. Les clients qui ont un jeton au moment de hello ACS tombe en panne peuvent continuer toouse Service Bus jusqu'à l’expiration de jetons de hello. durée de vie Hello par défaut est de 3 heures.

tooprotect contre les pannes d’ACS, utilisez les jetons de Signature d’accès partagé (SAS). Dans ce cas, hello s’authentifie directement avec le Bus de Service en signant un jeton auto-émis avec une clé de secret principal. Appels tooACS ne sont plus nécessaires. Pour plus d’informations sur les jetons SAS, consultez [Authentification Service Bus][Service Bus authentication].

## <a name="protecting-queues-and-topics-against-messaging-store-failures"></a>Protection des files d’attente et des rubriques contre les défaillances de la banque de messagerie
Une file d’attente de non partitionnée ou une rubrique est assigné tooone banque d’informations. Si cette banque de messagerie n’est pas disponible, toutes les opérations sur cette file d’attente ou rubrique échoueront. A partitionné file d’attente, sur hello autre part, se compose de plusieurs fragments. Chaque fragment est stocké dans une banque de messagerie différente. Lorsqu’un message est envoyé tooa la file d’attente partitionnée ou une rubrique, Service Bus assigne tooone de message hello de fragments de hello. Si la banque de messagerie correspondante hello n’est pas disponible, Service Bus écrit hello message tooa autre fragment, si possible. Pour plus d’informations sur les entités partitionnées, consultez [Files d’attente et rubriques partitionnées][Partitioned messaging entities].

## <a name="protecting-against-datacenter-outages-or-disasters"></a>Protection contre les pannes ou les sinistres du centre de données
tooallow pour un basculement entre deux centres de données, vous pouvez créer un espace de noms service Bus de Service dans chaque centre de données. Par exemple, hello espace de noms Service Bus service **contosoPrimary.servicebus.windows.net** peuvent se trouver dans la région Nord-Centre des États-Unis United States hello et **contosoSecondary.servicebus.windows.net**peut se trouver dans la région États-Unis Sud-Centre des États-Unis hello. Si une entité de messagerie de Service Bus doit rester accessible en présence de hello d’une panne du centre de données, vous pouvez créer cette entité dans les deux espaces de noms.

Pour plus d’informations, consultez hello section « Défaillance de Service Bus dans un centre de données Azure » dans [asynchrone haute disponibilité et modèles de messagerie][Asynchronous messaging patterns and high availability].

## <a name="protecting-relay-endpoints-against-datacenter-outages-or-disasters"></a>Protection des points de terminaison de relais contre les pannes ou les sinistres du centre de données
Géo-réplication des points de terminaison de relais permet à un service qui expose un toobe de point de terminaison de relais est accessible en présence de hello d’interruptions de Service Bus. tooachieve géo-réplication, service de hello doit créer deux points de terminaison de relais dans différents espaces de noms. espaces de noms Hello doit se trouver dans différents centres de données et deux points de terminaison hello doivent avoir des noms différents. Par exemple, un point de terminaison principal peut être accessible sous **contosoPrimary.servicebus.windows.net/myPrimaryService**, alors que son homologue secondaire peut être accessible sous **contosoSecondary.servicebus.windows.net/mySecondaryService**.

Hello service écoute alors les deux points de terminaison, et un client peut appeler le service hello via un point de terminaison. Une application cliente de façon aléatoire choisit l’un des relais de hello comme hello du point de terminaison principal et envoie son point de terminaison demande toohello active. Si l’opération de hello échoue avec un code d’erreur, cet échec indique ce point de terminaison de relais hello n’est pas disponible. l’application Hello ouvre un point de terminaison canal toohello sauvegarde et émet à nouveau la demande de hello. À ce stade hello active et points de terminaison hello sauvegarde permutent leurs rôles : application de client hello considère hello ancien point de terminaison actif toobe hello nouveau point de terminaison de sauvegarde et hello ancien point de terminaison de sauvegarde toobe hello nouveau point de terminaison actif. Si les deux opérations d’envoi échouent, les rôles hello de deux entités de hello restent inchangés et une erreur est retournée.

Hello [géo-réplication avec Service Bus relayée messages] [ Geo-replication with Service Bus relayed Messages] exemple illustre comment des relais tooreplicate.

## <a name="protecting-queues-and-topics-against-datacenter-outages-or-disasters"></a>Protection des files d’attente et des rubriques contre les pannes ou les sinistres du centre de données
tooachieve une tolérance aux pannes de centre de données lors de l’aide de la messagerie répartie, Service Bus prend en charge les deux approches : *active* et *passif* la réplication. Pour chaque approche, si une file d’attente ou une rubrique doit rester accessible en présence de hello d’une panne du centre de données, vous pouvez le créer dans les deux espaces de noms. Les deux entités peuvent avoir hello même nom. Par exemple, une file d’attente principale peut être accessible sous **contosoPrimary.servicebus.windows.net/myQueue**, alors que son homologue secondaire peut être accessible sous **contosoSecondary.servicebus.windows.net/myQueue**.

Si l’application hello ne requiert pas de communication permanente de l’expéditeur et le destinataire, application hello peut implémenter une file d’attente côté client durable tooprevent perte et tooshield hello expéditeur d’un message à partir de toutes les erreurs temporaires de Service Bus.

## <a name="active-replication"></a>Réplication active
La réplication active utilise des entités dans les deux espaces de noms pour chaque opération. Tout client qui envoie un message envoie deux copies de hello même message. la première copie Hello est envoyée entité principale de toohello (par exemple, **contosoPrimary.servicebus.windows.net/sales**), et hello seconde copie de message de type hello est envoyé entité secondaire de toohello (par exemple,  **contosoSecondary.servicebus.windows.net/sales**).

Un client reçoit des messages des deux files d'attente. processus de récepteur Hello hello première copie d’un message, et copie hello est supprimée. toosuppress des messages en double, l’expéditeur de hello devez baliser chaque message avec un identificateur unique. Les deux copies du message de type hello doivent être balisés avec hello même identificateur. Vous pouvez utiliser hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] ou [BrokeredMessage.Label] [ BrokeredMessage.Label] propriétés, ou un Bonjour tootag de propriété personnalisée Message. récepteur de Hello doit conserver une liste de messages qu’il a déjà reçu.

Hello [géo-réplication avec Messages répartie du Service Bus] [ Geo-replication with Service Bus Brokered Messages] exemple illustre la réplication active des entités de messagerie.

> [!NOTE]
> approche de la réplication active Hello double nombre hello d’opérations, par conséquent cette approche peut entraîner des coûts de toohigher.
> 
> 

## <a name="passive-replication"></a>Réplication passive
Dans le cas d’absence de panne hello, réplication passive utilise un seul hello deux entités de messagerie. Un client envoie l’entité active du toohello message hello. Si l’opération hello sur l’entité active de hello échoue avec un code d’erreur qui indique le centre de données hello que l’entité active de hello hôtes peut être indisponible, client de hello envoie une copie de l’entité de sauvegarde toohello message hello. À ce stade hello active et les entités de sauvegarde hello permutent leurs rôles : client d’envoi hello considère hello ancienne entité active toobe hello nouvelle entité de sauvegarde et hello ancien sauvegarde entité est hello nouveau active. Si les deux opérations d’envoi échouent, les rôles hello de deux entités de hello restent inchangés et une erreur est retournée.

Un client reçoit des messages des deux files d'attente. Car il existe un risque que récepteur hello reçoit deux copies du même message, hello de hello doit supprimer les messages en double. Vous pouvez supprimer les doublons dans hello même façon que celle décrite pour la réplication active.

En général, la réplication passive est moins onéreuse que la réplication active, car dans la plupart des cas, une seule opération est effectuée. Latence, le débit et coût monétaire sont scénario de non répliquée toohello identiques.

Lorsque vous utilisez la réplication passive, Bonjour messages scénarios suivants peuvent être perdus ou reçus en double :

* **Délai de message ou de perte**: supposent que l’expéditeur de hello envoyé à une file d’attente principale toohello message m1, et puis une file d’attente hello devienne indisponible avant la réception de hello m1. expéditeur de Hello envoie une file d’attente secondaire toohello ultérieures message m2. Si la file d’attente principale de hello est temporairement indisponible, hello réception m1 une fois que la file d’attente hello est à nouveau disponible. En cas de sinistre, récepteur de hello peut ne jamais recevoir m1.
* **Réception de doublons**: supposons que cet expéditeur hello envoie une file d’attente message m toohello principal. Bus de service traite m avec succès mais échoue toosend une réponse. Après hello envoyer l’opération arrive à expiration, l’expéditeur de hello envoie une copie identique de file d’attente secondaire de m toohello. Si le récepteur de hello est en mesure de tooreceive hello première copie de m avant de la file d’attente principale de hello devienne indisponible, récepteur de hello reçoit les deux copies de m à environ hello même temps. Si le récepteur de hello n’est pas en mesure de tooreceive hello première copie de m avant de la file d’attente principale de hello devienne indisponible, récepteur de hello reçoit initialement que hello deuxième copie de m, mais reçoit ensuite une deuxième copie de m lors de la file d’attente principale de hello devienne disponible.

Hello [géo-réplication avec Service Bus répartie messages] [ Geo-replication with Service Bus Brokered Messages] exemple illustre la réplication passive des entités de messagerie.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la récupération d’urgence, consultez les articles suivants :

* [Continuité de l’activité Azure SQL Database][Azure SQL Database Business Continuity]
* [Conception d’applications résilientes pour Azure][Azure resiliency technical guidance]

[Service Bus Authentication]: service-bus-authentication-and-authorization.md
[Partitioned messaging entities]: service-bus-partitioning.md
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md#failure-of-service-bus-within-an-azure-datacenter
[Geo-replication with Service Bus Relayed Messages]: http://code.msdn.microsoft.com/Geo-replication-with-16dbfecd
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[BrokeredMessage.Label]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label
[Geo-replication with Service Bus Brokered Messages]: http://code.msdn.microsoft.com/Geo-replication-with-f5688664
[Azure SQL Database Business Continuity]: ../sql-database/sql-database-business-continuity.md
[Azure resiliency technical guidance]: /azure/architecture/resiliency
