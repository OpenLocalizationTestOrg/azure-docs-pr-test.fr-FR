---
title: aaaWhat est Azure Event Hubs et pourquoi utiliser | Documents Microsoft
description: "Vue d’ensemble et introduction tooAzure concentrateurs d’événements - ingestion de télémétrie de l’échelle du Cloud à partir de sites Web, des applications et des périphériques"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Qu’est-ce qu’Event Hubs ?

Azure Event Hubs est une plateforme de diffusion de données hautement évolutive et de service d’ingestion d’événement capable de recevoir et de traiter des millions d’événements par seconde. Les concentrateurs d’événements peuvent traiter et stocker des événements, des données ou la télémétrie produits par des logiciels et appareils distribués. Les données envoyées tooan concentrateur d’événements peut être transformé et stockés à l’aide de n’importe quel fournisseur de l’analytique en temps réel ou les cartes de traitement par lot/stockage. Avec hello capacité tooprovide [fonctionnalités de publication / abonnement](https://msdn.microsoft.com/library/aa560414.aspx) avec une faible latence et à très grande échelle, les concentrateurs d’événements sert hello « sur le démarrage » pour les données volumineuses.

## <a name="why-use-event-hubs"></a>Pourquoi utiliser Azure Event Hubs ?

Les fonctionnalités de traitement des événements et données de télémétrie de cette solution sont particulièrement adaptées pour les opérations suivantes :

* L’instrumentation de l'application
* L’expérience de l'utilisateur ou le traitement du flux de travail
* Des scénarios Internet des objets (IoT)

Par exemple, les concentrateurs d’événements inclut une fonction de suivi du comportement dans les applications mobiles, des informations sur le trafic provenant de batteries de serveurs web, de capture d’événements de jeu dans les jeux de console ou des données de télémétrie collectées sur des machines industrielles, des véhicules connectés ou d’autres appareils.

## <a name="azure-event-hubs-overview"></a>Vue d'ensemble des hubs d'événements Azure

rôle courant que les concentrateurs d’événements lit dans les architectures de solution Hello est hello « porte d’entrée » pour un pipeline d’événements, souvent appelé un *ingesteur d’événements*. Un ingesteur d’événements est un composant ou service qui se trouve entre les éditeurs d’événements et de production de hello de toodecouple des consommateurs d’événements d’un flux d’événements à partir de la consommation de ces événements hello. Hello figure suivante illustre cette architecture :

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Cette solution fournit une fonctionnalité de gestion du flux de messages mais présente des caractéristiques différentes de la messagerie d’entreprise traditionnelle. Ses fonctionnalités reposent sur des scénarios de traitement des événements et un débit élevé. Par conséquent, les concentrateurs d’événements est différent de [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) de messagerie et n’implémente pas certaines des fonctionnalités hello qui sont disponibles pour [messagerie Service Bus](/azure/service-bus-messaging/) entités, telles que des rubriques.

## <a name="event-hubs-features"></a>Fonctionnalités des concentrateurs d’événements

Concentrateurs d’événements contient hello suit les éléments clés :

- [**Les éditeurs/producteurs d’événements**](event-hubs-features.md#event-publishers): une entité qui envoie le concentrateur d’événements de tooan de données. Un événement est publié via AMQP 1.0 ou HTTPS.
- [**Capturer**](event-hubs-features.md#capture): vous permet de toocapture les concentrateurs d’événements de diffusion en continu de données et les stocker dans un compte de stockage d’objets Blob Azure.
- [**Partitions**](event-hubs-features.md#partitions): permet à chaque tooonly consommateur lire un sous-ensemble spécifique, ou une partition, de hello flux d’événements.
- [**Jetons SAP**](event-hubs-features.md#sas-tokens): identifie et authentifie l’éditeur d’événements hello.
- [**Consommateurs d’événements**](event-hubs-features.md#event-consumers) : entité qui lit des données d’événement à partir d’un concentrateur d’événements. Les consommateurs d’événements se connectent via AMQP 1.0. 
- [**Groupes de consommateurs**](event-hubs-features.md#consumer-groups): fournit chaque multiple consommation d’application avec une vue distincte du flux d’événements hello, l’activation de ces tooact consommateurs indépendamment.
- [**Unités de débit**](event-hubs-features.md#capacity) : unités de capacité achetées préalablement. Une partition unique a une échelle maximale d’1 unité de débit.

Pour obtenir des détails techniques sur d’autres fonctionnalités de concentrateurs d’événements, consultez hello [vue d’ensemble des fonctionnalités de concentrateurs d’événements](event-hubs-features.md). 

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des informations de tarification détaillées des concentrateurs d’événements, consultez [Tarification des concentrateurs d’événements](https://azure.microsoft.com/pricing/details/event-hubs/).

Pour plus d’informations sur les concentrateurs d’événements, consultez hello suivant liens :

* Prise en main avec un [didacticiel des concentrateurs d’événements](event-hubs-dotnet-standard-getstarted-send.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)
* [Exemples d’applications qui utilisent des Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

