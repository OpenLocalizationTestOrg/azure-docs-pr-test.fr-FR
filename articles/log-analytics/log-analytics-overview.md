---
title: "aaaWhat est Analytique de journal dans Operations Management Suite (OMS) ? | Microsoft Docs"
description: "Log Analytics est un service d’Operations Management Suite (OMS) qui vous permet de collecter et d’analyser les données opérationnelles générées par les ressources de votre cloud et de vos environnements locaux.  Cet article fournit une vue d’ensemble de hello différents composants d’Analytique de journal et lie le contenu toodetailed."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Présentation de Log Analytics
Analytique de journal est un service de [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) qui surveille votre toomaintain environnements locaux et cloud leur disponibilité et les performances.  Il collecte les données générées par les ressources dans vos environnements locaux et cloud et à partir d’autres analyses de tooprovide outils analyse à plusieurs sources.  Cet article fournit une brève présentation de la valeur de hello fournit qu’Analytique de journal, une vue d’ensemble de la façon dont elle fonctionne, et des liens toomore détaillées contenu afin que vous pouvez explorer davantage.

## <a name="is-log-analytics-for-you"></a>Log Analytics est-il adapté à vos besoins ?
Si aucune analyse n’est actuellement mise en place pour votre environnement Azure, vous devez commencer avec [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) qui recueille et analyse les données de vos ressources Azure.  Analytique de journal peut [collecter des données à partir du moniteur de Azure](log-analytics-azure-storage.md) toocorrelate avec d’autres données et fournissent des analyses supplémentaires.

Si vous souhaitez toomonitor votre environnement local ou vous avez un contrôle existant à l’aide des services tels que le moniteur de Windows Azure ou System Center Operations Manager, Analytique de journal peut ajouter une valeur ajoutée significative.  La collecte peut s’effectuer directement à partir de vos agents et également de ces autres outils vers un référentiel unique.  Les outils d’analyse de Log Analytics, tels que les recherches de journaux, les vues et les solutions fonctionnent avec toutes les données collectées. Vous disposez ainsi d’une analyse centralisée de l’ensemble de votre environnement.


## <a name="using-log-analytics"></a>Utilisation de Log Analytics
Vous pouvez accéder Analytique de journal par le biais du portail OMS hello ou hello portail Azure, qui s’exécutent dans n’importe quel navigateur et fournir des paramètres d’accès tooconfiguration et plusieurs outils tooanalyze et agir sur les données collectées.  À partir du portail de hello vous pouvez tirer parti de [recherche de journal](log-analytics-log-searches.md) lorsque vous construisez la demande des données tooanalyze collectée, [tableaux de bord](log-analytics-dashboards.md) que vous pouvez personnaliser avec des vues graphiques des recherches plus importants, et [solutions](log-analytics-add-solutions.md) qui fournissent des outils d’analyse et de fonctionnalités supplémentaires.

