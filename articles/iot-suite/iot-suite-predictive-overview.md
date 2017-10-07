---
title: "solution préconfigurée de maintenance d’aaaPredictive | Documents Microsoft"
description: "Une description de la maintenance prédictive de hello Azure IoT Suite de solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a>Présentation de la solution préconfigurée de maintenance prédictive

Hello *maintenance prédictive* [solution préconfigurée] [ lnk_preconfigured_solutions] est un des hello [Microsoft Azure IoT Suite] [ lnk_iot_suite] préconfiguré de solutions. Cette solution intègre la collecte de données télémétriques en temps réel avec un modèle prédictif créé avec [Azure Machine Learning][lnk-machine-learning].

Avec Azure IoT Suite, vous pouvez rapidement et facilement connectez des ressources d’analyse tooand et analysez la télémétrie en temps réel dans les tableaux de bord et des visualisations. Dans la solution de maintenance prédictive hello, visualisations et des tableaux de bord hello fournissent avec les nouvelles informations qui vous peuvent de l’efficacité de lecteur et d’améliorer le flux de revenus.

## <a name="hello-scenario"></a>Hello scénario

Fabrikam est une compagnie aérienne régionale qui s’efforce d’offrir à ses clients une expérience optimale et à des prix compétitifs. Une des causes de retard des vols est liée à des problèmes de gestion, et la maintenance des moteurs d'avion est particulièrement complexe. Fabrikam doit éviter de défaillance du moteur pendant un vol à tout prix, pour qu’il examine ses moteurs régulièrement et planifie en fonction de tooa plan de maintenance. Toutefois, avion moteurs ne portez toujours hello identiques. Et certaines opérations de maintenance inutiles sont effectuées sur les moteurs. Plus important encore, les problèmes clouent les appareils au sol jusqu'à ce que l'opération de maintenance soit terminée. Si un appareil situé à un emplacement où hello techniciens droit ou pièces de rechange ne sont pas disponibles, ces problèmes peuvent être particulièrement coûteux.

moteurs Hello d’avion de Fabrikam sont instrumentés avec capteurs qui analyse les conditions du moteur au cours du vol. Fabrikam utilise hello maintenance prédictive solution toocollect hello capteur données collectées au cours du vol de hello. Après avoir années accumuler du moteur opérationnel et données de défaillance, les chercheurs de données de Fabrikam ont modélisée un Bonjour toopredict de façon restant cycle de vie (RUL) un moteur d’avion. modèle de Hello utilise une corrélation entre les données à partir de quatre des capteurs de moteur hello et usure moteur qui entraîne l’échec de tooeventual. Fabrikam interrompre la sécurité de tooensure tooperform contrôle régulier, elle peut désormais utiliser hello modèles toocompute hello RUL pour chaque moteur après chaque vol. modèle de Hello utilise télémétrie hello collectée à partir de moteurs de hello au cours du vol de hello. Fabrikam peut désormais anticiper les futurs points de défaillance, la planification de la maintenance et les réparations nécessaires.

> [!NOTE]
> modèle de solution Hello utilise des données d’usure de moteur réel.

La prédiction de point de hello lors de la maintenance n’est requise, Fabrikam peut optimiser ses coûts de tooreduce d’opérations.

Les coordinateurs de maintenance collaborent avec les planificateurs pour :

- Plan de maintenance toocoincide avec un appareil de l’arrêt à un emplacement particulier.
- Assurez-vous que suffisamment de temps est disponible pour toobe d’avion hello hors service sans provoquer l’interruption de la planification.
- tooensure de techniciens tooschedule que les appareils sont traitées efficacement sans temps d’attente.

Les responsables du contrôle des stocks reçoivent des plans de maintenance qui les aident à optimiser le processus de commande et le stock de pièces de rechange.

Ces activités activer l’heure de Fabrikam toominimize avion sol et réduisent les coûts d’exploitation tout en assurant la sécurité hello de passagers et personnel.

toounderstand comment [Azure IoT Suite] [ lnk_iot_suite] fournit aux clients les fonctionnalités de hello besoin potentiel de hello toorealize de maintenance prédictive, passez en revue cette [graphisme d’information] [lnk_infographic].

## <a name="how-hello-predictive-maintenance-solution-is-built"></a>La création de la solution de maintenance prédictive hello

solution de Hello utilise un modèle de disponibles en Azure Machine Learning existant comme un modèle tooshow ces fonctionnalités à partir de télémétrie recueillie via les services IoT Suite de l’appareil. Microsoft a créé un [modèle de régression] [ lnk_regression_model] un moteur d’avion en fonction des données disponibles publiquement<sup>\[1\]</sup>et pas à pas conseils sur la toouse hello modèle.

Hello solution de maintenance prédictive Azure IoT utilise un modèle de régression hello créé à partir de ce modèle. modèle de Hello est déployé dans votre abonnement Azure et exposée via une API générée automatiquement. solution de Hello inclut un sous-ensemble de hello représentant 4 (de 100 total) des données de test moteurs et flux de données de capteur hello 4 (de total de 21). Ces données sont suffisante tooprovide un résultat exact du modèle formé de hello.

*\[1\] A. Saxena and K. Goebel (2008). « Turbofan Engine Degradation Simulation Data Set », NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*

## <a name="get-started-with-predictive-maintenance"></a>Prise en main de la maintenance prédictive

