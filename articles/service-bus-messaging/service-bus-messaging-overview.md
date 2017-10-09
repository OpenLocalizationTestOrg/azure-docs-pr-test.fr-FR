---
title: "Présentation de messagerie Service Bus aaaAzure | Documents Microsoft"
description: "Description de la messagerie Service Bus et d’Azure Relay"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f99766cb-8f4b-4baf-b061-4b1e2ae570e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: ede2904e11544d8f9428a2d657dcc77dacd95ac4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-flexible-data-delivery-in-hello-cloud"></a>Messagerie Service Bus : livraison de données flexible dans le cloud de hello
Microsoft Azure Service Bus est un service fiable de distribution des informations. Hello vise de ce service de communication toomake plus facile. Si deux ou plusieurs parties souhaitez tooexchange d’informations, dont ils ont besoin d’un animateur de communication. Service Bus est un système de communication tiers ou réparti, Il s’agit comme service postal tooa Bonjour physique. Services postaux rendre toosend très facilement différents types de lettres et de packages avec diverses garanties de remise, n’importe où dans Bonjour.

Similaire postale toohello des lettres, des Bus de Service de remise est diffusion d’informations flexible hello expéditeur et destinataire de hello. service de messagerie de Hello garantit que les informations de hello sont livrées même si les parties hello deux ne sont jamais à la fois en ligne à hello en même temps, ou si elles ne sont pas disponibles à hello exacte même temps. De cette façon, la messagerie est similaire toosending une lettre, tandis que non répartie de communication est similaire tooplacing un appel téléphonique (ou comment un appel téléphonique utilisé toobe - avant en attente et appelant ID d’appel, qui sont beaucoup plus similaire à la messagerie répartie).

expéditeur du message Hello peut également nécessiter des diverses caractéristiques, notamment la détection des doublons, les transactions, heure d’expiration et le traitement par lots de la remise. Ces modèles présentent également certaines analogies avec le service postal : tentative renouvelée de distribution, signature obligatoire, changement d'adresse ou rappel.

Service Bus prend en charge deux modèles de messagerie distincts : *Azure Relay* et la *messagerie Service Bus*.

## <a name="azure-relay"></a>Azure Relay
Hello [WCF relais](../service-bus-relay/relay-what-is-it.md) composant de relais de Azure est un service centralisé (mais très équilibré en) qui prend en charge une variété de protocoles de transport et standards de services Web. Cela inclut SOAP, WS-* et même REST. Hello [service de relais](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md) fournit une variété d’options de connectivité de relais différent et peut aider à négocier des connexions pair à pair directes lorsque cela est possible. Service Bus est optimisé pour les développeurs .NET qui utilisent hello Windows Communication Foundation (WCF), chacun avec un compte tooperformance et la convivialité, et fournit un accès complet tooits service de relais via des interfaces SOAP et REST. Cela rend possible pour n’importe quel programmation SOAP ou REST toointegrate environnement avec Service Bus.

service de relais Hello prend en charge traditionnelle à sens unique de messagerie, de messagerie demande/réponse et pair à pair de messagerie. Il prend en charge également la distribution des événements au niveau de l’étendue d’Internet tooenable publication-abonnement scénarios et communication socket bidirectionnelle pour une efficacité accrue de point à point. Dans le modèle de messagerie hello relayée, un service local connecte de service de relais toohello via un port sortant et crée un socket bidirectionnel pour adresse rendezvous spécifique de tooa communications liées. Hello client peut ensuite communiquer avec service local de hello en envoyant des messages toohello service de relais ciblant hello rendezvous adresse. service de relais Hello sera ensuite « service de relais « messages toohello local via le socket bidirectionnel de hello déjà en place. Hello client un service local de toohello connexion directe n’a pas besoin, et n’est pas tooknow informatique requis hello service réside, alors que service local de hello n’a pas besoin de ports entrants ouverts sur les pare-feu hello.

Vous lancez connexion hello entre votre service local et le service de relais hello, à l’aide d’une suite de « relais » des liaisons WCF. Coulisses de hello, les liaisons de relais hello mappent tootransport liaison éléments conçus toocreate canal composants WCF qui s’intègrent à Service Bus dans le cloud de hello.

Relais de WCF offre de nombreux avantages, mais nécessite hello serveur et client tooboth être en ligne à hello en même temps dans l’ordre toosend et recevoir des messages. Cela n’est pas optimal pour la communication HTTP-style, dans quel hello demandes peut-être pas généralement à long terme, ni pour les clients qui se connectent qu’occasionnellement, tels que les navigateurs, les applications mobiles et ainsi de suite. La messagerie répartie prend en charge la communication répartie et a ses propres avantages ; les clients et les serveurs peuvent se connecter lorsque c’est nécessaire et effectuer leurs opérations de manière asynchrone.

## <a name="brokered-messaging"></a>Messagerie répartie
En revanche toohello relayer le schéma de messagerie, Service Bus ou [messagerie répartie](service-bus-queues-topics-subscriptions.md) peut être considéré comme asynchrone ou « temporairement découplée ». Les producteurs (expéditeurs) et les consommateurs (destinataires) n’ont pas de toobe en ligne à hello même temps. infrastructure de messagerie Hello stocke de manière fiable les messages dans un « répartiteur » (par exemple, une file d’attente) jusqu'à ce que le récepteur hello est prêt tooreceive les. Ceci permet aux composants hello de hello distribué application toobe est déconnecté, soit volontairement ; par exemple, pour la maintenance ou en raison du blocage d’un composant tooa, sans affecter l’ensemble du système hello. En outre, application de réception hello peut avoir uniquement toocome en ligne à certaines heures de la journée hello, tel qu’un système de gestion de l’inventaire uniquement est requis toorun à fin hello du jour ouvrable hello.

Hello principaux composants de l’infrastructure de messagerie répartie du Service Bus hello sont des files d’attente, rubriques et abonnements.  Hello principale différence est que les rubriques prennent en charge les fonctionnalités de publication/abonnement qui peuvent être utilisées pour en fonction du contenu routage et remise une logique sophistiquée, y compris envoi toomultiple destinataires. Ces composants donnent accès à de nouveaux scénarios de messagerie asynchrone, comme le découplage temporel, la publication/abonnement et l'équilibrage de charge. Pour plus d’informations sur ces éléments de messagerie, consultez [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md).

Comme avec l’infrastructure WCF relais hello, hello messagerie répartie fonctionnalité est fournie pour les programmeurs WCF et .NET Framework, ainsi que via REST.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le Bus des services de messagerie, consultez hello rubriques suivantes.

* [Concepts de base de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md)
* [Comment les files d’attente de toouse Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Comment toouse Service Bus rubriques et abonnements](service-bus-dotnet-how-to-use-topics-subscriptions.md)