image Hello ci-dessous est à partir du portail OMS hello quel tableau de bord affiche hello qui affiche des informations résumées pour hello [solutions](#add-functionality-with-management-solutions) qui sont installés dans l’espace de travail hello.  Vous pouvez cliquer sur n’importe quel toodrill vignette davantage en données hello pour cette solution.

![Portail OMS](media/log-analytics-overview/portal.png)

Analytique de journal inclut un récupérer de tooquickly de langage de requête et consolider les données dans le référentiel de hello.  Vous pouvez créer et enregistrer [recherches de journal](log-analytics-log-searches.md) toodirectly analyser les données dans le portail de hello ou des recherches de journaux exécutés automatiquement toocreate une alerte si des résultats de requête de hello hello indiquent une condition d’importantes.

![Recherche dans les journaux](media/log-analytics-overview/log-search.png)

tooget une rapide vue graphique d’intégrité hello de votre environnement global, vous pouvez ajouter des visualisations pour tooyour des recherches enregistrées de journal [tableau de bord](log-analytics-dashboards.md).   

![tableau de bord](media/log-analytics-overview/dashboard.png)

Dans le données de commandes tooanalyze en dehors de l’Analytique des journaux, vous pouvez exporter les données hello à partir du référentiel d’OMS hello dans les outils tels que [Power BI](log-analytics-powerbi.md) ou Excel.  Vous pouvez également exploiter hello [API de recherche de journal](log-analytics-log-search-api.md) toobuild des solutions personnalisées qui tirent parti des données de journal Analytique ou toointegrate avec d’autres systèmes.

## <a name="add-functionality-with-management-solutions"></a>Ajouter des fonctionnalités avec des solutions de gestion
[Solutions de gestion](log-analytics-add-solutions.md) ajouter des fonctionnalités tooOMS, en fournissant des données supplémentaires et analyse outils tooLog Analytique.  Ils peuvent également définir des nouveaux toobe types d’enregistrements collectée peut être analysée avec des recherches de journaux ou par l’interface utilisateur supplémentaire fournie par la solution hello dans le tableau de bord hello.  image d’un exemple Hello ci-dessous montre hello [solution de suivi des modifications](log-analytics-change-tracking.md)

![Solution de suivi des modifications](media/log-analytics-overview/change-tracking.png)

Les solutions sont disponibles pour diverses fonctions et des solutions supplémentaires sont ajoutées régulièrement.  Vous pouvez rechercher facilement des solutions disponibles et [les ajouter l’espace de travail OMS tooyour](log-analytics-add-solutions.md) à partir de la galerie des Solutions hello ou Azure Marketplace.  Nombre d’entre elles sont automatiquement déployées et immédiatement opérationnelles, tandis que d’autres peuvent nécessiter une configuration.

![Galerie de solutions](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Composants de Log Analytics
Centre d’Analytique de journal hello est référentiel OMS de hello qui est hébergé dans hello cloud Azure.  Collecte de données dans le référentiel de hello à partir de sources connectées par la configuration des sources de données et ajout abonnement tooyour de solutions.  Solutions et sources de données créent chacune différents types d’enregistrements qui ont leur propre jeu de propriétés, mais peuvent toujours être analysées ensemble dans le référentiel toohello de requêtes.  Cela vous permet de hello toouse même toowork outils et méthodes avec différents types de données collecté par différentes sources.

![Référentiel OMS](media/log-analytics-overview/overview.png)

Sources connectées sont les ordinateurs hello et autres ressources qui génèrent des données collectées par Analytique de journal.  Cela peut inclure des agents installés sur des ordinateurs [Windows](log-analytics-windows-agents.md) et [Linux](log-analytics-linux-agents.md) directement connectés, ou des agents d’un [groupe d’administration System Center Operations Manager connecté](log-analytics-om-agents.md).  Pour les ressources Azure, Log Analytics collecte des données à partir d’[Azure Monitor et Azure Diagnostics](log-analytics-azure-storage.md).

[Sources de données](log-analytics-data-sources.md) hello différents types de données collectées à partir de chaque source connectée.  Cela inclut les [événements](log-analytics-data-sources-windows-events.md) et [les données de performances](log-analytics-data-sources-performance-counters.md) de [Windows](log-analytics-data-sources-windows-events.md) et des agents de Linux dans toosources ajout comme [journaux IIS](log-analytics-data-sources-iis-logs.md)et [journaux texte personnalisé](log-analytics-data-sources-custom-logs.md).  Vous configurez chaque source de données que vous souhaitez toocollect et configuration de hello provient tooeach remis automatiquement connecté.

Si vous avez des besoins personnalisés, vous pouvez ensuite utiliser hello [API du collecteur de données HTTP](log-analytics-data-collector-api.md) toowrite toohello référentiel à partir d’un client de l’API REST.

## <a name="log-analytics-architecture"></a>Architecture Log Analytics
conditions de déploiement de Hello d’Analytique de journal sont minimes, car les composants centraux hello sont hébergés dans hello cloud Azure.  Cela inclut le référentiel de hello dans les services toohello Ajout toocorrelate et analyser les données collectées.  portail de Hello est accessible à partir de n’importe quel navigateur n’est pas obligatoire pour le logiciel client.

Vous devez installer les agents sur des ordinateurs [Windows](log-analytics-windows-agents.md) et [Linux](log-analytics-linux-agents.md), mais aucun agent supplémentaire n’est nécessaire pour les ordinateurs déjà membres d’un [groupe d’administration SCOM connecté](log-analytics-om-agents.md).  Agents SCOM continue toocommunicate avec les serveurs d’administration qui transfèrera leur tooLog données Analytique.  Bien que certaines solutions nécessitent toocommunicate agents directement avec Analytique de journal.  documentation Hello pour chaque solution spécifie ses besoins de communication.

Lorsque vous vous [inscrivez à Log Analytics](log-analytics-get-started.md), vous créez un espace de travail OMS.  Vous pouvez considérer de l’espace de travail hello constitue un environnement Analytique de journal unique avec son propre référentiel de données, les sources de données et les solutions. Vous pouvez créer plusieurs espaces de travail dans votre abonnement toosupport plusieurs environnements par exemple production et de test.

![Architecture Log Analytics](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Étapes suivantes
* [Inscrivez-vous gratuitement un compte Analytique de journal](log-analytics-get-started.md) tootest dans votre propre environnement.
* Hello vue différents [des Sources de données](log-analytics-data-sources.md) données toocollect disponibles dans le référentiel d’OMS hello.
* [Rechercher des solutions disponibles de hello Bonjour galerie des Solutions](log-analytics-add-solutions.md) tooadd fonctionnalité tooLog Analytique.

