---
title: "aaaExploring de mesures d’Application Azure Insights | Documents Microsoft"
description: "Comment toointerpret graphiques dans l’Explorateur de métriques et panneaux de métrique explorer toocustomize."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a>Exploration des mesures dans Application Insights
Les mesures dans [Application Insights][start] sont des mesures et le nombre des événements envoyés par la télémétrie de votre application. Elles vous permettent de détecter les problèmes de performances et de constater les tendances dans l'utilisation de votre application. Il existe un large éventail de mesures standard et vous pouvez également créer vos propres mesures personnalisées et vos propres événements personnalisés.

Les mesures et le nombre des événements sont affichés dans des graphiques présentant les valeurs agrégées, comme la somme, la moyenne ou le décompte.

Voici un exemple de jeu de graphiques :

![](./media/app-insights-metrics-explorer/01-overview.png)

Graphiques de métriques partout où se trouvent dans le portail d’Application Insights hello. Dans la plupart des cas, ils peuvent être personnalisés, et vous pouvez ajouter plusieurs panneau toohello de graphiques. À partir du Panneau de vue d’ensemble de hello, parcourez toomore détaillée des graphiques (qui possède des fonctions, telles que « Serveurs »), ou cliquez sur **Metrics Explorer** tooopen un nouveau panneau où vous pouvez créer des graphiques personnalisés.

## <a name="time-range"></a>Période
Vous pouvez modifier la période couverte par les graphiques hello ou des grilles dans n’importe quel panneau de hello.

![Panneau de vue d’ensemble de hello ouvrir de votre application Bonjour portail Azure](./media/app-insights-metrics-explorer/03-range.png)

Si vous attendez des données qui ne sont pas encore affichées, cliquez sur Actualiser. Graphiques eux-mêmes Actualiser à intervalles, mais les intervalles de salutation sont plus longs pour les plages de temps plus. Il peut prendre un certain temps pour toocome des données via le pipeline d’analyse hello sur un graphique.

toozoom dans la partie d’un graphique, faites glisser dessus :

