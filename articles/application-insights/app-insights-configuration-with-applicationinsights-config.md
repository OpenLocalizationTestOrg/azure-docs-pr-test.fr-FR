---
title: "référence aaaApplicationInsights.config - Azure | Documents Microsoft"
description: "Activez ou désactivez les modules de collecte de données et ajoutez des compteurs de performances et d’autres paramètres."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Configuration de l’Application Insights SDK de hello avec ApplicationInsights.config ou .xml
Hello Application Insights .NET SDK se compose d’un nombre de packages NuGet. Le [package core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fournit les API hello pour l’envoi de données de télémétrie Hello Application Insights. Des [packages supplémentaires](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fournissent les *modules* et les *initialiseurs* de télémétrie pour le suivi télémétrique automatique de votre application et de son contexte. En ajustant le fichier de configuration hello, vous pouvez activer ou désactiver les initialiseurs et les modules de télémétrie et définir les paramètres pour certains d'entre eux.

fichier de configuration Hello est nommé `ApplicationInsights.config` ou `ApplicationInsights.xml`, en fonction de type hello de votre application. Il est automatiquement ajouté tooyour projet lorsque vous [installer la plupart des versions du Kit de développement logiciel de hello][start]. Il est également ajouté application web de tooa par [Status Monitor sur un serveur IIS][redfield], ou lorsque vous sélectionnez hello importe quelle application Insights [extension pour une machine virtuelle ou un site Web Azure](app-insights-azure-web-apps.md).

Il n’est pas un hello toocontrol de fichier équivalent [SDK dans une page web][client].

Ce document décrit les sections hello que vous consultez dans la configuration de hello du fichier, la gestion des composants hello Hello SDK, et les packages NuGet chargement ces composants.

## <a name="telemetry-modules-aspnet"></a>Modules de télémétrie (ASP.NET)
Chaque module de télémétrie collecte un type de données spécifique et utilise des noyaux de hello données d’API toosend hello. modules de Hello sont installés à différents packages NuGet, ce qui est également ajouter le fichier .config de hello lignes requises toohello.

Il existe un nœud dans le fichier de configuration hello pour chaque module. toodisable un module, supprimez le nœud de hello ou commentez-le.

### <a name="dependency-tracking"></a>Suivi des dépendances
[Le suivi des dépendances](app-insights-asp-net-dependencies.md) collecte une télémétrie sur les appels de votre application toodatabases et les services externes et les bases de données. tooallow toowork de ce module dans un serveur IIS, vous devez trop[installer Status Monitor][redfield]. toouse dans les applications web Azure ou des machines virtuelles, [sélectionner l’extension d’Application Insights hello](app-insights-azure-web-apps.md).

Vous pouvez également écrire votre propre dépendance suivi du code à l’aide de hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .

### <a name="performance-collector"></a>Collecteur de performances
[Collecte les compteurs de performances système](app-insights-performance-counters.md), notamment l’UC, la mémoire et la charge réseau, à partir des installations IIS. Vous pouvez spécifier le compteurs toocollect, y compris les compteurs de performance que vous avez configuré vous-même.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .

### <a name="application-insights-diagnostics-telemetry"></a>Télémétrie des diagnostics Application Insights
Hello `DiagnosticsTelemetryModule` signale les erreurs dans hello le code d’instrumentation Application Insights lui-même. Par exemple, si le code de hello ne peut pas accéder aux compteurs de performance ou si un `ITelemetryInitializer` lève une exception. Télémétrie des traces suivie par ce module s’affiche dans hello [recherche Diagnostic][diagnostic]. Envoie des données de diagnostic toodc.services.vsallin.net.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Si vous installez uniquement ce package, fichier ApplicationInsights.config de hello n’est pas créé automatiquement.

### <a name="developer-mode"></a>Mode développeur
`DeveloperModeWithDebuggerAttachedTelemetryModule`force hello Application Insights `TelemetryChannel` toosend immédiatement les données, les éléments d’un télémétrie à la fois, quand un débogueur est attaché toohello processus d’application. Cela réduit la durée hello entre le moment de hello lorsque votre application effectue le suivi des données de télémétrie et lorsqu’il apparaît sur le portail Application Insights hello. Cela cause une surcharge importante au niveau de l'UC et de la bande passante réseau.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)

### <a name="web-request-tracking"></a>Suivi des requêtes web
Hello de rapports [code d’heure et les résultats de réponse](app-insights-asp-net.md) de requêtes HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)

### <a name="exception-tracking"></a>Suivi des exceptions
`ExceptionTrackingTelemetryModule` comptabilise le nombre d’exceptions non traitées dans votre application web. Consultez [Échecs et exceptions][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - suit [les exceptions de tâche non prises en charge](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - suit les exceptions non gérées pour les rôles de travail, les services Windows et les applications de console.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="eventsource-tracking"></a>Suivi EventSource
`EventSourceTelemetryModule`vous permet de tooconfigure toobe d’événements EventSource envoyé tooApplication Insights en tant que les traces. Pour plus d’informations sur le suivi des événements EventSource, consultez [Utilisation d’événements EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Suivi des événements ETW
`EtwCollectorTelemetryModule`vous permet d’événements tooconfigure toobe de fournisseurs ETW envoyé tooApplication Insights en tant que les traces. Pour plus d’informations sur le suivi des événements ETW, consultez [Utilisation d’événements ETW](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
Hello Microsoft.ApplicationInsights offre hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) Hello SDK. Hello autres modules de télémétrie utilisent, et vous pouvez également [toodefine l’utiliser vos propres données de télémétrie](app-insights-api-custom-events-metrics.md).

* Aucune entrée dans ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Si vous installez simplement ce package NuGet, aucun fichier .config n'est créé.

## <a name="telemetry-channel"></a>Canal de télémétrie
canal de données de télémétrie Hello gère la mise en mémoire tampon et la transmission des données de télémétrie toohello service Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`est le canal par défaut de hello pour les services. Il met les données en mémoire.
* `Microsoft.ApplicationInsights.PersistenceChannel` est une alternative pour les applications de console. Il peut enregistrer n’importe quel stockage toopersistent de données vidées lorsque votre application ferme et enverra lors de l’application hello démarre à nouveau.

## <a name="telemetry-initializers-aspnet"></a>Initialiseurs de télémétrie (ASP.NET)
Les initialiseurs de télémétrie définissent les propriétés de contexte envoyées avec chaque élément de télémétrie.

Vous pouvez [écrire vos propres initialiseurs](app-insights-api-filtering-sampling.md#add-properties) tooset les propriétés de contexte.

les initialiseurs standard Hello sont tous définis en hello Web ou WindowsServer NuGet packages :

* `AccountIdTelemetryInitializer`définit la propriété d’ID de compte hello.
* `AuthenticatedUserIdTelemetryInitializer`définit la propriété AuthenticatedUserId de hello en tant que jeu par hello SDK JavaScript.
* `AzureRoleEnvironmentTelemetryInitializer`hello de mises à jour `RoleName` et `RoleInstance` propriétés Hello `Device` contexte pour tous les éléments de télémétrie avec des informations extraites de l’environnement d’exécution Azure hello.
* `BuildInfoConfigComponentVersionTelemetryInitializer`hello de mises à jour `Version` propriété Hello `Component` contexte pour tous les éléments de télémétrie avec la valeur hello extraites hello `BuildInfo.config` fichier produit par MS Build.
* `ClientIpHeaderTelemetryInitializer`les mises à jour `Ip` propriété Hello `Location` le contexte de tous les éléments de télémétrie en fonction hello `X-Forwarded-For` en-tête HTTP de la demande de hello.
* `DeviceTelemetryInitializer`hello mises à jour les propriétés de hello suivantes `Device` contexte pour tous les éléments de télémétrie.
  * `Type`est défini trop « PC »
  * `Id`a la valeur toohello nom de domaine de l’ordinateur de hello où l’application web de hello est en cours d’exécution.
  * `OemName`a la valeur toohello extraite hello `Win32_ComputerSystem.Manufacturer` champ à l’aide de WMI.
  * `Model`a la valeur toohello extraite hello `Win32_ComputerSystem.Model` champ à l’aide de WMI.
  * `NetworkType`a la valeur toohello extraite hello `NetworkInterface`.
  * `Language`a la valeur nom toohello Hello `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`hello de mises à jour `RoleInstance` propriété Hello `Device` contexte pour tous les éléments de télémétrie avec le nom de domaine hello d’ordinateur hello où l’application web de hello est en cours d’exécution.
* `OperationNameTelemetryInitializer`hello de mises à jour `Name` propriété Hello `RequestTelemetry` et hello `Name` propriété Hello `Operation` contexte de tous les éléments de télémétrie en fonction de la méthode hello HTTP, ainsi que leurs noms de hello de tooprocess appelé contrôleur et d’action ASP.NET MVC demande.
* `OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` hello de mises à jour `Operation.Id` propriété de contexte de tous les éléments de télémétrie suivies lors du traitement d’une demande avec hello généré automatiquement `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`hello de mises à jour `Id` propriété Hello `Session` contexte pour tous les éléments de télémétrie avec la valeur extraite de hello `ai_session` cookie généré par hello le code d’instrumentation ApplicationInsights JavaScript en cours d’exécution dans le navigateur de l’utilisateur hello.
* `SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` hello de mises à jour `User`, `Session` et `Operation` des propriétés de contextes de tous les éléments de télémétrie suivies lors du traitement d’une demande émanant d’une source synthétique, comme une disponibilité de test ou robot de moteur de recherche. Par défaut, [Metrics Explorer](app-insights-metrics-explorer.md) n'affiche pas la télémétrie synthétique.

    Hello `<Filters>` définir l’identification des propriétés de demandes de hello.
* `UserAgentTelemetryInitializer`hello de mises à jour `UserAgent` propriété Hello `User` le contexte de tous les éléments de télémétrie en fonction hello `User-Agent` en-tête HTTP de la demande de hello.
* `UserTelemetryInitializer`hello de mises à jour `Id` et `AcquisitionDate` propriétés de `User` contexte pour tous les éléments de télémétrie avec des valeurs extraites hello `ai_user` cookie généré par le code d’instrumentation Application Insights JavaScript hello en hello navigateur de l’utilisateur.
* `WebTestTelemetryInitializer`jeux de hello id utilisateur, les id de session et les propriétés de la source de synthèse pour des requêtes HTTP provenant de [les tests de disponibilité](app-insights-monitor-web-app-availability.md).
  Hello `<Filters>` définir l’identification des propriétés de demandes de hello.

Pour les applications .NET en cours d’exécution dans l’infrastructure de Service, vous pouvez inclure hello `Microsoft.ApplicationInsights.ServiceFabric` package NuGet. Ce package comprend un `FabricTelemetryInitializer`, qui ajoute des éléments de tootelemetry de propriétés de l’infrastructure de Service. Pour plus d’informations, consultez hello [page GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sur les propriétés hello ajoutées par ce package NuGet.

## <a name="telemetry-processors-aspnet"></a>Processeurs de télémétrie (ASP.NET)
Processeurs de télémétrie peuvent filtrer et modifier chaque élément de données de télémétrie juste avant d’être envoyée à partir du portail de toohello hello Kit de développement logiciel.

Vous pouvez [écrire vos propres processeurs de télémétrie](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Processeur de télémétrie d'échantillonnage adaptatif (à partir de 2.0.0-beta3)
Cette option est activée par défaut. Si votre application envoie beaucoup de télémétrie, ce processeur en supprime une partie.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

paramètre Hello fournit cible hello hello algorithme tente tooachieve. Chaque instance de hello SDK fonctionne indépendamment, afin que si votre serveur est un cluster de plusieurs ordinateurs, volume effectif hello télémétrie sera multiplié en conséquence.

[En savoir plus sur l'échantillonnage](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Processeur de télémétrie d'échantillonnage à taux fixe (à partir de 2.0.0-beta1)
Il existe également un [processeur de télémétrie d’échantillonnage](app-insights-api-filtering-sampling.md) standard (à partir de 2.0.1) :

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Paramètres de canal (Java)
Ces paramètres affectent la hello Kit de développement logiciel Java doit stocker et vider les données de télémétrie hello qu’il collecte.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
nombre de Hello d’éléments de télémétrie qui peuvent être stockées dans le stockage en mémoire du Kit de développement hello. Lorsque ce nombre est atteint, mémoire tampon de données de télémétrie hello est vidé, autrement dit, les éléments de télémétrie hello sont envoyés de serveur d’Application Insights toohello.

* Min : 1
* Max : 1000
* Valeur par défaut : 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Détermine la fréquence à laquelle hello les données stockées dans le stockage en mémoire hello doivent être vidée (une tooApplication envoyée Insights).

* Min : 1
* Max : 300
* Valeur par défaut : 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Détermine la taille maximale de hello en Mo allouée toohello le stockage persistant sur le disque local hello. Ce stockage est utilisé pour les éléments de télémétrie persistants qui ont échoué le point de terminaison toobe transmis toohello Application Insights. Lorsque la taille de stockage hello a été rencontrée, les nouveaux éléments de télémétrie seront ignorées.

* Min : 1
* Max : 100
* Valeur par défaut : 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Cela détermine la ressource d’Application Insights hello dans lequel vos données s’affiche. En général, vous créez une ressource séparée, avec une clé distincte, pour chacune de vos applications.

Si vous souhaitez tooset hello clé dynamiquement, par exemple si vous souhaitez que les résultats de toosend à partir de vos ressources d’application toodifferent - vous pouvez omettre la clé hello à partir du fichier de configuration hello et définir dans le code.

clé de hello tooset pour toutes les instances de TelemetryClient, y compris les modules de télémétrie standard, définie des clé de hello dans TelemetryConfiguration.Active. Définissez-la dans une méthode d’initialisation, telle que global.aspx.cs dans un service ASP.NET :

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Si vous souhaitez simplement toosend un ensemble spécifique de ressources de différents événements tooa, vous pouvez définir la clé de hello pour un TelemetryClient spécifique :

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

une nouvelle clé de tooget [créer une ressource dans le portail d’Application Insights hello][new].

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur les API de hello][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
