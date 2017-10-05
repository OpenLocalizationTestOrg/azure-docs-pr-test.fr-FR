---
title: "Débogage d’applications à l’aide d’Azure Application Insights dans Visual Studio | Microsoft Docs"
description: "Analyse des performances d’application web et diagnostics en phase de débogage et de production."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: e0ac2bf01992520cdbea22a232dc42d678d77c7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="9c98d-103">Débogage d’applications à l’aide d’Azure Application Insights dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9c98d-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="9c98d-104">Visual Studio 2015 (et versions ultérieures) vous permet d’analyser les performances et de diagnostiquer les problèmes au niveau de votre application web ASP.NET aussi bien en phase de débogage qu’en production, à l’aide des données de télémétrie [d’Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c98d-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="9c98d-105">Si vous avez créé votre application web ASP.NET à l’aide de Visual Studio 2017 ou version ultérieure, celle-ci possède déjà le kit de développement logiciel (SDK) Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9c98d-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has the Application Insights SDK.</span></span> <span data-ttu-id="9c98d-106">Sinon, si vous ne l’avez pas encore fait, [ajoutez Application Insights à votre application](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9c98d-106">Otherwise, if you haven't done so already, [add Application Insights to your app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="9c98d-107">Pour analyser votre application lorsqu’elle se trouve dans un environnement de production actif, vous affichez normalement les données de télémétrie Application Insights dans le [portail Azure](https://portal.azure.com), où vous pouvez définir des alertes et utiliser des outils d’analyse puissants.</span><span class="sxs-lookup"><span data-stu-id="9c98d-107">To monitor your app when it's in live production, you normally view the Application Insights telemetry in the [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="9c98d-108">Mais pour le débogage, vous pouvez également rechercher et analyser les données de télémétrie dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c98d-108">But for debugging, you can also search and analyze the telemetry in Visual Studio.</span></span> <span data-ttu-id="9c98d-109">Vous pouvez utiliser Visual Studio pour analyser les données de télémétrie à la fois à partir de votre site de production et de votre environnement de débogage sur votre machine de développement.</span><span class="sxs-lookup"><span data-stu-id="9c98d-109">You can use Visual Studio to analyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="9c98d-110">Dans ce cas, vous pouvez analyser les opérations de débogage même si vous n’avez pas encore configuré le kit de développement logiciel pour que les données de télémétrie soient envoyées au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9c98d-110">In the latter case, you can analyze debugging runs even if you haven't yet configured the SDK to send telemetry to the Azure portal.</span></span> 

## <span data-ttu-id="9c98d-111"><a name="run"></a> Débogage de votre projet</span><span class="sxs-lookup"><span data-stu-id="9c98d-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="9c98d-112">Exécutez votre application web en mode de débogage local à l’aide de la touche F5.</span><span class="sxs-lookup"><span data-stu-id="9c98d-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="9c98d-113">Ouvrez différentes pages pour générer des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9c98d-113">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="9c98d-114">Dans Visual Studio, vous voyez un décompte des événements qui ont été consignés par le module Application Insights dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="9c98d-114">In Visual Studio, you see a count of the events that have been logged by the Application Insights module in your project.</span></span>

![Dans Visual Studio, le bouton Application Insights apparaît pendant le débogage.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="9c98d-116">Cliquez sur ce bouton pour rechercher vos données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9c98d-116">Click this button to search your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="9c98d-117">Recherche Application Insights</span><span class="sxs-lookup"><span data-stu-id="9c98d-117">Application Insights search</span></span>
<span data-ttu-id="9c98d-118">La fenêtre de recherche Application Insights affiche les événements qui ont été consignés.</span><span class="sxs-lookup"><span data-stu-id="9c98d-118">The Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="9c98d-119">(Si vous étiez connecté à Azure au moment de l’installation d’Application Insights, vous pouvez rechercher ces mêmes événements sur le portail Azure.)</span><span class="sxs-lookup"><span data-stu-id="9c98d-119">(If you signed in to Azure when you set up Application Insights, you can search the same events in the Azure portal.)</span></span>

![Cliquez avec le bouton droit sur le projet et sélectionnez Application Insights, Rechercher.](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="9c98d-121">Une fois que vous avez sélectionné ou désélectionné les filtres, cliquez sur le bouton Rechercher en regard du champ de recherche de texte.</span><span class="sxs-lookup"><span data-stu-id="9c98d-121">After you select or deselect filters, click the Search button at the end of the text search field.</span></span>
>

<span data-ttu-id="9c98d-122">La recherche en texte libre fonctionne sur tous les champs des événements.</span><span class="sxs-lookup"><span data-stu-id="9c98d-122">The free text search works on any fields in the events.</span></span> <span data-ttu-id="9c98d-123">Par exemple, vous pouvez effectuer une recherche sur une partie de l’URL d’une page, sur la valeur d’une propriété telle que la ville du client, ou encore sur des termes spécifiques contenus dans un journal de suivi.</span><span class="sxs-lookup"><span data-stu-id="9c98d-123">For example, search for part of the URL of a page; or the value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="9c98d-124">Cliquez sur n’importe quel événement pour afficher le détail de ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="9c98d-124">Click any event to see its detailed properties.</span></span>

<span data-ttu-id="9c98d-125">Pour afficher les requêtes envoyées à votre application web, vous pouvez parcourir le code.</span><span class="sxs-lookup"><span data-stu-id="9c98d-125">For requests to your web app, you can click through to the code.</span></span>

![Sous Request Details (Détails des requêtes), parcourez le code](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="9c98d-127">Vous pouvez également ouvrir l’onglet Éléments connexes pour analyser les requêtes ayant échoué ou les exceptions.</span><span class="sxs-lookup"><span data-stu-id="9c98d-127">You can also open related items to help diagnose failed requests or exceptions.</span></span>

![Sous Request Details (Détails des requêtes), accédez à Éléments connexes](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="9c98d-129">Afficher les exceptions et les requêtes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="9c98d-129">View exceptions and failed requests</span></span>
<span data-ttu-id="9c98d-130">Les rapports d’exceptions s’affichent dans la fenêtre de recherche.</span><span class="sxs-lookup"><span data-stu-id="9c98d-130">Exception reports show in the Search window.</span></span> <span data-ttu-id="9c98d-131">(Pour certains anciens types d’application ASP.NET, vous devez [configurer l’analyse des exceptions](app-insights-asp-net-exceptions.md) pour afficher les exceptions gérées par le framework.)</span><span class="sxs-lookup"><span data-stu-id="9c98d-131">(In some older types of ASP.NET application, you have to [set up exception monitoring](app-insights-asp-net-exceptions.md) to see exceptions that are handled by the framework.)</span></span>

<span data-ttu-id="9c98d-132">Cliquez sur une exception pour obtenir une trace de pile.</span><span class="sxs-lookup"><span data-stu-id="9c98d-132">Click an exception to get a stack trace.</span></span> <span data-ttu-id="9c98d-133">Si le code de l’application est ouvert dans Visual Studio, vous pouvez utiliser la trace de pile pour accéder à la ligne de code recherchée.</span><span class="sxs-lookup"><span data-stu-id="9c98d-133">If the code of the app is open in Visual Studio, you can click through from the stack trace to the relevant line of the code.</span></span>

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-the-code"></a><span data-ttu-id="9c98d-135">Afficher les résumés des requêtes et des exceptions dans le code</span><span class="sxs-lookup"><span data-stu-id="9c98d-135">View request and exception summaries in the code</span></span>
<span data-ttu-id="9c98d-136">Le nombre de requêtes et d’exceptions consignées par Application Insights dans les dernières 24 heures est indiqué dans la ligne de filtre Code au-dessus de chaque méthode de gestionnaire.</span><span class="sxs-lookup"><span data-stu-id="9c98d-136">In the Code Lens line above each handler method, you see a count of the requests and exceptions logged by Application Insights in the past 24 h.</span></span>

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="9c98d-138">Le filtre Code affiche les données Application Insights uniquement si vous avez [configuré votre application pour que les données de télémétrie soient envoyées au portail Application Insights](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9c98d-138">Code Lens shows Application Insights data only if you have [configured your app to send telemetry to the Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="9c98d-139">En savoir plus sur Application Insights dans le filtre Code</span><span class="sxs-lookup"><span data-stu-id="9c98d-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="9c98d-140">Trends</span><span class="sxs-lookup"><span data-stu-id="9c98d-140">Trends</span></span>
<span data-ttu-id="9c98d-141">Trends est un outil permettant de visualiser le comportement de votre application au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="9c98d-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="9c98d-142">Sélectionnez **Explorer les tendances de la télémétrie** à partir du bouton de la barre d’outils Application Insights ou de la fenêtre de recherche d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9c98d-142">Choose **Explore Telemetry Trends** from the Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="9c98d-143">Sélectionnez l’une des cinq requêtes courantes pour commencer.</span><span class="sxs-lookup"><span data-stu-id="9c98d-143">Choose one of five common queries to get started.</span></span> <span data-ttu-id="9c98d-144">Vous pouvez analyser différents jeux de données en fonction des types de télémétrie, des intervalles de temps ainsi que d’autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="9c98d-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="9c98d-145">Pour rechercher des anomalies dans vos données, sélectionnez l’une des options d’anomalie dans la liste déroulante « Type de vue ».</span><span class="sxs-lookup"><span data-stu-id="9c98d-145">To find anomalies in your data, choose one of the anomaly options under the "View Type" dropdown.</span></span> <span data-ttu-id="9c98d-146">Les options de filtrage en bas de la fenêtre facilitent l’obtention de sous-ensembles spécifiques de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9c98d-146">The filtering options at the bottom of the window make it easy to hone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="9c98d-148">[En savoir plus sur Tendances](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="9c98d-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="9c98d-149">Surveillance locale</span><span class="sxs-lookup"><span data-stu-id="9c98d-149">Local monitoring</span></span>
<span data-ttu-id="9c98d-150">(À partir de Visual Studio 2015 Mise à jour 2) Si vous n’avez pas configuré le Kit de développement logiciel pour envoyer les données de télémétrie au portail Application Insights (et qu’il n’existe donc aucune clé d’instrumentation dans ApplicationInsights.config), la fenêtre de diagnostic affiche les données de télémétrie de votre dernière session de débogage.</span><span class="sxs-lookup"><span data-stu-id="9c98d-150">(From Visual Studio 2015 Update 2) If you haven't configured the SDK to send telemetry to the Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then the diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="9c98d-151">C’est le comportement adéquat si vous avez déjà publié une version antérieure de votre application.</span><span class="sxs-lookup"><span data-stu-id="9c98d-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="9c98d-152">Vous ne voulez pas que les données de télémétrie de vos sessions de débogage soient confondues avec les données de télémétrie sur le portail Application Insights de l’application publiée.</span><span class="sxs-lookup"><span data-stu-id="9c98d-152">You don't want the telemetry from your debugging sessions to be mixed up with the telemetry on the Application Insights portal from the published app.</span></span>

<span data-ttu-id="9c98d-153">Cela est également utile si vous disposez de [données de télémétrie personnalisées](app-insights-api-custom-events-metrics.md) que vous souhaitez déboguer avant de les envoyer sur le portail.</span><span class="sxs-lookup"><span data-stu-id="9c98d-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want to debug before sending telemetry to the portal.</span></span>

* <span data-ttu-id="9c98d-154">*Dans un premier temps, j’ai entièrement configuré Application Insights pour envoyer des données de télémétrie au portail. À présent, j’aimerais afficher ces données uniquement dans Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="9c98d-154">*At first, I fully configured Application Insights to send telemetry to the portal. But now I'd like to see the telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="9c98d-155">Dans les paramètres de la fenêtre de recherche, il existe une option permettant de rechercher des diagnostics locaux même si votre application envoie des données de télémétrie au portail.</span><span class="sxs-lookup"><span data-stu-id="9c98d-155">In the Search window's Settings, there's an option to search local diagnostics even if your app sends telemetry to the portal.</span></span>
  * <span data-ttu-id="9c98d-156">Pour arrêter l’envoi de données de télémétrie au portail, commentez la ligne `<instrumentationkey>...` du fichier ApplicationInsights.config. Lorsque vous êtes prêt à envoyer de nouveau les données de télémétrie au portail, supprimez les commentaires.</span><span class="sxs-lookup"><span data-stu-id="9c98d-156">To stop telemetry being sent to the portal, comment out the line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready to send telemetry to the portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c98d-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9c98d-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="9c98d-158">**[Ajouter des données](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="9c98d-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="9c98d-159">Analysez l’utilisation, la disponibilité, les dépendances et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="9c98d-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="9c98d-160">Intégrer des traces à partir des frameworks de journalisation.</span><span class="sxs-lookup"><span data-stu-id="9c98d-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="9c98d-161">Écrire des données de télémétrie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9c98d-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="9c98d-163">**[Utilisation du portail Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="9c98d-163">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="9c98d-164">Affichez les tableaux de bord, les puissants outils de diagnostic et d’analyse, les alertes, le mappage direct des dépendances de votre application et les données de télémétrie exportées.</span><span class="sxs-lookup"><span data-stu-id="9c98d-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

