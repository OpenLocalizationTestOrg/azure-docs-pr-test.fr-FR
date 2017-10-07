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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Analyse des performances et de l’utilisation dans les applications de bureau Windows


[Azure Application Insights](app-insights-overview.md) et [HockeyApp](https://hockeyapp.net) vous permettent d’analyser vos applications déployées en termes d’utilisation et de performances.

> [!IMPORTANT]
> Nous vous recommandons de [HockeyApp](https://hockeyapp.net) toodistribute et surveiller des applications de bureau et de périphérique. Avec HockeyApp, vous pouvez gérer la distribution, le test direct et les commentaires des utilisateurs, de même que surveiller l’utilisation et les rapports d’incident. Vous pouvez également [exporter et interroger vos données de télémétrie avec Analytics](app-insights-hockeyapp-bridge-app.md).
> 
> Bien que les données de télémétrie peuvent être envoyée tooApplication Insights à partir d’une application de bureau, il s’agit principalement destinées à des fins de débogage et expérimentales.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend télémétrie tooApplication Insights à partir d’une application Windows
1. Bonjour [portail Azure](https://portal.azure.com), [créer une ressource Application Insights](app-insights-create-new-resource.md). Choisissez ASP.NET comme type d’application.
2. Création d’une copie de la clé d’Instrumentation de hello. Trouver la clé de hello Bonjour Essentials liste déroulante de la ressource hello que vous venez de créer. 
3. Dans Visual Studio, modifier les packages NuGet hello de votre projet d’application et ajoutez Microsoft.ApplicationInsights.WindowsServer. (Ou choisissez Microsoft.ApplicationInsights si vous souhaitez simplement hello API système, sans les modules de collecte de données de télémétrie standard hello).
4. La valeur clé d’instrumentation hello dans votre code :
   
    `TelemetryConfiguration.Active.InstrumentationKey = "`*votre clé*`";` 
   
    ou dans ApplicationInsights.config (si vous avez installé un des packages de télémétrie standard hello) :
   
    `<InstrumentationKey>`*votre clé*`</InstrumentationKey>` 
   
    Si vous utilisez ApplicationInsights.config, assurez-vous que ses propriétés dans l’Explorateur de solutions sont définies trop**Build Action = le contenu, copie tooOutput Directory = copie**.
5. [Utilisez les API hello](app-insights-api-custom-events-metrics.md) toosend télémétrie.
6. Exécuter votre application et consultez la télémétrie hello dans la ressource hello que vous avez créé dans hello portail Azure.

## <a name="telemetry"></a>Exemple de code
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

## <a name="next-steps"></a>Étapes suivantes
* [Création d’un tableau de bord](app-insights-dashboards.md)
* [Recherche de diagnostic](app-insights-diagnostic-search.md)
* [Exploration des mesures](app-insights-metrics-explorer.md)
* [Écriture de requêtes Analytics](app-insights-analytics.md)

