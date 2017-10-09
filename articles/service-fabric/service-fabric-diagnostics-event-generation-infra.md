---
title: aaaAzure analyse au niveau de Service Fabric plateforme | Documents Microsoft
description: "En savoir plus sur les événements de niveau plateforme et journaux utilisé toomonitor et diagnostiquer les clusters Azure Service Fabric."
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
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: f8fb1c8b546e05c517ae12c91906acc04cd6eaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="platform-level-event-and-log-generation"></a>Événement au niveau de la plateforme et génération de journal

## <a name="monitoring-hello-cluster"></a>Surveillance de cluster de hello

Il est important toomonitor à toodetermine de niveau de plate-forme hello ou non votre matériel et le cluster sont comportent comme prévu. Bien que le Service Fabric peuvent conserver des applications qui s’exécutent lors d’une défaillance matérielle, mais vous devez toujours toodiagnose si une erreur se produit dans une application ou dans l’infrastructure sous-jacente de hello. Vous également devez surveiller votre plan de toobetter de clusters de la capacité, aider dans les décisions sur l’ajout ou suppression de matériel.

Service Fabric fournit cinq autre journal canaux out-of-du-box qui génèrent hello suivant des événements :

* Canal opérationnel : dont disposent les opérations effectuées par le Service Fabric et cluster hello, y compris les événements d’un nœud à venir, une application en cours de déploiement, ou une mise à niveau de la restauration, etc. de df.
* Canal opérationnel - détaillé : rapports d’intégrité et décisions d’équilibrage de charge
* Canal de données et de messagerie : journaux critiques et les événements générés dans notre messagerie (actuellement uniquement hello ReverseProxy) et le chemin d’accès de données (modèles de services fiables)
* Canal de données & messagerie - détaillée : canal de commentaires qui contient tous les journaux non critiques hello à partir de données et de messagerie dans le cluster hello (cette chaîne a un volume très élevé d’événements)   
* [Événements Reliable Services](service-fabric-reliable-services-diagnostics.md) : événements spécifiques au modèle de programmation
* [Événements Reliable Actors](service-fabric-reliable-actors-diagnostics.md) : compteurs de performances et événements spécifiques au modèle de programmation
* Prend en charge les journaux : les journaux système générés par toobe uniquement de l’infrastructure de Service utilisé par nous lors de la prise en charge

Ces différents canaux couvre la majorité de journalisation au niveau hello plateforme recommandée. niveau de plate-forme tooimprove journalisation, envisagez d’utiliser une meilleure compréhension hello modèle d’intégrité et ajouter des rapports d’état personnalisé et ajout personnalisé **les compteurs de Performance** toobuild une incidence sur une compréhension en temps réel de hello vos services et les applications sur un cluster de hello.

### <a name="azure-service-fabric-health-and-load-reporting"></a>Rapports d’intégrité et de charge Azure Service Fabric

Service Fabric présente son propre modèle de contrôle d’intégrité, qui est détaillé dans les articles suivants :
- [Surveillance de l’intégrité de l’ensemble fibre optique tooService introduction](service-fabric-health-introduction.md)
- [Signaler et contrôler l’intégrité du service](service-fabric-diagnostics-how-to-report-and-check-service-health.md)
- [Ajout de rapports d’intégrité Service Fabric personnalisés](service-fabric-report-health.md)
- [Affichage rapports d’intégrité de Service Fabric](service-fabric-view-entities-aggregated-health.md)

Contrôle d’intégrité est critique toomultiple les aspects de l’exploitation d’un service. Le contrôle d’intégrité est particulièrement important lorsque Service Fabric effectue la mise à niveau d’une application nommée. Une fois chaque domaine de mise à niveau du service de hello est mise à niveau et les clients tooyour disponibles, domaine de mise à niveau hello doit passer les vérifications d’intégrité avant le déploiement de hello déplace le domaine de mise à niveau suivant toohello. Si l’état d’intégrité ne peut pas être atteinte, déploiement de hello est restaurée, afin que l’application hello est dans un état correct connu. Bien que certains clients peuvent être affectées avant que les services de hello sont annulées, la plupart des clients ne sont pas rencontrer un problème. En outre, une résolution se produit assez rapidement et sans avoir toowait pour l’action à partir d’un opérateur humain. Bonjour plusieurs vérifications d’intégrité qui sont incorporées dans votre code, hello plus fiable pour que votre service est toodeployment problèmes.

