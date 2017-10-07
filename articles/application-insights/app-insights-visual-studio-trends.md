---
title: Tendances aaaAnalyzing dans Visual Studio | Documents Microsoft
description: "Analysez, visualisez et examinez les tendances de vos données de télémétrie Application Insights dans Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 3150c6fc-2691-44f6-a290-fc5cd68e692a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: 5c623ec040363f05e80ca927dc8855eb016adc99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-trends-in-visual-studio"></a>Analyse des tendances dans Visual Studio
outil de tendances Application Insights Hello visualise comment les événements de télémétrie importantes de votre application web changent au fil du temps, ce qui vous permet d’identifier rapidement les problèmes et les anomalies. En liant les toomore diagnostic des informations détaillées, des tendances peuvent vous aider à améliorer les performances de votre application, détecter les causes hello des exceptions et menez à partir de vos événements personnalisés.

![Exemple de fenêtre Tendances](./media/app-insights-visual-studio-trends/app-insights-trends-hero-750.png)

## <a name="configure-your-web-app-for-application-insights"></a>Configurer votre application web pour Application Insights

Si vous ne l’avez pas encore fait, [configurez votre application web pour Application Insights](app-insights-overview.md). Cela lui permet de portail d’Application Insights toosend télémétrie toohello. outil de tendances Hello lit les données de télémétrie hello à partir de là.

L’outil Tendances Application Insights est disponible dans Visual Studio 2015 Update 3 et versions ultérieures.

## <a name="open-application-insights-trends"></a>Ouvrir Tendances Application Insights
fenêtre de tendances Application Insights tooopen hello :

* Bouton de barre d’outils Application Insights hello, choisissez **Explorer les tendances de télémétrie**, ou
* Dans le menu contextuel du projet hello, choisissez **Application Insights > Explorer les tendances de télémétrie**, ou
* Dans la barre de menus de Visual Studio hello, choisissez **vue > autres fenêtres > tendances Application Insights**.

Vous pouvez voir une invite de commandes tooselect une ressource. Cliquez sur **sélectionner une ressource**, connectez-vous à un abonnement Azure, puis choisissez une ressource Application Insights à partir de la liste hello pour lequel vous souhaitez que les tendances de télémétrie tooanalyze.

## <a name="choose-a-trend-analysis"></a>Choisir une analyse de tendances
![Menu des types courants d’analyse des tendances](./media/app-insights-visual-studio-trends/app-insights-trends-1-750.png)

Mise en route en choisissant une des cinq analyses tendance commune, chaque analyse les données à partir de hello des dernières 24 heures :

* **Résoudre les problèmes de performances de vos requêtes serveur** -demandes effectuées service tooyour, regroupé par temps de réponse
* **Analyser les erreurs dans vos requêtes serveur** -demandes effectuées service tooyour, regroupé par code de réponse HTTP
* **Examiner toutes les exceptions dans votre application hello** -Exceptions à partir de votre service, regroupés par type d’exception
* **Vérifier les performances de hello de dépendances de votre application** -Services appelés par votre service, regroupés par temps de réponse
* **Inspectez vos événements personnalisés** : événements personnalisés que vous avez configurés pour votre service, regroupés par type d’événement.

Analyses intégrées sont disponibles à partir de hello **permet d’afficher les types courants d’analyse de télémétrie** bouton dans le coin supérieur gauche de hello de fenêtre de tendances hello.

## <a name="visualize-trends-in-your-application"></a>Visualiser les tendances de votre application
L’outil Tendances Application Insights crée une visualisation de série chronologique à partir des données de télémétrie de votre application. Chaque visualisation de série chronologique affiche un type de données de télémétrie regroupées par propriété sur un intervalle de temps donné. Vous pourriez par exemple, les demandes de serveur tooview, regroupés par pays hello provient, sur hello des dernières 24 heures. Dans cet exemple, chaque bulle de visualisation de hello représente un nombre de demandes de serveur hello dans certains pays/région pendant une heure.

Utilisez les contrôles hello haut hello hello fenêtre tooadjust quels types de données de télémétrie vous permet d’afficher. Tout d’abord, choisissez les types de données de télémétrie hello qui vous intéresse :

* **Telemetry Type (Type de télémétrie)** : requêtes serveur, exceptions, dépendances ou événements personnalisés.
* **Intervalle de temps** : n’importe où dans hello dernière 30 minutes toohello 3 derniers jours
* **Grouper par** : type d’exception, ID du problème, pays/région, etc.

Ensuite, cliquez sur **analyser les données de télémétrie** requête de hello toorun.

toonavigate entre des bulles dans la visualisation de hello :

