---
title: "aaaHow tooadd un environnement de Azure temps série Insights IoT Hub événement source tooyour | Documents Microsoft"
description: "Ce didacticiel décrit comment tooadd un événement de source qui est connecté tooan environnement de temps série Insights tooyour IoT Hub"
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Comment tooadd une source d’événement IoT Hub

Ce didacticiel décrit comment toouse hello tooadd portail Azure, une source d’événement qui lit à partir d’un environnement de temps série Insights tooyour IoT Hub.

## <a name="prerequisites"></a>Composants requis

Vous avez créé un IoT Hub et l’écriture d’événements tooit. Pour plus d’informations sur les IoT Hubs, consultez <https://azure.microsoft.com/services/iot-hub/>

> [Groupes de consommateurs] Chaque source d’événement de temps série Insights doit toohave son propre groupe de consommateurs dédiés qui n’est pas partagé avec les autres consommateurs. Si plusieurs lecteurs de consomment les événements à partir de hello même groupe de consommateurs, tous les lecteurs sont toosee susceptibles d’échecs. Pour plus d’informations, consultez hello [guide du développeur IoT Hub](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Choisir une option d’importation

entrer manuellement les paramètres de Hello pour la source d’événement hello ou un hub IoT peut être sélectionné parmi les hubs IoT hello qui sont tooyou disponible.
Bonjour **Option d’importation** sélecteur, choisissez une des options suivantes de hello :

* Fournir des paramètres IoT Hub manuellement
* Utiliser l’IoT Hub à partir des abonnements disponibles

### <a name="select-an-available-iot-hub"></a>Sélectionner un IoT Hub disponible

Hello tableau suivant décrit chaque option de l’onglet de Source d’événement hello avec sa description lors de la sélection d’un IoT Hub disponible en tant que source d’événements :

| Nom de la propriété | Description |
| --- | --- |
| Nom de la source d’événement | nom Hello de votre source d’événements. Ce nom doit être unique au sein de votre environnement Time Series Insights.
| Source | Choisissez **IoT Hub** toocreate une source d’événement IoT Hub.
| ID d’abonnement | Sélectionnez l’abonnement hello dans laquelle ce hub IoT a été créé.
| Nom de l’IoT Hub | Sélectionnez le nom hello Hello IoT Hub.
| Nom de la stratégie IoT Hub | Sélectionnez la stratégie d’accès hello partagé qui se trouvent sur hello onglet Paramètres de IoT Hub. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. Hello partagée de la stratégie d’accès pour votre source d’événements *doit* ont **service de se connecter** autorisations.
| Groupe de consommateurs IoT Hub | événements tooread du groupe de consommateurs Hello de hello IoT Hub. Il est vivement recommandé de toouse un groupe de consommateurs dédiés pour votre source d’événements.

### <a name="provide-iot-hub-settings-manually"></a>Fournir des paramètres IoT Hub manuellement

Hello tableau suivant décrit chaque propriété de l’onglet de Source d’événement hello avec sa description lorsque vous entrez des paramètres manuellement :

| Nom de la propriété | Description |
| --- | --- |
| Nom de la source d’événement | nom Hello de votre source d’événements. Ce nom doit être unique au sein de votre environnement Time Series Insights.
| Source | Choisissez **IoT Hub** toocreate une source d’événement IoT Hub.
| ID d’abonnement | abonnement Hello dans laquelle ce hub IoT a été créé.
| Groupe de ressources | abonnement Hello dans laquelle ce hub IoT a été créé.
| Nom de l’IoT Hub | nom de Hello de votre IoT Hub. Lorsque vous avez créé votre IoT Hub, vous lui avez également donné un nom spécifique.
| Nom de la stratégie IoT Hub | stratégie d’accès partagé de Hello, qui peut être créé sur hello onglet Paramètres de IoT Hub. Chaque stratégie d’accès partagé a un nom, les autorisations que vous définissez ainsi que des clés d’accès. Hello partagée de la stratégie d’accès pour votre source d’événements *doit* ont **service de se connecter** autorisations.
| Clé de stratégie IoT Hub | clé d’accès partagé Hello utilisé l’espace de noms Service Bus tooauthenticate access toohello. Type hello clé primaire ou secondaire ici.
| Groupe de consommateurs IoT Hub | événements tooread du groupe de consommateurs Hello de hello IoT Hub. Il est vivement recommandé de toouse un groupe de consommateurs dédiés pour votre source d’événements.

## <a name="next-steps"></a>Étapes suivantes

1. Ajouter un environnement de données access stratégie tooyour [des stratégies d’accès aux données de définition](time-series-insights-data-access.md)
1. Accéder à votre environnement Bonjour [temps série Insights portail](https://insights.timeseries.azure.com)
