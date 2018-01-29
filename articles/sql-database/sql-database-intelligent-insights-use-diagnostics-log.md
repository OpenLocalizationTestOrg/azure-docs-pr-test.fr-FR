---
title: Journal de diagnostic du niveau de performance Intelligent Insights - Azure SQL Database | Microsoft Docs
description: "Intelligent Insights fournit un journal de diagnostic des problèmes de performance d’Azure SQL Database"
services: sql-database
documentationcenter: 
author: danimir
manager: drasumic
editor: carlrab
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Inactive
ms.date: 09/25/2017
ms.author: v-daljep
ms.openlocfilehash: e147ca57658c232580fd9867790e55c3454e7e05
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="use-the-intelligent-insights-azure-sql-database-performance-diagnostics-log"></a>Utiliser le journal de diagnostic Intelligent Insights des performances d’Azure SQL Database

Cette page fournit des informations sur l’utilisation du journal de diagnostic des performances d’Azure SQL Database généré par [Intelligent Insights](sql-database-intelligent-insights.md), son format et les données qu’il contient pour vos besoins de développement. Vous pouvez envoyer ce journal de diagnostic à [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md), [Azure Event Hubs](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md), [Stockage Azure](sql-database-metrics-diag-logging.md#stream-into-storage) ou une solution tierce pour des fonctionnalités d’alertes et de rapports DevOps personnalisées.

## <a name="log-header"></a>En-tête du journal

Le journal de diagnostic utilise le format standard JSON pour générer les résultats d’Intelligent Insights. La propriété de catégorie exacte permettant d’accéder au journal d’Intelligent Insights est la valeur fixe « SQLInsights ».

L’en-tête du journal est commun et se compose de l’horodatage (TimeGenerated) qui indique le moment où une entrée a été créée. Il inclut également un ID de ressource (ResourceId) qui fait référence à la base de données SQL Database à laquelle l’entrée se rapporte. La catégorie (Category), le niveau (Level) et le nom d’opération (OperationName) sont des propriétés fixes dont la valeur ne change pas. Ils indiquent que l’entrée de journal est fournie à titre d’information et qu’elle provient d’Intelligent Insights (SQLInsights).

```json
"TimeGenerated" : "2017-9-25 11:00:00", // time stamp of the log entry
"ResourceId" : "database identifier", // value points to a database resource
"Category": "SQLInsights", // fixed property
"Level" : "Informational", // fixed property
"OperationName" : "Insight", // fixed property
```

## <a name="issue-id-and-database-affected"></a>ID du problème et base de données concernés

La propriété d’identification des problèmes (issueId_d) offre un moyen unique d’assurer le suivi des problèmes de performances jusqu’à leur résolution. Intelligent Insights observe le cycle de vie de chaque problème comme étant « Actif », « En cours de vérification » ou « Terminé ». À travers chacune de ces phases d’état, Intelligent Insights peut enregistrer plusieurs enregistrements d’événement dans le journal. Pour chacune de ces entrées, le numéro d’identification du problème reste unique. Intelligent Insights effectue le suivi du problème via son cycle de vie et génère un insight dans le journal de diagnostic toutes les 15 minutes.

Une fois qu’un problème de performances est détecté et aussi longtemps qu’il dure, il est considéré comme étant « Actif » sous la propriété d’état (status_s). Une fois qu’un problème détecté est atténué, il est vérifié et signalé comme étant « En cours de vérification » sous la propriété d’état (status_s). Si le problème n’existe plus, la propriété d’état (status_s) le signale comme étant « Terminé ».

En plus de l’ID de problème, le journal de diagnostic indique les horodatages de début (intervalStartTime_t) et de fin (intervalEndTme_t) de l’événement particulier associé à un problème signalé dans le journal de diagnostic.

La propriété de pool élastique (elasticPoolName_s) indique à quel pool élastique appartient la base de données ayant un problème. Si la base de données ne fait pas partie d’un pool élastique, cette propriété n’a aucune valeur. La base de données dans laquelle un problème a été détecté est indiquée dans la propriété du nom de base de données (databaseName_s).

```json
"intervalStartTime_t": "2017-9-25 11:00", // start of the issue reported time stamp
"intervalEndTme_t":"2017-9-25 12:00", // end of the issue reported time stamp
"elasticPoolName_s" : "", // resource elastic pool (if applicable) 
"databaseName_s" : "db_name",  // database name
"issueId_d" : 1525, // unique ID of the issue detected
"status_s" : "Active" // status of the issue – possible values: "Active", "Verifying", and "Complete"
```

## <a name="detected-issues"></a>Problèmes détectés

La section suivante du journal de diagnostic des performances Intelligent Insights contient les problèmes de performances détectés via l’intelligence artificielle intégrée. Les détections sont indiquées dans les propriétés au sein du journal de diagnostic JSON. Ces détections comprennent la catégorie d’un problème, l’impact du problème, les requêtes affectées et les métriques. Les propriétés relatives aux détections peuvent contenir plusieurs problèmes de performances détectés.

Les problèmes de performance détectés sont signalés avec la structure de propriété de détection suivante :

```json
"detections_s" : [{
"impact" : 1 to 3, // impact of the issue detected, possible values 1-3 (1 low, 2 moderate, 3 high impact)
"category" : "Detectable performance pattern", // performance issue detected, see the table
"details": <Details outputted> // details of an issue (see the table)
}] 
```

Les modèles de performances détectables et les détails générés dans le journal de diagnostic figurent dans le tableau suivant.

### <a name="detection-category"></a>Catégorie de détection

La propriété de catégorie (category) décrit la catégorie des modèles de performances détectables. Consultez le tableau suivant pour toutes les catégories possibles des modèles de performance détectables. Pour plus d’informations, consultez [Résoudre les problèmes de performances liés à Azure SQL Database avec Intelligent Insights](sql-database-intelligent-insights-troubleshoot-performance.md).

Selon le problème de performances détecté, les détails générés dans le fichier journal de diagnostic diffèrent.

| Modèles de performances détectables | Détails générés |
| :------------------- | ------------------- |
| Atteinte des limites de ressources | <li>Ressources affectées</li><li>Hachages de requête</li><li>Pourcentage de la consommation de ressources</li> |
| Augmentation de la charge de travail | <li>Nombre de requêtes dont l’exécution a augmenté</li><li>Hachages de requêtes avec la plus grande contribution à l’augmentation de la charge de travail</li> |
| Sollicitation de la mémoire | <li>Régisseur de mémoire</li> |
| Verrouillage | <li>Hachages de requête affectés</li><li>Blocage des hachages de requête</li> |
| Augmentation de MAXDOP | <li>Hachages de requête</li><li>Temps d’attente CXP</li><li>Temps d’attente</li> |
| Contention de verrous de page | <li>Interroger les hachages de requêtes à l’origine de la contention</li> |
| Index manquant | <li>Hachages de requête</li> |
| Nouvelle requête | <li>Hachage de requête des nouvelles requêtes</li> |
| Statistiques d’attente inhabituelles | <li>Types d’attente inhabituels</li><li>Hachages de requête</li><li>Temps d’attente de requête</li> |
| Contention de TempDB | <li>Interroger les hachages de requêtes à l’origine de la contention</li><li>Attribution de requête au délai d’attente de contention de verrous de page de la base de données globale [%]</li> |
| Pénurie de DTU du pool élastique | <li>Pool élastique</li><li>Base de données qui consomme le plus de DTU</li><li>Pourcentage du DTU du pool utilisé par le consommateur supérieur</li> |
| Régression de plan | <li>Hachages de requête</li><li>ID de plan corrects</li><li>ID de plan incorrects</li> |
| Changement de la valeur de configuration à l’échelle de la base de données | <li>Changements de configuration à l’échelle de la base de données par rapport aux valeurs par défaut</li> |
| Client lent | <li>Hachages de requête</li><li>Temps d’attente</li> |
| Passage à une version antérieure du niveau tarifaire | <li>Notification de texte</li> |

### <a name="impact"></a>Impact

La propriété d’impact (impact) décrit le niveau auquel un comportement détecté a contribué au problème rencontré par une base de données. Les impacts vont de 1 à 3 : 3 représente la contribution la plus élevée, 2 représente une contribution modérée et 1 représente la contribution la plus faible. La valeur d’impact peut être utilisée comme entrée pour l’automatisation d’alerte personnalisée, en fonction de vos besoins spécifiques. La propriété relative aux requêtes impactées (QueryHashes) fournit une liste des codes de hachage de requêtes affectés par une détection particulière.

### <a name="impacted-queries"></a>Requêtes impactées

La section suivante du journal Intelligent Insights fournit des informations sur les requêtes particulières qui ont été affectées par les problèmes de performances détectés. Cette information est indiquée en tant que tableau d’objets incorporés dans la propriété impact_s. La propriété d’impact se compose d’entités et de métriques. Les entités font référence à une requête spécifique (type : Query). Le code de hachage de requête unique est indiqué sous la propriété de valeur (Value). De plus, chacune des requêtes présentées est suivie d’une métrique et d’une valeur, lesquelles indiquent un problème de performances détecté.

Dans l’exemple de journal suivant, la requête dont le code de hachage est 0x9102EXZ4 a été détectée en raison d’une augmentation de sa durée d’exécution (métrique : DurationIncreaseSeconds). La valeur 110 secondes indique que cette requête particulière a pris 110 secondes de plus pour s’exécuter. Dans la mesure où plusieurs requêtes peuvent être détectées, cette section de journal spécifique peut inclure plusieurs entrées de requête.

```json
"impact" : [{
"entity" : { 
"Type" : "Query", // type of entity - query
"Value" : "query hash value", // for example "0x9102EXZ4" query hash value },
"Metric" : "DurationIncreaseSeconds", // measured metric and the measurement unit (in this case seconds)
"Value" : 110 // value of the measured metric (in this case seconds)
}]
```

### <a name="metrics"></a>Mesures

L’unité de mesure de chaque métrique signalée est fournie sous la propriété de métrique (metric) avec les valeurs possibles suivantes : secondes, nombre et pourcentage. La valeur d’une métrique mesurée est indiquée dans la propriété de valeur (value).

La propriété DurationIncreaseSeconds fournit l’unité de mesure en secondes. L’unité de mesure CriticalErrorCount est une valeur qui représente un nombre d’erreurs.

```json
"metric" : "DurationIncreaseSeconds", // issue metric type – possible values: DurationIncreaseSeconds, CriticalErrorCount, WaitingSeconds
"value" : 102 // value of the measured metric (in this case seconds)
```

## <a name="root-cause-analysis-and-improvement-recommendations"></a>Recommandations en matière d’analyse et d’amélioration de la cause racine

La dernière partie du journal de diagnostic des performances Intelligent Insights se rapporte à l’analyse automatisée de la cause racine du problème de détérioration des performances ayant été identifié. Ces informations se présentent sous une forme conviviale dans la propriété d’analyse de cause racine (rootCauseAnalysis_s). Les recommandations d’amélioration sont incluses dans le journal chaque fois que cela est possible.

```json
// example of reported root cause analysis of the detected performance issue, in a human-readable format

"rootCauseAnalysis_s" : "High data IO caused performance to degrade. It seems that this database is missing some indexes that could help."
```

Vous pouvez utiliser le journal de diagnostic des performances Intelligent Insights avec [Azure Log Analytics]( https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-sql) ou une solution tierce pour des fonctionnalités d’alertes et de rapports DevOps personnalisées.

## <a name="next-steps"></a>Étapes suivantes
- Découvrez les concepts [Intelligent Insights](sql-database-intelligent-insights.md).
- Découvrez comment [résoudre les problèmes de performances liés à Azure SQL Database avec Intelligent Insights](sql-database-intelligent-insights-troubleshoot-performance.md).
- Découvrez comment [surveiller Azure SQL Database avec Azure SQL Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-sql).
- Découvrez comment [collecter et consommer les données des journaux de vos ressources Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).



