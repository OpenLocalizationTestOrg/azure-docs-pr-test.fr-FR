---
title: aaaAzure analyse au niveau de Service Fabric Application | Documents Microsoft
description: "En savoir plus sur l’application et les journaux et les événements de niveau de service utilisé toomonitor et diagnostiquer les clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a>Génération de journaux et d’événements de niveau application et service

## <a name="instrumenting-hello-code-with-custom-events"></a>L’instrumentation de code hello avec des événements personnalisés

Instrumentation de hello code sert hello pour la plupart des autres aspects de vos services d’analyse. L’instrumentation est hello seule façon que vous saurez que pose problème, et toodiagnose, ce qui doit toobe fixe. Bien que techniquement possible tooconnect un service de débogueur tooa production, il n’est pas une pratique courante. Par conséquent, il est important de disposer de données d’instrumentation détaillées.

Certains produits instrumentent automatiquement votre code. Bien que ces solutions soient très efficaces, une instrumentation manuelle est presque toujours nécessaire. Final de hello, vous devez disposer d’assez tooforensically informations déboguer l’application hello. Ce document décrit les différentes approches tooinstrumenting votre code, et lorsque toochoose une approche vers un autre.

## <a name="eventsource"></a>EventSource
Lorsque vous créez une solution Service Fabric à partir d’un modèle dans Visual Studio, une classe dérivée **EventSource** (**ServiceEventSource** ou **ActorEventSource**) est générée. Un modèle dans lequel vous pouvez ajouter des événements pour votre application ou votre service est créé. Hello **EventSource** nom **doit** être unique et doit être renommé à partir de la chaîne de modèle par défaut hello MyCompany -&lt;solution&gt; - &lt; projet&gt;. Présence de plusieurs **EventSource** définitions qui utilisent hello même causes nom un problème au moment de l’exécution. Chaque événement défini doit avoir un identificateur unique. Si l’identificateur n’est pas unique, l’exécution échoue. Certaines organisations preassign des plages de valeurs pour les conflits de tooavoid identificateurs entre les équipes de développement distinct. Pour plus d’informations, consultez [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou hello [documentation MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Utilisation d’événements EventSource structurés

Chacun des événements hello dans les exemples de code hello dans cette section sont définis pour un incident spécifique, par exemple, lorsqu’un type de service est enregistré. Lorsque vous définissez des messages en cas d’usage, de données peuvent être empaquetées avec texte hello d’erreur de hello, et vous pouvez plus facilement rechercher et filtre basé sur les noms de hello ou les valeurs de hello les propriétés spécifiées. Structuration de sortie d’instrumentation hello rend tooconsume plus facile, mais nécessite plus de réflexion et une heure toodefine un nouvel événement pour chaque cas d’usage. Des définitions d’événement peuvent être partagées entre l’ensemble de l’application hello. Par exemple, un événement de commencement ou d’arrêt de méthode peut être réutilisé dans plusieurs services d’une même application. Un service spécifique d’un domaine, comme un système de commande, peut est associé à un événement **CreateOrder**, qui présente son propre événement unique. Cette approche est susceptible de générer de nombreux événements et peut requérir la coordination des identificateurs entre les équipes de projet. 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a>Utilisation générale d’EventSource

Étant donné la complexité de la définition d’événements spécifiques, de nombreuses personnes définissent quelques événements avec un ensemble commun de paramètres qui sortent généralement les informations sous forme de chaîne. Une grande partie de l’aspect de hello structuré est perdue, et il est plus difficiles toosearch et filtre hello les résultats. Dans cette approche, quelques événements qui correspondent généralement des niveaux de journalisation de toohello sont définis. Hello suivant extrait de code définit un message d’erreur et de débogage :

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

Une approche hybride d’instrumentation structurée et générique peut aussi fonctionner. L’instrumentation structurée sert à créer des rapports sur les erreurs et les mesures. Événements génériques peuvent être utilisés pour hello détaillée journalisation qui est consommée par les ingénieurs de dépannage.

## <a name="aspnet-core-logging"></a>Journalisation ASP.NET Core

Toocarefully important son plan vous serez comment instrumenter votre code. plan d’instrumentation droite Hello peut vous aider à éviter potentiellement déstabiliser votre base de code et puis avoir besoin de code de hello tooreinstrument. tooreduce risque, vous pouvez choisir une bibliothèque d’instrumentation, par exemple [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), qui fait partie de Microsoft ASP.NET Core. ASP.NET Core a un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que vous pouvez utiliser avec le fournisseur hello de votre choix, tout en réduisant les effets de hello sur du code existant. Vous pouvez utiliser du code hello dans ASP.NET Core sur Windows et Linux et Bonjour complète .NET Framework, donc votre code d’instrumentation est normalisé. Cette opération est examinée plus en détail ci-dessous :

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Utilisation de Microsoft.Extensions.Logging dans Service Fabric

1. Ajoutez hello Microsoft.Extensions.Logging NuGet package toohello projet tooinstrument. En outre, ajoutez tous les packages de fournisseur (pour un package tiers, consultez hello exemple suivant). Pour plus d’informations, consultez l’article [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Journalisation dans ASP.NET Core).
2. Ajouter un **à l’aide de** directive Microsoft.Extensions.Logging tooyour fichier de service.
3. Définissez une variable privée dans votre classe de service.

  ```csharp
  private ILogger _logger = null;

  ```
4. Dans le constructeur de hello de votre classe de service, ajoutez ce code :

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Démarrez l’instrumentation de votre code dans vos méthodes. Voici quelques exemples :

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Utilisation d’autres fournisseurs de journalisation

Certains fournisseurs tiers utilisent ETL hello hello précédant la section, y compris [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), et [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Vous pouvez connecter chacun d’eux à la journalisation ASP.NET Core ou les utiliser séparément. Serilog offre une fonctionnalité qui enrichit tous les messages envoyés par un enregistreur d’événements. Cette fonctionnalité peut être utile toooutput hello nom, type et les informations de partition. toouse cette fonctionnalité Bonjour infrastructure d’ASP.NET Core, procédez comme suit :

1. Ajouter hello Serilog, Serilog.Extensions.Logging, et Serilog.Sinks.Observable NuGet packages toohello projet. Par exemple suivant de hello, également ajouter Serilog.Sinks.Literate. Une meilleure approche est présentée plus loin dans cet article.
2. Dans Serilog, créez une instance de journal LoggerConfiguration et hello.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Ajoutez un constructeur de service Serilog.ILogger argument toohello et passez hello nouvellement créé enregistreur d’événements.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. Dans le constructeur du service hello, ajouter hello suivant le code qui crée hello enrichers de propriété pour hello **ServiceTypeName**, **ServiceName**, **PartitionId**et  **InstanceId** propriétés du service de hello. Il ajoute également un toohello enrichisseur de propriété fabrique de journalisation ASP.NET Core, vous pouvez donc utiliser Microsoft.Extensions.Logging.ILogger dans votre code.

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. Code de hello instrument hello même que si vous utilisez ASP.NET Core sans Serilog.

  >[!NOTE]
  >Nous recommandons que vous n’utilisez pas hello statique Log.Logger avec hello précédent exemple. L’infrastructure de service peut héberger plusieurs instances de hello même type dans un seul processus de service. Si vous utilisez hello Log.Logger statique, l’enregistreur de dernière hello d’enrichers de propriété hello affichera les valeurs pour toutes les instances qui sont en cours d’exécution. Il s’agit de l’une des raisons pour lesquelles hello _logger variable est un membre privé de la classe de service hello. En outre, vous devez vous code hello _logger toocommon disponibles, qui peut-être être utilisé entre les services.

## <a name="choosing-a-logging-provider"></a>Choix d’un fournisseur de journalisation

Si votre application repose sur des performances élevées, **EventSource** constitue généralement une bonne approche. **EventSource** *généralement* utilise moins de ressources et plus performante que ASP.NET Core journalisation ou l’une des solutions tierces disponibles de hello.  Cela ne représente pas un problème pour de nombreux services, mais si votre service est axé sur les performances, le recours à **EventSource** peut être plus judicieux. Toutefois, tooget ces avantages de structuré journalisation, **EventSource** nécessite un plus grand investissement de votre équipe d’ingénieurs. Si possible, effectuez un prototype rapide de quelques options de journalisation, puis choisissez hello qui répond le mieux à vos besoins.

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez choisi vos tooinstrument de fournisseur de journalisation de vos applications et services, événements et les journaux doivent toobe agrégée avant de la plateforme d’analyse tooany peuvent être envoyées. En savoir plus sur [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) et [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendre certains des hello options recommandée.
