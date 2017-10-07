---
title: aaaUsing recherche dans Azure Application Insights | Documents Microsoft
description: "Recherchez et filtrez la télémétrie brute envoyée par votre application web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="87e6f-103">Utilisation de la recherche dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="87e6f-103">Using Search in Application Insights</span></span>
<span data-ttu-id="87e6f-104">La recherche est une fonctionnalité de [Application Insights](app-insights-overview.md) que vous utilisez toofind et Explorer des éléments de télémétrie individuels, tels que les vues de page, des exceptions ou requêtes web.</span><span class="sxs-lookup"><span data-stu-id="87e6f-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="87e6f-105">Vous pouvez également afficher le suivi et les événements de journal que vous avez codés.</span><span class="sxs-lookup"><span data-stu-id="87e6f-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="87e6f-106">(Pour les requêtes plus complexes sur vos données, utilisez [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="87e6f-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="87e6f-107">Où voyez-vous Recherche ?</span><span class="sxs-lookup"><span data-stu-id="87e6f-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="87e6f-108">Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="87e6f-108">In hello Azure portal</span></span>
<span data-ttu-id="87e6f-109">Vous pouvez ouvrir la recherche de diagnostic explicitement à partir du Panneau de vue d’ensemble de Application Insights hello de votre application :</span><span class="sxs-lookup"><span data-stu-id="87e6f-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="87e6f-111">Il s’affiche également lorsque vous parcourez certains graphiques et éléments de la grille.</span><span class="sxs-lookup"><span data-stu-id="87e6f-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="87e6f-112">Dans ce cas, les filtres sont prédéfinis toofocus sur le type hello de l’élément sélectionné.</span><span class="sxs-lookup"><span data-stu-id="87e6f-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="87e6f-113">Par exemple, dans Panneau de vue d’ensemble de hello, est un graphique à barres des demandes classés par temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="87e6f-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="87e6f-114">Cliquez sur via un toosee de plage de performances une liste des requêtes individuelles dans cette plage de temps de réponse :</span><span class="sxs-lookup"><span data-stu-id="87e6f-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Cliquer sur les performances des demandes](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="87e6f-116">corps de Hello de Diagnostic de recherche est une liste d’éléments de télémétrie - demandes de serveur, de page vues, les événements personnalisés que vous avez codé et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="87e6f-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="87e6f-117">En haut de la liste de hello hello est un graphique de synthèse indiquant le nombre d’événements au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="87e6f-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="87e6f-118">Cliquez sur Actualiser tooget nouveaux événements.</span><span class="sxs-lookup"><span data-stu-id="87e6f-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="87e6f-119">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="87e6f-119">In Visual Studio</span></span>

<span data-ttu-id="87e6f-120">Dans Visual Studio, il existe également une fenêtre de recherche Application Insights.</span><span class="sxs-lookup"><span data-stu-id="87e6f-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="87e6f-121">Il est très utile pour l’affichage des événements de télémétrie générés par l’application hello que vous déboguez.</span><span class="sxs-lookup"><span data-stu-id="87e6f-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="87e6f-122">Mais il peut également afficher les événements hello collectés à partir de votre application publiée à hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="87e6f-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="87e6f-123">Ouvrez la fenêtre de recherche hello dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="87e6f-123">Open hello Search window in Visual Studio:</span></span>

![Recherche Application Insights dans Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="87e6f-125">fenêtre de recherche Hello possède un portail web toohello similaire de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="87e6f-125">hello Search window has features similar toohello web portal:</span></span>

![Fenêtre de recherche Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="87e6f-127">onglet d’opération de suivi Hello est disponible lorsque vous ouvrez une requête ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="87e6f-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="87e6f-128">Une « opération » est une séquence d’événements qui est associée à tooa une seule vue de demande ou de la page.</span><span class="sxs-lookup"><span data-stu-id="87e6f-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="87e6f-129">Par exemple, les appels de dépendance, les exceptions, les journaux de suivi et les événements personnalisés peuvent faire partie d’une opération unique.</span><span class="sxs-lookup"><span data-stu-id="87e6f-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="87e6f-130">onglet de l’opération de suivi Hello affiche hello graphiquement échéance et la durée de ces événements dans l’affichage de demande ou de la page de toohello de relation.</span><span class="sxs-lookup"><span data-stu-id="87e6f-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="87e6f-131">Inspecter les éléments un par un</span><span class="sxs-lookup"><span data-stu-id="87e6f-131">Inspect individual items</span></span>
<span data-ttu-id="87e6f-132">Sélectionnez les champs clés toosee d’élément de données de télémétrie et les éléments associés.</span><span class="sxs-lookup"><span data-stu-id="87e6f-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="87e6f-133">Si vous souhaitez toosee hello ensemble de champs, cliquez sur «... ».</span><span class="sxs-lookup"><span data-stu-id="87e6f-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Cliquez sur le nouvel élément de travail, modifier des champs de hello, puis cliquez sur OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="87e6f-135">Filtrer les types d’événement</span><span class="sxs-lookup"><span data-stu-id="87e6f-135">Filter event types</span></span>
<span data-ttu-id="87e6f-136">Ouvrez le panneau de filtre hello et sélectionner les types d’événements de hello vous souhaitez toosee.</span><span class="sxs-lookup"><span data-stu-id="87e6f-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="87e6f-137">(Si, ultérieurement, vous souhaitez que les filtres de hello toorestore avec lequel vous avez ouvert le panneau de hello, cliquez sur Réinitialiser).</span><span class="sxs-lookup"><span data-stu-id="87e6f-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Choisissez le filtre et sélectionnez les types de télémétrie](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="87e6f-139">types d’événements Hello sont :</span><span class="sxs-lookup"><span data-stu-id="87e6f-139">hello event types are:</span></span>

* <span data-ttu-id="87e6f-140">**Suivi** - [Les journaux de diagnostic](app-insights-asp-net-trace-logs.md) comprennent les appels TrackTrace, log4Net, NLog et System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="87e6f-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="87e6f-141">**Demandes** : demandes HTTP reçues par votre serveur d’applications, dont les pages, les scripts, les images, les fichiers de style et les données.</span><span class="sxs-lookup"><span data-stu-id="87e6f-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="87e6f-142">Ces événements sont utilisés toocreate hello demande et réponse vue d’ensemble des graphiques.</span><span class="sxs-lookup"><span data-stu-id="87e6f-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="87e6f-143">**Affichage de page** - [télémétrie envoyé par le client web de hello](app-insights-javascript.md), utilisé toocreate page Afficher les rapports.</span><span class="sxs-lookup"><span data-stu-id="87e6f-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="87e6f-144">**Événement personnalisé** : Si vous avez inséré trop d’appels tooTrackEvent() dans l’ordre[surveiller l’utilisation de](app-insights-api-custom-events-metrics.md), vous pouvez les rechercher ici.</span><span class="sxs-lookup"><span data-stu-id="87e6f-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="87e6f-145">**Exception** - non interceptée [exceptions dans le serveur de hello](app-insights-asp-net-exceptions.md)et celles que vous vous connectez à l’aide de TrackException().</span><span class="sxs-lookup"><span data-stu-id="87e6f-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="87e6f-146">**Dépendance** - [appels à partir de votre application serveur](app-insights-asp-net-dependencies.md) tooother services tels que les API REST ou des bases de données et des appels AJAX à partir de votre [code client](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="87e6f-147">**Disponibilité** : résultats des [tests de disponibilité](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="87e6f-148">Filtrer des valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="87e6f-148">Filter on property values</span></span>
<span data-ttu-id="87e6f-149">Vous pouvez filtrer les événements sur les valeurs hello de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="87e6f-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="87e6f-150">les propriétés disponibles Hello dépendent des types d’événements hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="87e6f-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="87e6f-151">Par exemple, les demandes avec un code de réponse spécifique.</span><span class="sxs-lookup"><span data-stu-id="87e6f-151">For example, pick out requests with a specific response code.</span></span> 

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="87e6f-153">Le choix d’aucune valeur d’une propriété particulière a hello même effet que le choix de toutes les valeurs.</span><span class="sxs-lookup"><span data-stu-id="87e6f-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="87e6f-154">Cela désactive le filtrage sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="87e6f-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="87e6f-155">Affiner votre recherche</span><span class="sxs-lookup"><span data-stu-id="87e6f-155">Narrow your search</span></span>
<span data-ttu-id="87e6f-156">Notez que hello compte toohello à droite des valeurs de filtre de hello indiquer le nombre d’occurrences il dans ensemble filtré de hello en cours.</span><span class="sxs-lookup"><span data-stu-id="87e6f-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="87e6f-157">Dans cet exemple, il est clair que demande ' Rpt/Employees' hello des résultats dans la plupart des erreurs de hello '500' :</span><span class="sxs-lookup"><span data-stu-id="87e6f-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="87e6f-159">Rechercher des événements par hello même propriété</span><span class="sxs-lookup"><span data-stu-id="87e6f-159">Find events with hello same property</span></span>
<span data-ttu-id="87e6f-160">Rechercher tous les hello les éléments hello même valeur de propriété :</span><span class="sxs-lookup"><span data-stu-id="87e6f-160">Find all hello items with hello same property value:</span></span>

![Cliquez avec le bouton droit sur une propriété](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="87e6f-162">Rechercher les données hello</span><span class="sxs-lookup"><span data-stu-id="87e6f-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="87e6f-163">toowrite des requêtes plus complexes, ouvrez [ **Analytique** ](app-insights-analytics-tour.md) de haut hello du Panneau de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="87e6f-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="87e6f-164">Vous pouvez rechercher des termes du contrat d’une des valeurs de propriété hello.</span><span class="sxs-lookup"><span data-stu-id="87e6f-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="87e6f-165">Cela est particulièrement utile si vous avez écrit des [événements personnalisés](app-insights-api-custom-events-metrics.md) avec des valeurs de propriété.</span><span class="sxs-lookup"><span data-stu-id="87e6f-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="87e6f-166">Vous souhaiterez peut-être tooset une plage de temps que les recherches sur une plage plus courte sont plus rapides.</span><span class="sxs-lookup"><span data-stu-id="87e6f-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="87e6f-168">Recherchez des mots entiers, pas des sous-chaînes.</span><span class="sxs-lookup"><span data-stu-id="87e6f-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="87e6f-169">Utilisez des guillemets tooenclose des caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="87e6f-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="87e6f-170">string</span><span class="sxs-lookup"><span data-stu-id="87e6f-170">string</span></span> | <span data-ttu-id="87e6f-171">n’est *pas* trouvé par</span><span class="sxs-lookup"><span data-stu-id="87e6f-171">is *not* found by</span></span> | <span data-ttu-id="87e6f-172">mais ceux-ci la trouvent</span><span class="sxs-lookup"><span data-stu-id="87e6f-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87e6f-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="87e6f-173">HomeController.About</span></span> |<span data-ttu-id="87e6f-174">home</span><span class="sxs-lookup"><span data-stu-id="87e6f-174">home</span></span><br/><span data-ttu-id="87e6f-175">contrôleur</span><span class="sxs-lookup"><span data-stu-id="87e6f-175">controller</span></span><br/><span data-ttu-id="87e6f-176">out</span><span class="sxs-lookup"><span data-stu-id="87e6f-176">out</span></span> | <span data-ttu-id="87e6f-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="87e6f-177">homecontroller</span></span><br/><span data-ttu-id="87e6f-178">about</span><span class="sxs-lookup"><span data-stu-id="87e6f-178">about</span></span><br/><span data-ttu-id="87e6f-179">« homecontroller.about »</span><span class="sxs-lookup"><span data-stu-id="87e6f-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="87e6f-180">États-Unis</span><span class="sxs-lookup"><span data-stu-id="87e6f-180">United States</span></span>|<span data-ttu-id="87e6f-181">Uni</span><span class="sxs-lookup"><span data-stu-id="87e6f-181">Uni</span></span><br/><span data-ttu-id="87e6f-182">ted</span><span class="sxs-lookup"><span data-stu-id="87e6f-182">ted</span></span>|<span data-ttu-id="87e6f-183">états</span><span class="sxs-lookup"><span data-stu-id="87e6f-183">united</span></span><br/><span data-ttu-id="87e6f-184">unis</span><span class="sxs-lookup"><span data-stu-id="87e6f-184">states</span></span><br/><span data-ttu-id="87e6f-185">états ET unis</span><span class="sxs-lookup"><span data-stu-id="87e6f-185">united AND states</span></span><br/><span data-ttu-id="87e6f-186">« états-unis »</span><span class="sxs-lookup"><span data-stu-id="87e6f-186">"united states"</span></span>

<span data-ttu-id="87e6f-187">Vous pouvez utiliser des expressions de recherche hello sont :</span><span class="sxs-lookup"><span data-stu-id="87e6f-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="87e6f-188">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="87e6f-188">Sample query</span></span> | <span data-ttu-id="87e6f-189">Résultat</span><span class="sxs-lookup"><span data-stu-id="87e6f-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="87e6f-190">Rechercher tous les événements dans la plage de temps hello dont les champs incluent le mot hello « apple »</span><span class="sxs-lookup"><span data-stu-id="87e6f-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="87e6f-191">Trouve les événements qui contiennent les deux mots.</span><span class="sxs-lookup"><span data-stu-id="87e6f-191">Find events that contain both words.</span></span> <span data-ttu-id="87e6f-192">Utilisez « AND » en lettres majuscules (et non « and » en lettres minuscules).</span><span class="sxs-lookup"><span data-stu-id="87e6f-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="87e6f-193">Trouve les événements qui contiennent un des deux mots.</span><span class="sxs-lookup"><span data-stu-id="87e6f-193">Find events that contain either word.</span></span> <span data-ttu-id="87e6f-194">Utilisez « OR » en lettres capitales (et non « or » en lettres minuscules).</span><span class="sxs-lookup"><span data-stu-id="87e6f-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="87e6f-195">Forme abrégée.</span><span class="sxs-lookup"><span data-stu-id="87e6f-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="87e6f-196">Rechercher des événements qui contiennent un mot, mais pas hello autres.</span><span class="sxs-lookup"><span data-stu-id="87e6f-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="87e6f-197">échantillonnage</span><span class="sxs-lookup"><span data-stu-id="87e6f-197">Sampling</span></span>
<span data-ttu-id="87e6f-198">Si votre application génère un grand nombre de télémétrie (et que vous utilisez hello ASP.NET SDK version 2.0.0-beta3 ou version ultérieure), module d’échantillonnage adaptive hello réduit automatiquement le volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements.</span><span class="sxs-lookup"><span data-stu-id="87e6f-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="87e6f-199">Toutefois, les événements qui sont associée toohello même demande sont sélectionnées ou désélectionnées en tant que groupe, afin que vous pouvez naviguer entre les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="87e6f-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="87e6f-200">[En savoir plus sur l'échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="87e6f-201">Création d’un élément de travail</span><span class="sxs-lookup"><span data-stu-id="87e6f-201">Create work item</span></span>
<span data-ttu-id="87e6f-202">Vous pouvez créer un bogue dans GitHub ou Visual Studio Team Services avec les détails de hello à partir de n’importe quel élément de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="87e6f-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Cliquez sur le nouvel élément de travail, modifier des champs de hello, puis cliquez sur OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="87e6f-204">Bonjour première fois que vous procédez ainsi, vous êtes invité à tooconfigure un tooyour lien Team Services compte et de projet.</span><span class="sxs-lookup"><span data-stu-id="87e6f-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Remplir les URL hello de votre serveur Team Services et le nom du projet hello et cliquez sur Autoriser](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="87e6f-206">(Vous pouvez également configurer hello lien sur le panneau d’éléments de travail hello).</span><span class="sxs-lookup"><span data-stu-id="87e6f-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="87e6f-207">Enregistrer votre recherche</span><span class="sxs-lookup"><span data-stu-id="87e6f-207">Save your search</span></span>
<span data-ttu-id="87e6f-208">Lorsque vous avez défini tous les filtres hello que vous le souhaitez, vous pouvez enregistrer hello recherche en tant que favori.</span><span class="sxs-lookup"><span data-stu-id="87e6f-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="87e6f-209">Si vous travaillez dans un compte de société, vous pouvez choisir si tooshare avec d’autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="87e6f-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Favori, hello nom du jeu, puis cliquez sur Enregistrer](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="87e6f-211">recherche de hello toosee, **Panneau de vue d’ensemble toohello accédez** et ouvrir Favoris :</span><span class="sxs-lookup"><span data-stu-id="87e6f-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Vignette des favoris](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="87e6f-213">Si vous avez enregistré avec l’intervalle de temps relatif, panneau de rouvrir hello possède les données les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="87e6f-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="87e6f-214">Si vous avez enregistré avec l’intervalle de temps absolu, vous voyez hello mêmes données chaque fois.</span><span class="sxs-lookup"><span data-stu-id="87e6f-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="87e6f-215">(Si 'Relative' n’est pas disponible lorsque vous souhaitez toosave favoris, cliquez sur la plage de temps dans l’en-tête de hello et définir une plage de temps qui n’est pas une plage personnalisée).</span><span class="sxs-lookup"><span data-stu-id="87e6f-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="87e6f-216">Envoyer la télémétrie plus tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="87e6f-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="87e6f-217">En outre toohello out of box données de télémétrie envoyée par l’Application Insights SDK, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="87e6f-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="87e6f-218">Capturer le suivi du journal dans votre infrastructure de journalisation favorite dans [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="87e6f-219">Cela signifie que vous pouvez effectuer des recherches dans le suivi du journal et les mettre en corrélation avec les pages vues, les exceptions et autres événements.</span><span class="sxs-lookup"><span data-stu-id="87e6f-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="87e6f-220">[Écrire du code](app-insights-api-custom-events-metrics.md) toosend événements personnalisés, des vues de page et des exceptions.</span><span class="sxs-lookup"><span data-stu-id="87e6f-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="87e6f-221">[Découvrez comment toosend se connecte et télémétrie personnalisée tooApplication Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="87e6f-222"><a name="questions"></a>Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="87e6f-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="87e6f-223"><a name="limits"></a>Quelle est la quantité de données conservée ?</span><span class="sxs-lookup"><span data-stu-id="87e6f-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="87e6f-224">Consultez hello [résumé des limites](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="87e6f-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="87e6f-225">Comment puis-je consulter les données POST dans mes demandes serveur ?</span><span class="sxs-lookup"><span data-stu-id="87e6f-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="87e6f-226">Nous n’enregistre pas automatiquement les données de publication hello, mais vous pouvez utiliser [TrackTrace ou journal des appels](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="87e6f-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="87e6f-227">Placez les données de publication hello dans le paramètre de message hello.</span><span class="sxs-lookup"><span data-stu-id="87e6f-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="87e6f-228">Vous ne pouvez pas filtrer sur le message de type hello Bonjour même façon, vous pouvez filtrer sur les propriétés, mais limite de taille hello est plus long.</span><span class="sxs-lookup"><span data-stu-id="87e6f-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="87e6f-229">Vidéo</span><span class="sxs-lookup"><span data-stu-id="87e6f-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="87e6f-230"><a name="add"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87e6f-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="87e6f-231">Écrire des requêtes complexes dans Analytics</span><span class="sxs-lookup"><span data-stu-id="87e6f-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="87e6f-232">Envoyer les journaux et les données de télémétrie personnalisées tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="87e6f-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="87e6f-233">Configuration des tests de disponibilité et de réactivité</span><span class="sxs-lookup"><span data-stu-id="87e6f-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="87e6f-234">Dépannage</span><span class="sxs-lookup"><span data-stu-id="87e6f-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
