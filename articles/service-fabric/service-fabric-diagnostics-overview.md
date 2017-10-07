---
title: "aaaAzure vue d’ensemble de Diagnostics et de surveillance de l’infrastructure de Service | Documents Microsoft"
description: "Découvrez la surveillance et les diagnostics pour les clusters, applications et services Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 1ef6419863b056b76d81e915ab78df4facae88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-diagnostics-for-azure-service-fabric"></a>Surveillance et diagnostics pour Azure Service Fabric

Analyse et diagnostics sont critiques toodeveloping, tester et déployer des applications et des services dans n’importe quel environnement. Les solutions Service Fabric conviennent mieux pour planifier et implémenter une surveillance et des diagnostics afin de s’assurer que les applications et services fonctionnent comme prévu dans un environnement de développement local ou de production.

Hello principaux objectifs de l’analyse et de diagnostics sont :
* Détecter et diagnostiquer les problèmes de matériel et d’infrastructure
* Détecter les problèmes des logiciels et applications, et réduire les temps d’arrêt de service
* Comprendre la consommation des ressources et aider aux prises de décision relatives aux opérations
* Optimiser les performances des applications, des services et de l’infrastructure
* Générer des connaissances professionnelles et identifier les domaines d’amélioration


Hello workflow global de l’analyse et de diagnostics se compose de trois étapes :

1. **Génération d’événements**: inclut des événements (journaux, des traces, les événements personnalisés) au niveau d’application / service, plateforme et de l’infrastructure hello (cluster)
2. **L’agrégation d’événements**: les événements générés doivent toobe collectées et agrégées avant d’être affichées
3. **Analyse**: les événements doivent toobe visualisé et accessible dans le format ou certains tooallow pour l’analyse et l’affichage en fonction des besoins

Plusieurs produits sont disponibles qui couvre ces trois zones, et que vous êtes libre toochoose différentes technologies pour chacun. Il est important toomake vraiment qui hello divers toodeliver du ensemble en travail pièces une solution d’analyse de bout en bout pour votre cluster.

## <a name="event-generation"></a>Génération d’événement

Hello première étape de flux de travail analyse et aux diagnostics hello est la création de hello et la génération des événements et les journaux. Ces événements, les journaux et traces sont générées à deux niveaux : hello couche de plate-forme (y compris le cluster de hello, hello ordinateurs ou les actions de l’infrastructure de Service) ou hello couche d’application (aucune instrumentation ajouté tooapps et les services déploiement toohello cluster). Les événements à chacun de ces niveaux sont personnalisables, bien que Service Fabric ne fournisse pas certaines instrumentations par défaut.

En savoir plus sur [les événements de niveau plateforme](service-fabric-diagnostics-event-generation-infra.md) et [les événements de niveau application](service-fabric-diagnostics-event-generation-app.md) toounderstand, ce qui est indiqué, et comment tooadd plus d’instrumentation.

Après avoir établi une décision sur hello vous aimeriez toouse de fournisseur de journalisation, vous devez toomake que vos journaux sont en cours agrégées et stockées correctement.

## <a name="event-aggregation"></a>Agrégation des événements

Pour recueillir des journaux de hello et les événements générés par vos applications et de votre cluster, nous recommandons généralement à l’aide de [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) (collection de journal tooagent plus similaire) ou [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)(de-processus de collecte de journaux).

Collecter les journaux de l’application à l’aide d’extension de Diagnostics Windows Azure est une bonne option pour les services de Fabric de Service si la valeur de sources de journal hello et destinations ne changent pas souvent et il existe un mappage simple entre des sources de hello et leurs destinations. raison de Hello pour cela consiste à configurer des Diagnostics Windows Azure se produit au niveau du Gestionnaire de ressources hello, afin de la configuration de toohello apporter des modifications significatives nécessite la mise à jour/redéploiement de cluster de hello. En outre, son utilisation est particulièrement appropriée pour s’assurer que les journaux sont stockés dans un endroit un peu plus permanent, à partir duquel ils sont accessibles par différentes plateformes d’analyse. Cela signifie qu’elle finit par être moins efficace comme pipeline que l’utilisation d’EventFlow.