* Cliquez sur tooselect une bulle, qui met à jour des filtres hello bas hello de fenêtre hello, synthèse des événements hello simplement se sont produites pendant une période spécifique
* Double-cliquez sur un outil de recherche en bulles toonavigate toohello et afficher tous les événements de télémétrie individuels hello qui s’est produite pendant la période
* CTRL + clic à bulles toode-select dans la visualisation de hello.

> [!TIP]
> Hello recherche des tendances et des outils fonctionnent ensemble toohelp identifier les causes hello des problèmes dans votre service parmi des milliers d’événements de télémétrie. Par exemple, si un après-midi vos clients remarquent que votre application est moins réactive, utilisez l’outil Tendances. Analyser les demandes effectuées tooyour service sur hello cours des dernières heures, regroupés par temps de réponse. Vérifiez si un groupe de requêtes lentes inhabituellement volumineux existe, Puis double-cliquez sur cet outil de recherche de bulle toogo toohello, les événements de requête filtrée toothose. À partir de la recherche, vous pouvez explorer le contenu de hello de ces demandes et parcourir le code de toohello impliqués problème de hello tooresolve.
> 
> 

## <a name="filter"></a>Filtrer
Découvrir des tendances plus spécifiques avec des contrôles de filtre hello bas hello de fenêtre hello. tooapply un filtre, cliquez sur son nom. Vous pouvez rapidement basculer entre les tendances toodiscover différents filtres qui peuvent être masquer dans une dimension particulière de votre télémétrie. Si vous appliquez un filtre dans une dimension, comme le Type d’Exception, des filtres dans d’autres dimensions restent interactifs, même si elles apparaissent grisées. tooun-appliquer un filtre, cliquez de nouveau dessus. CTRL + clic tooselect plusieurs filtres dans hello même dimension.

![Filtres de tendances](./media/app-insights-visual-studio-trends/TrendsFiltering-750.png)

Que se passe-t-il si vous souhaitez tooapply plusieurs filtres ? 

1. Appliquer un filtre de premier hello. 
2. Cliquez sur hello **appliquer des filtres sélectionnés et interroger à nouveau** bouton par nom hello de dimension hello de votre premier filtre. Il interroge nouveau vos données de télémétrie pour seulement les événements qui correspondent au filtre de premier hello. 
3. Appliquez un second filtre. 
4. Répétez hello processus toofind les tendances des sous-ensembles spécifiques de votre télémétrie. Exemple : les requêtes serveur nommées « GET Home/Index » *et* provenant d’Allemagne *et* ayant reçu le code de réponse 500. 

tooun-appliquer un de ces filtres, cliquez sur hello **supprimez les filtres sélectionnés et interroger à nouveau** bouton pour la dimension de hello.

![Filtres multiples](./media/app-insights-visual-studio-trends/TrendsFiltering2-750.png)

## <a name="find-anomalies"></a>Rechercher des anomalies
outil de tendances Hello peut mettre en surbrillance des bulles d’événements qui sont des bulles tooother comparés anormale Bonjour même série chronologique. Dans la liste déroulante Type d’affichage de hello, choisissez **décomptes dans l’intervalle de planification (anomalies en surbrillance)** ou **pourcentages dans l’intervalle de planification (anomalies en surbrillance)**. Les bulles rouges sont anormales. Anomalies sont définies sous forme de bulles avec un nombre/pourcentage excédant 2.1 fois hello écart de nombre/pourcentage hello qui s’est produite dans hello au-delà des deux périodes de temps (48 heures si vous visualisez hello dernières 24 heures, etc..).

![Les points colorés indiquent des anomalies](./media/app-insights-visual-studio-trends/TrendsAnomalies-750.png)

> [!TIP]
> La mise en surbrillance des anomalies est particulièrement utile pour détecter les valeurs hors norme dans les séries chronologiques des petites bulles dont les tailles pourraient sinon sembler identiques.  
> 
> 

## <a name="next"></a>Étapes suivantes
|  |  |
| --- | --- |
| **[Utilisation d’Application Insights dans Visual Studio](app-insights-visual-studio.md)**<br/>Rechercher les données de télémétrie, voir les données dans CodeLens et configurer Application Insights. le tout dans Visual Studio. |![Droit hello projet, puis choisissez Application Insights, recherche](./media/app-insights-visual-studio-trends/34.png) |
| **[Ajouter des données](app-insights-asp-net-more.md)**<br/>Analysez l’utilisation, la disponibilité, les dépendances et les exceptions. Intégrer des traces à partir des frameworks de journalisation. Écrire des données de télémétrie personnalisées. |![Visual Studio](./media/app-insights-visual-studio-trends/64.png) |
| **[Utilisation de portail d’Application Insights hello](app-insights-dashboards.md)**<br/>Tableaux de bord, puissants outils de diagnostic et d’analyse, alertes, mappage direct des dépendances de votre application et exportation des données de télémétrie. |![Visual Studio](./media/app-insights-visual-studio-trends/62.png) |

