---
title: "Analyse des performances et de l’utilisation pour les applications de bureau Windows"
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
ms.openlocfilehash: 9d7e2a390adf10cbf5d88dd0084ce09136987309
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="ce5c6-103">Analyse des performances et de l’utilisation dans les applications de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="ce5c6-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="ce5c6-104">[Azure Application Insights](app-insights-overview.md) et [HockeyApp](https://hockeyapp.net) vous permettent d’analyser vos applications déployées en termes d’utilisation et de performances.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ce5c6-105">Nous vous recommandons [HockeyApp](https://hockeyapp.net) pour distribuer et surveiller des applications de bureau et pour périphérique.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-105">We recommend [HockeyApp](https://hockeyapp.net) to distribute and monitor desktop and device apps.</span></span> <span data-ttu-id="ce5c6-106">Avec HockeyApp, vous pouvez gérer la distribution, le test direct et les commentaires des utilisateurs, de même que surveiller l’utilisation et les rapports d’incident.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="ce5c6-107">Vous pouvez également [exporter et interroger vos données de télémétrie avec Analytics](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="ce5c6-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="ce5c6-108">Bien que les données de télémétrie puissent être envoyées à Application Insights à partir d’une application de bureau, ceci est principalement utile à des fins de débogage et d’expérimentation.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-108">Although telemetry can be sent to Application Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="to-send-telemetry-to-application-insights-from-a-windows-application"></a><span data-ttu-id="ce5c6-109">Pour envoyer la télémétrie à Application Insights à partir d’une application Windows</span><span class="sxs-lookup"><span data-stu-id="ce5c6-109">To send telemetry to Application Insights from a Windows application</span></span>
1. <span data-ttu-id="ce5c6-110">Dans le [portail Azure](https://portal.azure.com), [créez une ressource Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ce5c6-110">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="ce5c6-111">Choisissez ASP.NET comme type d’application.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="ce5c6-112">Copiez la clé d'instrumentation.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-112">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="ce5c6-113">Recherchez la clé dans la liste déroulante Essentials de la nouvelle ressource que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-113">Find the key in the Essentials drop-down of the new resource you just created.</span></span> 
3. <span data-ttu-id="ce5c6-114">Dans Visual Studio, modifiez les packages NuGet de votre projet d’application et ajoutez Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-114">In Visual Studio, edit the NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="ce5c6-115">(Ou choisissez Microsoft.ApplicationInsights si vous souhaitez simplement l’API nue, sans modules de collecte de télémétrie standard.)</span><span class="sxs-lookup"><span data-stu-id="ce5c6-115">(Or choose Microsoft.ApplicationInsights if you just want the bare API, without the standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="ce5c6-116">Définissez la clé d’instrumentation dans votre code :</span><span class="sxs-lookup"><span data-stu-id="ce5c6-116">Set the instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="ce5c6-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *votre clé* `";`</span><span class="sxs-lookup"><span data-stu-id="ce5c6-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="ce5c6-118">ou dans ApplicationInsights.config (si vous avez installé l’un des packages de télémétrie standard) :</span><span class="sxs-lookup"><span data-stu-id="ce5c6-118">or in ApplicationInsights.config (if you installed one of the standard telemetry packages):</span></span>
   
    <span data-ttu-id="ce5c6-119">`<InstrumentationKey>`*votre clé*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ce5c6-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="ce5c6-120">Si vous utilisez ApplicationInsights.config, assurez-vous que ses propriétés dans l’Explorateur de solutions sont définies sur **Build Action = Content, Copy to Output Directory = Copy**.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>
5. <span data-ttu-id="ce5c6-121">[Utilisez l’API](app-insights-api-custom-events-metrics.md) pour envoyer les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-121">[Use the API](app-insights-api-custom-events-metrics.md) to send telemetry.</span></span>
6. <span data-ttu-id="ce5c6-122">Exécutez votre application et consultez la télémétrie dans la ressource que vous avez créée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ce5c6-122">Run your app, and see the telemetry in the resource you created in the Azure Portal.</span></span>

## <span data-ttu-id="ce5c6-123"><a name="telemetry"></a>Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ce5c6-123"><a name="telemetry"></a>Example code</span></span>
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative to setting ikey in config file:
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

## <a name="next-steps"></a><span data-ttu-id="ce5c6-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce5c6-124">Next steps</span></span>
* [<span data-ttu-id="ce5c6-125">Création d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="ce5c6-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="ce5c6-126">Recherche de diagnostic</span><span class="sxs-lookup"><span data-stu-id="ce5c6-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="ce5c6-127">Exploration des mesures</span><span class="sxs-lookup"><span data-stu-id="ce5c6-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="ce5c6-128">Écriture de requêtes Analytics</span><span class="sxs-lookup"><span data-stu-id="ce5c6-128">Write Analytics queries</span></span>](app-insights-analytics.md)

