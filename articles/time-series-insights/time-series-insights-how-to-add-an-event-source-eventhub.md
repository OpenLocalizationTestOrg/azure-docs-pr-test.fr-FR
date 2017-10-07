---
title: "aaaHow tooadd un environnement Azure temps série Insights de concentrateur d’événements événements source tooyour | Documents Microsoft"
description: "Ce didacticiel décrit comment tooadd un événement de source qui est connecté tooan concentrateur d’événements tooyour temps série Insights environnement"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Comment tooadd une source d’événement de concentrateur d’événements

Ce didacticiel décrit comment toouse hello tooadd portail Azure, une source d’événement qui lit à partir d’un environnement de temps série Insights tooyour concentrateur d’événements.

## <a name="prerequisites"></a>Composants requis

Vous avez créé un concentrateur d’événements et l’écriture d’événements tooit. Pour plus d’informations sur les Event Hubs, consultez <https://azure.microsoft.com/services/event-hubs/>

> [Groupes de consommateurs] Chaque source d’événement de temps série Insights doit toohave son propre groupe de consommateurs dédiés qui n’est pas partagé avec les autres consommateurs. Si plusieurs lecteurs de consomment les événements à partir de hello même groupe de consommateurs, tous les lecteurs sont toosee susceptibles d’échecs. Notez qu’il existe également une limite de 20 groupes de consommateurs par hub d’événements. Pour plus d’informations, consultez hello [Guide de programmation de concentrateurs d’événements](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Choisir une option d’importation

entrer manuellement les paramètres de Hello pour la source d’événement hello ou un concentrateur d’événements peut être sélectionné à partir des concentrateurs d’événements hello qui sont tooyou disponible.
Bonjour **Option d’importation** sélecteur, choisissez une des options suivantes de hello :

* Fournir des paramètres Event Hub manuellement
* Utiliser Event Hub événements à partir d’abonnements disponibles

### <a name="select-an-available-event-hub"></a>Sélectionner un Event Hub disponible

Hello tableau suivant décrit chaque option de l’onglet de Source d’événement hello avec sa description lors de la sélection d’un concentrateur d’événements disponibles en tant que source d’événements :

| Nom de la propriété | Description |
| --- | --- |
| Nom de la source d’événement | nom Hello de votre source d’événements. Ce nom doit être unique au sein de votre environnement Time Series Insights.
| Source | Choisissez **concentrateur d’événements** toocreate une source d’événement de concentrateur d’événements.
| ID d’abonnement | Sélectionnez l’abonnement de hello dans lequel ce concentrateur d’événements a été créé.
| Espace de noms Service Bus | Sélectionnez l’espace de noms hello Bus de Service contenant hello concentrateur d’événements.
| Nom du hub d’événements | Sélectionnez le nom hello Hello concentrateur d’événements.
| Nom de la stratégie du hub d’événements | Sélectionnez la stratégie d’accès hello partagé qui peut être créé sur l’onglet de configuration du Hub d’événements hello. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. Hello partagée de la stratégie d’accès pour votre source d’événements *doit* ont **lire** autorisations.
| Groupe de consommateurs du Event Hub | événements tooread du groupe de consommateurs Hello de hello concentrateur d’événements. Il est vivement recommandé de toouse un groupe de consommateurs dédiés pour votre source d’événements.

### <a name="provide-event-hub-settings-manually"></a>Fournir des paramètres Event Hub manuellement

Hello tableau suivant décrit chaque propriété de l’onglet de Source d’événement hello avec sa description lorsque vous entrez des paramètres manuellement :

| Nom de la propriété | Description |
| --- | --- |
| Nom de la source d’événement | nom Hello de votre source d’événements. Ce nom doit être unique au sein de votre environnement Time Series Insights.
| Source | Choisissez **concentrateur d’événements** toocreate une source d’événement de concentrateur d’événements.
| ID d’abonnement | abonnement de Hello dans lequel ce concentrateur d’événements a été créé.
| Groupe de ressources | abonnement de Hello dans lequel ce concentrateur d’événements a été créé.
| Espace de noms Service Bus | Un espace de noms Service Bus est un conteneur pour un jeu d’entités de messagerie. En créant un hub d’événements, vous avez également créé un espace de noms Service Bus.
| Nom du hub d’événements | nom de Hello de votre Hub d’événements. Lorsque vous avez créé votre Event Hub, vous lui avez également donné un nom spécifique.
| Nom de la stratégie du hub d’événements | Bonjour la stratégie d’accès partagé, qui peut être créé sur l’onglet de configuration du Hub d’événements hello. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. Hello partagée de la stratégie d’accès pour votre source d’événements *doit* ont **lire** autorisations.
| Clé de la stratégie du Event Hub | clé d’accès partagé Hello utilisé l’espace de noms Service Bus tooauthenticate access toohello. Type hello clé primaire ou secondaire ici.
| Groupe de consommateurs du Event Hub | événements tooread du groupe de consommateurs Hello de hello concentrateur d’événements. Il est vivement recommandé de toouse un groupe de consommateurs dédiés pour votre source d’événements.

## <a name="next-steps"></a>Étapes suivantes

1. Ajouter un environnement de données access stratégie tooyour [des stratégies d’accès aux données de définition](time-series-insights-data-access.md)
1. Accéder à votre environnement Bonjour [temps série Insights portail](https://insights.timeseries.azure.com)
