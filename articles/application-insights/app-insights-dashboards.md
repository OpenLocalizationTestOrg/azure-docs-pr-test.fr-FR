---
title: aaaDashboards et navigation dans hello Azure Application Insights | Documents Microsoft
description: "Créez des vues de votre principaux graphiques et requêtes APM."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>Navigation et des tableaux de bord dans le portail Application Insights de hello
Une fois que vous avez [configurer Application Insights sur votre projet](app-insights-overview.md), les données télémétriques sur les performances et l’utilisation de votre application seront affiche dans la ressource d’Application Insights de votre projet dans hello [portail Azure](https://portal.azure.com).

## <a name="find-your-telemetry"></a>Rechercher vos données de télémétrie
Connectez-vous à toohello [portail Azure](https://portal.azure.com) et accédez ressource Application Insights toohello que vous avez créé pour votre application.

![Cliquez sur Parcourir, sélectionnez Application Insights, puis sélectionnez votre application.](./media/app-insights-dashboards/00-start.png)

Panneau de vue d’ensemble de Hello (page) pour votre application affiche un résumé des métriques de diagnostic clés hello de votre application et est une passerelle toohello autres fonctionnalités du portail de hello.

![Les principales itinéraires tooview votre télémétrie](./media/app-insights-dashboards/010-oview.png)

Vous pouvez personnaliser une des grilles et des graphiques de hello et épingler un tableau de bord tooa. De cette façon, vous pouvez rassembler télémétrie de clé hello à partir de différentes applications dans un tableau de bord central.

## <a name="dashboards"></a>Tableaux de bord
Hello première chose que vous voyez lorsque vous êtes connecté toohello [portail Microsoft Azure](https://portal.azure.com) est un tableau de bord. Ici vous pouvez rassembler des graphiques hello qui sont plus importante tooyou sur toutes vos ressources Azure, y compris les données de télémétrie des [Azure Application Insights](app-insights-overview.md).

![Un tableau de bord personnalisé.](./media/app-insights-dashboards/31.png)

1. **Accédez toospecific ressources** telles que votre application dans Application Insights : utiliser la barre gauche hello.
2. **Tableau de bord actuel toohello retour**, ou basculer entre les vues récente tooother : utilisez hello déroulante en haut à gauche.
3. **Passer des tableaux de bord**: utilisez hello déroulante sur le titre du tableau de bord hello
4. **Créer, modifier et partager des tableaux de bord** dans la barre d’outils du tableau de bord hello.
5. **Modifier le tableau de bord hello**: placez le curseur sur une vignette, puis utiliser son haut barre toomove, personnaliser, ou le supprimer.

## <a name="add-tooa-dashboard"></a>Ajouter le tableau de bord tooa
Lorsque vous examinez un panneau ou un ensemble de graphiques qui est particulièrement intéressante, vous pouvez épingler une copie du tableau de bord toohello. Celui-ci sera affiché lors de votre prochain accès au tableau de bord.

![toopin un graphique, pointez sur celui-ci, puis sur «... » dans l’en-tête de hello.](./media/app-insights-dashboards/33.png)

1. Épingler le graphique toodashboard. Une copie du graphique de hello s’affiche sur le tableau de bord hello.
2. Tableau de bord de toohello de code confidentiel hello ensemble panneau - il apparaît dans le tableau de bord hello sous forme de vignette que vous pouvez cliquer.
3. Cliquez sur hello en haut à gauche tooreturn toohello tableau de bord actuel. Puis vous pouvez utiliser la vue actuelle du toohello tooreturn menu déroulant hello.

Notez que les graphiques sont regroupés en vignettes : une vignette peut contenir plusieurs graphiques. Vous épinglez toohello du tableau de bord entier vignette hello.

Hello graphique est automatiquement actualisé avec une fréquence qui varie selon l’intervalle de temps du graphique hello :

* La période d’heure de too1 : actualiser toutes les 5 minutes
* Intervalle de temps entre 1 et 24 heures : actualisation toutes les 15 minutes
* Intervalle de temps supérieur à 24 heures : (intervalle de temps)/60.

### <a name="pin-any-query-in-analytics"></a>Épinglez n’importe quelle requête dans Analytics
Vous pouvez également [épingler Analytique](app-insights-analytics-using.md#pin-to-dashboard) graphiques tooa [partagé](#share-dashboards-with-your-team) tableau de bord. Cela vous permet de graphiques tooadd de toute requête arbitraire en même temps que les métriques standard hello. 

Les résultats sont recalculés automatiquement toutes les heures. Cliquez sur icône d’actualisation hello sur hello graphique toorecalculate immédiatement. (L’actualisation du navigateur ne permet pas de lancer un nouveau calcul.)

## <a name="adjust-a-tile-on-hello-dashboard"></a>Ajuster une vignette de tableau de bord hello
Une fois une vignette de tableau de bord hello, vous pouvez la modifier.

![Placez-la sur un graphique dans la commande tooedit.](./media/app-insights-dashboards/36.png)

1. Ajouter une vignette de toohello graphique.
2. Définir la métrique de hello, dimension group by et le style (table, graphique) d’un graphique.
3. Faites glisser toozoom de diagramme hello dans ; Cliquez sur hello annulation bouton tooreset hello timespan ; Définissez les propriétés de filtre pour les graphiques hello sur la vignette de hello.
4. Définissez le titre de la vignette.

Les vignettes épinglées à partir des panneaux de Metrics Explorer ont davantage d’options d’édition que les vignettes épinglées à partir d’un panneau Vue d’ensemble.

vignette d’origine Hello que vous avez épinglées n’est pas affectée par vos modifications.

## <a name="switch-between-dashboards"></a>Basculement entre les tableaux de bord
Vous pouvez enregistrer plusieurs tableaux de bord et basculer entre ceux-ci. Quand vous épinglez un graphique ou un panneau, elles sont ajoutées toohello de tableau de bord actuel.

![tooswitch entre les tableaux de bord, cliquez sur tableau de bord et sélectionnez un tableau de bord enregistré. toocreate et enregistrer un nouveau tableau de bord, cliquez sur Nouveau. toorearrange, cliquez sur Modifier.](./media/app-insights-dashboards/32.png)

Par exemple, vous pouvez avoir un tableau de bord pour l’affichage plein écran dans la salle d’équipe hello et l’autre pour le développement général.

Tableau de bord de hello, un panneau s’affiche sous forme de vignette : activez-la toogo toohello panneau. Un graphique réplique graphique hello dans son emplacement d’origine.

![Cliquez sur une lame de hello tooopen vignette qu’elle représente](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>Partager des tableaux de bord
Lorsque vous avez créé un tableau de bord, vous pouvez le partager avec d’autres utilisateurs.

![Dans l’en-tête du tableau de bord hello, cliquez sur Partager](./media/app-insights-dashboards/41.png)

Apprenez-en davantage sur [les rôles et le contrôle d’accès](app-insights-resources-roles-access-control.md).

## <a name="app-navigation"></a>Navigation au sein d’une application
Panneau de vue d’ensemble de Hello est hello passerelle toomore plus d’informations sur votre application.

* **Tout graphique ou la vignette** - cliquez sur n’importe quelle vignette ou un graphique toosee plus en détail ce qu’il affiche.

### <a name="overview-blade-buttons"></a>Boutons du panneau Vue d’ensemble
![Barre de navigation supérieure du panneau Vue d’ensemble](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**Metrics Explorer**](app-insights-metrics-explorer.md) : créez vos propres graphiques sur les performances et l’utilisation.
* [**Rechercher**](app-insights-diagnostic-search.md) : analysez des instances spécifiques d’événements telles que les demandes, les exceptions ou les suivis de journal.
* [**Analytics**](app-insights-analytics.md) : pour des requêtes puissantes sur vos données de télémétrie.
* **Intervalle de temps** -ajuster la plage hello affichée par tous les graphiques hello sur le panneau de hello.
* **Supprimer** -supprimer la ressource d’Application Insights hello pour cette application. Vous devez également supprimer les packages d’Application Insights hello de code de votre application, ou modifier hello [clé d’instrumentation](app-insights-create-new-resource.md#copy-the-instrumentation-key) dans votre application toodirect télémétrie tooa autre Application Insights ressource.

### <a name="essentials-tab"></a>Onglet Bases
* [Clé d’instrumentation](app-insights-create-new-resource.md#copy-the-instrumentation-key) : identifie la ressource de cette application.
* Tarification : mettez les fonctionnalités à disposition et définissez des plafonds de volume.

### <a name="app-navigation-bar"></a>Barre de navigation au sein d’une application
![Barre de navigation gauche](./media/app-insights-dashboards/app-left-nav-bar.png)

* **Vue d’ensemble** -panneau Vue d’ensemble de l’application toohello retour.
* **Journal d’activité** : alertes et événements d’administration Azure.
* [**Contrôle d’accès** ](app-insights-resources-roles-access-control.md) -fournissent l’accès aux membres de tooteam et d’autres.
* [**Balises** ](../azure-resource-manager/resource-group-using-tags.md) -utilisation des balises toogroup votre application avec d’autres utilisateurs.

EXAMINER

* [**Mappage d’application** ](app-insights-app-map.md) -carte Active affichant les composants de votre application, d’hello dérivé des informations de dépendance hello.
* [**Détection intelligente**](app-insights-proactive-diagnostics.md) : consultez les récentes alertes sur les performances.
* [**Flux en direct**](app-insights-live-stream.md) pour un ensemble de mesures quasi instantanées, ce qui est utile lors du déploiement d’une nouvelle version ou du débogage.
* [**Disponibilité / tests Web** ](app-insights-monitor-web-app-availability.md) -envoyer les requêtes régulières tooyour application web à partir d’autour hello monde.*
* [**Les échecs, performances** ](app-insights-web-monitor-performance.md) -Exceptions, les taux d’échec et réponse arrive trop de demandes tooyour application et des requêtes à partir de votre application[dépendances](app-insights-asp-net-dependencies.md).
* [**Performances**](app-insights-web-monitor-performance.md) : temps de réponse, temps de réponse de dépendance.
* [Serveurs](app-insights-web-monitor-performance.md) : compteurs de performances. Disponible si vous [installez Status Monitor](app-insights-monitor-performance-live-website-now.md).
* **Navigateur** : nombre de pages consultées et performances AJAX. Disponible si vous [instrumentez vos pages web](app-insights-javascript.md).
* **Utilisation** : nombre de pages consultées, d’utilisateurs et de sessions. Disponible si vous [instrumentez vos pages web](app-insights-javascript.md).

CONFIGURER

* **Prise en main** : didacticiel en ligne.
* **Propriétés** : clé d’instrumentation, abonnement et ID de ressource.
* [Alertes](app-insights-alerts.md) : configuration des alertes de métriques.
* [Exportation continue](app-insights-export-telemetry.md) -configurer l’exportation de stockage tooAzure de télémétrie.
* [Tests de performances](app-insights-monitor-web-app-availability.md#performance-tests) : configurez une charge synthétique sur votre site web.
* [Quota et tarification](app-insights-pricing.md)et [échantillonnage d’ingestion](app-insights-sampling.md).
* **Accès aux API** -créer [annotations de version](app-insights-annotations.md) et pourquoi les API d’accès aux données.
* [**Éléments de travail** ](app-insights-diagnostic-search.md#create-work-item) -se connecter travail tooa système de suivi afin que vous pouvez créer des bogues lors de l’examen des données de télémétrie.

PARAMÈTRES

* [**Verrous**](../azure-resource-manager/resource-group-lock-resources.md) : verrouillez les ressources Azure.
* [**Script d’automatisation** ](app-insights-powershell.md) -exporter une définition de ressource Azure de hello afin que vous puissiez l’utiliser comme un modèle toocreate nouvelle des ressources.


## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes

|  |  |
| --- | --- |
| [Metrics Explorer](app-insights-metrics-explorer.md)<br/>Filtrez et segmentez les mesures. |![Exemple de recherche](./media/app-insights-dashboards/64.png) |
| [Recherche de diagnostic](app-insights-diagnostic-search.md)<br/>Recherchez et examinez des événements, ainsi que les événements associés, et créez des bogues. |![Exemple de recherche](./media/app-insights-dashboards/61.png) |
| [Analytics](app-insights-analytics.md)<br/>Tirez parti d’un puissant langage de requête. |![Exemple de recherche](./media/app-insights-dashboards/63.png) |
