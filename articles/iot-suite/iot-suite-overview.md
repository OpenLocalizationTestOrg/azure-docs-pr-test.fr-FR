---
title: "Vue d’ensemble de la suite Microsoft Azure IoT | Microsoft Docs"
description: "Présentation de la façon dont Azure IoT Suite offre des solutions préconfigurées de l’Internet des objets pour collecter, analyser et stocker des données, fournir des visualisations et s’intégrer à d’autres systèmes."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="overview-of-azure-iot-suite"></a>Vue d’ensemble de la suite Azure IoT

Les services Azure IoT (Internet des objets) offrent un large éventail de fonctionnalités. Ces services de niveau professionnel vous permettent d’effectuer les tâches suivantes :

* Collecter des données à partir des appareils
* Analyser les flux de données en mouvement
* Stocker et interroger des jeux de données volumineux
* Visualiser les données historiques et en temps réel
* Intégrer des systèmes back-office
* Gestion de vos appareils

Pour fournir ces fonctionnalités, Azure IoT Suite regroupe plusieurs services Azure avec des extensions personnalisées en tant que *solutions préconfigurées*. Ces solutions préconfigurées sont des implémentations de base des modèles de solution IoT courants qui aident à réduire le temps dont vous avez besoin pour fournir vos solutions IoT. Les [Kits de développement logiciel IoT][lnk-sdks] vous permettent de personnaliser et d’étendre ces solutions pour répondre à vos besoins. Vous pouvez également utiliser ces solutions comme des exemples ou modèles lorsque vous développez de nouvelles solutions IoT.

La vidéo suivante offre une présentation d’Azure IoT Suite :

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Services Azure IoT de la suite Azure IoT
Les solutions préconfigurées utilisent généralement les services suivants :

* Azure IoT Suite se situe au cœur du service [Azure IoT Hub][lnk-iot-hub]. Ce service fournit les fonctionnalités de messagerie Appareil vers cloud et Cloud vers appareil, et agit comme la passerelle vers le cloud et les autres services clés IoT Suite. Le service vous permet de recevoir à grande échelle des messages provenant de vos périphériques et d’envoyer des commandes à vos périphériques. Le service vous permet également de [gérer vos appareils][lnk-device-management]. Par exemple, vous pouvez configurer, redémarrer ou effectuer une réinitialisation aux paramètres d’usine sur un ou plusieurs appareils connectés au hub.
* [Azure Stream Analytics][lnk-asa] fournit l’analyse des données en mouvement. IoT Suite utilise ce service pour traiter la télémétrie entrante, effectuer l’agrégation et détecter les événements. Les solutions préconfigurées utilisent également Stream Analytics pour traiter les messages d’information qui contiennent des données telles que les réponses de métadonnées ou de commandes provenant des appareils. Les solutions utilisent Stream Analytics pour traiter les messages provenant de vos périphériques et pour remettre ces messages à d'autres services.
* [Stockage Azure][lnk-azure-storage] et [Azure Cosmos DB][lnk-document-db] fournissent les capacités de stockage de données. Les solutions préconfigurées utilisent Blob Storage pour stocker les données de télémétrie et les rendre disponibles pour l’analyse. Les solutions utilisent Cosmos DB pour stocker les métadonnées de l’appareil et activer les fonctionnalités de gestion des appareils des solutions.
* [Azure Web Apps][lnk-web-apps] et [Microsoft Power BI][lnk-power-bi] fournissent des fonctionnalités de visualisation des données. La flexibilité de Power BI vous permet de créer rapidement vos propres tableaux de bord interactifs utilisant des données IoT Suite.

Pour une vue d’ensemble de l’architecture d’une solution IoT standard, consultez [Microsoft Azure et l’Internet des objets (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>solutions préconfigurées

IoT Suite comprend des solutions préconfigurées qui vous permettent une prise en main et une exploration rapides des scénarios IoT courants comme :

* Surveillance à distance
* Maintenance prédictive
* Fabrique connectée

Vous pouvez déployer ces solutions sur votre abonnement Azure, puis exécuter un scénario IoT complet, de bout en bout.

## <a name="next-steps"></a>Étapes suivantes

À présent que vous avez découvert une vue d’ensemble des fonctionnalités et des principaux composants d’IoT Suite, vous pouvez en apprendre davantage sur les solutions préconfigurées dans IoT Suite. Pour plus d’informations, consultez [Que sont les solutions préconfigurées IoT Azure ?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
