---
title: les journaux de suivi de .NET aaaExplore dans Application Insights
description: "Effectuez une recherche dans les journaux générés avec Trace, NLog ou Log4Net."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Exploration des journaux .NET dans Application Insights
Si vous utilisez NLog, log4Net ou System.Diagnostics.Trace pour le suivi de diagnostic dans votre application ASP.NET, vous pouvez avoir vos journaux envoyés trop[Azure Application Insights][start], où vous pouvez Explorer et rechercher les. Les journaux sont fusionnées avec hello autres télémétrie en provenance de votre application, afin que vous puissiez identifier hello traces associés à chaque demande de l’utilisateur de maintenance et les mettre en corrélation avec d’autres événements et les rapports d’exception.

> [!NOTE]
> Module de capture de journal hello avez-vous besoin ? Il s’agit d’un adaptateur très utile pour les enregistreurs d’événements tiers. Cependant, si vous n’utilisez pas déjà NLog, log4Net ou System.Diagnostics.Trace, vous pouvez appeler [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directement.
>
>

## <a name="install-logging-on-your-app"></a>Installation de la journalisation sur votre application
Installez votre infrastructure de journalisation choisie dans votre projet. Ceci devrait générer une entrée dans le fichier app.config ou web.config.

Si vous utilisez System.Diagnostics.Trace, vous devez tooadd une tooweb.config d’entrée :

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Configurer les journaux d’Application Insights toocollect
**[Ajouter le projet d’Application Insights tooyour](app-insights-asp-net.md)**  si vous n’avez pas encore fait. Vous verrez un collecteur de journaux option tooinclude hello.

Ou **configurez Application Insights** en cliquant avec le bouton droit dans l’Explorateur de solutions. L’option hello trop**configurer la collecte de trace**.

*Menu Application Insights non disponible ou aucune option pour le collecteur de journaux ?* Consultez la [Résolution des problèmes](#troubleshooting).

## <a name="manual-installation"></a>Installation manuelle
Utilisez cette méthode si votre type de projet n’est pas pris en charge par le programme d’installation de l’Application Insights hello (par exemple un projet de bureau Windows).

1. Si vous envisagez de toouse log4Net ou NLog, l’installer dans votre projet.
2. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis sélectionnez **Gérer les packages NuGet**.
3. Recherchez « Application Insights »
4. Sélectionnez le package approprié de hello - un des :

   * Microsoft.ApplicationInsights.TraceListener (appels de System.Diagnostics.Trace toocapture)
   * Microsoft.ApplicationInsights.EventSourceListener (événements EventSource de toocapture)
   * Microsoft.ApplicationInsights.EtwListener (événements ETW de toocapture)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

package NuGet de Hello installe les assemblys nécessaires hello et modifie également le fichier web.config ou app.config.

## <a name="insert-diagnostic-log-calls"></a>Insertion d'appels de journaux de diagnostic
Si vous utilisez System.Diagnostics.Trace, un appel standard serait :

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Si vous préférez log4net ou NLog :

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Utilisation des événements EventSource
Vous pouvez configurer [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) événements toobe envoyé tooApplication Insights en tant que les traces. Pour commencer, installez hello `Microsoft.ApplicationInsights.EventSourceListener` package NuGet. Puis modifiez `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Pour chaque source, vous pouvez définir hello paramètres suivants :
 * `Name`Spécifie le nom hello de hello EventSource toocollect.
 * `Level`Spécifie les hello toocollect au niveau de journalisation. Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Facultatif) spécifie la valeur entière hello toouse de combinaisons de mots clés.

## <a name="using-diagnosticsource-events"></a>Utilisation des événements DiagnosticSource
Vous pouvez configurer [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) événements toobe envoyé tooApplication Insights en tant que les traces. Pour commencer, installez hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) package NuGet. Puis modifiez hello `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Pour chaque DiagnosticSource vous souhaitez tootrace, ajoutez une entrée avec hello `Name` attribut nommez toohello votre DiagnosticSource.

## <a name="using-etw-events"></a>Utilisation des événements ETW
Vous pouvez configurer toobe d’événements ETW envoyé tooApplication Insights en tant que les traces. Pour commencer, installez hello `Microsoft.ApplicationInsights.EtwCollector` package NuGet. Puis modifiez `TelemetryModules` section Hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) fichier.

> [!NOTE] 
> Événements ETW peuvent uniquement être collectés si hello hébergement du processus hello SDK s’exécute sous une identité qui est un membre de « Utilisateurs du journal de performances » ou les administrateurs.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Pour chaque source, vous pouvez définir hello paramètres suivants :
 * `ProviderName`désigne hello toocollect de fournisseur ETW hello.
 * `ProviderGuid`Spécifie les hello GUID de hello toocollect de fournisseur ETW, peut être utilisé à la place de `ProviderName`.
 * `Level`définit hello toocollect au niveau de journalisation. Peut être `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(Facultatif) définit hello entier toouse de combinaisons de mot clé.

## <a name="using-hello-trace-api-directly"></a>À l’aide de hello Trace API directement
Vous pouvez appeler directement les API de suivi d’Application Insights hello. adaptateurs de journalisation Hello utilisent cette API.

Par exemple :

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

L’avantage de TrackTrace est que vous pouvez placer des données relativement longues dans le message de type hello. Par exemple, vous pourriez y encoder des données POST.

En outre, vous pouvez ajouter un message tooyour au niveau de gravité. Et, comme les autres données de télémétrie, vous pouvez ajouter des valeurs de propriété que vous pouvez utiliser le filtre de toohelp ou de recherche pour différents ensembles de traces. Par exemple :

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Cela vous permettrait, dans [recherche][diagnostic], filtre tooeasily tous les messages hello d’un niveau de gravité spécifique concernant tooa la base de données particulière.

## <a name="explore-your-logs"></a>Exploration de vos journaux
Exécutez votre application en mode débogage ou déployez-la en direct.

Dans le panneau de vue d’ensemble de votre application dans [portail Application Insights de hello][portal], choisissez [recherche][diagnostic].

![Dans Application Insights, cliquez sur Recherche.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Recherche](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Vous pouvez par exemple :

* Filtrer selon les traces de journal ou les éléments avec des propriétés spécifiques
* Inspecter un élément spécifique en détail
* Rechercher d’autres données de télémétrie relatives toohello même demande de l’utilisateur (autrement dit, avec hello même OperationId)
* Enregistrer la configuration de hello de cette page en tant que favori

> [!NOTE]
> **Échantillonnage.** Si votre application envoie une grande quantité de données et que vous utilisez hello Application Insights SDK pour ASP.NET version 2.0.0-beta3 ou version ultérieure, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie. [En savoir plus sur l’échantillonnage.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Étapes suivantes
[Diagnostiquer les défaillances et les exceptions dans ASP.NET][exceptions]

[En savoir plus sur Recherche][diagnostic].

## <a name="troubleshooting"></a>résolution des problèmes
### <a name="how-do-i-do-this-for-java"></a>Comment faire pour Java ?
Hello d’utilisation [cartes de journal Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Il n’existe aucune option d’Application Insights sur le menu contextuel du projet hello
* Vérifiez que les outils Application Insights sont installés sur cet ordinateur de développement. Dans le menu Outils, Extensions et mises à jour de Visual Studio, recherchez les outils Application Insights. Si elle n’est pas dans l’onglet de hello installé, ouvrez hello en ligne onglet et installez-le.
* Il peut s’agir d’un type de projet non pris en charge par les outils Application Insights. Utilisez [l’installation manuelle](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Aucune option de carte de journal dans l’outil de configuration hello
* Vous devez tout d’abord tooinstall hello journalisation.
* Si vous utilisez System.Diagnostics.Trace, assurez-vous que vous l’avez [configuré dans `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* Avez-vous hello dernière version d’Application Insights ? Dans Visual Studio **outils** menu, choisissez **Extensions et mises à jour**et ouvrez hello **mises à jour** onglet. Si les outils de développement Analytique n’y figure, cliquez sur tooupdate il.

### <a name="emptykey"></a>J’obtiens une erreur « La clé d’instrumentation ne peut pas être vide ».
Il semble que vous avez installé hello journalisation de package Nuget de la carte sans installer Application Insights.

Dans l’Explorateur de solutions, cliquez avec le bouton droit sur `ApplicationInsights.config` , puis sélectionnez **Mettre à jour Application Insights**. Vous obtenez une boîte de dialogue qui vous invite toosign dans tooAzure et créez une ressource Application Insights, ou réutiliser un existant. Ceci devrait résoudre le problème.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Je peux voir les traces dans la recherche de diagnostic, mais pas hello autres événements
Il peut parfois prendre un certain temps pour tous les tooget d’événements et les demandes de hello via le pipeline de hello.

### <a name="limits"></a>Quelle est la quantité de données conservée ?
Plusieurs critères influent sur la quantité de hello de conservation des données. Consultez hello [limites](app-insights-api-custom-events-metrics.md#limits) section de page de métriques hello client événements pour plus d’informations. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Je ne vois pas d’entrées de journal hello attendus
Si votre application envoie une grande quantité de données et que vous utilisez hello Application Insights SDK pour ASP.NET version 2.0.0-beta3 ou version ultérieure, fonctionnalité d’adaptative d’échantillonnage de hello peut fonctionner et envoyer seulement un pourcentage de votre télémétrie. [En savoir plus sur l’échantillonnage.](app-insights-sampling.md)

## <a name="add"></a>Étapes suivantes
* [Configuration des tests de disponibilité et de réactivité][availability]
* [Résolution des problèmes][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
