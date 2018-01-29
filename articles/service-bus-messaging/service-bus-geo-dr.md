---
title: "Géorécupération d’urgence Azure Service Bus | Microsoft Docs"
description: "Utiliser les régions géographiques pour le basculement et la récupération d’urgence dans Azure Service Bus"
services: service-bus-messaging
documentationcenter: 
author: christianwolf42
manager: timlt
editor: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: sethm
ms.openlocfilehash: fdeb9ba55fc8eade95f6fca88f47dd12aa18a480
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/16/2017
---
# <a name="azure-service-bus-geo-disaster-recovery"></a>Géorécupération d’urgence Azure Service Bus

Si tout un centre de données ou une région Azure complète (si aucune [zone de disponibilité](../availability-zones/az-overview.md) n’est utilisée) connaît un temps d’arrêt, il est essentiel que le traitement des données puisse continuer dans les autres régions ou centres de données. Pour cette raison, la *géorécupération d’urgence* et la *géoréplication* sont des fonctionnalités importantes pour les entreprises. Azure Service Bus prend en charge la géorécupération d’urgence et la géoréplication au niveau de l’espace de noms. 

La fonctionnalité de géorécupération d’urgence est disponible de manière globale pour la référence SKU Premium de Service Bus. 

## <a name="outages-and-disasters"></a>Pannes et sinistres

Il est important de noter la différence entre « panne » et « sinistre ». Une *panne* se définit comme l’indisponibilité temporaire d’Azure Service Bus. La panne impacte certains composants du service, comme une banque de messages, ou le centre de données entier. Toutefois, une fois le problème résolu, Service Bus redevient disponible. En règle générale, une panne ne provoque aucune perte de messages ou d’autres données. Une coupure de courant dans le centre de données est un exemple de panne. Certaines pannes sont uniquement dues à une courte perte de la connexion en raison de problèmes réseau ou de soucis temporaires. 

Un *sinistre* se définit comme une perte définitive ou à long terme d’un cluster Service Bus, d’une région Azure ou d’un centre de données. La région ou le centre de données peut redevenir disponible ou pas, et rester arrêté(e) pendant plusieurs heures ou jours. Les incendies, les inondations ou les tremblements de terre sont des exemples de sinistres. Un sinistre qui devient permanent peut entraîner la perte de certains messages, événements ou d’autres données. Toutefois, dans la plupart des cas, il ne doit y avoir aucune perte de données et les messages peuvent être récupérés une fois que le centre de données est sauvegardé.

La fonctionnalité de géorécupération d’urgence d’Azure Service Bus est une solution de récupération d’urgence. Les concepts et le workflow décrits dans cet article concernent des scénarios de sinistres, pas des pannes temporaires ou transitoires. Pour obtenir une présentation détaillée de la récupération d’urgence dans Microsoft Azure, consultez [cet article](/azure/architecture/resiliency/disaster-recovery-azure-applications).   

## <a name="basic-concepts-and-terms"></a>Concepts et terminologie de base

La fonctionnalité de récupération d’urgence implémente la récupération d’urgence des métadonnées, en s’appuyant sur les espaces de noms de récupération d’urgence principal et secondaire. Notez que la fonctionnalité de géorécupération d’urgence est disponible uniquement pour la [référence SKU Premium](service-bus-premium-messaging.md). Vous n’avez pas besoin de modifier la chaîne de connexion, car la connexion est établie à l’aide d’un alias.

Cet article emploie les termes suivants :

-  *Alias* : nom d’une configuration de récupération d’urgence que vous avez configurée. L’alias fournit une chaîne de connexion de nom de domaine complet (FQDN) stable. Les applications utilisent cet alias de chaîne de connexion pour se connecter à un espace de noms. 

-  *Espace de noms principal/secondaire* : espaces de noms qui correspondent à l’alias. L’espace de noms principal est « actif » et reçoit les messages (il peut s’agir d’un espace de noms existant ou nouveau). L’espace de noms secondaire est « passif » et ne reçoit pas de messages. Les métadonnées sont synchronisées entre ces deux espaces de noms, qui peuvent ainsi accepter facilement les messages sans aucune modification du code d’application ou de la chaîne de connexion. Pour vous assurer que seul l’espace de noms actif reçoit des messages, vous devez utiliser l’alias. 

-  *Métadonnées* : entités telles que des files d’attentes, des rubriques et des abonnements ; incluent également leurs propriétés sur le service associé à l’espace de noms. Notez que seules les entités et leurs paramètres sont automatiquement répliqués. Les messages ne sont pas répliqués. 

-  *Basculement* : processus d’activation de l’espace de noms secondaire.

## <a name="setup-and-failover-flow"></a>Flux de configuration et de basculement

La section suivante présente une vue d’ensemble du processus de basculement et explique comment configurer le basculement initial. 

![1][]

### <a name="setup"></a>Paramétrage