Un autre aspect de l’intégrité du service signale les métriques à partir du service de hello. Métriques sont importantes dans l’infrastructure de Service, car ils sont utilisés toobalance l’utilisation des ressources. Les mesures peuvent aussi servir d’indicateur de l’intégrité du système. Par exemple, vous pouvez avoir une application qui comporte de nombreux services, chaque instance envoyant des rapports sur une mesure de demandes par seconde (RPS). Si un service utilise davantage de ressources qu’un autre service, Service Fabric déplace des instances de service autour de cluster de hello, l’utilisation des ressources même tootry toomaintain. Pour une explication plus détaillée du fonctionnement de l’utilisation des ressources, consultez [Gestion de la consommation des ressources et des charges dans Service Fabric à l’aide de mesures](service-fabric-cluster-resource-manager-metrics.md).

Les mesures peuvent également vous renseigner sur les performances de votre service. Au fil du temps, vous pouvez utiliser toocheck de métriques hello service fonctionne dans les paramètres attendus. Par exemple, si les tendances révèlent sur hello du lundi matin à 9 moyenne RPS est 1 000, vous pouvez configurer un rapport d’intégrité qui vous alerte si hello RPS est inférieur à 500 ou au-dessus de 1 500. Tous les éléments peuvent être parfaitement, mais il peut être intéressant d’un aspect toobe sûr que vos clients bénéficient d’une expérience optimale. Votre service peut définir un ensemble de mesures qui peuvent être signalées pour à des fins de vérification d’intégrité, mais qui n’affectent pas l’équilibrage des ressources hello du cluster de hello. toodo, toozero de poids (métrique) hello ensemble. Nous vous recommandons de démarrer toutes les métriques avec un poids de zéro pas augmenter les poids hello jusqu'à ce que vous êtes sûr que vous comprenez l’impact de la pondération des métriques de hello sur les ressources de votre cluster d’équilibrage.

> [!TIP]
> N’utilisez pas un trop grand nombre de mesures pondérées. Il peut être difficile toounderstand pourquoi les instances de service sont déplacés pour équilibrage de charge. Quelques mesures peuvent en dire long !

Toutes les informations qui indiquent la santé hello et les performances de votre application sont un candidat pour les rapports d’intégrité et de métriques. Un compteur de performances du processeur peut vous renseigner sur l’utilisation de votre nœud, mais il ne vous permet pas de savoir si un service particulier est intègre, car plusieurs services peuvent s’exécuter sur un seul nœud. Mais, RPS, éléments de traitement, comme les métriques et latence des demandes tous les peut indiquer intégrité hello d’un service spécifique.

