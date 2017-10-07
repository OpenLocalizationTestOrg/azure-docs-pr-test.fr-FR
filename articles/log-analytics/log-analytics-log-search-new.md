---
title: recherche aaaLog dans Analytique des journaux OMS | Documents Microsoft
description: "Vous avez besoin une tooretrieve de recherche de journal de toutes les données de journal Analytique.  Cet article décrit comment les nouveaux journaux recherches sont utilisées dans le journal Analytique et fournit les concepts que vous devez toounderstand avant de créer un."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 08fda1d9eb9e6ab824ffb9e12af09832c3e3fad2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-log-searches-in-log-analytics"></a>Présentation des recherches dans les journaux dans Log Analytics

> [!NOTE]
> Cet article décrit les recherches de journaux dans Azure Analytique de journal à l’aide du nouveau langage de requête hello.  Vous pouvez en savoir plus sur le nouveau langage de hello et obtenir hello procédure tooupgrade votre espace de travail à [mise à niveau de votre recherche de journal toonew espace de travail Analytique des journaux Azure](log-analytics-log-search-upgrade.md).  
>
> Si votre espace de travail n’a pas été mis à niveau toohello nouveau langage de requête, vous devez faire référence trop[trouver des données à l’aide de recherches de journal dans le journal Analytique](log-analytics-log-searches.md).

