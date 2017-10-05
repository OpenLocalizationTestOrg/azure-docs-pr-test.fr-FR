---
title: Utilisation de la recherche dans Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: e2d12f807756b778a64920b12a66fba184a99844
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="c7d08-103">Utilisation de la recherche dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7d08-103">Using Search in Application Insights</span></span>
<span data-ttu-id="c7d08-104">Recherche (Search) est la fonctionnalité [d’Application Insights](app-insights-overview.md) qui vous permet de rechercher et d’explorer les éléments de télémétrie, par exemple des pages vues, des exceptions ou des requêtes web.</span><span class="sxs-lookup"><span data-stu-id="c7d08-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use to find and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="c7d08-105">Vous pouvez également afficher le suivi et les événements de journal que vous avez codés.</span><span class="sxs-lookup"><span data-stu-id="c7d08-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="c7d08-106">(Pour les requêtes plus complexes sur vos données, utilisez [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="c7d08-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="c7d08-107">Où voyez-vous Recherche ?</span><span class="sxs-lookup"><span data-stu-id="c7d08-107">Where do you see Search?</span></span>
### <a name="in-the-azure-portal"></a><span data-ttu-id="c7d08-108">Dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c7d08-108">In the Azure portal</span></span>
<span data-ttu-id="c7d08-109">Vous pouvez ouvrir explicitement la recherche de diagnostics à partir du panneau Vue d’ensemble d’Application Insights de votre application :</span><span class="sxs-lookup"><span data-stu-id="c7d08-109">You can open diagnostic search explicitly from the Application Insights Overview blade of your application:</span></span>

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="c7d08-111">Il s’affiche également lorsque vous parcourez certains graphiques et éléments de la grille.</span><span class="sxs-lookup"><span data-stu-id="c7d08-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="c7d08-112">Dans ce cas, les filtres sont prédéfinis pour vous permettre de vous concentrer sur le type d’élément que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c7d08-112">In this case, its filters are pre-set to focus on the type of item you selected.</span></span> 

<span data-ttu-id="c7d08-113">Par exemple, dans le volet Vue d’ensemble, vous trouverez un graphique à barres de requêtes classées par temps de réponse.</span><span class="sxs-lookup"><span data-stu-id="c7d08-113">For example, on the Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="c7d08-114">Cliquez sur une plage de performances pour afficher la liste des demandes individuelles dans cette plage de temps de réponse :</span><span class="sxs-lookup"><span data-stu-id="c7d08-114">Click through a performance range to see a list of individual requests in that response time range:</span></span>

![Cliquer sur les performances des demandes](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="c7d08-116">La partie principale de Recherche de diagnostic est une liste d’éléments de télémétrie : demandes serveur, pages vues, événements personnalisés que vous avez codés, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="c7d08-116">The main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="c7d08-117">En haut de la liste se trouve un graphique de synthèse indiquant le nombre d’événements au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="c7d08-117">At the top of the list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="c7d08-118">Cliquez sur Actualiser pour obtenir les nouveaux événements.</span><span class="sxs-lookup"><span data-stu-id="c7d08-118">Click Refresh to get new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="c7d08-119">Dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7d08-119">In Visual Studio</span></span>

<span data-ttu-id="c7d08-120">Dans Visual Studio, il existe également une fenêtre de recherche Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c7d08-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="c7d08-121">Elle est particulièrement utile pour l’affichage des événements de télémétrie générés par l’application que vous déboguez.</span><span class="sxs-lookup"><span data-stu-id="c7d08-121">It's most useful for displaying telemetry events generated by the application that you're debugging.</span></span> <span data-ttu-id="c7d08-122">Mais elle peut également afficher les événements collectés à partir de votre application publiée sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c7d08-122">But it can also show the events collected from your published app at the Azure portal.</span></span>

<span data-ttu-id="c7d08-123">Ouvrez la fenêtre de recherche dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="c7d08-123">Open the Search window in Visual Studio:</span></span>

![Recherche Application Insights dans Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="c7d08-125">La fenêtre de recherche comporte les mêmes fonctionnalités que le portail web :</span><span class="sxs-lookup"><span data-stu-id="c7d08-125">The Search window has features similar to the web portal:</span></span>

![Fenêtre de recherche Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="c7d08-127">L’onglet Suivi des opérations est disponible lorsque vous ouvrez une requête ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="c7d08-127">The Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="c7d08-128">Une 'Opération' est une séquence d’événements qui est associée à une demande ou un affichage de page unique.</span><span class="sxs-lookup"><span data-stu-id="c7d08-128">An 'operation' is a sequence of events that is associated with to a single request or page view.</span></span> <span data-ttu-id="c7d08-129">Par exemple, les appels de dépendance, les exceptions, les journaux de suivi et les événements personnalisés peuvent faire partie d’une opération unique.</span><span class="sxs-lookup"><span data-stu-id="c7d08-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="c7d08-130">L’onglet Suivi des opérations représente graphiquement la chronologie et la durée de ces événements par rapport à la demande ou à l’affichage de page.</span><span class="sxs-lookup"><span data-stu-id="c7d08-130">The Track Operation tab shows graphically the timing and duration of these events in relation to the request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="c7d08-131">Inspecter les éléments un par un</span><span class="sxs-lookup"><span data-stu-id="c7d08-131">Inspect individual items</span></span>
<span data-ttu-id="c7d08-132">Sélectionnez un élément de télémétrie pour afficher les champs clés et les éléments associés.</span><span class="sxs-lookup"><span data-stu-id="c7d08-132">Select any telemetry item to see key fields and related items.</span></span> <span data-ttu-id="c7d08-133">Si vous voulez voir l’ensemble des champs, cliquez sur « ... ».</span><span class="sxs-lookup"><span data-stu-id="c7d08-133">If you want to see the full set of fields, click "...".</span></span> 

![Cliquez sur Nouvel élément de travail, modifiez les champs, puis cliquez sur OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="c7d08-135">Filtrer les types d’événement</span><span class="sxs-lookup"><span data-stu-id="c7d08-135">Filter event types</span></span>
<span data-ttu-id="c7d08-136">Ouvrez le panneau Filtre et choisissez les types d’événement que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="c7d08-136">Open the Filter blade and choose the event types you want to see.</span></span> <span data-ttu-id="c7d08-137">(Si vous souhaitez restaurer plus tard les filtres avec lesquels vous avez ouvert le panneau, cliquez sur Réinitialiser).</span><span class="sxs-lookup"><span data-stu-id="c7d08-137">(If, later, you want to restore the filters with which you opened the blade, click Reset.)</span></span>

![Choisissez le filtre et sélectionnez les types de télémétrie](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="c7d08-139">Les types d'événements sont :</span><span class="sxs-lookup"><span data-stu-id="c7d08-139">The event types are:</span></span>

* <span data-ttu-id="c7d08-140">**Suivi** - [Les journaux de diagnostic](app-insights-asp-net-trace-logs.md) comprennent les appels TrackTrace, log4Net, NLog et System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="c7d08-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="c7d08-141">**Demandes** : demandes HTTP reçues par votre serveur d’applications, dont les pages, les scripts, les images, les fichiers de style et les données.</span><span class="sxs-lookup"><span data-stu-id="c7d08-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="c7d08-142">Ces événements sont utilisés pour créer les graphiques de présentation de la demande et la réponse.</span><span class="sxs-lookup"><span data-stu-id="c7d08-142">These events are used to create the request and response overview charts.</span></span>
* <span data-ttu-id="c7d08-143">**Affichage de page** - [Télémétrie envoyée par le client web](app-insights-javascript.md) et utilisée pour créer les rapports d’affichage des pages.</span><span class="sxs-lookup"><span data-stu-id="c7d08-143">**Page View** - [Telemetry sent by the web client](app-insights-javascript.md), used to create page view reports.</span></span> 
* <span data-ttu-id="c7d08-144">**Événement personnalisé** : si vous avez inséré des appels vers TrackEvent() pour [surveiller l’utilisation](app-insights-api-custom-events-metrics.md), vous pouvez les rechercher ici.</span><span class="sxs-lookup"><span data-stu-id="c7d08-144">**Custom Event** - If you inserted calls to TrackEvent() in order to [monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="c7d08-145">**Exception** : [exceptions non interceptées sur le serveur](app-insights-asp-net-exceptions.md) et celles que vous enregistrez avec TrackException().</span><span class="sxs-lookup"><span data-stu-id="c7d08-145">**Exception** - Uncaught [exceptions in the server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="c7d08-146">**Dépendance** - [Appels de votre application de serveur ](app-insights-asp-net-dependencies.md) à d’autres services tels que des API REST ou des bases de données, et appels AJAX à partir de votre [code client](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) to other services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="c7d08-147">**Disponibilité** : résultats des [tests de disponibilité](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="c7d08-148">Filtrer des valeurs de propriétés</span><span class="sxs-lookup"><span data-stu-id="c7d08-148">Filter on property values</span></span>
<span data-ttu-id="c7d08-149">Vous pouvez filtrer les événements en fonction des valeurs de leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="c7d08-149">You can filter events on the values of their properties.</span></span> <span data-ttu-id="c7d08-150">Les propriétés disponibles varient en fonction des types d’événement que vous avez sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="c7d08-150">The available properties depend on the event types you selected.</span></span> 

<span data-ttu-id="c7d08-151">Par exemple, les demandes avec un code de réponse spécifique.</span><span class="sxs-lookup"><span data-stu-id="c7d08-151">For example, pick out requests with a specific response code.</span></span> 

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="c7d08-153">Si vous ne choisissez aucune valeur pour une propriété, cela a le même effet que si vous sélectionniez toutes les valeurs.</span><span class="sxs-lookup"><span data-stu-id="c7d08-153">Choosing no values of a particular property has the same effect as choosing all values.</span></span> <span data-ttu-id="c7d08-154">Cela désactive le filtrage sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="c7d08-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="c7d08-155">Affiner votre recherche</span><span class="sxs-lookup"><span data-stu-id="c7d08-155">Narrow your search</span></span>
<span data-ttu-id="c7d08-156">Notez que les nombres à droite des valeurs de filtre affichent le nombre d’occurrences dans le jeu actuellement filtré.</span><span class="sxs-lookup"><span data-stu-id="c7d08-156">Notice that the counts to the right of the filter values show how many occurrences there are in the current filtered set.</span></span> 

<span data-ttu-id="c7d08-157">Dans cet exemple, il est clair que la demande 'Rpt/Employees' provoque la majorité des erreurs '500' :</span><span class="sxs-lookup"><span data-stu-id="c7d08-157">In this example, it's clear that the 'Rpt/Employees' request results in most of the '500' errors:</span></span>

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-the-same-property"></a><span data-ttu-id="c7d08-159">Rechercher des événements avec la même propriété</span><span class="sxs-lookup"><span data-stu-id="c7d08-159">Find events with the same property</span></span>
<span data-ttu-id="c7d08-160">Recherchez tous les éléments dont la valeur de la propriété est la même :</span><span class="sxs-lookup"><span data-stu-id="c7d08-160">Find all the items with the same property value:</span></span>

![Cliquez avec le bouton droit sur une propriété](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-the-data"></a><span data-ttu-id="c7d08-162">Recherche dans les données</span><span class="sxs-lookup"><span data-stu-id="c7d08-162">Search the data</span></span>

> [!NOTE]
> <span data-ttu-id="c7d08-163">Pour écrire des requêtes plus complexes, ouvrez [**Analytics**](app-insights-analytics-tour.md) à partir du haut du panneau Recherche.</span><span class="sxs-lookup"><span data-stu-id="c7d08-163">To write more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from the top of the Search blade.</span></span>
> 

<span data-ttu-id="c7d08-164">Vous pouvez rechercher des termes dans une des valeurs des propriétés.</span><span class="sxs-lookup"><span data-stu-id="c7d08-164">You can search for terms in any of the property values.</span></span> <span data-ttu-id="c7d08-165">Cela est particulièrement utile si vous avez écrit des [événements personnalisés](app-insights-api-custom-events-metrics.md) avec des valeurs de propriété.</span><span class="sxs-lookup"><span data-stu-id="c7d08-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="c7d08-166">Vous pouvez définir une durée, car les recherches sur les plages courtes sont plus rapides.</span><span class="sxs-lookup"><span data-stu-id="c7d08-166">You might want to set a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="c7d08-168">Recherchez des mots entiers, pas des sous-chaînes.</span><span class="sxs-lookup"><span data-stu-id="c7d08-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="c7d08-169">Utilisez des guillemets pour délimiter les caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="c7d08-169">Use quotation marks to enclose special characters.</span></span>

| <span data-ttu-id="c7d08-170">string</span><span class="sxs-lookup"><span data-stu-id="c7d08-170">string</span></span> | <span data-ttu-id="c7d08-171">n’est *pas* trouvé par</span><span class="sxs-lookup"><span data-stu-id="c7d08-171">is *not* found by</span></span> | <span data-ttu-id="c7d08-172">mais ceux-ci la trouvent</span><span class="sxs-lookup"><span data-stu-id="c7d08-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c7d08-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="c7d08-173">HomeController.About</span></span> |<span data-ttu-id="c7d08-174">home</span><span class="sxs-lookup"><span data-stu-id="c7d08-174">home</span></span><br/><span data-ttu-id="c7d08-175">contrôleur</span><span class="sxs-lookup"><span data-stu-id="c7d08-175">controller</span></span><br/><span data-ttu-id="c7d08-176">out</span><span class="sxs-lookup"><span data-stu-id="c7d08-176">out</span></span> | <span data-ttu-id="c7d08-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="c7d08-177">homecontroller</span></span><br/><span data-ttu-id="c7d08-178">about</span><span class="sxs-lookup"><span data-stu-id="c7d08-178">about</span></span><br/><span data-ttu-id="c7d08-179">« homecontroller.about »</span><span class="sxs-lookup"><span data-stu-id="c7d08-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="c7d08-180">États-Unis</span><span class="sxs-lookup"><span data-stu-id="c7d08-180">United States</span></span>|<span data-ttu-id="c7d08-181">Uni</span><span class="sxs-lookup"><span data-stu-id="c7d08-181">Uni</span></span><br/><span data-ttu-id="c7d08-182">ted</span><span class="sxs-lookup"><span data-stu-id="c7d08-182">ted</span></span>|<span data-ttu-id="c7d08-183">états</span><span class="sxs-lookup"><span data-stu-id="c7d08-183">united</span></span><br/><span data-ttu-id="c7d08-184">unis</span><span class="sxs-lookup"><span data-stu-id="c7d08-184">states</span></span><br/><span data-ttu-id="c7d08-185">états ET unis</span><span class="sxs-lookup"><span data-stu-id="c7d08-185">united AND states</span></span><br/><span data-ttu-id="c7d08-186">« états-unis »</span><span class="sxs-lookup"><span data-stu-id="c7d08-186">"united states"</span></span>

<span data-ttu-id="c7d08-187">Expressions de recherche utilisables :</span><span class="sxs-lookup"><span data-stu-id="c7d08-187">Here are the search expressions you can use:</span></span>

| <span data-ttu-id="c7d08-188">Exemple de requête</span><span class="sxs-lookup"><span data-stu-id="c7d08-188">Sample query</span></span> | <span data-ttu-id="c7d08-189">Résultat</span><span class="sxs-lookup"><span data-stu-id="c7d08-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="c7d08-190">Trouve tous les événements dont la période comprend le mot « apple »</span><span class="sxs-lookup"><span data-stu-id="c7d08-190">Find all events in the time range whose fields include the word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="c7d08-191">Trouve les événements qui contiennent les deux mots.</span><span class="sxs-lookup"><span data-stu-id="c7d08-191">Find events that contain both words.</span></span> <span data-ttu-id="c7d08-192">Utilisez « AND » en lettres majuscules (et non « and » en lettres minuscules).</span><span class="sxs-lookup"><span data-stu-id="c7d08-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="c7d08-193">Trouve les événements qui contiennent un des deux mots.</span><span class="sxs-lookup"><span data-stu-id="c7d08-193">Find events that contain either word.</span></span> <span data-ttu-id="c7d08-194">Utilisez « OR » en lettres capitales (et non « or » en lettres minuscules).</span><span class="sxs-lookup"><span data-stu-id="c7d08-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="c7d08-195">Forme abrégée.</span><span class="sxs-lookup"><span data-stu-id="c7d08-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="c7d08-196">Trouve les événements qui contiennent un mot, mais pas l’autre.</span><span class="sxs-lookup"><span data-stu-id="c7d08-196">Find events that contain one word but not the other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="c7d08-197">échantillonnage</span><span class="sxs-lookup"><span data-stu-id="c7d08-197">Sampling</span></span>
<span data-ttu-id="c7d08-198">Si votre application génère un volume important de télémétrie (et si vous utilisez le Kit SDK ASP.NET version 2.0.0-beta3 ou ultérieure), le module d'échantillonnage adaptatif réduit automatiquement le volume qui est envoyé vers le portail en envoyant uniquement une fraction représentative des événements.</span><span class="sxs-lookup"><span data-stu-id="c7d08-198">If your app generates a lot of telemetry (and you are using the ASP.NET SDK version 2.0.0-beta3 or later), the adaptive sampling module automatically reduces the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="c7d08-199">Cependant, les événements liés à la même demande sont activés ou désactivés en tant que groupe, afin que vous puissiez naviguer entre les événements connexes.</span><span class="sxs-lookup"><span data-stu-id="c7d08-199">However, events that are related to the same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="c7d08-200">[En savoir plus sur l'échantillonnage](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="c7d08-201">Création d’un élément de travail</span><span class="sxs-lookup"><span data-stu-id="c7d08-201">Create work item</span></span>
<span data-ttu-id="c7d08-202">Vous pouvez créer un bogue dans GitHub ou Visual Studio Team Services avec les détails d’un élément de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="c7d08-202">You can create a bug in GitHub or Visual Studio Team Services with the details from any telemetry item.</span></span> 

![Cliquez sur Nouvel élément de travail, modifiez les champs, puis cliquez sur OK.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="c7d08-204">La première fois que vous procédez ainsi, vous êtes invité à configurer un lien vers votre compte et votre projet Team Services.</span><span class="sxs-lookup"><span data-stu-id="c7d08-204">The first time you do this, you are asked to configure a link to your Team Services account and project.</span></span>

![Indiquez l’URL de votre serveur Team Services et le nom du projet, puis cliquez sur Autoriser](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="c7d08-206">(Vous pouvez également configurer le lien dans le panneau des éléments de travail).</span><span class="sxs-lookup"><span data-stu-id="c7d08-206">(You can also configure the link on the Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="c7d08-207">Enregistrer votre recherche</span><span class="sxs-lookup"><span data-stu-id="c7d08-207">Save your search</span></span>
<span data-ttu-id="c7d08-208">Une fois que vous avez défini tous les filtres que vous voulez, vous pouvez enregistrer la recherche dans vos recherches favorites.</span><span class="sxs-lookup"><span data-stu-id="c7d08-208">When you've set all the filters you want, you can save the search as a favorite.</span></span> <span data-ttu-id="c7d08-209">Si vous travaillez avec un compte professionnel, vous pouvez choisir de la partager avec d’autres membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="c7d08-209">If you work in an organizational account, you can choose whether to share it with other team members.</span></span>

![Cliquez sur Favori, définissez le nom et cliquez sur Enregistrer](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="c7d08-211">Pour réafficher la recherche, **allez dans le panneau Vue d’ensemble** et ouvrez Favoris :</span><span class="sxs-lookup"><span data-stu-id="c7d08-211">To see the search again, **go to the overview blade** and open Favorites:</span></span>

![Vignette des favoris](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="c7d08-213">Si vous avez enregistré une période relative, le panneau rouvert comporte les données les plus récentes.</span><span class="sxs-lookup"><span data-stu-id="c7d08-213">If you saved with Relative time range, the re-opened blade has the latest data.</span></span> <span data-ttu-id="c7d08-214">Si vous avez enregistré une période absolue, vous voyez les mêmes données à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="c7d08-214">If you saved with Absolute time range, you see the same data every time.</span></span> <span data-ttu-id="c7d08-215">(si 'Relatif' n’est pas disponible lorsque vous souhaitez enregistrer un favori, cliquez sur Intervalle de temps dans l’en-tête et définissez un intervalle de temps qui n’est pas un intervalle personnalisé).</span><span class="sxs-lookup"><span data-stu-id="c7d08-215">(If 'Relative' isn't available when you want to save a favorite, click Time Range in the header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-to-application-insights"></a><span data-ttu-id="c7d08-216">Envoyer plus de télémétrie à Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7d08-216">Send more telemetry to Application Insights</span></span>
<span data-ttu-id="c7d08-217">En plus de la télémétrie fournie par le Kit de développement logiciel (SDK) Application Insights, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="c7d08-217">In addition to the out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="c7d08-218">Capturer le suivi du journal dans votre infrastructure de journalisation favorite dans [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="c7d08-219">Cela signifie que vous pouvez effectuer des recherches dans le suivi du journal et les mettre en corrélation avec les pages vues, les exceptions et autres événements.</span><span class="sxs-lookup"><span data-stu-id="c7d08-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="c7d08-220">[Écrire du code](app-insights-api-custom-events-metrics.md) pour envoyer des événements personnalisés, des affichages de page et des exceptions.</span><span class="sxs-lookup"><span data-stu-id="c7d08-220">[Write code](app-insights-api-custom-events-metrics.md) to send custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="c7d08-221">[Découvrez comment envoyer les journaux et la télémétrie personnalisée à Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-221">[Learn how to send logs and custom telemetry to Application Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="c7d08-222"><a name="questions"></a>Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="c7d08-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="c7d08-223"><a name="limits"></a>Quelle est la quantité de données conservée ?</span><span class="sxs-lookup"><span data-stu-id="c7d08-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="c7d08-224">Voir la section [Synthèse des limites](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="c7d08-224">See the [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="c7d08-225">Comment puis-je consulter les données POST dans mes demandes serveur ?</span><span class="sxs-lookup"><span data-stu-id="c7d08-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="c7d08-226">Nous n’enregistrons pas automatiquement les données POST, mais vous pouvez utiliser [TrackTrace ou le journal des appels](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="c7d08-226">We don't log the POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="c7d08-227">Placez les données POST dans le paramètre de message.</span><span class="sxs-lookup"><span data-stu-id="c7d08-227">Put the POST data in the message parameter.</span></span> <span data-ttu-id="c7d08-228">Vous ne pouvez pas filtrer les messages comme vous le feriez pour les propriétés, mais la limite de taille est plus importante.</span><span class="sxs-lookup"><span data-stu-id="c7d08-228">You can't filter on the message in the same way you can filter on properties, but the size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="c7d08-229">Vidéo</span><span class="sxs-lookup"><span data-stu-id="c7d08-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="c7d08-230"><a name="add"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c7d08-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="c7d08-231">Écrire des requêtes complexes dans Analytics</span><span class="sxs-lookup"><span data-stu-id="c7d08-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="c7d08-232">Envoi des journaux et de la télémétrie personnalisée à Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7d08-232">Send logs and custom telemetry to Application Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="c7d08-233">Configuration des tests de disponibilité et de réactivité</span><span class="sxs-lookup"><span data-stu-id="c7d08-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="c7d08-234">Dépannage</span><span class="sxs-lookup"><span data-stu-id="c7d08-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