contrôle d’intégrité tooreport, toothis similaire de code utiliser :

  ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
  ```

tooreport une mesure, utilisez toothis similaire de code :

  ```csharp
    this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("MemoryInMb", 1234), new LoadMetric("metric1", 42) });
  ```

### <a name="service-fabric-support-logs"></a>Journaux de support Service Fabric

Si vous devez toocontact prise en charge de Microsoft pour de l’aide avec votre cluster Azure Service Fabric, les journaux de prise en charge sont presque toujours nécessaires. Si votre cluster est hébergé dans Azure, ces journaux sont automatiquement configurés et collectés lors de la création du cluster. Hello journaux sont stockés dans un compte de stockage dédié dans le groupe de ressources de votre cluster. compte de stockage Hello ne dispose pas un nom fixe, alors que le compte de hello, conteneurs d’objets blob et les tables dont les noms qui commencent par *l’ensemble fibre optique*. Pour plus d’informations sur la configuration de la collecte de journaux pour un cluster autonome, consultez [Créer et gérer un cluster Azure Service Fabric autonome](service-fabric-cluster-creation-for-windows-server.md) et [Paramètres de configuration pour un cluster Windows autonome](service-fabric-cluster-manifest.md). Pour les instances de Service Fabric autonomes, hello journaux doivent être envoyés par partage de fichiers local tooa. Vous êtes **requis** toohave ces journaux pour prise en charge, mais ils ne sont pas prévu toobe utilisable par tout le monde en dehors de l’équipe de support client Microsoft hello.

## <a name="enabling-diagnostics-for-a-cluster"></a>Activation des diagnostics pour un cluster

Dans parti de tootake ordre de ces journaux, il est recommandé que « Diagnostics » est activé lors de la création du cluster. En activant les diagnostics, lorsque hello cluster est déployé, les Diagnostics Windows Azure est en mesure de tooacknowledge hello opérationnel, des Services fiables et les canaux Reliable actors et données du magasin de hello comme expliqué plus en détail [agréger des événements avec Diagnostics Azure](service-fabric-diagnostics-event-aggregation-wad.md).

Comme indiqué ci-dessus, il existe également un champ facultatif de tooadd une clé d’instrumentation Application Insights (AI). Si vous choisissez toouse AI pour l’analyse de n’importe quel événement (en savoir plus à ce sujet dans [analyse des événements avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)), insérez hello AppInsights ressource instrumentationKey (GUID) à cet emplacement.


Si vous vous apprêtez à cluster de tooyour toodeploy conteneurs, activez toopick WAD des statistiques de docker en ajoutant cette tooyour « DiagnosticMonitorConfiguration de > WadCfg » :

```json
"DockerSources": {
    "Stats": {
        "enabled": true,
        "sampleRate": "PT1M"
    }
},

```

## <a name="measuring-performance"></a>Mesure des performances

Mesurer les performances de votre cluster vous aidera à comprendre la façon dont il toohandle en mesure des décisions de charge et le lecteur autour de la mise à l’échelle de votre cluster (voir plus d’informations sur la mise à l’échelle d’un cluster [sur Azure](service-fabric-cluster-scale-up-down.md), ou [local](service-fabric-cluster-windows-server-add-remove-nodes.md)). Données de performances est également utile lorsque comparée tooactions vous ou vos applications et services aura fallu, lors de l’analyse des journaux Bonjour futures. 

Pour obtenir la liste de toocollect de compteurs de performances lors de l’utilisation de l’infrastructure de Service, consultez [compteurs de Performance dans le Service Fabric](service-fabric-diagnostics-event-generation-perf.md)

Voici deux manières fréquentes de configurer la collecte des compteurs de performances pour votre cluster :

* À l’aide d’un agent : il s’agit moyen hello préféré de collecte des performances d’un ordinateur, étant donné que les agents ont généralement une liste des mesures de performances possibles qui peuvent être recueillies, et il s’agit d’une métrique de hello processus relativement simple toochoose vous souhaitez toocollect ou les modifiez . En savoir plus sur [comment tooconfigure hello OMS pour Service Fabric](service-fabric-diagnostics-event-analysis-oms.md) et [configuration hello l’Agent OMS Windows](../log-analytics/log-analytics-windows-agents.md) toolearn articles plus d’informations sur l’agent OMS hello, qui est une telle agent d’analyse est en mesure de toopick données de performances pour les machines virtuelles du cluster et déployée.

* Configuration des performances de diagnostics toowrite compteurs tooa table : pour les clusters sur Azure, cela signifie remplaçant toopick de configuration des Diagnostics Windows Azure hello des compteurs de performance appropriés hello hello machines virtuelles dans votre cluster et en l’activant toopick des statistiques de docker si vous déployez tous les conteneurs. En savoir plus sur la configuration [compteurs de Performance dans WAD](service-fabric-diagnostics-event-aggregation-wad.md) dans tooset de l’infrastructure de Service de collecte des compteurs de performances.

## <a name="next-steps"></a>Étapes suivantes

Événements et les journaux doivent toobe agrégée avant de la plateforme d’analyse tooany peuvent être envoyées. En savoir plus sur [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) et [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendre certains des hello options recommandée.
