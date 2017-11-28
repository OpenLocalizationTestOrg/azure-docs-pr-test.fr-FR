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
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="51d75-103">Exploration des mesures dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="51d75-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="51d75-104">Les mesures dans [Application Insights][start] sont des mesures et le nombre des événements envoyés par la télémétrie de votre application.</span><span class="sxs-lookup"><span data-stu-id="51d75-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="51d75-105">Elles vous permettent de détecter les problèmes de performances et de constater les tendances dans l'utilisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="51d75-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="51d75-106">Il existe un large éventail de mesures standard et vous pouvez également créer vos propres mesures personnalisées et vos propres événements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="51d75-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="51d75-107">Les mesures et le nombre des événements sont affichés dans des graphiques présentant les valeurs agrégées, comme la somme, la moyenne ou le décompte.</span><span class="sxs-lookup"><span data-stu-id="51d75-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="51d75-108">Voici un exemple de jeu de graphiques :</span><span class="sxs-lookup"><span data-stu-id="51d75-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="51d75-109">Graphiques de métriques partout où se trouvent dans le portail d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="51d75-110">Dans la plupart des cas, ils peuvent être personnalisés, et vous pouvez ajouter plusieurs panneau toohello de graphiques.</span><span class="sxs-lookup"><span data-stu-id="51d75-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="51d75-111">À partir du Panneau de vue d’ensemble de hello, parcourez toomore détaillée des graphiques (qui possède des fonctions, telles que « Serveurs »), ou cliquez sur **Metrics Explorer** tooopen un nouveau panneau où vous pouvez créer des graphiques personnalisés.</span><span class="sxs-lookup"><span data-stu-id="51d75-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="51d75-112">Période</span><span class="sxs-lookup"><span data-stu-id="51d75-112">Time range</span></span>
<span data-ttu-id="51d75-113">Vous pouvez modifier la période couverte par les graphiques hello ou des grilles dans n’importe quel panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Panneau de vue d’ensemble de hello ouvrir de votre application Bonjour portail Azure](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="51d75-115">Si vous attendez des données qui ne sont pas encore affichées, cliquez sur Actualiser.</span><span class="sxs-lookup"><span data-stu-id="51d75-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="51d75-116">Graphiques eux-mêmes Actualiser à intervalles, mais les intervalles de salutation sont plus longs pour les plages de temps plus.</span><span class="sxs-lookup"><span data-stu-id="51d75-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="51d75-117">Il peut prendre un certain temps pour toocome des données via le pipeline d’analyse hello sur un graphique.</span><span class="sxs-lookup"><span data-stu-id="51d75-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="51d75-118">toozoom dans la partie d’un graphique, faites glisser dessus :</span><span class="sxs-lookup"><span data-stu-id="51d75-118">toozoom into part of a chart, drag over it:</span></span>

![Sélectionnez une partie d'un graphique.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="51d75-120">Cliquez sur toorestore de bouton Annuler Zoom hello il.</span><span class="sxs-lookup"><span data-stu-id="51d75-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="51d75-121">Valeurs de granularité et de point</span><span class="sxs-lookup"><span data-stu-id="51d75-121">Granularity and point values</span></span>
<span data-ttu-id="51d75-122">Placez votre souris sur les valeurs de hello toodisplay hello graphique des métriques de hello à ce stade.</span><span class="sxs-lookup"><span data-stu-id="51d75-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Pointez la souris de hello sur un graphique](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="51d75-124">valeur Hello de métrique hello à un moment donné est agrégé sur hello précédant l’intervalle d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="51d75-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="51d75-125">intervalle d’échantillonnage de Hello ou « granularité » s’affiche en haut de hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![en-tête Hello un panneau.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="51d75-127">Vous pouvez ajuster la granularité hello dans le panneau de plage de temps hello :</span><span class="sxs-lookup"><span data-stu-id="51d75-127">You can adjust hello granularity in hello Time range blade:</span></span>

![en-tête Hello un panneau.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="51d75-129">granularités Hello disponibles dépendent de l’intervalle de temps hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="51d75-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="51d75-130">granularités explicite de Hello sont des alternatives toohello « automatic » la granularité de la plage de temps hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="51d75-131">Modification des graphiques et des grilles</span><span class="sxs-lookup"><span data-stu-id="51d75-131">Editing charts and grids</span></span>
<span data-ttu-id="51d75-132">tooadd un nouveau panneau toohello de graphique :</span><span class="sxs-lookup"><span data-stu-id="51d75-132">tooadd a new chart toohello blade:</span></span>

![Dans Metrics Explorer, sélectionnez Ajouter un graphique](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="51d75-134">Sélectionnez **modifier** sur une tooedit graphique existante ou nouvelle ce qu’elle affiche :</span><span class="sxs-lookup"><span data-stu-id="51d75-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Sélectionner une ou plusieurs mesures](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="51d75-136">Vous pouvez afficher plus d’une mesure sur un graphique, bien qu’il existe des restrictions sur les combinaisons de hello qui peuvent être affichés ensemble.</span><span class="sxs-lookup"><span data-stu-id="51d75-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="51d75-137">Dès que vous choisissez une métrique, certaines des hello qu'autres sont désactivés.</span><span class="sxs-lookup"><span data-stu-id="51d75-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="51d75-138">Si vous avez codé [des mesures personnalisées] [ track] dans votre application (appels tooTrackMetric et TrackEvent) qu’ils sont répertoriés ici.</span><span class="sxs-lookup"><span data-stu-id="51d75-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="51d75-139">Segmenter vos données</span><span class="sxs-lookup"><span data-stu-id="51d75-139">Segment your data</span></span>
<span data-ttu-id="51d75-140">Vous pouvez fractionner une métrique par propriété - par exemple, les vues de page toocompare sur des clients avec différents systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="51d75-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="51d75-141">Sélectionnez un graphique ou une grille, basculez sur le regroupement et choisir un toogroup de propriété par :</span><span class="sxs-lookup"><span data-stu-id="51d75-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Activez le regroupement, puis une propriété de regroupement](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="51d75-143">Lorsque vous utilisez le regroupement, les types de zone et graphique à barres hello fournissent un affichage empilé.</span><span class="sxs-lookup"><span data-stu-id="51d75-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="51d75-144">Cela est adapté, où la méthode d’agrégation hello est Sum.</span><span class="sxs-lookup"><span data-stu-id="51d75-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="51d75-145">Mais lorsque le type d’agrégation hello est moyenne, choisir les types d’affichage hello ligne ou de grille.</span><span class="sxs-lookup"><span data-stu-id="51d75-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="51d75-146">Si vous avez codé [des mesures personnalisées] [ track] dans votre application et elles incluent des valeurs de propriété, vous pouvez tooselect en mesure de propriété de hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="51d75-147">Graphique de hello n’est trop petite pour les données segmentées ?</span><span class="sxs-lookup"><span data-stu-id="51d75-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="51d75-148">Ajustez la hauteur :</span><span class="sxs-lookup"><span data-stu-id="51d75-148">Adjust its height:</span></span>

![Déplacez le curseur hello](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="51d75-150">Types d’agrégation</span><span class="sxs-lookup"><span data-stu-id="51d75-150">Aggregation types</span></span>
<span data-ttu-id="51d75-151">légende Hello côté hello par défaut affiche généralement hello agrégée valeur période hello graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="51d75-152">Si vous pointez sur le graphique de hello, il affiche la valeur de hello à ce stade.</span><span class="sxs-lookup"><span data-stu-id="51d75-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="51d75-153">Chaque point de données sur le graphique de hello est un agrégat des valeurs des données de hello Bonjour précédent d’échantillonnage de l’intervalle ou « granularité ».</span><span class="sxs-lookup"><span data-stu-id="51d75-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="51d75-154">granularité de Hello est indiquée en haut de hello du Panneau de hello et varie en fonction de hello une échelle globale du graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="51d75-155">Les mesures sont agrégées de différentes façons :</span><span class="sxs-lookup"><span data-stu-id="51d75-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="51d75-156">**Nombre de** est le nombre d’événements hello reçu dans l’intervalle d’échantillonnage de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="51d75-157">Il est utilisé pour des événements tels que les requêtes.</span><span class="sxs-lookup"><span data-stu-id="51d75-157">It is used for events such as requests.</span></span> <span data-ttu-id="51d75-158">Variations de hauteur de hello du graphique de hello indique des variations de taux de hello auquel hello se produisent.</span><span class="sxs-lookup"><span data-stu-id="51d75-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="51d75-159">Notez toutefois que la valeur numérique de hello change lorsque vous modifiez l’intervalle d’échantillonnage de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="51d75-160">**Somme** additionner les valeurs hello de tous les points de données hello reçus sur l’intervalle d’échantillonnage de hello ou période hello du graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="51d75-161">**Moyenne** divise hello somme par un nombre de points de données reçus sur un intervalle de salutation hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="51d75-162">**Unique** est utilisé pour comptabiliser les nombres d'utilisateurs et de comptes.</span><span class="sxs-lookup"><span data-stu-id="51d75-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="51d75-163">Sur l’intervalle d’échantillonnage de hello ou période hello graphique de hello, hello illustration nombre hello d’utilisateurs différents dans cette période.</span><span class="sxs-lookup"><span data-stu-id="51d75-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="51d75-164">**%** - versions en pourcentage de chaque agrégation utilisées uniquement avec des graphiques segmentés.</span><span class="sxs-lookup"><span data-stu-id="51d75-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="51d75-165">Hello total ajoute toujours too100 % et graphique de hello indique la contribution relative de hello des différents composants d’un total.</span><span class="sxs-lookup"><span data-stu-id="51d75-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Agrégation de pourcentage](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="51d75-167">Modifier le type d’agrégation hello</span><span class="sxs-lookup"><span data-stu-id="51d75-167">Change hello aggregation type</span></span>

![Modifier le graphique de hello, puis sélectionnez d’agrégation](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="51d75-169">méthode par défaut de Hello pour chaque mesure s’affiche lorsque vous créez un graphique ou lorsque toutes les métriques sont désactivées :</span><span class="sxs-lookup"><span data-stu-id="51d75-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Désélectionnez les valeurs par défaut de toutes les mesures toosee hello](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="51d75-171">Épingler l’axe des ordonnées</span><span class="sxs-lookup"><span data-stu-id="51d75-171">Pin Y-axis</span></span> 
<span data-ttu-id="51d75-172">Par défaut, un graphique affiche les valeurs d’axe Y à partir de zéro jusqu'à ce que les valeurs maximales dans la plage de données hello, toogive une représentation visuelle du quantum de valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="51d75-173">Mais dans certains cas plusieurs quantum hello il peut être intéressant toovisually inspecter les valeurs des modifications mineures.</span><span class="sxs-lookup"><span data-stu-id="51d75-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="51d75-174">Pour les personnalisations tels que cette utilisation hello l’axe des y plage édition fonctionnalité toopin hello l’axe des y valeur minimale ou maximale à l’emplacement souhaité.</span><span class="sxs-lookup"><span data-stu-id="51d75-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="51d75-175">Cliquez sur toobring de case à cocher « Paramètres avancés » des hello plage de l’axe des y paramètres</span><span class="sxs-lookup"><span data-stu-id="51d75-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Cliquez sur Paramètres avancés, sélectionnez une plage personnalisée et spécifiez les valeurs minimale et maximale.](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="51d75-177">Filtrer vos données</span><span class="sxs-lookup"><span data-stu-id="51d75-177">Filter your data</span></span>
<span data-ttu-id="51d75-178">métriques de hello simplement toosee pour un ensemble de valeurs de propriété sélectionné :</span><span class="sxs-lookup"><span data-stu-id="51d75-178">toosee just hello metrics for a selected set of property values:</span></span>

![Cliquez sur le filtre, développez une propriété et vérifiez les valeurs](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="51d75-180">Si vous ne sélectionnez pas toutes les valeurs pour une propriété particulière, il a même hello que la sélection de toutes les : il n’existe aucun filtre sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="51d75-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="51d75-181">Le nombre hello de notification des événements en même temps que chaque valeur de propriété.</span><span class="sxs-lookup"><span data-stu-id="51d75-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="51d75-182">Lorsque vous sélectionnez des valeurs d’une propriété, hello compte en même temps que les autres valeurs sont ajustées de propriété.</span><span class="sxs-lookup"><span data-stu-id="51d75-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="51d75-183">Les filtres s’appliquent à des graphiques de hello tooall dans un panneau.</span><span class="sxs-lookup"><span data-stu-id="51d75-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="51d75-184">Si vous souhaitez appliquer des filtres différents toodifferent graphiques, créez et enregistrez les panneaux des mesures différentes.</span><span class="sxs-lookup"><span data-stu-id="51d75-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="51d75-185">Si vous le souhaitez, vous pouvez épingler des graphiques à partir des différents panneaux toohello du tableau de bord, afin que vous pouvez les visualiser en même temps que l’autre.</span><span class="sxs-lookup"><span data-stu-id="51d75-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="51d75-186">Supprimer le robot et tester le trafic web</span><span class="sxs-lookup"><span data-stu-id="51d75-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="51d75-187">Utiliser le filtre hello **trafic réel ou synthétique** et **réel**.</span><span class="sxs-lookup"><span data-stu-id="51d75-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="51d75-188">Vous pouvez également filtrer par **source du trafic synthétique**.</span><span class="sxs-lookup"><span data-stu-id="51d75-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="51d75-189">liste de filtres toohello tooadd propriétés</span><span class="sxs-lookup"><span data-stu-id="51d75-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="51d75-190">Voulez-vous toofilter la télémétrie sur une catégorie de vos propres choix ?</span><span class="sxs-lookup"><span data-stu-id="51d75-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="51d75-191">Par exemple, vous pouvez diviser vos utilisateurs en catégories différentes et segmenter vos données à l’aide de ces catégories.</span><span class="sxs-lookup"><span data-stu-id="51d75-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="51d75-192">[Créez votre propriété](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="51d75-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="51d75-193">Définir dans un [initialiseur de télémétrie](app-insights-api-custom-events-metrics.md#defaults) toohave apparaissent dans toutes les données de télémétrie - y compris les données de télémétrie standard hello envoyés par différents modules du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="51d75-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="51d75-194">Modifier le type de graphique hello</span><span class="sxs-lookup"><span data-stu-id="51d75-194">Edit hello chart type</span></span>
<span data-ttu-id="51d75-195">Notez que vous pouvez basculer entre les grilles et les graphiques :</span><span class="sxs-lookup"><span data-stu-id="51d75-195">Notice that you can switch between grids and graphs:</span></span>

![Sélectionnez une grille ou un graphique, puis choisissez un type de graphique](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="51d75-197">Enregistrer votre panneau de mesures</span><span class="sxs-lookup"><span data-stu-id="51d75-197">Save your metrics blade</span></span>
<span data-ttu-id="51d75-198">Une fois que vous avez créé des graphiques, enregistrez-les en tant que favoris.</span><span class="sxs-lookup"><span data-stu-id="51d75-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="51d75-199">Vous pouvez choisir si tooshare il avec d’autres membres de l’équipe, si vous utilisez un compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="51d75-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Choisissez Favori](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="51d75-201">Panneau de hello toosee, **Panneau de vue d’ensemble toohello accédez** et ouvrir Favoris :</span><span class="sxs-lookup"><span data-stu-id="51d75-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Dans le panneau de vue d’ensemble de hello, choisissez Favoris](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="51d75-203">Si vous avez choisi d’intervalle de temps relatif lorsque vous avez enregistré, panneau de hello sera mis à jour avec les mesures de dernière hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="51d75-204">Si vous avez choisi d’intervalle de temps absolu, il affichera hello les mêmes données chaque fois.</span><span class="sxs-lookup"><span data-stu-id="51d75-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="51d75-205">Panneau hello de réinitialisation</span><span class="sxs-lookup"><span data-stu-id="51d75-205">Reset hello blade</span></span>
<span data-ttu-id="51d75-206">Si vous modifiez un panneau, mais ensuite vous aimeriez tooget toohello arrière d’origine enregistrée ensemble, cliquez sur Réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="51d75-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![Dans les boutons hello haut hello de l’Explorateur de métrique](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="51d75-208">Flux de métriques temps réel</span><span class="sxs-lookup"><span data-stu-id="51d75-208">Live metrics stream</span></span>

<span data-ttu-id="51d75-209">Pour obtenir une vue bien plus immédiate de votre télémétrie, ouvrez le [Flux temps réel](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="51d75-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="51d75-210">La plupart des mesures prennent quelques minutes tooappear, en raison des processus hello d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="51d75-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="51d75-211">En revanche, les métriques temps réel sont optimisées pour avoir une faible latence.</span><span class="sxs-lookup"><span data-stu-id="51d75-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="51d75-212">Définir des alertes</span><span class="sxs-lookup"><span data-stu-id="51d75-212">Set alerts</span></span>
<span data-ttu-id="51d75-213">toobe informé par courrier électronique de valeurs inhabituelles de toute mesure, ajouter une alerte.</span><span class="sxs-lookup"><span data-stu-id="51d75-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="51d75-214">Vous pouvez choisir des administrateurs de comptes toohello toosend hello par courrier électronique, ou d’adresses de messagerie toospecific.</span><span class="sxs-lookup"><span data-stu-id="51d75-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![Dans Metrics Explorer, sélectionnez Règles d'alerte, Ajouter une alerte](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="51d75-216">[En savoir plus sur les alertes][alerts].</span><span class="sxs-lookup"><span data-stu-id="51d75-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="51d75-217">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="51d75-217">Continuous Export</span></span>
<span data-ttu-id="51d75-218">Si vous souhaitez mettre en place une exportation continue des données pour les traiter en externe, envisagez d’utiliser l [’Exportation continue](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="51d75-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="51d75-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="51d75-219">Power BI</span></span>
<span data-ttu-id="51d75-220">Si vous souhaitez que les vues enrichies de vos données, vous pouvez [exporter tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="51d75-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="51d75-221">Analyse</span><span class="sxs-lookup"><span data-stu-id="51d75-221">Analytics</span></span>
<span data-ttu-id="51d75-222">[Analytique](app-insights-analytics.md) est un tooanalyze de façon plus polyvalente votre télémétrie à l’aide d’un langage de requête puissantes.</span><span class="sxs-lookup"><span data-stu-id="51d75-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="51d75-223">Utilisez-le si vous souhaitez toocombine ou calculer les résultats à partir de métriques ou effectuez une exploration approfondie de performances récente de votre application.</span><span class="sxs-lookup"><span data-stu-id="51d75-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="51d75-224">À partir d’un graphique de métrique, vous pouvez cliquer sur hello Analytique icône tooget directement toohello Analytique requête équivalente.</span><span class="sxs-lookup"><span data-stu-id="51d75-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="51d75-225">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="51d75-225">Troubleshooting</span></span>
<span data-ttu-id="51d75-226">*Mon graphique ne contient aucune donnée.*</span><span class="sxs-lookup"><span data-stu-id="51d75-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="51d75-227">Les filtres s’appliquent à des graphiques de hello tooall sur le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="51d75-228">Assurez-vous que, pendant que vous vous concentrez sur un graphique, vous n’avez pas définir un filtre qui exclut toutes les données hello sur un autre.</span><span class="sxs-lookup"><span data-stu-id="51d75-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="51d75-229">Si vous souhaitez tooset différents filtres sur les différents graphiques, créez-les dans différents panneaux, enregistrez les Favoris séparés.</span><span class="sxs-lookup"><span data-stu-id="51d75-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="51d75-230">Si vous le souhaitez, vous pouvez les épingler toohello le tableau de bord afin que vous pouvez les visualiser en même temps que l’autre.</span><span class="sxs-lookup"><span data-stu-id="51d75-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="51d75-231">Si vous regroupez un graphique par une propriété qui n’est pas définie sur métrique de hello, puis il y aura rien sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="51d75-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="51d75-232">Essayez de désélectionner l’option « regrouper par » ou choisissez une propriété de regroupement différente.</span><span class="sxs-lookup"><span data-stu-id="51d75-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="51d75-233">Les données de performances (UC, taux d’E/S, etc.) sont disponibles pour les services web Java, les applications de bureau Windows, les [services et applications web IIS si vous installez le moniteur d’état](app-insights-monitor-performance-live-website-now.md) (Status monitor) et [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="51d75-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="51d75-234">Ces données ne sont pas disponibles pour les sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="51d75-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="51d75-235">Vidéo</span><span class="sxs-lookup"><span data-stu-id="51d75-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="51d75-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51d75-236">Next steps</span></span>
* [<span data-ttu-id="51d75-237">Surveillance de l’utilisation avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="51d75-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="51d75-238">Utilisation de Diagnostic Search</span><span class="sxs-lookup"><span data-stu-id="51d75-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
