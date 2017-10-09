---
title: "contrôle d’intégrité du véhicule aaaPredict et du pilotage habitudes - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Manuel de la solution Vehicle Telemetry Analytics
Cela **menu** lie chapitres toohello dans ce manuel. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Vue d'ensemble
Ordinateurs super ont déplacé hors de laboratoire de hello et sont désormais stationnés dans notre garage ! Ces automobiles pointe contiennent une multitude de capteurs, en leur donnant hello capacité tootrack et surveiller des millions d’événements par seconde. Nous espérons que par 2020, la plupart de ces voitures auront déjà été connecté toohello Internet. Imaginez appuyé dans grâce à cette multitude de sécurité supérieure des tooprovide de données, de fiabilité et une expérience mieux conduite ! Microsoft a réalisé ce rêve en développant Cortana Intelligence.

Intelligence de Cortana de Microsoft est de type données big entièrement gérées et avancé analytique suite vous tootransform vos données en action intelligente. Nous souhaitons toointroduce toohello Cortana Intelligence véhicule télémétrie Analytique Solution de modèle. Cette solution montre comment concessions de voiture et sociétés d’assurance automobiles fabricants peuvent utiliser des fonctions de hello de toogain Cortana Intelligence en temps réel et des analyses prédictives sur l’intégrité du véhicule et du pilotage habituelles. 

solution de Hello est implémentée comme un [modèle d’architecture lambda](https://en.wikipedia.org/wiki/Lambda_architecture) montrant le potentiel de plateforme d’analyse décisionnelle de Cortana hello pour hello en temps réel et le traitement par lots. solution de Hello : 

* fournit un simulateur de télématique des véhicules ;
* utilise Event Hubs pour la réception dans Azure de millions d’événements de télémétrie virtuels associés aux véhicules ; 
* utilise les informations de flux de données Analytique toogain en temps réel sur l’intégrité du véhicule
* conserve les données de hello dans le stockage à long terme pour l’analytique de lot plus riche. 
* bénéficie de l’apprentissage pour la détection d’anomalies dans en temps réel et insights prédictive toogain de traitement du lot.
* s’appuie sur des données de tootransform HDInsight à l’échelle et orchestration toohandle de fabrique de données, en planifiant, gestion des ressources et d’analyse de pipeline de traitement par lots hello 
* offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives à l’aide de Power BI.

## <a name="architecture"></a>Architecture
![Diagramme d’architecture de solution](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*Figure 1 – Architecture d’analyse de télémétrie de véhicule*

Cette solution inclut des éléments suivants de hello **composants Cortana Intelligence** et présente leur intégration tooend de fin :

* **Event Hubs** , pour la réception dans Azure de millions d’événements de télémétrie associés aux véhicules.
* **STREAM ANALYTICS** , pour une visibilité en temps réel sur l’état des véhicules et une conservation de ces données dans un stockage à long terme afin d’enrichir les analyses par lots.
* **Apprentissage** pour la détection d’anomalie en temps réel et les analyses prédictives toogain de traitement par lots.
* **HDInsight** est exploitée tootransform des données à grande échelle
* **Fabrique de données** gère l’orchestration, la planification, la gestion des ressources et la surveillance de pipeline de traitement par lots hello.
* **POWER BI** offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.

Cette solution utilise deux **sources de données**différentes : 

* **Simulée véhicule signaux et les diagnostics**: un simulateur de télématique véhicule émet des informations de diagnostic et des signaux qui correspondent état toohello du véhicule de hello et hello gérant le modèle à un moment donné dans le temps. 
* **Catalogue de véhicule**: un dataset de référence contenant un mappage de toomodel VIN.

