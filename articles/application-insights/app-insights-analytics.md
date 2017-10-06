---
title: "aaaAnalytics - hello puissant outil de recherche de l’Application Azure Insights | Documents Microsoft"
description: "Vue d’ensemble de l’Analytique, hello diagnostic outil puissant d’Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Analytics dans Application Insights
[Analytique](app-insights-analytics.md) fonctionnalité de recherche puissant de hello de [Application Insights](app-insights-overview.md). Ces pages décrivent le langage de requête Log Analytics. 

* **[Regardez la vidéo de présentation hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Testez l’Analytique sur nos données simulées](https://analytics.applicationinsights.io/demo)**  si votre application n’envoie pas de données tooApplication Insights encore.
* **[Feuille de graphique SQL utilisateurs](https://aka.ms/sql-analytics)**  traduit idiomes courants de hello.
* **[Référence du langage](app-insights-analytics-reference.md)**  apprendre comment toouse tous les hello puissantes fonctionnalités de langage de requête Analytique de journal de hello.


## <a name="queries-in-analytics"></a>Requêtes dans Analytics
Une requête classique est une table *source* suivie d’une série *d’opérateurs* séparés par des `|`. 

Par exemple, voyons quelle heure du jour hello éléments de premier ordre de Hyderabad Essayez notre application web. Et pendant que nous sommes il, nous allons voir les codes de résultat sont retournées les demandes tootheir HTTP. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Nous compter les adresses IP de client distincts, les regrouper par hello heure hello sur hello des 7 derniers jours. 

> [!NOTE]
> résultats tooget en dehors de hello précédente 24h, inclure explicitement des « timestamp » dans votre requête, ou utilisez le menu de liste déroulante de plage de temps hello.
>

Résultats hello avec hello barre présentation graphique, en sélectionnant toostack hello les résultats à partir des codes de réponse différents s’affichent :

![Sélectionnez le graphique à barres, les axes x et y, puis la segmentation](./media/app-insights-analytics/020.png)

Il semblerait que notre application soit plus populaire lors de la pause déjeuner et à l’heure du coucher à Hyderabad. (Et nous devrions examiner ces 500 codes).

Il existe également des opérations statistiques puissantes :

![Résultats d’une requête statistique](./media/app-insights-analytics/025.png)

langue de Hello propose de nombreuses fonctionnalités intéressante :


* [Filtrer](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) vos données de télémétrie d’application brutes sur tous les champs, y compris les propriétés et métriques personnalisées.
* [Joindre](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) plusieurs tables ; mettez en corrélation les demandes avec les affichages de page, les appels de dépendance, les exceptions et les suivis du journal.
* [Agrégations](https://docs.loganalytics.io/learn/tutorials/aggregations.html)statistiques puissantes.
* Tout aussi puissantes que SQL, mais il est beaucoup plus facile pour les requêtes complexes : au lieu de l’imbrication d’instructions, vous diriger les données de salutation à partir d’une opération élémentaire toohello ensuite.
* Visualisations immédiates et puissantes.
* [Code confidentiel graphiques des tableaux de bord tooAzure](app-insights-analytics-using.md#pin-to-dashboard).
* [Exporter des requêtes tooPower BI](app-insights-analytics-using.md#export-to-power-bi).
* Il existe un [API REST](https://dev.applicationinsights.io/) que vous pouvez utiliser les requêtes toorun par programme, par exemple à partir de Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Connecter des données d’Application Insights tooyour
Ouvrez Analytics à partir du [panneau Vue d’ensemble](app-insights-dashboards.md) de votre application dans Application Insights : 

![Ouvrez portal.azure.com, ouvrez votre ressource Application Insights, puis cliquez sur Analyse.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Exemples de requête

Essayez ces puissance hello tooillustrate procédures pas à pas à l’aide d’Analytique :

 *  [Diagnostic automatique des pics et sauts d’étape dans les durées des demandes](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Analyse des baisses de performances avec l’analyse de séries chronologiques](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Analyse des défaillances d’application avec le cluster automatique et les modèles différentiels](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Détections de formes avancées avec l’analyse des séries chronologiques](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [À l’aide de glissante fenêtre opérations tooanalyze l’utilisation des applications (déploiement de MAU/DAU etc.)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Détection des interruptions de service en fonction de l’analyse des journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Profilage des performances des applications à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Mesure la durée hello pour chaque étape dans votre flux de code à l’aide des journaux de débogage simple](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) et un billet de blog correspondant [ici](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Analyse de l’accès concurrentiel à l’aide de simples journaux de débogage](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) et billet de blog sur le même sujet disponible [ici](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Étapes suivantes
* Nous vous recommandons de commencer par hello [visite guidée du langage](app-insights-analytics-tour.md). 
* En savoir plus sur [l’utilisation de l’analytique](app-insights-analytics-using.md). 
* [Informations de référence sur le langage](app-insights-analytics-reference.md). 
