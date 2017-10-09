---
title: "aaaOverview de la série de temps Azure Insights | Documents Microsoft"
description: "Introduction tooAzure temps série Insight, un nouveau service pour l’analytique de données de série de temps et les solutions IoT"
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Qu’est-ce que Azure Time Series Insights

Azure Insights de série de temps est un service cloud géré avec le stockage, analytique et les composants de visualisation qui la rendent facile tooingest, stocker, Explorer et analyser simultanément des milliards d’événements. Time Series Insights offre une vue globale de vos données, ce qui vous permet de valider rapidement vos solutions IoT et d’éviter les temps d’arrêt coûteux sur les appareils en vous aidant à identifier les tendances et anomalies cachées et à effectuer des analyses de la cause première en temps presque réel. Temps série Insights reçoit des données de série chronologique à partir de l’événement courtiers (IoT Hubs ou concentrateurs d’événements), hello de données d’index et retire les données selon une stratégie de rétention configurable. Les utilisateurs consomment des données de hello, via une expérience utilisateur ou l’API REST de requête intuitive.

![Vue d’ensemble de Time Series Insights](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Principaux scénarios

* Surveillez et validez des solutions de IoT en quelques minutes.
* Visualisez et analysez les données IoT mises à l’échelle.
* Accélérez l’analyse de la cause première et de la détection des anomalies.
* Créez une vue globale de plusieurs périphériques, sites et données.

## <a name="capabilities-and-benefits"></a>Avantages et fonctionnalités clés

* **Tooget facile démarré**: série de temps Azure Insights ne requiert aucune préparation de données initial et qu’il est extrêmement rapides. Se connecter toobillions d’événements dans votre Azure IoT Hub ou un concentrateur d’événements en quelques minutes. Une fois connecté, visualiser et interagir avec les données de capteur en secondes tooquickly valider vos solutions IoT. Temps série Insights est facile toouse ; Vous pouvez interagir avec vos données sans écrire une seule ligne de code.  Il n’existe aucune nouvelle toolearn de langage ; Aperçu de série en temps fournit une surface de la requête en texte libre granulaire pour les utilisateurs expérimentés et pointez et cliquez sur l’exploration pour tous les.

* **Près des informations en temps réel**: temps série Insights peuvent traiter des centaines de millions d’événements de capteur par jour, avec une latence d’une minute, afin de réagir rapidement toochanges. Time Series Insights vous aide à obtenir des informations approfondies sur vos données de capteur en vous aidant à identifier rapidement les tendances et anomalies rapidement, à effectuer des analyses de la cause première complexes et à éviter des interruptions de service coûteuses. En activant cross-corrélation entre les données en temps réel et historiques, temps série Insights vous permet de déverrouiller des tendances masquées dans les données de salutation.

* **Créer des solutions personnalisées** : intégrez les données Azure Time Series Insights à vos applications existantes ou créez de nouvelles solutions personnalisées avec les API REST de Time Series Insights. Création et de partage personnalisé des affichages que vous pouvez partager pour d’autres tooexplore vos découvertes.

* **Évolutivité**: temps série Insights est conçu toosupport IoT à grande échelle. Dans l’aperçu, il peut en entrée à partir de too100 1 million s’étendent sur des millions d’événements par jour, avec une durée de rétention par défaut de 31 jours. Vous pouvez visualiser et analyser les flux de données en direct en temps presque réel, en plus de quantités importantes de données historiques. Déplacement vers l’avant, taux d’entrée et de rétention augmentera tooaccommodate une échelle de l’entreprise en constante évolution.

## <a name="time-series-insights-glossary"></a>Glossaire Time Series Insights

* **Environnement** : un environnement Time Series est une ressource Azure disposant d’une capacité d’entrée et de stockage.  Clients fournir des environnements via hello portail Azure avec leur capacité requise.
* **Source d’événement** : une source d’événement Time Series Insights est dérivée d’un service Broker pour les événements tel que les concentrateurs d’événements Azure.  Un aperçu en temps série se connecte directement tooEvent Sources, de réception du flux de données hello sans écrire de code. Actuellement, Time Series Insights prend en charge les concentrateurs d’événements Azure et les IoT Hubs.
* **Données de référence**: temps série Insights fournit aux utilisateurs les données de série chronologique hello capacité toojoin avec les données de référence.  Les données de référence peuvent inclure des métadonnées sur les périphériques ou d’autres données statiques qui changent relativement peu souvent. Un aperçu en temps série joint les données de référence hello avec flux de données, ce qui permet aux utilisateurs toovisualize et analyser ces données dans quasiment en temps réel.