À l’aide de [EventFlow](https://github.com/Azure/diagnostics-eventflow) permet de vous toohave services envoyer les journaux directement tooan analyse et plate-forme de visualisation, et/ou toostorage. Autres bibliothèques (ILogger, Serilog, etc.) peuvent être utilisées pour hello même objectif, mais EventFlow offre hello d’ayant été conçu spécifiquement pour les services Service Fabric intra-processus journal toosupport et de la collection. Cela a tendance toohave plusieurs avantages potentiels :

* Simplicité de configuration et de déploiement
    * configuration de Hello de collecte de données de diagnostic est simplement dans le cadre de la configuration du service hello. Il s’agit de conserver facilement tooalways « synchronisé » avec hello il le reste de l’application hello
    * Vous pouvez facilement réaliser une configuration par application ou par service.
    * Configuration des destinations de données via EventFlow est simplement ajouter un package de NuGet hello approprié et en modifiant les hello *eventFlowConfig.json* fichier
* Flexibilité
    * application Hello peut envoyer des données de hello qu’elle puisse toogo, tant qu’il existe une bibliothèque de client qui prend en charge le système de stockage de données hello ciblé. Vous pouvez ajouter de nouvelles destinations selon vos besoins.
    * Vous pouvez également implémenter des règles de capture, de filtrage et d’agrégation de données complexes.
* Contexte et des données d’application toointernal accès
    * sous-système de diagnostic Hello en cours d’exécution à l’intérieur du processus de service ou application hello peut accroître facilement les traces hello avec des informations contextuelles

Une chose toonote est que ces deux options ne sont pas mutuellement exclusives et tooget possible effectuée à l’aide d’une des fonctions similaires ou autres hello, il peut également être judicieux pour vous tooset des deux. Dans la plupart des cas, combinant un agent dans le processus collection risque de tooa plus fiable de flux de travail d’analyse. Hello l’extension Azure Diagnostics (agent) peut être votre chemin d’accès choisi pour les journaux de niveau plateforme pendant que vous pouvez utiliser EventFlow (dans le processus de collection) pour les journaux de niveau application. Une fois que vous avez deviné ce qui vous convient le mieux, il est toothink temps comment vous souhaitez que votre toobe de données affichées et analysées.

## <a name="event-analysis"></a>Analyse des événements

Il existe plusieurs plateformes excellentes qui existent dans le marché de hello lorsqu’il s’agit d’analyse de toohello et la visualisation des données de surveillance et de diagnostic. Hello deux que nous recommandons sont [OMS](service-fabric-diagnostics-event-analysis-oms.md) et [Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) en raison d’une meilleure intégration de tootheir avec l’infrastructure de Service, mais vous devez également passer en revue hello [pile élastique](https://www.elastic.co/products) (en particulier si vous envisagez de l’exécution d’un cluster dans un environnement hors connexion), [Splunk](https://www.splunk.com/), ou n’importe quelle autre plateforme de votre choix.

Hello points clés pour n’importe quelle plateforme que vous choisissez doit inclure l’importance sont avec l’interface utilisateur hello et l’interrogation des options, hello données toovisualize de capacité et créer des tableaux de bord lisible et hello outils supplémentaires fournissent tooenhance votre surveillance, telles que la génération d’alertes automatisés.

En outre la plateforme toohello que vous choisissez, lorsque vous configurez un cluster Service Fabric comme une ressource Azure, vous obtenez également accès tooAzure out of box analyse pour les ordinateurs, ce qui peuvent être utiles pour les performances spécifiques et métrique.

### <a name="azure-monitor"></a>Azure Monitor

Vous pouvez utiliser [moniteur Azure](../monitoring-and-diagnostics/monitoring-overview.md) toomonitor nombreux hello ressources Azure sur lequel un cluster Service Fabric est construit. Un ensemble de mesures pour hello [ensemble d’échelle de machine virtuelle](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets) et individuels [virtuels](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesetsvirtualmachines) sont automatiquement collectées et affichées dans hello portail Azure. tooview hello collecte des informations, Bonjour portail Azure, le groupe de ressources hello select qui contient le cluster Service Fabric de hello. Ensuite, sélectionnez hello machine virtuelle ensemble d’échelle que vous souhaitez tooview. Bonjour **analyse** section, sélectionnez **métriques** tooview un graphique de valeurs de hello.

![Vue des informations de mesure collectées sur le portail Azure](media/service-fabric-diagnostics-overview/azure-monitoring-metrics.png)

graphiques de hello toocustomize, suivez les instructions de hello dans [métriques dans Microsoft Azure](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md). Vous pouvez également créer des alertes basées sur ces mesures, comme décrit dans l’article [Créer des alertes dans Azure Monitor pour les services Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Vous pouvez envoyer des alertes service de notification tooa à l’aide de crochets de web, comme décrit dans [configurer un raccordement web sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Azure Monitor ne prend en charge qu’un seul abonnement. Si vous devez toomonitor plusieurs abonnements, ou si vous avez besoin des fonctionnalités supplémentaires, [Analytique de journal](https://azure.microsoft.com/documentation/services/log-analytics/), partie de Microsoft Operations Management Suite, fournit une solution de gestion informatique globale pour locales et cloud infrastructure. Vous pouvez acheminer des données à partir du moniteur de Azure directement tooLog Analytique, afin de voir les journaux et les métriques pour votre environnement complet dans un emplacement unique.

## <a name="next-steps"></a>Étapes suivantes

### <a name="watchdogs"></a>Agents de surveillance

Une surveillance est un service séparé qui peut surveiller l’intégrité et la charge entre les services et le signalement d’intégrité pour n’importe où dans la hiérarchie du modèle d’intégrité hello. Cela peut aider à éviter les erreurs qui ne sont pas détectées en fonction de la vue hello d’un service unique. Agents de surveillance sont également un bon endroit toohost code qui effectue des actions correctives sans intervention de l’utilisateur (par exemple, le nettoyage des fichiers journaux dans le stockage à intervalles réguliers). Vous trouverez un exemple d’implémentation de service d’agent de surveillance [ici](https://github.com/Azure-Samples/service-fabric-watchdog-service).

Prise en main comprendre comment les événements et les journaux sont générés au hello [au niveau de la plateforme](service-fabric-diagnostics-event-generation-infra.md) et hello [niveau application](service-fabric-diagnostics-event-generation-app.md).