Ce didacticiel vous montre comment tooprovision hello solution de maintenance prédictive. Il vous guide également dans les fonctionnalités de base hello de solution de maintenance prédictive hello. Vous pouvez accéder à la plupart de ces fonctionnalités via hello solution du tableau de bord qui déploie en même temps que la solution de hello préconfiguré.

toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.

> [!NOTE]
> Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk_free_trial].

1. Ouvrez une session trop[azureiotsuite.com] [ lnk-azureiotsuite] à l’aide de votre Azure des informations d’identification de compte, puis cliquez sur  **+**  toocreate une solution.
1. Cliquez sur **sélectionnez** hello **maintenance prédictive** vignette.
1. Entrez un **Nom de solution** pour votre solution préconfigurée de maintenance prédictive.
1. Sélectionnez hello **région** et **abonnement** vous souhaitez toouse tooprovision hello solution.
1. Cliquez sur **créer une Solution** hello toobegin processus de configuration. Ce processus dure généralement plusieurs minutes toorun.

### <a name="wait-for-hello-provisioning-process-toocomplete"></a>Attendez que hello toocomplete du processus de configuration

1. Cliquez sur la vignette hello pour votre solution avec **Provisioning** état.
1. Hello d’avis **les États de configuration** comme des services Azure sont déployés dans votre abonnement Azure.
1. Une fois la configuration terminée, modifications d’état hello trop**prêt**.
1. Cliquez sur Détails de hello toosee hello vignette de votre solution dans le volet de droite hello. Dans ce volet, vous pouvez lancer hello solution tableau de bord et des accès hello apprentissage espace de travail.

> [!NOTE]
> Si vous rencontrez des problèmes de déploiement de solution de hello préconfiguré, passez en revue [autorisations sur le site de azureiotsuite.com hello] [ lnk-permissions] et hello [FAQ] [ lnk-faq]. Si les problèmes de hello persistent, créer un ticket de service sur hello [portal][lnk-portal].

Existe-t-il des détails que toosee souhaitées et qui ne sont pas répertoriés pour votre solution ? Faites-nous part de vos suggestions concernant les fonctionnalités sur [UserVoice](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="view-hello-solution"></a>Afficher la solution hello

Cette section vous guide tout au long de la solution de hello l’interface utilisateur.

### <a name="predictive-maintenance-dashboard"></a>Tableau de bord de maintenance prédictive

Cette page dans l’application web de hello utilise les contrôles de PowerBI JavaScript (voir hello [référentiel de PowerBI-visuals][lnk-powerbi]) toovisualize :

* Hello les données de sortie de tâches de flux de données Analytique hello dans le stockage blob.
* Hello RUL et cycle de nombre par le moteur d’avion.

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a>En observant comportement hello de solution de cloud hello

Dans l’hello portail Azure, accédez de groupe de ressources toohello avec le nom de la solution hello choisis tooview vos ressources configurées.

![][img-resource-group]

Lorsque vous configurez la solution de hello préconfiguré, vous recevez un message électronique contenant un espace de travail de lien toohello Machine Learning. Vous pouvez également naviguer toohello espace de travail Machine Learning à partir de hello [azureiotsuite.com] [ lnk-azureiotsuite] page de votre solution approvisionnée. Une mosaïque est disponible sur cette page lors de la solution de hello est Bonjour **prêt** état.

![][img-machine-learning]

Dans le portail de solution hello, vous pouvez voir que cet exemple hello est doté d’appareils de deux toorepresent quatre périphériques simulé avec deux moteurs par avion, chacun avec quatre capteurs. Lorsque vous accédez d’abord portal de solution toohello, la simulation hello est arrêtée.

![][img-simulation-stopped]

Cliquez sur **démarrer simulation** toobegin la simulation hello. Hello historique de capteur, RUL, Cycles et RUL historique remplir le tableau de bord hello.

![][img-simulation-running]

Lorsque RUL est inférieur à 160 (un seuil arbitraire choisi à des fins de démonstration), portail de solution hello affiche un avertissement symbole suivant toohello RUL afficher. portail de solution Hello met également en surbrillance le moteur d’avion hello en jaune. Notez comment les valeurs hello RUL ont une tendance vers le bas générale globale, mais ont tendance toobounce haut et bas. Ce comportement les résultats de différentes longueurs de cycle hello et la précision du modèle hello.

![][img-simulation-warning]

la simulation complète Hello prend environ 35 minutes toocomplete 148 cycles. seuil RUL 160 Hello est remplie pour hello première fois à environ 5 minutes et les deux moteurs atteint le seuil de hello à environ 8 minutes.

simulation de Hello s’exécute via un jeu de données complet hello pour les cycles de 148 et règle sur les valeurs finales RUL et cycle.

Vous pouvez arrêter la simulation hello à n’importe quel point, mais en cliquant sur **démarrer la Simulation** relectures hello simulation du début de hello du jeu de données hello.

## <a name="next-steps"></a>Étapes suivantes

toolearn plus en détail comment Azure IoT permet des scénarios de maintenance prédictive, lire [capturer la valeur à partir de hello Internet of Things][lnk_capture_value].

Prendre un [procédure pas à pas] [ lnk-predictive-walkthrough] de solution de maintenance prédictive hello.

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Forum Aux Questions (FAQ) relatives à IoT Suite][lnk-faq]
* [IoT hello d’arrière-plan la sécurité][lnk-security-groundup]

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/