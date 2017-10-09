---
title: "procédure pas à pas d’aaaPredictive maintenance | Documents Microsoft"
description: "Une procédure pas à pas de maintenance prédictive de hello Azure IoT de solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 900d6351019489a8e2f4b98908364e3bd14975c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a>Procédure pas à pas de la solution préconfigurée de maintenance prédictive

solution de maintenance prédictive préconfigurée Hello est une solution de bout en bout pour un scénario d’entreprise qui prédit point hello auquel un échec est probablement toooccur. Vous pouvez utiliser cette solution préconfigurée de manière proactive pour des activités telles que l’optimisation de la maintenance. solution de Hello combine des services Azure IoT Suite clés, telles que IoT Hub, analytique de flux de données et un [Azure Machine Learning] [ lnk-machine-learning] espace de travail. Cet espace de travail contienne un modèle, basé sur un jeu de données exemple public, toopredict hello restant cycle de vie (RUL) un moteur d’avion. solution de Hello implémente un scénario d’entreprise IoT hello en tant que point de départ pour vous tooplan entièrement et implémenter une solution qui répond à vos propres besoins professionnels spécifiques.

## <a name="logical-architecture"></a>Architecture logique

Hello suivant schéma présente des composants logiques de hello de solution de hello préconfiguré :

![][img-architecture]

les éléments de Hello bleue sont des services Azure configurés dans la région de hello où vous avez déployé la solution de hello préconfiguré. liste de Hello des régions où vous pouvez déployer des solutions de hello préconfiguré affiche sur hello [page de configuration][lnk-azureiotsuite].

élément de Hello verte est un appareil simulé qui représente un moteur d’avion. Pour plus d’informations sur ces appareils simulés Bonjour suivant la section.

Hello éléments gris représentent des composants qui implémentent *gestion des appareils* fonctionnalités. version actuelle de Hello de solution de maintenance prédictive préconfigurée hello ne prépare pas ces ressources. toolearn savoir plus sur la gestion des appareils, consultez toohello [solution préconfigurée de surveillance à distance][lnk-remote-monitoring].

## <a name="simulated-devices"></a>Simulations d’appareils

Dans la solution de hello préconfiguré, un appareil simulé représente un moteur d’avion. solution de Hello est dotée de deux moteurs qui mappent les appareils unique tooa. Chaque moteur émet des quatre types de données de télémétrie : capteur 9, 11 de capteur, capteur 14 et capteur 15 fournissent des données de hello nécessaires pour hello apprentissage modèle toocalculate hello RUL pour le moteur de hello. Chaque appareil simulé envoie hello suivant télémétrie messages tooIoT Hub :

*Nombre de cycles*. Un cycle représente un vol d’une durée comprise entre deux et dix heures. Au cours du vol de hello, les données de télémétrie sont capturées toutes les demi-heures.

*Télémétrie*. Quatre capteurs représentent les attributs du moteur. capteurs de Hello sont génériquement étiquetés capteur 9, capteur 11, capteur 14 et 15 de capteur. Ces quatre capteurs représentent la télémétrie suffisamment tooobtain des résultats utiles à partir du modèle RUL hello. modèle de Hello utilisé dans les solutions hello préconfiguré est créé à partir d’un jeu de données publique qui inclut des données de capteur moteur réel. Pour plus d’informations sur la création de jeu de données d’origine hello hello du modèle, consultez hello [le modèle de Maintenance prédictive Cortana Intelligence galerie][lnk-cortana-analytics].

les appareils Hello simulée peuvent gérer hello suivant des commandes envoyées à partir de hello IoT hub dans les solutions hello :

| Commande | Description |
| --- | --- |
| StartTelemetry |Contrôles hello l’état de la simulation de hello.<br/>Appareil de hello démarre l’envoi de données de télémétrie |
| StopTelemetry |Contrôles hello l’état de la simulation de hello.<br/>Appareil de hello s’arrête l’envoi de données de télémétrie |

IoT Hub fournit un accusé de réception de la commande de l’appareil.

## <a name="azure-stream-analytics-job"></a>Tâche Azure Stream Analytics

**Travail : Données de télémétrie** opère sur hello appareil télémétrie flux entrant à l’aide de deux instructions :

* tout d’abord, Hello sélectionne toutes les données de télémétrie à partir d’appareils de hello et envoie ce stockage tooblob de données. À ce stade, il n’est affichée dans l’application web hello.
* Hello calcule ensuite capteur moyenne des valeurs sur une fenêtre glissante de deux minutes et les envoie via tooan de concentrateur d’événements hello **processeur d’événements**.

## <a name="event-processor"></a>Processeur d’événements
Hello **processeur d’événements hôte** s’exécute dans une tâche Web d’Azure. Hello **processeur d’événements** prend les valeurs de capteur moyenne hello pour un cycle terminé. Il transmet ensuite ces tooan valeurs API qui expose le hello formé toocalculate RUL pour un moteur. Hello API est exposé par un espace de travail Machine Learning est configuré en tant que partie de la solution de hello.

## <a name="machine-learning"></a>Machine Learning
composant d’apprentissage Hello utilise un modèle dérivé des données collectées à partir de moteurs réel. Vous pouvez naviguer toohello espace de travail Machine Learning à partir de la vignette hello sur hello [azureiotsuite.com] [ lnk-azureiotsuite] page de votre solution approvisionnée. Hello mosaïque est disponible lors de la solution de hello est Bonjour **prêt** état.


## <a name="next-steps"></a>Étapes suivantes
Maintenant vous avez vu les principaux composants de hello de solution de maintenance prédictive préconfigurée hello, vous souhaiterez peut-être toocustomize il. Consultez [Conseils sur la personnalisation des solutions préconfigurées][lnk-customize].

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]
* [IoT hello d’arrière-plan la sécurité][lnk-security-groundup]

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/