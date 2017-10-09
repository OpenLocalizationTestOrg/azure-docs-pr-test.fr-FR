---
title: "Présentation de l’architecture de traitement du message de Service Bus aaaAzure | Documents Microsoft"
description: "Décrit l’architecture de traitement des messages hello du Bus des services Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>Architecture de Service Bus
Cet article décrit l’architecture de traitement des messages hello du Bus des services Azure.

## <a name="service-bus-scale-units"></a>Unités d'échelle de Service Bus
Service Bus est organisé par *unités d'échelle*. Une unité d’échelle est une unité de déploiement et contenait tous les composants de service hello exécution requis. Chaque région déploie une ou plusieurs unités d'échelle Service Bus.

Un espace de noms Service Bus est l’unité d’échelle tooa mappé. unité d’échelle Hello gère tous les types d’entités Service Bus (files d’attente, rubriques, abonnements). Une unité d’échelle Service Bus comprend hello suivant des composants :

* **Un ensemble de nœuds de passerelle.** Les nœuds de passerelle authentifient les requêtes entrantes. Chaque nœud de passerelle a une adresse IP publique.
* **Un ensemble de nœuds de broker de messagerie.** Les nœuds de broker de messagerie traitent les requêtes concernant les entités de messagerie.
* **Une banque de passerelle.** magasin de passerelle Hello conserve des données de hello pour chaque entité définie dans cette unité d’échelle. magasin de passerelle Hello est implémenté sur une base de données SQL Azure.
* **Plusieurs banques de messagerie.** Banques de messages contiennent des messages hello de toutes les files d’attente, rubriques et abonnements qui sont définis dans cette unité d’échelle. Elles contiennent également toutes les données d’abonnement. À moins que [partitionnement des entités de messagerie](service-bus-partitioning.md) est activé, une file d’attente ou une rubrique est mappé tooone banque de messagerie. Les abonnements sont stockés dans hello même banque de messagerie en tant que leur rubrique parente. À l’exception de Service Bus [Premium-Messaging](service-bus-premium-messaging.md), des banques de messages hello sont implémentées sur les bases de données SQL Azure.

## <a name="containers"></a>Conteneurs
Un conteneur spécifique est assigné à chaque entité de messagerie. Un conteneur est une construction logique qui utilise un seul toostore banque de messagerie toutes les données pour ce conteneur. Chaque conteneur est assigné tooa nœud service broker de messagerie. En règle générale, il existe plus de conteneurs que de nœuds de broker de messagerie. Par conséquent, chaque nœud de broker de messagerie charge plusieurs conteneurs. distribution Hello du nœud de broker messagerie conteneurs tooa est organisée de sorte que tous les nœuds de broker de messagerie sont également chargés. Si les modifications de modèle de charge de hello (par exemple, un Obtient des conteneurs hello très occupé) ou si un nœud de broker de messagerie devient temporairement indisponible, hello conteneurs sont redistribuées entre hello nœuds de broker de messagerie.

## <a name="processing-of-incoming-messaging-requests"></a>Traitement des requêtes de messagerie entrantes
Lorsqu’un client envoie une demande de tooService Bus, équilibrage de charge Azure hello achemine tooany de nœuds de passerelle hello. nœud de passerelle Hello autorise la demande de hello. Si la demande de hello s’applique à une entité de messagerie (file d’attente, rubrique, abonnement), nœud de passerelle hello recherche entité hello dans le magasin de passerelle hello et détermine dans quel hello de magasin de messagerie entité se trouve. Il recherche ensuite le nœud service broker de messagerie traite actuellement ce conteneur et envoie toothat de demande hello nœud service broker de messagerie. Hello nœud service broker de messagerie traite la demande de hello et met à jour d’état de l’entité dans le magasin de conteneur hello hello. Hello nœud service broker de messagerie puis envoie hello réponse toohello précédent nœud passerelle, qui envoie un client toohello arrière de réponse appropriée cette demande d’origine hello émis.

![Traitement des requêtes de messagerie entrantes](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez lu une vue d’ensemble de l’architecture de Service Bus, visitez hello suivant les liens pour plus d’informations :

* [Présentation de la messagerie Service Bus](service-bus-messaging-overview.md)
* [Concepts de base de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Solution de messages de file d’attente utilisant les files d’attente Service Bus](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