![Sélectionnez une partie d'un graphique.](./media/app-insights-metrics-explorer/12-drag.png)

Cliquez sur toorestore de bouton Annuler Zoom hello il.

## <a name="granularity-and-point-values"></a>Valeurs de granularité et de point
Placez votre souris sur les valeurs de hello toodisplay hello graphique des métriques de hello à ce stade.

![Pointez la souris de hello sur un graphique](./media/app-insights-metrics-explorer/02-focus.png)

valeur Hello de métrique hello à un moment donné est agrégé sur hello précédant l’intervalle d’échantillonnage.

intervalle d’échantillonnage de Hello ou « granularité » s’affiche en haut de hello du Panneau de hello.

![en-tête Hello un panneau.](./media/app-insights-metrics-explorer/11-grain.png)

Vous pouvez ajuster la granularité hello dans le panneau de plage de temps hello :

![en-tête Hello un panneau.](./media/app-insights-metrics-explorer/grain.png)

granularités Hello disponibles dépendent de l’intervalle de temps hello sélectionné. granularités explicite de Hello sont des alternatives toohello « automatic » la granularité de la plage de temps hello.


## <a name="editing-charts-and-grids"></a>Modification des graphiques et des grilles
tooadd un nouveau panneau toohello de graphique :

![Dans Metrics Explorer, sélectionnez Ajouter un graphique](./media/app-insights-metrics-explorer/04-add.png)

Sélectionnez **modifier** sur une tooedit graphique existante ou nouvelle ce qu’elle affiche :

![Sélectionner une ou plusieurs mesures](./media/app-insights-metrics-explorer/08-select.png)

Vous pouvez afficher plus d’une mesure sur un graphique, bien qu’il existe des restrictions sur les combinaisons de hello qui peuvent être affichés ensemble. Dès que vous choisissez une métrique, certaines des hello qu'autres sont désactivés.

Si vous avez codé [des mesures personnalisées] [ track] dans votre application (appels tooTrackMetric et TrackEvent) qu’ils sont répertoriés ici.

## <a name="segment-your-data"></a>Segmenter vos données
Vous pouvez fractionner une métrique par propriété - par exemple, les vues de page toocompare sur des clients avec différents systèmes d’exploitation.

Sélectionnez un graphique ou une grille, basculez sur le regroupement et choisir un toogroup de propriété par :

![Activez le regroupement, puis une propriété de regroupement](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> Lorsque vous utilisez le regroupement, les types de zone et graphique à barres hello fournissent un affichage empilé. Cela est adapté, où la méthode d’agrégation hello est Sum. Mais lorsque le type d’agrégation hello est moyenne, choisir les types d’affichage hello ligne ou de grille.
>
>

Si vous avez codé [des mesures personnalisées] [ track] dans votre application et elles incluent des valeurs de propriété, vous pouvez tooselect en mesure de propriété de hello dans la liste de hello.

Graphique de hello n’est trop petite pour les données segmentées ? Ajustez la hauteur :

![Déplacez le curseur hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a>Types d’agrégation
légende Hello côté hello par défaut affiche généralement hello agrégée valeur période hello graphique de hello. Si vous pointez sur le graphique de hello, il affiche la valeur de hello à ce stade.

Chaque point de données sur le graphique de hello est un agrégat des valeurs des données de hello Bonjour précédent d’échantillonnage de l’intervalle ou « granularité ». granularité de Hello est indiquée en haut de hello du Panneau de hello et varie en fonction de hello une échelle globale du graphique de hello.

Les mesures sont agrégées de différentes façons :

* **Nombre de** est le nombre d’événements hello reçu dans l’intervalle d’échantillonnage de hello. Il est utilisé pour des événements tels que les requêtes. Variations de hauteur de hello du graphique de hello indique des variations de taux de hello auquel hello se produisent. Notez toutefois que la valeur numérique de hello change lorsque vous modifiez l’intervalle d’échantillonnage de hello.
* **Somme** additionner les valeurs hello de tous les points de données hello reçus sur l’intervalle d’échantillonnage de hello ou période hello du graphique de hello.
* **Moyenne** divise hello somme par un nombre de points de données reçus sur un intervalle de salutation hello.
* **Unique** est utilisé pour comptabiliser les nombres d'utilisateurs et de comptes. Sur l’intervalle d’échantillonnage de hello ou période hello graphique de hello, hello illustration nombre hello d’utilisateurs différents dans cette période.
* **%** - versions en pourcentage de chaque agrégation utilisées uniquement avec des graphiques segmentés. Hello total ajoute toujours too100 % et graphique de hello indique la contribution relative de hello des différents composants d’un total.

    ![Agrégation de pourcentage](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a>Modifier le type d’agrégation hello

![Modifier le graphique de hello, puis sélectionnez d’agrégation](./media/app-insights-metrics-explorer/05-aggregation.png)

méthode par défaut de Hello pour chaque mesure s’affiche lorsque vous créez un graphique ou lorsque toutes les métriques sont désactivées :

![Désélectionnez les valeurs par défaut de toutes les mesures toosee hello](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a>Épingler l’axe des ordonnées 
Par défaut, un graphique affiche les valeurs d’axe Y à partir de zéro jusqu'à ce que les valeurs maximales dans la plage de données hello, toogive une représentation visuelle du quantum de valeurs de hello. Mais dans certains cas plusieurs quantum hello il peut être intéressant toovisually inspecter les valeurs des modifications mineures. Pour les personnalisations tels que cette utilisation hello l’axe des y plage édition fonctionnalité toopin hello l’axe des y valeur minimale ou maximale à l’emplacement souhaité.
Cliquez sur toobring de case à cocher « Paramètres avancés » des hello plage de l’axe des y paramètres

![Cliquez sur Paramètres avancés, sélectionnez une plage personnalisée et spécifiez les valeurs minimale et maximale.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a>Filtrer vos données
métriques de hello simplement toosee pour un ensemble de valeurs de propriété sélectionné :

![Cliquez sur le filtre, développez une propriété et vérifiez les valeurs](./media/app-insights-metrics-explorer/19-filter.png)

Si vous ne sélectionnez pas toutes les valeurs pour une propriété particulière, il a même hello que la sélection de toutes les : il n’existe aucun filtre sur cette propriété.

Le nombre hello de notification des événements en même temps que chaque valeur de propriété. Lorsque vous sélectionnez des valeurs d’une propriété, hello compte en même temps que les autres valeurs sont ajustées de propriété.

Les filtres s’appliquent à des graphiques de hello tooall dans un panneau. Si vous souhaitez appliquer des filtres différents toodifferent graphiques, créez et enregistrez les panneaux des mesures différentes. Si vous le souhaitez, vous pouvez épingler des graphiques à partir des différents panneaux toohello du tableau de bord, afin que vous pouvez les visualiser en même temps que l’autre.

### <a name="remove-bot-and-web-test-traffic"></a>Supprimer le robot et tester le trafic web
Utiliser le filtre hello **trafic réel ou synthétique** et **réel**.

Vous pouvez également filtrer par **source du trafic synthétique**.

### <a name="tooadd-properties-toohello-filter-list"></a>liste de filtres toohello tooadd propriétés
Voulez-vous toofilter la télémétrie sur une catégorie de vos propres choix ? Par exemple, vous pouvez diviser vos utilisateurs en catégories différentes et segmenter vos données à l’aide de ces catégories.

[Créez votre propriété](app-insights-api-custom-events-metrics.md#properties). Définir dans un [initialiseur de télémétrie](app-insights-api-custom-events-metrics.md#defaults) toohave apparaissent dans toutes les données de télémétrie - y compris les données de télémétrie standard hello envoyés par différents modules du Kit de développement logiciel.

## <a name="edit-hello-chart-type"></a>Modifier le type de graphique hello
Notez que vous pouvez basculer entre les grilles et les graphiques :

![Sélectionnez une grille ou un graphique, puis choisissez un type de graphique](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a>Enregistrer votre panneau de mesures
Une fois que vous avez créé des graphiques, enregistrez-les en tant que favoris. Vous pouvez choisir si tooshare il avec d’autres membres de l’équipe, si vous utilisez un compte professionnel.

![Choisissez Favori](./media/app-insights-metrics-explorer/21-favorite-save.png)

Panneau de hello toosee, **Panneau de vue d’ensemble toohello accédez** et ouvrir Favoris :

![Dans le panneau de vue d’ensemble de hello, choisissez Favoris](./media/app-insights-metrics-explorer/22-favorite-get.png)

Si vous avez choisi d’intervalle de temps relatif lorsque vous avez enregistré, panneau de hello sera mis à jour avec les mesures de dernière hello. Si vous avez choisi d’intervalle de temps absolu, il affichera hello les mêmes données chaque fois.

## <a name="reset-hello-blade"></a>Panneau hello de réinitialisation
Si vous modifiez un panneau, mais ensuite vous aimeriez tooget toohello arrière d’origine enregistrée ensemble, cliquez sur Réinitialiser.

![Dans les boutons hello haut hello de l’Explorateur de métrique](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a>Flux de métriques temps réel

Pour obtenir une vue bien plus immédiate de votre télémétrie, ouvrez le [Flux temps réel](app-insights-live-stream.md). La plupart des mesures prennent quelques minutes tooappear, en raison des processus hello d’agrégation. En revanche, les métriques temps réel sont optimisées pour avoir une faible latence. 

## <a name="set-alerts"></a>Définir des alertes
toobe informé par courrier électronique de valeurs inhabituelles de toute mesure, ajouter une alerte. Vous pouvez choisir des administrateurs de comptes toohello toosend hello par courrier électronique, ou d’adresses de messagerie toospecific.

![Dans Metrics Explorer, sélectionnez Règles d'alerte, Ajouter une alerte](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

[En savoir plus sur les alertes][alerts].


## <a name="continuous-export"></a>Exportation continue
Si vous souhaitez mettre en place une exportation continue des données pour les traiter en externe, envisagez d’utiliser l [’Exportation continue](app-insights-export-telemetry.md).

### <a name="power-bi"></a>Power BI
Si vous souhaitez que les vues enrichies de vos données, vous pouvez [exporter tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).

## <a name="analytics"></a>Analyse
[Analytique](app-insights-analytics.md) est un tooanalyze de façon plus polyvalente votre télémétrie à l’aide d’un langage de requête puissantes. Utilisez-le si vous souhaitez toocombine ou calculer les résultats à partir de métriques ou effectuez une exploration approfondie de performances récente de votre application. 

À partir d’un graphique de métrique, vous pouvez cliquer sur hello Analytique icône tooget directement toohello Analytique requête équivalente.

## <a name="troubleshooting"></a>Résolution des problèmes
*Mon graphique ne contient aucune donnée.*

* Les filtres s’appliquent à des graphiques de hello tooall sur le panneau de hello. Assurez-vous que, pendant que vous vous concentrez sur un graphique, vous n’avez pas définir un filtre qui exclut toutes les données hello sur un autre.

    Si vous souhaitez tooset différents filtres sur les différents graphiques, créez-les dans différents panneaux, enregistrez les Favoris séparés. Si vous le souhaitez, vous pouvez les épingler toohello le tableau de bord afin que vous pouvez les visualiser en même temps que l’autre.
* Si vous regroupez un graphique par une propriété qui n’est pas définie sur métrique de hello, puis il y aura rien sur le graphique de hello. Essayez de désélectionner l’option « regrouper par » ou choisissez une propriété de regroupement différente.
* Les données de performances (UC, taux d’E/S, etc.) sont disponibles pour les services web Java, les applications de bureau Windows, les [services et applications web IIS si vous installez le moniteur d’état](app-insights-monitor-performance-live-website-now.md) (Status monitor) et [Azure Cloud Services](app-insights-azure.md). Ces données ne sont pas disponibles pour les sites web Azure.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Étapes suivantes
* [Surveillance de l’utilisation avec Application Insights](app-insights-web-track-usage.md)
* [Utilisation de Diagnostic Search](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
