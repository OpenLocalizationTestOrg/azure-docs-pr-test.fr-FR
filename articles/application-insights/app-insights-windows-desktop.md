---
title: "utilisation d’aaaMonitoring et les performances des applications de bureau Windows"
description: "Analysez l’utilisation et les performances de votre application de bureau Windows avec HockeyApp et Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="d53c3-103">Analyse des performances et de l’utilisation dans les applications de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="d53c3-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="d53c3-104">[Azure Application Insights](app-insights-overview.md) et [HockeyApp](https://hockeyapp.net) vous permettent d’analyser vos applications déployées en termes d’utilisation et de performances.</span><span class="sxs-lookup"><span data-stu-id="d53c3-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d53c3-105">Nous vous recommandons de [HockeyApp](https://hockeyapp.net) toodistribute et surveiller des applications de bureau et de périphérique.</span><span class="sxs-lookup"><span data-stu-id="d53c3-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="d53c3-106">Avec HockeyApp, vous pouvez gérer la distribution, le test direct et les commentaires des utilisateurs, de même que surveiller l’utilisation et les rapports d’incident.</span><span class="sxs-lookup"><span data-stu-id="d53c3-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="d53c3-107">Vous pouvez également [exporter et interroger vos données de télémétrie avec Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="d53c3-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="d53c3-108">Bien que les données de télémétrie peuvent être envoyée tooApplication Insights à partir d’une application de bureau, il s’agit principalement destinées à des fins de débogage et expérimentales.</span><span class="sxs-lookup"><span data-stu-id="d53c3-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="d53c3-109">toosend télémétrie tooApplication Insights à partir d’une application Windows</span><span class="sxs-lookup"><span data-stu-id="d53c3-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="d53c3-110">Bonjour [portail Azure](https://portal.azure.com), [créer une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="d53c3-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="d53c3-111">Choisissez ASP.NET comme type d’application.</span><span class="sxs-lookup"><span data-stu-id="d53c3-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="d53c3-112">Création d’une copie de la clé d’Instrumentation de hello.</span><span class="sxs-lookup"><span data-stu-id="d53c3-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="d53c3-113">Trouver la clé de hello Bonjour Essentials liste déroulante de la ressource hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="d53c3-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="d53c3-114">Dans Visual Studio, modifier les packages NuGet hello de votre projet d’application et ajoutez Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="d53c3-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="d53c3-115">(Ou choisissez Microsoft.ApplicationInsights si vous souhaitez simplement hello API système, sans les modules de collecte de données de télémétrie standard hello).</span><span class="sxs-lookup"><span data-stu-id="d53c3-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="d53c3-116">La valeur clé d’instrumentation hello dans votre code :</span><span class="sxs-lookup"><span data-stu-id="d53c3-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="d53c3-117">`TelemetryConfiguration.Active.InstrumentationKey = "`*votre clé*`";`</span><span class="sxs-lookup"><span data-stu-id="d53c3-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="d53c3-118">ou dans ApplicationInsights.config (si vous avez installé un des packages de télémétrie standard hello) :</span><span class="sxs-lookup"><span data-stu-id="d53c3-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="d53c3-119">`<InstrumentationKey>`*votre clé*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="d53c3-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="d53c3-120">Si vous utilisez ApplicationInsights.config, assurez-vous que ses propriétés dans l’Explorateur de solutions sont définies trop**Build Action = le contenu, copie tooOutput Directory = copie**.</span><span class="sxs-lookup"><span data-stu-id="d53c3-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="d53c3-121">[Utilisez les API hello](app-insights-api-custom-events-metrics.md) toosend télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d53c3-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="d53c3-122">Exécuter votre application et consultez la télémétrie hello dans la ressource hello que vous avez créé dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d53c3-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="d53c3-123"><a name="telemetry"></a>Exemple de code</span><span class="sxs-lookup"><span data-stu-id="d53c3-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a><span data-ttu-id="d53c3-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d53c3-124">Next steps</span></span>
* [<span data-ttu-id="d53c3-125">Création d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="d53c3-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="d53c3-126">Recherche de diagnostic</span><span class="sxs-lookup"><span data-stu-id="d53c3-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="d53c3-127">Exploration des mesures</span><span class="sxs-lookup"><span data-stu-id="d53c3-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="d53c3-128">Écriture de requêtes Analytics</span><span class="sxs-lookup"><span data-stu-id="d53c3-128">Write Analytics queries</span></span>](app-insights-analytics.md)

