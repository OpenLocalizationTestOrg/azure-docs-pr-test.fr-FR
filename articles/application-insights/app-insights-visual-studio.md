---
title: applications aaaDebug avec Azure Application Insights dans Visual Studio | Documents Microsoft
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
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="9e66a-103">Débogage d’applications à l’aide d’Azure Application Insights dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e66a-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="9e66a-104">Visual Studio 2015 (et versions ultérieures) vous permet d’analyser les performances et de diagnostiquer les problèmes au niveau de votre application web ASP.NET aussi bien en phase de débogage qu’en production, à l’aide des données de télémétrie [d’Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e66a-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="9e66a-105">Si vous avez créé votre application de web ASP.NET à l’aide de Visual Studio 2017 ou une version ultérieure, il a déjà hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="9e66a-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="9e66a-106">Sinon, si vous n’avez pas déjà fait, [ajouter Application Insights tooyour application](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9e66a-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="9e66a-107">toomonitor votre application lorsqu’il est dans un environnement de production, vous normalement Affichez les données de télémétrie Application Insights hello Bonjour [portail Azure](https://portal.azure.com), où vous pouvez définir des alertes et appliquer des outils d’analyse puissants.</span><span class="sxs-lookup"><span data-stu-id="9e66a-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="9e66a-108">Mais, pour le débogage, vous pouvez également rechercher et analysez la télémétrie hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e66a-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="9e66a-109">Vous pouvez utiliser les données de télémétrie tooanalyze Visual Studio de votre site de production et de débogage s’exécute sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="9e66a-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="9e66a-110">Dans ce dernier cas de hello, vous pouvez analyser les séries de débogage même si vous n’avez pas encore configuré hello SDK toosend télémétrie toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e66a-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="9e66a-111"><a name="run"></a> Débogage de votre projet</span><span class="sxs-lookup"><span data-stu-id="9e66a-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="9e66a-112">Exécutez votre application web en mode de débogage local à l’aide de la touche F5.</span><span class="sxs-lookup"><span data-stu-id="9e66a-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="9e66a-113">Ouvrir des pages différentes toogenerate certaines données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e66a-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="9e66a-114">Dans Visual Studio, vous consultez un nombre d’événements de hello qui ont été consignés par le module d’Application Insights hello dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="9e66a-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![Dans Visual Studio, le bouton d’Application Insights hello montre pendant le débogage.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="9e66a-116">Cliquez sur ce bouton toosearch votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e66a-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="9e66a-117">Recherche Application Insights</span><span class="sxs-lookup"><span data-stu-id="9e66a-117">Application Insights search</span></span>
<span data-ttu-id="9e66a-118">fenêtre de recherche Application Insights Hello présente les événements qui ont été enregistrés.</span><span class="sxs-lookup"><span data-stu-id="9e66a-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="9e66a-119">(Si vous connecté tooAzure lorsque vous installez Application Insights, vous pouvez rechercher hello les mêmes événements Bonjour portail Azure.)</span><span class="sxs-lookup"><span data-stu-id="9e66a-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Droit hello projet, puis choisissez Application Insights, recherche](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="9e66a-121">Une fois que vous sélectionnez ou désélectionnez les filtres, cliquez sur le bouton de recherche hello à fin hello du champ de recherche de texte hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="9e66a-122">recherche en texte libre Hello fonctionne sur tous les champs dans les événements hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="9e66a-123">Par exemple, rechercher une partie de l’URL de hello d’une page ; ou valeur hello d’une propriété telle que ville du client ; ou des mots spécifiques dans un journal des traces.</span><span class="sxs-lookup"><span data-stu-id="9e66a-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="9e66a-124">Cliquez sur n’importe quel toosee événement ses propriétés détaillées.</span><span class="sxs-lookup"><span data-stu-id="9e66a-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="9e66a-125">Pour les demandes tooyour web app, vous pouvez cliquer sur toohello code.</span><span class="sxs-lookup"><span data-stu-id="9e66a-125">For requests tooyour web app, you can click through toohello code.</span></span>

![Sous Détails de la demande, cliquez sur dans le code de toohello](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="9e66a-127">Vous pouvez également ouvrir des éléments connexes toohelp diagnostiquer les échecs de demandes ou des exceptions.</span><span class="sxs-lookup"><span data-stu-id="9e66a-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![Sous Détails de la demande, faites défiler la liste des éléments toorelated](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="9e66a-129">Afficher les exceptions et les requêtes ayant échoué</span><span class="sxs-lookup"><span data-stu-id="9e66a-129">View exceptions and failed requests</span></span>
<span data-ttu-id="9e66a-130">Exception afficher de rapports dans la fenêtre de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="9e66a-131">(Dans certains types plus anciens d’application ASP.NET, vous avez trop[configurer l’analyse des exceptions](app-insights-asp-net-exceptions.md) toosee les exceptions qui sont gérées par le framework de hello.)</span><span class="sxs-lookup"><span data-stu-id="9e66a-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="9e66a-132">Cliquez sur une exception de tooget une trace de pile.</span><span class="sxs-lookup"><span data-stu-id="9e66a-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="9e66a-133">Si le code hello de l’application hello est ouvert dans Visual Studio, vous pouvez cliquer à partir de hello pile trace toohello ligne appropriée du code de hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="9e66a-135">Afficher les récapitulatifs de demande et de l’exception dans le code hello</span><span class="sxs-lookup"><span data-stu-id="9e66a-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="9e66a-136">Dans la ligne de Code thématique au-dessus de chaque méthode de gestionnaire de hello, vous consultez un nombre de demandes de hello et exceptions consignées par Application Insights Bonjour dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="9e66a-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Arborescence des appels de procédure d’exception](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="9e66a-138">Codelens affiche uniquement les données d’Application Insights si vous avez [configuré votre portail Application Insights toohello de télémétrie de toosend application](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9e66a-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="9e66a-139">En savoir plus sur Application Insights dans le filtre Code</span><span class="sxs-lookup"><span data-stu-id="9e66a-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="9e66a-140">Trends</span><span class="sxs-lookup"><span data-stu-id="9e66a-140">Trends</span></span>
<span data-ttu-id="9e66a-141">Trends est un outil permettant de visualiser le comportement de votre application au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="9e66a-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="9e66a-142">Choisissez **Explorer les tendances de télémétrie** à partir de bouton de barre d’outils Application Insights hello ou recherche Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e66a-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="9e66a-143">Choisissez une des cinq tooget de requêtes courantes a démarré.</span><span class="sxs-lookup"><span data-stu-id="9e66a-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="9e66a-144">Vous pouvez analyser différents jeux de données en fonction des types de télémétrie, des intervalles de temps ainsi que d’autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="9e66a-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="9e66a-145">anomalies toofind dans vos données, choisissez une des options d’anomalie hello sous la liste déroulante du « Type d’affichage » hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="9e66a-146">options de filtrage Hello bas hello de fenêtre hello qu’il soit facile toohone dans sur des sous-ensembles spécifiques de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e66a-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Trends](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="9e66a-148">[En savoir plus sur Tendances](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="9e66a-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="9e66a-149">Surveillance locale</span><span class="sxs-lookup"><span data-stu-id="9e66a-149">Local monitoring</span></span>
<span data-ttu-id="9e66a-150">(À partir de Visual Studio 2015 Update 2) Si vous n’avez pas configuré le portail Application Insights de hello SDK toosend télémétrie toohello (pour qu’il n’y a aucune clé d’instrumentation dans ApplicationInsights.config) puis hello diagnostics affiche télémétrie à partir de votre session de débogage plus récentes.</span><span class="sxs-lookup"><span data-stu-id="9e66a-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="9e66a-151">C’est le comportement adéquat si vous avez déjà publié une version antérieure de votre application.</span><span class="sxs-lookup"><span data-stu-id="9e66a-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="9e66a-152">Vous ne souhaitez pas que votre toobe de sessions de débogage télémétrie hello confondues télémétrie hello sur hello portail Application Insights à partir de l’application publiée hello.</span><span class="sxs-lookup"><span data-stu-id="9e66a-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="9e66a-153">Il est également utile si vous disposez d’un [une télémétrie personnalisée](app-insights-api-custom-events-metrics.md) que vous souhaitez toodebug avant d’envoyer le portail de toohello de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e66a-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="9e66a-154">*Dans un premier temps, j’ai configuré entièrement portail de toohello télémétrie Application Insights toosend. Mais maintenant je souhaite que les données de télémétrie toosee hello uniquement dans Visual Studio.*</span><span class="sxs-lookup"><span data-stu-id="9e66a-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="9e66a-155">Paramètres de la fenêtre de recherche hello, est une option toosearch local de diagnostic même si votre application envoie un portail toohello de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="9e66a-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="9e66a-156">télémétrie toostop envoyée portail toohello, commentez la ligne de hello `<instrumentationkey>...` à partir de ApplicationInsights.config. Lorsque vous êtes à nouveau portail de toohello toosend prêt télémétrie, supprimez les commentaires.</span><span class="sxs-lookup"><span data-stu-id="9e66a-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9e66a-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e66a-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="9e66a-158">**[Ajouter des données](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="9e66a-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="9e66a-159">Analysez l’utilisation, la disponibilité, les dépendances et les exceptions.</span><span class="sxs-lookup"><span data-stu-id="9e66a-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="9e66a-160">Intégrer des traces à partir des frameworks de journalisation.</span><span class="sxs-lookup"><span data-stu-id="9e66a-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="9e66a-161">Écrire des données de télémétrie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="9e66a-161">Write custom telemetry.</span></span> |![Visual Studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="9e66a-163">**[Utilisation de portail d’Application Insights hello](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="9e66a-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="9e66a-164">Affichez les tableaux de bord, les puissants outils de diagnostic et d’analyse, les alertes, le mappage direct des dépendances de votre application et les données de télémétrie exportées.</span><span class="sxs-lookup"><span data-stu-id="9e66a-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual Studio](./media/app-insights-visual-studio/62.png) |

