---
title: Comparaison des services de messagerie Azure
description: "Compare Azure Event Grid, Event Hubs et Service Bus. Recommande le service à utiliser pour différents scénarios."
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 11/15/2017
ms.author: tomfitz
ms.openlocfilehash: 94771578d94b5b9bc23451049a78506e80c87d26
ms.sourcegitcommit: 7d107bb9768b7f32ec5d93ae6ede40899cbaa894
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/16/2017
---
# <a name="choose-between-azure-services-that-deliver-messages"></a>Choisir entre des services Azure qui remettent des messages

Azure propose trois services qui facilitent la remise des messages d’événement dans une solution. Ces services sont :

* [Event Grid](/azure/event-grid/)
* [Concentrateurs d'événements](/azure/event-hubs/)
* [Service Bus](/azure/service-bus-messaging/)

Même si ces services ont des similitudes, chacun d’eux est conçu pour certains scénarios particuliers. Cet article décrit les différences entre ces services et vous aide à déterminer celui qui convient à votre application. Dans de nombreux cas, les services de messagerie sont complémentaires et peuvent être utilisés ensemble.

## <a name="event-vs-message-services"></a>Services d’événement et services de message

Il existe une distinction importante entre les services qui remettent un événement et les services qui remettent un message.

### <a name="event"></a>Événement

Un événement est une notification légère d’une action ou d’un changement d’état. Les données d’événement contiennent des informations sur ce qui est arrivé, mais ne comportent pas les données qui ont déclenché l’événement. Par exemple, un événement avertit les abonnés qu’un fichier a été créé. Il peut contenir des informations générales sur le fichier, mais pas le fichier lui-même. En règle générale, les événements déclenchent des gestionnaires d’événements pour agir en temps réel.

### <a name="message"></a>Message

Un message est constitué de données brutes générées par un service et destinées à être consommées ou stockées ailleurs. Le message contient les données qui ont déclenché le pipeline de message. Ce message peut contenir une commande en ligne tout comme des données de télémétrie utilisateur. Contrairement à une notification d’événement, l’éditeur d’un message peut attendre une réponse. Par exemple, un message contient les données brutes, mais la partie suivante du système est censée créer un fichier à partir de ces données.

## <a name="comparison-of-services"></a>Comparaison des services

| Service | Objectif | Type | Quand utiliser |
| ------- | ------- | ---- | ----------- |
| Event Grid | Programmation réactive | Répartition des événements | Réagir aux changements d’état |
| Event Hubs | Pipeline de Big Data | Diffusion en continu des événements | Données de télémétrie et streaming de données distribuées |
| Service Bus | Messages importants de l’entreprise | Message | Traitement des commandes et transactions financières |

### <a name="event-grid"></a>Event Grid

Event Grid est un fond de panier de gestion des événements qui permet la programmation réactive, pilotée par événements. Il utilise un modèle publication-abonnement. Les éditeurs émettent des événements, mais ne savent pas quels événements sont traités. Les abonnés décident quels événements ils souhaitent traiter.

Event Grid est pleinement intégré aux services Azure et peut être intégré à des services tiers. Il simplifie la consommation d’événements et réduit les coûts en éliminant la nécessité d’une interrogation constante. Event Grid achemine les événements à partir de ressources Azure et non-Azure de façon efficace et fiable. Il distribue les événements à des points de terminaison d’abonné inscrits. Le message d’événement contient les informations dont vous avez besoin pour réagir aux modifications apportées aux services et applications. Event Grid n’est pas un pipeline de données et ne fournit pas l’objet réel qui a été mis à jour.

Il présente les caractéristiques suivantes :

* Dynamiquement scalable
* Économique
* Serverless

### <a name="event-hubs"></a>Event Hubs

Azure Event Hubs est un pipeline de Big Data. Il facilite la capture, la rétention et la relecture des données de télémétrie et des données de flux d’événements. Les données peuvent provenir de nombreuses sources simultanées. Event Hubs permet de mettre les données de télémétrie et d’événements à la disposition d’un grand nombre de services d’analytique et d’infrastructures de traitement de flux. Les données sont disponibles sous forme de flux de données ou de lots d’événements regroupés. Ce service fournit une solution unique pour la récupération rapide de données à traiter en temps réel et pour la relecture répétée de données brutes stockées. Il peut capturer les données de diffusion en continu dans un fichier à des fins de traitement et d’analyse.

Il présente les caractéristiques suivantes :

* Latence faible
* Capable de recevoir et de traiter des millions d’événements par seconde

### <a name="service-bus"></a>Service Bus

Service Bus est destiné aux applications d’entreprise traditionnelles. Ces applications d’entreprise traditionnelles nécessitent des transactions, des classements, la détection des doublons et une cohérence instantanée. Service Bus permet aux applications cloud natives de fournir une gestion fiable des transitions d’état pour les processus d’entreprise. Pour le traitement de messages importants qui ne peuvent pas être perdus ou dupliqués, utilisez Azure Service Bus. De plus, Service Bus facilite la communication hautement sécurisée entre les solutions cloud hybrides et peut connecter des systèmes locaux existants aux solutions cloud.

Service Bus est un système de messagerie réparti. Il stocke les messages dans un « broker » (par exemple, une file d’attente) jusqu’à ce que le récepteur soit prêt à les recevoir.

Il présente les caractéristiques suivantes :

* Remise de messages asynchrone fiable (messagerie d’entreprise en tant que service) qui nécessite une interrogation
* Fonctionnalités de messagerie avancées telles que FIFO, traitement par lot/sessions, transactions, lettres mortes, contrôle temporel, routage, filtrage et détection des doublons

## <a name="use-the-services-together"></a>Utiliser les services ensemble

Dans certains cas, vous utilisez les services côte à côte afin qu’ils remplissent des rôles distincts. Par exemple, un site marchand peut utiliser Service Bus pour traiter les commandes, Event Hubs pour capturer les données de télémétrie du site et Event Grid pour répondre aux événements tels que l’expédition d’un article.

Dans d’autres cas, vous les liez pour former un pipeline d’événements et de données. Event Grid vous permet de répondre aux événements dans les autres services. Pour obtenir un exemple d’utilisation d’Event Grid avec Event Hubs afin de migrer des données vers un entrepôt de données, consultez [Flux de Big Data dans un entrepôt de données](event-grid-event-hubs-integration.md). L’image suivante montre le flux de travail du flux des données.

![Vue d’ensemble du flux des données](./media/compare-messaging-services/overview.png)

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur les services de messagerie Azure, consultez le billet de blog [Events, Data Points, and Messages - Choosing the right Azure messaging service for your data](https://azure.microsoft.com/blog/events-data-points-and-messages-choosing-the-right-azure-messaging-service-for-your-data/) (Événements, points de données et messages : choisir le service de messagerie Azure adéquat pour vos données).
* Pour une présentation d’Event Grid, consultez [À propos d’Event Grid](overview.md).
* Pour bien démarrer avec Event Grid, consultez [Créer et acheminer des événements personnalisés avec Azure Event Grid](custom-event-quickstart.md).
* Pour bien démarrer avec Event Hubs, consultez [Créer un espace de noms Event Hubs et un hub d’événements à l’aide du portail Azure](../event-hubs/event-hubs-create.md).
* Pour bien démarrer avec Service Bus, consultez [Créer un espace de noms Service Bus à l’aide du Portail Azure](../service-bus-messaging/service-bus-create-namespace-portal.md).