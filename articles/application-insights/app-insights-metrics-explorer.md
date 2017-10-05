---
title: Exploration des mesures dans Azure Application Insights | Microsoft Docs
description: "Comment interpréter les graphiques dans Metric Explorer et comment personnaliser les panneaux de Metrics Explorer."
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
ms.openlocfilehash: a13500284caab79bbe221060ccf3d925ffb1fab5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="cfc7f-103">Exploration des mesures dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfc7f-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="cfc7f-104">Les mesures dans [Application Insights][start] sont des mesures et le nombre des événements envoyés par la télémétrie de votre application.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="cfc7f-105">Elles vous permettent de détecter les problèmes de performances et de constater les tendances dans l'utilisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="cfc7f-106">Il existe un large éventail de mesures standard et vous pouvez également créer vos propres mesures personnalisées et vos propres événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="cfc7f-107">Les mesures et le nombre des événements sont affichés dans des graphiques présentant les valeurs agrégées, comme la somme, la moyenne ou le décompte.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="cfc7f-108">Voici un exemple de jeu de graphiques :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="cfc7f-109">Tous les graphiques de mesures se trouvent dans le portail Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-109">You find metrics charts everywhere in the Application Insights portal.</span></span> <span data-ttu-id="cfc7f-110">Dans la plupart des cas, ils peuvent être personnalisés, et vous pouvez ajouter plusieurs graphiques dans le panneau.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-110">In most cases, they can be customized, and you can add more charts to the blade.</span></span> <span data-ttu-id="cfc7f-111">Dans le volet d’aperçu, cliquez pour accéder aux graphiques plus détaillés (ayant des titres tels que « Server »), ou cliquez sur **Metrics Explorer** pour ouvrir un nouveau panneau où vous pouvez créer des graphiques personnalisés.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-111">From the Overview blade, click through to more detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** to open a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="cfc7f-112">Période</span><span class="sxs-lookup"><span data-stu-id="cfc7f-112">Time range</span></span>
<span data-ttu-id="cfc7f-113">Vous pouvez modifier l’intervalle de temps sur lequel portent les graphiques et les grilles dans n’importe quel panneau.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-113">You can change the Time range covered by the charts or grids on any blade.</span></span>

