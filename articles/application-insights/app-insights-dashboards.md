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
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="66c5e-103">Navigation et des tableaux de bord dans le portail Application Insights de hello</span><span class="sxs-lookup"><span data-stu-id="66c5e-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="66c5e-104">Une fois que vous avez [configurer Application Insights sur votre projet](app-insights-overview.md), les données télémétriques sur les performances et l’utilisation de votre application seront affiche dans la ressource d’Application Insights de votre projet dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="66c5e-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="66c5e-105">Rechercher vos données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="66c5e-105">Find your telemetry</span></span>
<span data-ttu-id="66c5e-106">Connectez-vous à toohello [portail Azure](https://portal.azure.com) et accédez ressource Application Insights toohello que vous avez créé pour votre application.</span><span class="sxs-lookup"><span data-stu-id="66c5e-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Cliquez sur Parcourir, sélectionnez Application Insights, puis sélectionnez votre application.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="66c5e-108">Panneau de vue d’ensemble de Hello (page) pour votre application affiche un résumé des métriques de diagnostic clés hello de votre application et est une passerelle toohello autres fonctionnalités du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Les principales itinéraires tooview votre télémétrie](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="66c5e-110">Vous pouvez personnaliser une des grilles et des graphiques de hello et épingler un tableau de bord tooa.</span><span class="sxs-lookup"><span data-stu-id="66c5e-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="66c5e-111">De cette façon, vous pouvez rassembler télémétrie de clé hello à partir de différentes applications dans un tableau de bord central.</span><span class="sxs-lookup"><span data-stu-id="66c5e-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="66c5e-112">Tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="66c5e-112">Dashboards</span></span>
<span data-ttu-id="66c5e-113">Hello première chose que vous voyez lorsque vous êtes connecté toohello [portail Microsoft Azure](https://portal.azure.com) est un tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="66c5e-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="66c5e-114">Ici vous pouvez rassembler des graphiques hello qui sont plus importante tooyou sur toutes vos ressources Azure, y compris les données de télémétrie des [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Un tableau de bord personnalisé.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="66c5e-116">**Accédez toospecific ressources** telles que votre application dans Application Insights : utiliser la barre gauche hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="66c5e-117">**Tableau de bord actuel toohello retour**, ou basculer entre les vues récente tooother : utilisez hello déroulante en haut à gauche.</span><span class="sxs-lookup"><span data-stu-id="66c5e-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="66c5e-118">**Passer des tableaux de bord**: utilisez hello déroulante sur le titre du tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="66c5e-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="66c5e-119">**Créer, modifier et partager des tableaux de bord** dans la barre d’outils du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="66c5e-120">**Modifier le tableau de bord hello**: placez le curseur sur une vignette, puis utiliser son haut barre toomove, personnaliser, ou le supprimer.</span><span class="sxs-lookup"><span data-stu-id="66c5e-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="66c5e-121">Ajouter le tableau de bord tooa</span><span class="sxs-lookup"><span data-stu-id="66c5e-121">Add tooa dashboard</span></span>
<span data-ttu-id="66c5e-122">Lorsque vous examinez un panneau ou un ensemble de graphiques qui est particulièrement intéressante, vous pouvez épingler une copie du tableau de bord toohello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="66c5e-123">Celui-ci sera affiché lors de votre prochain accès au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="66c5e-123">You'll see it next time you return there.</span></span>

![toopin un graphique, pointez sur celui-ci, puis sur «... » dans l’en-tête de hello.](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="66c5e-125">Épingler le graphique toodashboard.</span><span class="sxs-lookup"><span data-stu-id="66c5e-125">Pin chart toodashboard.</span></span> <span data-ttu-id="66c5e-126">Une copie du graphique de hello s’affiche sur le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="66c5e-127">Tableau de bord de toohello de code confidentiel hello ensemble panneau - il apparaît dans le tableau de bord hello sous forme de vignette que vous pouvez cliquer.</span><span class="sxs-lookup"><span data-stu-id="66c5e-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="66c5e-128">Cliquez sur hello en haut à gauche tooreturn toohello tableau de bord actuel.</span><span class="sxs-lookup"><span data-stu-id="66c5e-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="66c5e-129">Puis vous pouvez utiliser la vue actuelle du toohello tooreturn menu déroulant hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="66c5e-130">Notez que les graphiques sont regroupés en vignettes : une vignette peut contenir plusieurs graphiques.</span><span class="sxs-lookup"><span data-stu-id="66c5e-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="66c5e-131">Vous épinglez toohello du tableau de bord entier vignette hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="66c5e-132">Hello graphique est automatiquement actualisé avec une fréquence qui varie selon l’intervalle de temps du graphique hello :</span><span class="sxs-lookup"><span data-stu-id="66c5e-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="66c5e-133">La période d’heure de too1 : actualiser toutes les 5 minutes</span><span class="sxs-lookup"><span data-stu-id="66c5e-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="66c5e-134">Intervalle de temps entre 1 et 24 heures : actualisation toutes les 15 minutes</span><span class="sxs-lookup"><span data-stu-id="66c5e-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="66c5e-135">Intervalle de temps supérieur à 24 heures : (intervalle de temps)/60.</span><span class="sxs-lookup"><span data-stu-id="66c5e-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="66c5e-136">Épinglez n’importe quelle requête dans Analytics</span><span class="sxs-lookup"><span data-stu-id="66c5e-136">Pin any query in Analytics</span></span>
<span data-ttu-id="66c5e-137">Vous pouvez également [épingler Analytique](app-insights-analytics-using.md#pin-to-dashboard) graphiques tooa [partagé](#share-dashboards-with-your-team) tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="66c5e-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="66c5e-138">Cela vous permet de graphiques tooadd de toute requête arbitraire en même temps que les métriques standard hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="66c5e-139">Les résultats sont recalculés automatiquement toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="66c5e-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="66c5e-140">Cliquez sur icône d’actualisation hello sur hello graphique toorecalculate immédiatement.</span><span class="sxs-lookup"><span data-stu-id="66c5e-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="66c5e-141">(L’actualisation du navigateur ne permet pas de lancer un nouveau calcul.)</span><span class="sxs-lookup"><span data-stu-id="66c5e-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="66c5e-142">Ajuster une vignette de tableau de bord hello</span><span class="sxs-lookup"><span data-stu-id="66c5e-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="66c5e-143">Une fois une vignette de tableau de bord hello, vous pouvez la modifier.</span><span class="sxs-lookup"><span data-stu-id="66c5e-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Placez-la sur un graphique dans la commande tooedit.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="66c5e-145">Ajouter une vignette de toohello graphique.</span><span class="sxs-lookup"><span data-stu-id="66c5e-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="66c5e-146">Définir la métrique de hello, dimension group by et le style (table, graphique) d’un graphique.</span><span class="sxs-lookup"><span data-stu-id="66c5e-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="66c5e-147">Faites glisser toozoom de diagramme hello dans ; Cliquez sur hello annulation bouton tooreset hello timespan ; Définissez les propriétés de filtre pour les graphiques hello sur la vignette de hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="66c5e-148">Définissez le titre de la vignette.</span><span class="sxs-lookup"><span data-stu-id="66c5e-148">Set tile title.</span></span>

<span data-ttu-id="66c5e-149">Les vignettes épinglées à partir des panneaux de Metrics Explorer ont davantage d’options d’édition que les vignettes épinglées à partir d’un panneau Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="66c5e-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="66c5e-150">vignette d’origine Hello que vous avez épinglées n’est pas affectée par vos modifications.</span><span class="sxs-lookup"><span data-stu-id="66c5e-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="66c5e-151">Basculement entre les tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="66c5e-151">Switch between dashboards</span></span>
<span data-ttu-id="66c5e-152">Vous pouvez enregistrer plusieurs tableaux de bord et basculer entre ceux-ci.</span><span class="sxs-lookup"><span data-stu-id="66c5e-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="66c5e-153">Quand vous épinglez un graphique ou un panneau, elles sont ajoutées toohello de tableau de bord actuel.</span><span class="sxs-lookup"><span data-stu-id="66c5e-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![tooswitch entre les tableaux de bord, cliquez sur tableau de bord et sélectionnez un tableau de bord enregistré.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="66c5e-157">Par exemple, vous pouvez avoir un tableau de bord pour l’affichage plein écran dans la salle d’équipe hello et l’autre pour le développement général.</span><span class="sxs-lookup"><span data-stu-id="66c5e-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="66c5e-158">Tableau de bord de hello, un panneau s’affiche sous forme de vignette : activez-la toogo toohello panneau.</span><span class="sxs-lookup"><span data-stu-id="66c5e-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="66c5e-159">Un graphique réplique graphique hello dans son emplacement d’origine.</span><span class="sxs-lookup"><span data-stu-id="66c5e-159">A chart replicates hello chart in its original location.</span></span>

![Cliquez sur une lame de hello tooopen vignette qu’elle représente](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="66c5e-161">Partager des tableaux de bord</span><span class="sxs-lookup"><span data-stu-id="66c5e-161">Share dashboards</span></span>
<span data-ttu-id="66c5e-162">Lorsque vous avez créé un tableau de bord, vous pouvez le partager avec d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66c5e-162">When you've created a dashboard, you can share it with other users.</span></span>

![Dans l’en-tête du tableau de bord hello, cliquez sur Partager](./media/app-insights-dashboards/41.png)

<span data-ttu-id="66c5e-164">Apprenez-en davantage sur [les rôles et le contrôle d’accès](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="66c5e-165">Navigation au sein d’une application</span><span class="sxs-lookup"><span data-stu-id="66c5e-165">App navigation</span></span>
<span data-ttu-id="66c5e-166">Panneau de vue d’ensemble de Hello est hello passerelle toomore plus d’informations sur votre application.</span><span class="sxs-lookup"><span data-stu-id="66c5e-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="66c5e-167">**Tout graphique ou la vignette** - cliquez sur n’importe quelle vignette ou un graphique toosee plus en détail ce qu’il affiche.</span><span class="sxs-lookup"><span data-stu-id="66c5e-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="66c5e-168">Boutons du panneau Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="66c5e-168">Overview blade buttons</span></span>
![Barre de navigation supérieure du panneau Vue d’ensemble](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="66c5e-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) : créez vos propres graphiques sur les performances et l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="66c5e-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="66c5e-171">[**Rechercher**](app-insights-diagnostic-search.md) : analysez des instances spécifiques d’événements telles que les demandes, les exceptions ou les suivis de journal.</span><span class="sxs-lookup"><span data-stu-id="66c5e-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="66c5e-172">[**Analytics**](app-insights-analytics.md) : pour des requêtes puissantes sur vos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="66c5e-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="66c5e-173">**Intervalle de temps** -ajuster la plage hello affichée par tous les graphiques hello sur le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="66c5e-174">**Supprimer** -supprimer la ressource d’Application Insights hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="66c5e-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="66c5e-175">Vous devez également supprimer les packages d’Application Insights hello de code de votre application, ou modifier hello [clé d’instrumentation](app-insights-create-new-resource.md#copy-the-instrumentation-key) dans votre application toodirect télémétrie tooa autre Application Insights ressource.</span><span class="sxs-lookup"><span data-stu-id="66c5e-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="66c5e-176">Onglet Bases</span><span class="sxs-lookup"><span data-stu-id="66c5e-176">Essentials tab</span></span>
* <span data-ttu-id="66c5e-177">[Clé d’instrumentation](app-insights-create-new-resource.md#copy-the-instrumentation-key) : identifie la ressource de cette application.</span><span class="sxs-lookup"><span data-stu-id="66c5e-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="66c5e-178">Tarification : mettez les fonctionnalités à disposition et définissez des plafonds de volume.</span><span class="sxs-lookup"><span data-stu-id="66c5e-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="66c5e-179">Barre de navigation au sein d’une application</span><span class="sxs-lookup"><span data-stu-id="66c5e-179">App navigation bar</span></span>
![Barre de navigation gauche](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="66c5e-181">**Vue d’ensemble** -panneau Vue d’ensemble de l’application toohello retour.</span><span class="sxs-lookup"><span data-stu-id="66c5e-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="66c5e-182">**Journal d’activité** : alertes et événements d’administration Azure.</span><span class="sxs-lookup"><span data-stu-id="66c5e-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="66c5e-183">[**Contrôle d’accès** ](app-insights-resources-roles-access-control.md) -fournissent l’accès aux membres de tooteam et d’autres.</span><span class="sxs-lookup"><span data-stu-id="66c5e-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="66c5e-184">[**Balises** ](../azure-resource-manager/resource-group-using-tags.md) -utilisation des balises toogroup votre application avec d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66c5e-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="66c5e-185">EXAMINER</span><span class="sxs-lookup"><span data-stu-id="66c5e-185">INVESTIGATE</span></span>

* <span data-ttu-id="66c5e-186">[**Mappage d’application** ](app-insights-app-map.md) -carte Active affichant les composants de votre application, d’hello dérivé des informations de dépendance hello.</span><span class="sxs-lookup"><span data-stu-id="66c5e-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="66c5e-187">[**Détection intelligente**](app-insights-proactive-diagnostics.md) : consultez les récentes alertes sur les performances.</span><span class="sxs-lookup"><span data-stu-id="66c5e-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="66c5e-188">[**Flux en direct**](app-insights-live-stream.md) pour un ensemble de mesures quasi instantanées, ce qui est utile lors du déploiement d’une nouvelle version ou du débogage.</span><span class="sxs-lookup"><span data-stu-id="66c5e-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="66c5e-189">[**Disponibilité / tests Web** ](app-insights-monitor-web-app-availability.md) -envoyer les requêtes régulières tooyour application web à partir d’autour hello monde.*</span><span class="sxs-lookup"><span data-stu-id="66c5e-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="66c5e-190">[**Les échecs, performances** ](app-insights-web-monitor-performance.md) -Exceptions, les taux d’échec et réponse arrive trop de demandes tooyour application et des requêtes à partir de votre application[dépendances](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="66c5e-191">[**Performances**](app-insights-web-monitor-performance.md) : temps de réponse, temps de réponse de dépendance.</span><span class="sxs-lookup"><span data-stu-id="66c5e-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="66c5e-192">[Serveurs](app-insights-web-monitor-performance.md) : compteurs de performances.</span><span class="sxs-lookup"><span data-stu-id="66c5e-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="66c5e-193">Disponible si vous [installez Status Monitor](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="66c5e-194">**Navigateur** : nombre de pages consultées et performances AJAX.</span><span class="sxs-lookup"><span data-stu-id="66c5e-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="66c5e-195">Disponible si vous [instrumentez vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="66c5e-196">**Utilisation** : nombre de pages consultées, d’utilisateurs et de sessions.</span><span class="sxs-lookup"><span data-stu-id="66c5e-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="66c5e-197">Disponible si vous [instrumentez vos pages web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="66c5e-198">CONFIGURER</span><span class="sxs-lookup"><span data-stu-id="66c5e-198">CONFIGURE</span></span>

* <span data-ttu-id="66c5e-199">**Prise en main** : didacticiel en ligne.</span><span class="sxs-lookup"><span data-stu-id="66c5e-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="66c5e-200">**Propriétés** : clé d’instrumentation, abonnement et ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="66c5e-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="66c5e-201">[Alertes](app-insights-alerts.md) : configuration des alertes de métriques.</span><span class="sxs-lookup"><span data-stu-id="66c5e-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="66c5e-202">[Exportation continue](app-insights-export-telemetry.md) -configurer l’exportation de stockage tooAzure de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="66c5e-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="66c5e-203">[Tests de performances](app-insights-monitor-web-app-availability.md#performance-tests) : configurez une charge synthétique sur votre site web.</span><span class="sxs-lookup"><span data-stu-id="66c5e-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="66c5e-204">[Quota et tarification](app-insights-pricing.md)et [échantillonnage d’ingestion](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="66c5e-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="66c5e-205">**Accès aux API** -créer [annotations de version](app-insights-annotations.md) et pourquoi les API d’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="66c5e-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="66c5e-206">[**Éléments de travail** ](app-insights-diagnostic-search.md#create-work-item) -se connecter travail tooa système de suivi afin que vous pouvez créer des bogues lors de l’examen des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="66c5e-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="66c5e-207">PARAMÈTRES</span><span class="sxs-lookup"><span data-stu-id="66c5e-207">SETTINGS</span></span>

* <span data-ttu-id="66c5e-208">[**Verrous**](../azure-resource-manager/resource-group-lock-resources.md) : verrouillez les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="66c5e-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="66c5e-209">[**Script d’automatisation** ](app-insights-powershell.md) -exporter une définition de ressource Azure de hello afin que vous puissiez l’utiliser comme un modèle toocreate nouvelle des ressources.</span><span class="sxs-lookup"><span data-stu-id="66c5e-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="66c5e-210">Vidéo</span><span class="sxs-lookup"><span data-stu-id="66c5e-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="66c5e-211">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66c5e-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="66c5e-212">Metrics Explorer</span><span class="sxs-lookup"><span data-stu-id="66c5e-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="66c5e-213">Filtrez et segmentez les mesures.</span><span class="sxs-lookup"><span data-stu-id="66c5e-213">Filter and segment metrics</span></span> |![Exemple de recherche](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="66c5e-215">Recherche de diagnostic</span><span class="sxs-lookup"><span data-stu-id="66c5e-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="66c5e-216">Recherchez et examinez des événements, ainsi que les événements associés, et créez des bogues.</span><span class="sxs-lookup"><span data-stu-id="66c5e-216">Find and inspect events, related events, and create bugs</span></span> |![Exemple de recherche](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="66c5e-218">Analytics</span><span class="sxs-lookup"><span data-stu-id="66c5e-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="66c5e-219">Tirez parti d’un puissant langage de requête.</span><span class="sxs-lookup"><span data-stu-id="66c5e-219">Powerful query language</span></span> |![Exemple de recherche](./media/app-insights-dashboards/63.png) |