Vous avez besoin une tooretrieve de recherche de journal de toutes les données de journal Analytique.  Si vous analysez les données dans le portail de hello, configuration d’une règle d’alerte de toobe averti d’une condition particulière, ou la récupération des données à l’aide de hello API Analytique de journal, vous allez utiliser une recherche de journal toospecify données hello souhaité.  Cet article décrit comment sont utilisées les recherches dans les journaux dans Log Analytics, et présente les concepts que vous devez comprendre avant de créer une recherche. Consultez hello [étapes](#next-steps) section pour plus d’informations sur la création et modification des recherches de journaux et des références sur le langage de requête hello.

## <a name="where-log-searches-are-used"></a>Où les recherches dans les journaux sont-elles utilisées ?

Hello différentes manières que vous allez utiliser les recherches de journal dans le journal Analytique hello suivants :

- **Portails.** Vous pouvez effectuer une analyse interactive des données dans le référentiel hello avec hello [portal de recherche de journal](log-analytics-log-search-log-search-portal.md) ou hello [portal d’Analytique de Advanced](https://go.microsoft.com/fwlink/?linkid=856587).  Cela vous permet de tooedit votre requête et d’analyser les résultats de hello dans divers formats et les visualisations.  La plupart des requêtes que vous créez va démarrer dans un des portails de hello, puis copiés après avoir vérifié qu’il fonctionne comme prévu.
- **Règles d’alerte.** Les [règles d’alerte](log-analytics-alerts.md) identifient de façon proactive les problèmes à partir des données dans votre espace de travail.  Chaque règle d’alerte est basée sur une recherche dans les journaux qui est exécutée automatiquement à intervalles réguliers.  les résultats de Hello sont inspecté toodetermine si une alerte doit être créée.
- **Vues.**  Vous pouvez créer des visualisations de toobe de données inclus dans les tableaux de bord utilisateur avec [Concepteur de vue](log-analytics-view-designer.md).  Recherches de journal fournissent des données hello utilisées par [vignettes](log-analytics-view-designer-tiles.md) et [des parties de visualisation](log-analytics-view-designer-parts.md) dans chaque vue.  Vous pouvez approfondir à partir des parties de visualisation hello recherche de journal tooperform portail approfondir l’analyse sur les données de salutation.
- **Exportation.**  Lorsque vous exportez des données à partir de tooExcel d’espace de travail hello Analytique de journal ou [Power BI](log-analytics-powerbi.md), vous créez un tooexport de données de journal recherche toodefine hello.
- **PowerShell.** Vous pouvez exécuter un script PowerShell à partir d’une ligne de commande ou d’un runbook Azure Automation qui utilise [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/get-azurermoperationalinsightssearchresults?view=azurermps-4.0.0) tooretrieve des données à partir de l’Analytique des journaux.  Cette applet de commande requiert un tooretrieve de données de requête toodetermine hello.
- **API Log Analytics.**  Hello [Analytique de journal journal API de recherche](log-analytics-log-search-api.md) permet de n’importe quel client de l’API REST tooretrieve des données à partir de l’espace de travail hello.  demande d’API Hello inclut une requête qui est exécutée sur tooretrieve de données Analytique de journal toodetermine hello.

![Recherches dans les journaux](media/log-analytics-log-search-new/log-search-overview.png)

## <a name="how-log-analytics-data-is-organized"></a>Organisation des données Log Analytics
Lorsque vous générez une requête, vous démarrez en déterminant les tables contiennent des données de hello que vous recherchez. Chaque [source de données](log-analytics-data-sources.md) et [solution](../operations-management-suite/operations-management-suite-solutions.md) stocke ses données dans des tables dédiées dans l’espace de travail Analytique de journal hello.  Documentation pour chaque source de données et la solution inclut le nom hello hello du type de données qu’il crée et une description de chacune de ses propriétés.     De nombreuses requêtes ne nécessitent que les données à partir d’une seule des tables, mais d’autres peuvent utiliser diverses options tooinclude des données provenant de plusieurs tables.

![Tables](media/log-analytics-log-search-new/queries-tables.png)


## <a name="writing-a-query"></a>Écriture d’une requête
Au cœur de hello du journal des recherches dans le journal Analytique est [un langage de requête étendu](https://docs.loganalytics.io/) qui vous permet de récupérer et analyser les données de référentiel hello dans de diverses façons.  Ce même langage de requête est utilisé pour [Application Insights](../application-insights/app-insights-analytics.md).  Apprendre comment toowrite une requête est critique toocreating les recherches de journal dans le journal Analytique.  Vous devez généralement commencer par les requêtes de base et puis progression toouse plus des fonctions avancées lorsque vos besoins deviennent plus complexes.

structure de base Hello d’une requête est une table source suivie d’une série d’opérateurs séparés par une barre verticale `|`.  Vous pouvez chaîner plusieurs opérateurs toorefine hello de données et effectuer des fonctions avancées.

Par exemple, supposons que vous souhaitiez toofind hello supérieur dix ordinateurs avec hello la plupart des événements d’erreur sur hello hier.

    Event
    | where (EventLevelName == "Error")
    | where (TimeGenerated > ago(1days))
    | summarize ErrorCount = count() by Computer
    | top 10 by ErrorCount desc

Ou peut-être toofind les ordinateurs qui n’ont pas eu une pulsation Bonjour dernier jour.

    Heartbeat
    | where TimeGenerated > ago(7d)
    | summarize max(TimeGenerated) by Computer
    | where max_TimeGenerated < ago(1d)  

Comment sur un graphique en courbes avec l’utilisation du processeur de hello pour chaque ordinateur à partir de la semaine dernière ?

    Perf
    | where ObjectName == "Processor" and CounterName == "% Processor Time"
    | where TimeGenerated  between (startofweek(ago(7d)) .. endofweek(ago(7d)) )
    | summarize avg(CounterValue) by Computer, bin(TimeGenerated, 5min)
    | render timechart    

Vous pouvez voir la structure de requête de hello est similaire à partir de ces exemples rapides qui, quel que soit le type de hello de données que vous travaillez, hello.  Vous pouvez décomposer en étapes distinctes, où les données de salutation résultant d’une commande sont envoyées via la commande suivante de hello pipeline toohello.

Pour obtenir une documentation complète sur le langage de requête Analytique de journal Azure hello, y compris la référence du langage et les didacticiels, consultez hello [documentation de langage de requête Analytique de journal Azure](https://docs.loganalytics.io/).

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur hello [portails que vous utilisez toocreate et modifiez des recherches de journal](log-analytics-log-search-portals.md).
- Extraire un [didacticiel sur l’écriture de requêtes](https://go.microsoft.com/fwlink/?linkid=856078) à l’aide du nouveau langage de requête hello.