Tout d’abord, vous créez ou utilisez un espace de noms principal existant et un espace de noms secondaire, avant d’associer les deux. Cette association crée un alias qui vous servira à vous connecter. Étant donné que vous utilisez un alias, vous n’avez pas besoin de modifier les chaînes de connexion existantes. Vous pouvez uniquement ajouter de nouveaux espaces de noms à votre association de basculement. Enfin, vous devez ajouter un système de surveillance afin de détecter si un basculement est nécessaire. Dans la plupart des cas, le service fait partie d’un écosystème de grande taille. C’est pourquoi les basculements automatiques sont rarement possibles, dans la mesure où, très souvent, les basculements doivent être synchronisés avec le reste de l’infrastructure ou du sous-système.

### <a name="example"></a>exemples

Dans un exemple de ce scénario, imaginez une solution de Point de vente (PDV) qui émet des messages ou des événements. Service Bus transmet ces événements à une solution de mappage ou de reformatage, qui envoie ensuite les données mappées à un autre système pour traitement. À ce stade, tous ces systèmes peuvent être hébergés dans la même région Azure. Le choix du moment du basculement et des éléments à basculer varie selon le flux de données dans votre infrastructure. 

Vous pouvez automatiser le basculement à l’aide de systèmes de surveillance ou à l’aide de solutions de surveillance personnalisées. Toutefois, cette automatisation nécessite des tâches de planification et du travail supplémentaires, qui ne seront pas abordés dans cet article.

### <a name="failover-flow"></a>Flux de basculement

Si vous lancez le basculement, deux étapes sont requises :

1. Vous voulez être sûr de pouvoir refaire un basculement en cas de nouvelle panne. Pour cela, configurez un autre espace de noms passif et mettez à jour l’association. 

2. Tirez (pull) les messages à partir de l’ancien espace de noms principal une fois qu’il est de nouveau disponible. Après cela, utilisez cet espace de noms pour les messages réguliers en dehors de votre configuration de géorécupération ou supprimez l’ancien espace de noms principal.

> [!NOTE]
> Seule la sémantique de transfert du basculement est prise en charge. Dans ce scénario, vous basculez puis effectuez un nouveau couplage avec un nouvel espace de noms. La restauration automatique n’est pas prise en charge ; par exemple, dans un cluster SQL. 

![2][]

## <a name="management"></a>gestion

Si vous avez fait une erreur (par exemple, vous avez associé les mauvaises régions lors de la configuration initiale), vous pouvez rompre le couplage des deux espaces de noms à tout moment. Si vous souhaitez utiliser les espaces de noms couplés comme des espaces de noms standard, supprimez l’alias.

## <a name="use-existing-namespace-as-alias"></a>Utiliser l’espace de noms existant en tant qu’alias

Si vous avez un scénario dans lequel vous ne pouvez pas modifier les connexions des producteurs et des consommateurs, vous pouvez réutiliser le nom de votre espace de noms en tant que nom d’alias. Voir l’[exemple de code sur GitHub ici](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR_existing_namespace_name).

## <a name="samples"></a>Exemples

Les [exemples sur GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR2) montrent comment configurer et lancer un basculement. Ces exemples illustrent les concepts suivants :

- Paramètres requis dans Azure Active Directory pour utiliser Azure Resource Manager avec Service Bus. 
- Étapes requises pour exécuter l’exemple de code. 
- Envoi et réception à partir de l’espace de noms principal actuel. 
- Comment utiliser un espace de noms existant en tant qu’alias.

## <a name="considerations"></a>Considérations

Notez les points suivants pour cette version :

1. Dans votre planification de basculement, vous devez également tenir compte du facteur temps. Par exemple, si vous perdez la connectivité pendant plus de 15 à 20 minutes, vous pouvez décider de lancer le basculement. 
 
2. Le fait qu’aucune donnée ne soit répliquée signifie que les sessions actuellement actives ne sont pas répliquées. En outre, la détection des doublons et les messages planifiés peuvent ne pas fonctionner. Les nouvelles sessions, les messages planifiés et les nouveaux doublons fonctionneront. 

3. Le basculement d’une infrastructure distribuée complexe doit être [répétée](/azure/architecture/resiliency/disaster-recovery-azure-applications#disaster-simulation) au moins une fois. 

4. La synchronisation des entités peut prendre un certain temps, à raison d’environ 50 à 100 entités par minute. Les abonnements et les règles comptent également comme des entités. 

## <a name="next-steps"></a>étapes suivantes

- Consultez les [informations de référence de l’API REST](/rest/api/servicebus/disasterrecoveryconfigs) sur la géorécupération d’urgence.
- Exécutez [l’exemple de géorécupération d’urgence sur GitHub](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/SBGeoDR2/SBGeoDR2).
- Consultez [l’exemple d’envoi de messages à un alias](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/GeoDR/TestGeoDR/ConsoleApp1) pour la géorécupération d’urgence.

Pour en savoir plus sur la messagerie Service Bus, consultez les articles suivants :

* [Concepts de base de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Files d’attente, rubriques et abonnements Service Bus](service-bus-queues-topics-subscriptions.md)
* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Utilisation des rubriques et abonnements Service Bus](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* [API REST](/rest/api/servicebus/) 

[1]: ./media/service-bus-geo-dr/geo1.png
[2]: ./media/service-bus-geo-dr/geo2.png