![Ouvrez le panneau Vue d'ensemble de votre application dans le portail Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="cfc7f-115">Si vous attendez des données qui ne sont pas encore affichées, cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="cfc7f-116">Les graphiques s’actualisent régulièrement, mais plus les intervalles de temps sur lesquels ils portent sont étendus, plus les intervalles d’actualisation sont longs.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-116">Charts refresh themselves at intervals, but the intervals are longer for larger time ranges.</span></span> <span data-ttu-id="cfc7f-117">Les données peuvent mettre un certain temps pour passer du pipeline d’analyse au graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-117">It can take a while for data to come through the analysis pipeline onto a chart.</span></span>

<span data-ttu-id="cfc7f-118">Pour faire un zoom sur une partie d’un graphique, placez le curseur dessus :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-118">To zoom into part of a chart, drag over it:</span></span>

![Sélectionnez une partie d'un graphique.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="cfc7f-120">Cliquez sur le bouton d’annulation du zoom pour restaurer l’état initial.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-120">Click the Undo Zoom button to restore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="cfc7f-121">Valeurs de granularité et de point</span><span class="sxs-lookup"><span data-stu-id="cfc7f-121">Granularity and point values</span></span>
<span data-ttu-id="cfc7f-122">Pointez votre souris sur le graphique pour afficher les valeurs des mesures à ce stade.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-122">Hover your mouse over the chart to display the values of the metrics at that point.</span></span>

![Pointez la souris sur un graphique](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="cfc7f-124">La valeur de la mesure à un moment donné est agrégée à l'intervalle d'échantillonnage précédent.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-124">The value of the metric at a particular point is aggregated over the preceding sampling interval.</span></span>

<span data-ttu-id="cfc7f-125">L’intervalle d’échantillonnage, ou « granularité », s’affiche en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-125">The sampling interval or "granularity" is shown at the top of the blade.</span></span>

![En-tête du panneau.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="cfc7f-127">Vous pouvez ajuster le niveau de granularité dans le panneau Période :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-127">You can adjust the granularity in the Time range blade:</span></span>

![En-tête du panneau.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="cfc7f-129">Les niveaux de granularité disponibles dépendent de la période que vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-129">The granularities available depend on the time range you select.</span></span> <span data-ttu-id="cfc7f-130">Les niveaux de granularité explicites sont des alternatives à la granularité « automatique » pour la période.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-130">The explicit granularities are alternatives to the "automatic" granularity for the time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="cfc7f-131">Modification des graphiques et des grilles</span><span class="sxs-lookup"><span data-stu-id="cfc7f-131">Editing charts and grids</span></span>
<span data-ttu-id="cfc7f-132">Pour ajouter un nouveau graphique au panneau :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-132">To add a new chart to the blade:</span></span>

![Dans Metrics Explorer, sélectionnez Ajouter un graphique](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="cfc7f-134">Sélectionnez **Modifier** sur un graphique nouveau ou existant pour modifier ce qui est affiché :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-134">Select **Edit** on an existing or new chart to edit what it shows:</span></span>

![Sélectionner une ou plusieurs mesures](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="cfc7f-136">Vous pouvez afficher plusieurs mesures dans un graphique, bien qu'il existe des restrictions sur les combinaisons affichables.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-136">You can display more than one metric on a chart, though there are restrictions about the combinations that can be displayed together.</span></span> <span data-ttu-id="cfc7f-137">Dès que vous sélectionnez une mesure, certaines autres sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-137">As soon as you choose one metric, some of the others are disabled.</span></span>

<span data-ttu-id="cfc7f-138">Si vous avez ajouté des [mesures personnalisées][track] au code de votre application (appels à TrackMetric et TrackEvent), elles sont répertoriées ici.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-138">If you coded [custom metrics][track] into your app (calls to TrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="cfc7f-139">Segmenter vos données</span><span class="sxs-lookup"><span data-stu-id="cfc7f-139">Segment your data</span></span>
<span data-ttu-id="cfc7f-140">Vous pouvez fractionner une mesure par propriété, par exemple, pour comparer des affichages de page sur des clients avec différents systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-140">You can split a metric by property - for example, to compare page views on clients with different operating systems.</span></span>

<span data-ttu-id="cfc7f-141">Sélectionnez un graphique ou une grille, basculez vers le regroupement et choisissez une propriété de regroupement :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-141">Select a chart or grid, switch on grouping and pick a property to group by:</span></span>

![Activez le regroupement, puis une propriété de regroupement](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="cfc7f-143">Lorsque vous utilisez le regroupement, les types de graphiques en aires et à barres fournissent un affichage empilé.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-143">When you use grouping, the Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="cfc7f-144">Cet affichage convient pour la méthode d’agrégation Somme.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-144">This is suitable where the Aggregation method is Sum.</span></span> <span data-ttu-id="cfc7f-145">Mais si le type d’agrégation est Moyenne, choisissez les types d’affichage en ligne ou en grille.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-145">But where the aggregation type is Average, choose the Line or Grid display types.</span></span>
>
>

<span data-ttu-id="cfc7f-146">Si vous avez ajouté des [mesures personnalisées][track] au code de votre application et qu'elles incluent des valeurs de propriétés, vous pourrez sélectionner la propriété dans la liste.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able to select the property in the list.</span></span>

<span data-ttu-id="cfc7f-147">Le graphique est trop petit pour les données segmentées ?</span><span class="sxs-lookup"><span data-stu-id="cfc7f-147">Is the chart too small for segmented data?</span></span> <span data-ttu-id="cfc7f-148">Ajustez la hauteur :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-148">Adjust its height:</span></span>

![Ajustez le curseur.](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="cfc7f-150">Types d’agrégation</span><span class="sxs-lookup"><span data-stu-id="cfc7f-150">Aggregation types</span></span>
<span data-ttu-id="cfc7f-151">La légende sur le côté affiche généralement par défaut la valeur agrégée sur la période couverte par le graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-151">The legend at the side by default usually shows the aggregated value over the period of the chart.</span></span> <span data-ttu-id="cfc7f-152">Si vous pointez sur le graphique, il affiche la valeur au niveau de ce point.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-152">If you hover over the chart, it shows the value at that point.</span></span>

<span data-ttu-id="cfc7f-153">Chaque point de données du graphique est un agrégat des valeurs de données reçues dans l’intervalle d’échantillonnage précédent, encore appelé « granularité ».</span><span class="sxs-lookup"><span data-stu-id="cfc7f-153">Each data point on the chart is an aggregate of the data values received in the preceding sampling interval or "granularity".</span></span> <span data-ttu-id="cfc7f-154">La granularité est indiquée en haut du panneau et varie en fonction de l’échelle de temps globale du graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-154">The granularity is shown at the top of the blade, and varies with the overall timescale of the chart.</span></span>

<span data-ttu-id="cfc7f-155">Les mesures sont agrégées de différentes façons :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="cfc7f-156">**Count** est un décompte des événements reçus dans l’intervalle d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-156">**Count** is a count of the events received in the sampling interval.</span></span> <span data-ttu-id="cfc7f-157">Il est utilisé pour des événements tels que les requêtes.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-157">It is used for events such as requests.</span></span> <span data-ttu-id="cfc7f-158">Les variations dans la hauteur du graphique indiquent les variations de la vitesse à laquelle les événements se produisent.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-158">Variations in the height of the chart indicates variations in the rate at which the events occur.</span></span> <span data-ttu-id="cfc7f-159">Mais notez que la valeur numérique change lorsque vous modifiez l’intervalle d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-159">But note that the numeric value changes when you change the sampling interval.</span></span>
* <span data-ttu-id="cfc7f-160">**Sum** ajoute les valeurs de tous les points de données reçus pendant un intervalle d’échantillonnage ou la période du graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-160">**Sum** adds up the values of all the data points received over the sampling interval, or the period of the chart.</span></span>
* <span data-ttu-id="cfc7f-161">**Average** divise la somme par le nombre de points de données reçus durant l'intervalle.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-161">**Average** divides the Sum by the number of data points received over the interval.</span></span>
* <span data-ttu-id="cfc7f-162">**Unique** est utilisé pour comptabiliser les nombres d'utilisateurs et de comptes.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="cfc7f-163">Sur l’intervalle d’échantillonnage ou sur la période du graphique, la figure indique le nombre d’utilisateurs différents dans cette période.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-163">Over the sampling interval, or over the period of the chart, the figure shows the count of different users seen in that time.</span></span>
* <span data-ttu-id="cfc7f-164">**%** - versions en pourcentage de chaque agrégation utilisées uniquement avec des graphiques segmentés.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="cfc7f-165">Le total équivaut toujours à 100 %, et le graphique montre la contribution relative des différents composants d’un total.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-165">The total always adds up to 100%, and the chart shows the relative contribution of different components of a total.</span></span>

    ![Agrégation de pourcentage](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-the-aggregation-type"></a><span data-ttu-id="cfc7f-167">Modification du type d’agrégation</span><span class="sxs-lookup"><span data-stu-id="cfc7f-167">Change the aggregation type</span></span>

![Modification du graphique, puis sélection de l’agrégation](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="cfc7f-169">La méthode par défaut de chaque mesure s’affiche lorsque vous créez un graphique ou lorsque toutes les mesures sont désélectionnées :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-169">The default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Désélectionnez toutes les métriques afin d’afficher les valeurs par défaut](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="cfc7f-171">Épingler l’axe des ordonnées</span><span class="sxs-lookup"><span data-stu-id="cfc7f-171">Pin Y-axis</span></span> 
<span data-ttu-id="cfc7f-172">Par défaut, un graphique affiche les ordonnées à partir de zéro jusqu’aux valeurs maximales dans la plage de données, afin de donner une représentation visuelle du quantum des valeurs.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-172">By default a chart shows Y axis values starting from zero till maximum values in the data range, to give a visual representation of quantum of the values.</span></span> <span data-ttu-id="cfc7f-173">Mais parfois, plus que le quantum, il peut être intéressant d’examiner visuellement les changements mineurs dans les valeurs.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-173">But in some cases more than the quantum it might be interesting to visually inspect minor changes in values.</span></span> <span data-ttu-id="cfc7f-174">Pour ce genre de personnalisations, utilisez la fonction d’édition de la plage des ordonnées afin d’épingler la valeur Y minimale ou maximale à l’endroit souhaité.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-174">For customizations like this use the Y-axis range editing feature to pin the Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="cfc7f-175">Activez la case à cocher « Paramètres avancés » pour afficher les paramètres de la plage des ordonnées.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-175">Click on "Advanced Settings" check box to bring up the Y-axis range Settings</span></span>

![Cliquez sur Paramètres avancés, sélectionnez une plage personnalisée et spécifiez les valeurs minimale et maximale.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="cfc7f-177">Filtrer vos données</span><span class="sxs-lookup"><span data-stu-id="cfc7f-177">Filter your data</span></span>
<span data-ttu-id="cfc7f-178">Pour afficher uniquement les mesures d'un jeu de valeurs de propriété sélectionné :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-178">To see just the metrics for a selected set of property values:</span></span>

![Cliquez sur le filtre, développez une propriété et vérifiez les valeurs](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="cfc7f-180">Si vous ne sélectionnez aucune valeur pour une propriété particulière, c'est la même chose que si vous aviez sélectionné toutes les valeurs : il n'existe aucun filtre sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-180">If you don't select any values for a particular property, it's the same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="cfc7f-181">Notez le nombre d'événements en même temps que chaque valeur de propriété.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-181">Notice the counts of events alongside each property value.</span></span> <span data-ttu-id="cfc7f-182">Lorsque vous sélectionnez les valeurs d'une propriété, le nombre est modifié, en même temps que les autres valeurs de la propriété.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-182">When you select values of one property, the counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="cfc7f-183">Les filtres s’appliquent à tous les graphiques dans un panneau.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-183">Filters apply to all the charts on a blade.</span></span> <span data-ttu-id="cfc7f-184">Si vous souhaitez que différents filtres s’appliquent à différents graphiques, créez et enregistrez des panneaux de mesure différents.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-184">If you want different filters applied to different charts, create and save different metrics blades.</span></span> <span data-ttu-id="cfc7f-185">Si vous le souhaitez, vous pouvez épingler des graphiques à partir de différents panneaux au tableau de bord, afin de les afficher parallèlement.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-185">If you want, you can pin charts from different blades to the dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="cfc7f-186">Supprimer le robot et tester le trafic web</span><span class="sxs-lookup"><span data-stu-id="cfc7f-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="cfc7f-187">Utilisez le filtre de **trafic réel ou synthétique** et activez l’option **réel**.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-187">Use the filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="cfc7f-188">Vous pouvez également filtrer par **source du trafic synthétique**.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="to-add-properties-to-the-filter-list"></a><span data-ttu-id="cfc7f-189">Pour ajouter des propriétés à la liste de filtres</span><span class="sxs-lookup"><span data-stu-id="cfc7f-189">To add properties to the filter list</span></span>
<span data-ttu-id="cfc7f-190">Vous souhaitez filtrer la télémétrie pour une catégorie de votre choix ?</span><span class="sxs-lookup"><span data-stu-id="cfc7f-190">Would you like to filter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="cfc7f-191">Par exemple, vous pouvez diviser vos utilisateurs en catégories différentes et segmenter vos données à l’aide de ces catégories.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="cfc7f-192">[Créez votre propriété](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="cfc7f-193">Définissez-la dans un [Initialiseur de télémétrie](app-insights-api-custom-events-metrics.md#defaults) pour qu'elle s'affiche dans toute la télémétrie, notamment la télémétrie standard envoyée par différents modules de kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) to have it appear in all telemetry - including the standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-the-chart-type"></a><span data-ttu-id="cfc7f-194">Modifier le type de graphique</span><span class="sxs-lookup"><span data-stu-id="cfc7f-194">Edit the chart type</span></span>
<span data-ttu-id="cfc7f-195">Notez que vous pouvez basculer entre les grilles et les graphiques :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-195">Notice that you can switch between grids and graphs:</span></span>

![Sélectionnez une grille ou un graphique, puis choisissez un type de graphique](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="cfc7f-197">Enregistrer votre panneau de mesures</span><span class="sxs-lookup"><span data-stu-id="cfc7f-197">Save your metrics blade</span></span>
<span data-ttu-id="cfc7f-198">Une fois que vous avez créé des graphiques, enregistrez-les en tant que favoris.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="cfc7f-199">Si vous travaillez avec un compte professionnel, vous pouvez choisir de les partager avec d'autres membres de l'équipe.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-199">You can choose whether to share it with other team members, if you use an organizational account.</span></span>

![Choisissez Favori](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="cfc7f-201">Pour réafficher le panneau, **allez dans le panneau Vue d'ensemble** et ouvrez Favoris :</span><span class="sxs-lookup"><span data-stu-id="cfc7f-201">To see the blade again, **go to the overview blade** and open Favorites:</span></span>

![Dans le panneau Vue d'ensemble, cliquez sur Favoris](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="cfc7f-203">Si vous avez choisi une période relative lorsque vous avez enregistré, le panneau sera mis à jour avec les dernières mesures.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-203">If you chose Relative time range when you saved, the blade will be updated with the latest metrics.</span></span> <span data-ttu-id="cfc7f-204">Si vous avez choisi une période absolue, il affiche les mêmes données à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-204">If you chose Absolute time range, it will show the same data every time.</span></span>

## <a name="reset-the-blade"></a><span data-ttu-id="cfc7f-205">Réinitialiser le panneau</span><span class="sxs-lookup"><span data-stu-id="cfc7f-205">Reset the blade</span></span>
<span data-ttu-id="cfc7f-206">Si vous modifiez un panneau, mais que vous souhaitez revenir à la configuration originale enregistrée, cliquez sur Réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-206">If you edit a blade but then you'd like to get back to the original saved set, just click Reset.</span></span>

![Dans les boutons en haut de Metrics Explorer](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="cfc7f-208">Flux de métriques temps réel</span><span class="sxs-lookup"><span data-stu-id="cfc7f-208">Live metrics stream</span></span>

<span data-ttu-id="cfc7f-209">Pour obtenir une vue bien plus immédiate de votre télémétrie, ouvrez le [Flux temps réel](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="cfc7f-210">La plupart des mesures s’affichent au bout de quelques minutes en raison du processus d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-210">Most metrics take a few minutes to appear, because of the process of aggregation.</span></span> <span data-ttu-id="cfc7f-211">En revanche, les métriques temps réel sont optimisées pour avoir une faible latence.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="cfc7f-212">Définir des alertes</span><span class="sxs-lookup"><span data-stu-id="cfc7f-212">Set alerts</span></span>
<span data-ttu-id="cfc7f-213">Pour être averti par courrier électronique en cas de valeurs inhabituelles pour une métrique, ajoutez une alerte.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-213">To be notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="cfc7f-214">Vous pouvez choisir d'envoyer le courrier électronique aux administrateurs de compte ou à des adresses de messagerie spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-214">You can choose either to send the email to the account administrators, or to specific email addresses.</span></span>

![Dans Metrics Explorer, sélectionnez Règles d'alerte, Ajouter une alerte](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="cfc7f-216">[En savoir plus sur les alertes][alerts].</span><span class="sxs-lookup"><span data-stu-id="cfc7f-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="cfc7f-217">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="cfc7f-217">Continuous Export</span></span>
<span data-ttu-id="cfc7f-218">Si vous souhaitez mettre en place une exportation continue des données pour les traiter en externe, envisagez d’utiliser l [’Exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="cfc7f-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="cfc7f-219">Power BI</span></span>
<span data-ttu-id="cfc7f-220">Si vous souhaitez obtenir des vues enrichies de vos données, vous pouvez [exporter vers Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-220">If you want even richer views of your data, you can [export to Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="cfc7f-221">Analyse</span><span class="sxs-lookup"><span data-stu-id="cfc7f-221">Analytics</span></span>
<span data-ttu-id="cfc7f-222">[Analyse](app-insights-analytics.md) est un moyen plus souple d’analyser vos données de télémétrie à l’aide d’un langage de requête puissant.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-222">[Analytics](app-insights-analytics.md) is a more versatile way to analyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="cfc7f-223">Utilisez l’analyse si vous souhaitez combiner ou calculer les résultats à partir des mesures ou effectuer une exploration approfondie des performances récentes de votre application.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-223">Use it if you want to combine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="cfc7f-224">Dans un graphique de mesures, vous pouvez cliquer sur l’icône Analyse pour accéder directement à la requête d’analyse correspondante.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-224">From a metric chart, you can click the Analytics icon to get directly to the equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cfc7f-225">résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="cfc7f-225">Troubleshooting</span></span>
<span data-ttu-id="cfc7f-226">*Mon graphique ne contient aucune donnée.*</span><span class="sxs-lookup"><span data-stu-id="cfc7f-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="cfc7f-227">Les filtres s’appliquent à tous les graphiques du panneau.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-227">Filters apply to all the charts on the blade.</span></span> <span data-ttu-id="cfc7f-228">Lorsque vous vous concentrez sur un graphique, vérifiez que vous n’avez pas défini un filtre qui exclut toutes les données d’un autre graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all the data on another.</span></span>

    <span data-ttu-id="cfc7f-229">Si vous souhaitez définir des filtres différents sur différents graphiques, créez-les dans des panneaux différents, enregistrez-les sous forme de favoris distincts.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-229">If you want to set different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="cfc7f-230">Si vous le souhaitez, vous pouvez les épingler au tableau de bord afin de les afficher parallèlement.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-230">If you want, you can pin them to the dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="cfc7f-231">Si vous regroupez un graphique en fonction d’une propriété qui n’est pas définie dans la mesure, alors il n’y aura rien à afficher sur le graphique.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-231">If you group a chart by a property that is not defined on the metric, then there will be nothing on the chart.</span></span> <span data-ttu-id="cfc7f-232">Essayez de désélectionner l’option « regrouper par » ou choisissez une propriété de regroupement différente.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="cfc7f-233">Les données de performances (UC, taux d’E/S, etc.) sont disponibles pour les services web Java, les applications de bureau Windows, les [services et applications web IIS si vous installez le moniteur d’état](app-insights-monitor-performance-live-website-now.md) (Status monitor) et [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="cfc7f-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="cfc7f-234">Ces données ne sont pas disponibles pour les sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc7f-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="cfc7f-235">Vidéo</span><span class="sxs-lookup"><span data-stu-id="cfc7f-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="cfc7f-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfc7f-236">Next steps</span></span>
* [<span data-ttu-id="cfc7f-237">Surveillance de l’utilisation avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="cfc7f-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="cfc7f-238">Utilisation de Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="cfc7f-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
