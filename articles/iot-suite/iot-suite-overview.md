---
title: "vue d’ensemble de Azure IoT Suite aaaMicrosoft | Documents Microsoft"
description: "Vue d’ensemble de la façon dont Azure IoT Suite remet internet de choses solutions préconfigurées toocollect, analyser et stocker des données, fournissent des visualisations et intégrer avec d’autres systèmes."
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
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Vue d’ensemble de la suite Azure IoT

Hello internet Azure des services de choses (IoT) offrent un large éventail de fonctionnalités. Ces services de niveau professionnel vous permettent d’effectuer les tâches suivantes :

* Collecter des données à partir des appareils
* Analyser les flux de données en mouvement
* Stocker et interroger des jeux de données volumineux
* Visualiser les données historiques et en temps réel
* Intégrer des systèmes back-office
* Gestion de vos appareils

toodeliver ces fonctionnalités, Azure IoT Suite packages ensemble plusieurs services Azure avec extensions personnalisées que *préconfiguré solutions*. Ces solutions préconfigurées sont des implémentations de base des modèles de solution IoT courants qui aident à tooreduce hello le temps vous toodeliver vos solutions IoT. À l’aide de hello [kits de développement logiciel IoT][lnk-sdks], vous pouvez personnaliser et étendre ces toomeet solutions vos propres exigences. Vous pouvez également utiliser ces solutions comme des exemples ou modèles lorsque vous développez de nouvelles solutions IoT.

Hello vidéo suivante fournit une introduction de tooAzure IoT Suite :

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Services Azure IoT de la suite Azure IoT
les solutions de Hello préconfiguré utilisent généralement hello suivant services :

* Core tooAzure IoT Suite est hello [Azure IoT Hub] [ lnk-iot-hub] service. Ce service fournit hello appareil-à-cloud et les fonctionnalités de messagerie cloud sur l’appareil et agit comme hello toohello de passerelle de cloud computing et hello autres principaux services IoT Suite. service de Hello vous tooreceive des messages à partir de vos appareils à grande échelle et envoyer des commandes tooyour périphériques. service de Hello vous permet également de trop[gérer vos appareils][lnk-device-management]. Par exemple, vous pouvez configurer, redémarrer ou effectuer d’usine sur un ou plusieurs hub toohello connecté de périphériques.
* [Azure Stream Analytics][lnk-asa] fournit l’analyse des données en mouvement. IoT Suite utilise ces données de télémétrie service tooprocess entrants, effectuer l’agrégation et détecter des événements. les solutions de Hello préconfiguré utilisent également les flux analytique tooprocess messages d’information qui contiennent des données telles que les réponses de métadonnées ou une commande à partir d’appareils. solutions de Hello utilisent des messages de type hello tooprocess Analytique de flux de données à partir de vos appareils et fournir des services de tooother de ces messages.
* [Le stockage Azure] [ lnk-azure-storage] et [base de données Azure Cosmos] [ lnk-document-db] fournir des capacités de stockage de données hello. Hello solutions préconfigurées utilisent télémétrie toostore de stockage blob et toomake disponible pour l’analyse. solutions de Hello utilisent les métadonnées de périphérique Cosmos DB toostore et activent les fonctionnalités de gestion des appareils hello de solutions de hello.
* [Azure Web Apps] [ lnk-web-apps] et [Microsoft Power BI] [ lnk-power-bi] fournir des capacités de visualisation de données hello. flexibilité Hello de Power BI vous permet de tooquickly générer vos propres tableaux de bord interactifs qui utilisent des données IoT Suite.

Pour une vue d’ensemble de l’architecture de hello d’une solution IoT classique, consultez [Microsoft Azure et hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>solutions préconfigurées

IoT Suite inclut des solutions préconfigurées qui activer vous tooquickly prise en main et une tooexplore hello IoT les scénarios courants, tels que :

* Surveillance à distance
* Maintenance prédictive
* Fabrique connectée

Vous pouvez déployer ces solutions de tooyour abonnement Azure, puis exécutez un scénario IoT complète, de bout en bout.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez une vue d’ensemble des possibilités de IoT Suite et quelles sont ses composants principaux, vous pouvez en savoir plus sur les solutions hello préconfiguré dans IoT Suite. Pour plus d’informations, consultez [que hello Azure IoT préconfigurées solutions ?][lnk-what-are-preconfig]

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
