---
title: "aaaMonitor l’utilisation et des statistiques dans un service Azure Search | Documents Microsoft"
description: "Suivez la consommation de ressource et la taille de l'index pour Azure Search, un service de recherche cloud hébergé sur Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Surveillance d’un service Azure Search

Azure Search propose diverses ressources pour le suivi des performances et de l’utilisation des services de recherche. Elle vous donne accès toometrics, les journaux, les statistiques d’index et les capacités d’analyse étendues sur Power BI. Cet article décrit comment tooenable hello différentes stratégies de surveillance et comment toointerpret hello les données résultantes.

## <a name="azure-search-metrics"></a>Mesures Azure Search
Les mesures vous donnent une visibilité en quasi temps réel sur votre service de recherche et sont disponibles pour chaque service, sans configuration supplémentaire. Elles vous permettent de suivre les performances de hello de votre service pour too30 jours.

Azure Search collecte les données de trois mesures différentes :

* Rechercher la latence : temps service de recherche hello nécessaire tooprocess requêtes de recherche, agrégés par minute.
* Requêtes de recherche par seconde (QPS) : nombre de requêtes de recherche reçues par seconde, agrégé par minute.
* Pourcentage de requêtes de recherche limitées : pourcentage de requêtes de recherche qui ont été limitées, agrégé par minute.

![Capture d’écran de l’activité RPS][1]

### <a name="set-up-alerts"></a>Configurer des alertes
À partir de la page des détails de métrique hello, vous pouvez configurer alertes tootrigger une notification par courrier électronique ou une action automatisée quand une métrique dépasse un seuil que vous avez définies.

Pour plus d’informations sur les métriques, consultez la documentation complète de hello sur le moniteur de Windows Azure.  

## <a name="how-tootrack-resource-usage"></a>Comment l’utilisation des ressources tootrack
Croissance hello d’index et la taille du document de suivi peut vous aider à ajuster proactive la capacité avant d’atteindre la limite supérieure de hello que vous avez défini pour votre service. Pour cela, sur le portail de hello ou par programmation à l’aide d’API REST de hello.

### <a name="using-hello-portal"></a>À l’aide du portail de hello

l’utilisation des ressources toomonitor, afficher les nombres hello et les statistiques de votre service Bonjour [portal](https://portal.azure.com).

1. Connectez-vous à toohello [portal](https://portal.azure.com).
2. Ouvrez le tableau de bord du service de hello de votre service Azure Search. Vignettes pour service de hello se trouvent sur la page d’accueil hello, ou vous pouvez parcourir le service toohello de parcourir sur hello JumpBar.

Hello section Utilisation comprend un compteur qui vous indique quelle partie des ressources disponibles sont actuellement en cours d’utilisation. Pour plus d’informations sur les limites par service des index, des documents et du stockage, consultez [Limites du service](search-limits-quotas-capacity.md).

  ![Mosaïque Utilisation][2]

> [!NOTE]
> capture d’écran Hello ci-dessus pour hello libre service, ce qui a une limite maximale d’un réplica et chaque partition et peut uniquement les index de l’hôte, 3, 10 000 documents ou 50 Mo de données, selon ce qui se produit en premier. Les services créés avec un niveau De base ou Standard ont des limites de service bien plus étendues. Pour plus d’informations sur le choix des niveaux, consultez [Choisir une référence (SKU) ou un niveau tarifaire](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>À l’aide des API REST de hello
Hello API REST Azure Search et hello SDK .NET donnent des indications de tooservice de l’accès par programme.  Si vous utilisez [indexeurs](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload un index à partir de la base de données SQL Azure ou base de données Azure Cosmos, une API supplémentaire est numéros de hello tooget disponible vous avez besoin.

* [Obtention de statistiques d'index](/rest/api/searchservice/get-index-statistics)
* [Nombre de documents](/rest/api/searchservice/count-documents)
* [Obtention de l’état d’indexeur](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Mode de journalisation des tooexport et des mesures

Vous pouvez exporter des journaux des opérations de hello pour votre service et hello des données brutes pour les métriques hello décrites dans hello précédant la section. Journaux des opérations vous permettent de savoir comment le service de hello est utilisé et peut être utilisé à partir de Power BI lorsque les données sont copiées de compte de stockage tooa. Azure Search fournit un pack de contenu Power BI de surveillance à cet effet.


### <a name="enabling-monitoring"></a>Activation de la surveillance
Ouvrez votre service Azure Search Bonjour [portail Azure](http://portal.azure.com) sous hello option d’activer l’analyse.

Choisissez les données de salutation souhaité tooexport : journaux, les métriques ou les deux. Vous pouvez copier le compte de stockage tooa, envoyer le concentrateur d’événements tooan ou exportez-le tooLog Analytique.

![Comment tooenable analyse dans le portail de hello][3]

tooenable à l’aide de PowerShell ou hello CLI d’Azure, consultez la documentation de hello [ici](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Journaux et schémas de mesure
Lorsque les données de salutation sont copié tooa stockage compte, hello données sont au format JSON et sa place dans deux conteneurs :

* journaux-Insights-operationlogs : pour les journaux de trafic de recherche
* mesures-Insights-pt1m : pour les mesures

Il y a un seul objet blob par heure et par conteneur.

Exemple de chemin d’accès : `resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Schéma du journal
Hello, journaux des objets BLOB contiennent vos journaux de trafic de service de recherche.
Chaque objet blob a un objet racine appelé **enregistrements** qui contient un tableau d’objets du journal.
Chaque objet blob a des enregistrements sur tous les opération hello qui ont eu lieu au cours de hello la même heure.

| Nom | Type | Exemple | Remarques |
| --- | --- | --- | --- |
| time |datetime |« 2015-12-07T00:00:43.6872559Z » |Horodateur de l’opération de hello |
| resourceId |string |«/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/> MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE » |Votre ID de ressource |
| operationName |string |« Query.Search » |nom Hello d’opération de hello |
| operationVersion |string |« 2015-02-28 » |Hello api-version utilisée |
| category |string |« OperationLogs » |constant |
| resultType |string |« Success » |Valeurs possibles : Réussite ou Échec |
| resultSignature |int |200 |Code de résultat HTTP |
| durationMS |int |50 |Durée de l’opération de hello en millisecondes |
| properties |objet |consultez hello tableau suivant |Objet contenant des données propres à l’opération |

**Schéma de propriétés**
| Nom | Type | Exemple | Remarques |
| --- | --- | --- | --- |
| Description |string |« GET /indexes(’content’)/docs » |point de terminaison de l’opération Hello |
| Interroger |string |« ?search=AzureSearch&$count=true&api-version=2015-02-28 » |paramètres de requête Hello |
| Documents |int |42 |Nombre de documents traités |
| IndexName |string |« testindex » |Nom d’index hello associé hello opération |

#### <a name="metrics-schema"></a>Schéma de mesures
| Nom | Type | Exemple | Remarques |
| --- | --- | --- | --- |
| resourceId |string |«/SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111/<br/>RESOURCEGROUPS/DEFAULT/PROVIDERS/<br/>MICROSOFT.SEARCH/SEARCHSERVICES/SEARCHSERVICE » |Votre ID de ressource |
| metricName |string |« Latency » |nom Hello de métrique de hello |
| time |datetime |« 2015-12-07T00:00:43.6872559Z » |horodateur de l’opération Hello |
| average |int |64 |valeur moyenne de Hello d’échantillons de brut hello dans l’intervalle de temps de métrique hello |
| minimum |int |37 |valeur minimale de Hello d’échantillons de brut hello dans l’intervalle de temps de métrique hello |
| maximum |int |78 |valeur maximale de Hello d’échantillons de brut hello dans l’intervalle de temps de métrique hello |
| total |int |258 |valeur totale de Hello d’échantillons de brut hello dans l’intervalle de temps de métrique hello |
| count |int |4 |nombre de Hello d’échantillons bruts utilisé métrique de hello toogenerate |
| timegrain |string |« PT1M » |fragment de temps Hello de métrique hello en ISO 8601 |

Toutes les mesures sont consignées dans des intervalles d’une minute. Chaque mesure expose des valeurs minimales, maximales et moyennes par minute.

Pour une métrique de SearchQueriesPerSecond hello minimale est hello plus petite valeur pour les requêtes de recherche par seconde a été enregistré pendant cette minute. Hello va de même valeur maximale de toohello. Moyenne, est hello d’agrégation sur minute entière de hello.
Pensez à ce scénario pendant une minute : 58 secondes de la charge moyenne suivie d’une seconde de charge élevée qui est hello maximale pour SearchQueriesPerSecond, et enfin une seconde avec une seule requête, qui est hello minimale.

Pour ThrottledSearchQueriesPercentage, minimum, maximum, moyenne et total, tous les avoir hello même valeur : hello pourcentage de requêtes de recherche qui a été limitée à partir du nombre total de hello de requêtes de recherche pendant une minute.

## <a name="analyzing-your-data-with-power-bi"></a>Analyse de vos données avec Power Bi

Nous vous recommandons d’utiliser [Power BI](https://powerbi.microsoft.com) tooexplore et visualiser vos données. Vous pouvez facilement connecter tooyour compte de stockage Azure et rapidement commencer à analyser vos données.

Azure Search fournit un [Pack de contenu Power BI](https://app.powerbi.com/getdata/services/azure-search) qui vous permet de toomonitor et comprendre votre trafic aux tables et graphiques prédéfinis. Il contient un ensemble de rapports Power BI qui se connecter aux données tooyour automatiquement et qui fournissent des informations graphiques sur votre service de recherche. Pour plus d’informations, consultez hello [page d’aide de pack de contenu](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Tableau de bord Power BI pour Azure Search][4]

## <a name="next-steps"></a>Étapes suivantes
Révision [mettre à l’échelle des réplicas et partitions](search-limits-quotas-capacity.md) pour obtenir des conseils sur la façon dont toobalance hello d’allocation de partitions et réplicas pour un service existant.

Pour plus d’informations sur l’administration des services, consultez [Gestion du service Recherche sur Microsoft Azure](search-manage.md). Pour obtenir de l’aide sur le paramétrage, consultez [Performances et optimisation](search-performance-optimization.md).

En savoir plus sur la création de rapports exceptionnels. Pour plus d’informations, consultez [Prise en main de Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
