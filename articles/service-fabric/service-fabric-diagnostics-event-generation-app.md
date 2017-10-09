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
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="ce143-103">Génération de journaux et d’événements de niveau application et service</span><span class="sxs-lookup"><span data-stu-id="ce143-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="ce143-104">L’instrumentation de code hello avec des événements personnalisés</span><span class="sxs-lookup"><span data-stu-id="ce143-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="ce143-105">Instrumentation de hello code sert hello pour la plupart des autres aspects de vos services d’analyse.</span><span class="sxs-lookup"><span data-stu-id="ce143-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="ce143-106">L’instrumentation est hello seule façon que vous saurez que pose problème, et toodiagnose, ce qui doit toobe fixe.</span><span class="sxs-lookup"><span data-stu-id="ce143-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="ce143-107">Bien que techniquement possible tooconnect un service de débogueur tooa production, il n’est pas une pratique courante.</span><span class="sxs-lookup"><span data-stu-id="ce143-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="ce143-108">Par conséquent, il est important de disposer de données d’instrumentation détaillées.</span><span class="sxs-lookup"><span data-stu-id="ce143-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="ce143-109">Certains produits instrumentent automatiquement votre code.</span><span class="sxs-lookup"><span data-stu-id="ce143-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="ce143-110">Bien que ces solutions soient très efficaces, une instrumentation manuelle est presque toujours nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ce143-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="ce143-111">Final de hello, vous devez disposer d’assez tooforensically informations déboguer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="ce143-112">Ce document décrit les différentes approches tooinstrumenting votre code, et lorsque toochoose une approche vers un autre.</span><span class="sxs-lookup"><span data-stu-id="ce143-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="ce143-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="ce143-113">EventSource</span></span>
<span data-ttu-id="ce143-114">Lorsque vous créez une solution Service Fabric à partir d’un modèle dans Visual Studio, une classe dérivée **EventSource** (**ServiceEventSource** ou **ActorEventSource**) est générée.</span><span class="sxs-lookup"><span data-stu-id="ce143-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="ce143-115">Un modèle dans lequel vous pouvez ajouter des événements pour votre application ou votre service est créé.</span><span class="sxs-lookup"><span data-stu-id="ce143-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="ce143-116">Hello **EventSource** nom **doit** être unique et doit être renommé à partir de la chaîne de modèle par défaut hello MyCompany -&lt;solution&gt; - &lt; projet&gt;.</span><span class="sxs-lookup"><span data-stu-id="ce143-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="ce143-117">Présence de plusieurs **EventSource** définitions qui utilisent hello même causes nom un problème au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce143-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="ce143-118">Chaque événement défini doit avoir un identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="ce143-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="ce143-119">Si l’identificateur n’est pas unique, l’exécution échoue.</span><span class="sxs-lookup"><span data-stu-id="ce143-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="ce143-120">Certaines organisations preassign des plages de valeurs pour les conflits de tooavoid identificateurs entre les équipes de développement distinct.</span><span class="sxs-lookup"><span data-stu-id="ce143-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="ce143-121">Pour plus d’informations, consultez [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou hello [documentation MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="ce143-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="ce143-122">Utilisation d’événements EventSource structurés</span><span class="sxs-lookup"><span data-stu-id="ce143-122">Using structured EventSource events</span></span>

<span data-ttu-id="ce143-123">Chacun des événements hello dans les exemples de code hello dans cette section sont définis pour un incident spécifique, par exemple, lorsqu’un type de service est enregistré.</span><span class="sxs-lookup"><span data-stu-id="ce143-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="ce143-124">Lorsque vous définissez des messages en cas d’usage, de données peuvent être empaquetées avec texte hello d’erreur de hello, et vous pouvez plus facilement rechercher et filtre basé sur les noms de hello ou les valeurs de hello les propriétés spécifiées.</span><span class="sxs-lookup"><span data-stu-id="ce143-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="ce143-125">Structuration de sortie d’instrumentation hello rend tooconsume plus facile, mais nécessite plus de réflexion et une heure toodefine un nouvel événement pour chaque cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="ce143-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="ce143-126">Des définitions d’événement peuvent être partagées entre l’ensemble de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="ce143-127">Par exemple, un événement de commencement ou d’arrêt de méthode peut être réutilisé dans plusieurs services d’une même application.</span><span class="sxs-lookup"><span data-stu-id="ce143-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="ce143-128">Un service spécifique d’un domaine, comme un système de commande, peut est associé à un événement **CreateOrder**, qui présente son propre événement unique.</span><span class="sxs-lookup"><span data-stu-id="ce143-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="ce143-129">Cette approche est susceptible de générer de nombreux événements et peut requérir la coordination des identificateurs entre les équipes de projet.</span><span class="sxs-lookup"><span data-stu-id="ce143-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

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

### <a name="using-eventsource-generically"></a><span data-ttu-id="ce143-130">Utilisation générale d’EventSource</span><span class="sxs-lookup"><span data-stu-id="ce143-130">Using EventSource generically</span></span>

<span data-ttu-id="ce143-131">Étant donné la complexité de la définition d’événements spécifiques, de nombreuses personnes définissent quelques événements avec un ensemble commun de paramètres qui sortent généralement les informations sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ce143-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="ce143-132">Une grande partie de l’aspect de hello structuré est perdue, et il est plus difficiles toosearch et filtre hello les résultats.</span><span class="sxs-lookup"><span data-stu-id="ce143-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="ce143-133">Dans cette approche, quelques événements qui correspondent généralement des niveaux de journalisation de toohello sont définis.</span><span class="sxs-lookup"><span data-stu-id="ce143-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="ce143-134">Hello suivant extrait de code définit un message d’erreur et de débogage :</span><span class="sxs-lookup"><span data-stu-id="ce143-134">hello following snippet defines a debug and error message:</span></span>

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

<span data-ttu-id="ce143-135">Une approche hybride d’instrumentation structurée et générique peut aussi fonctionner.</span><span class="sxs-lookup"><span data-stu-id="ce143-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="ce143-136">L’instrumentation structurée sert à créer des rapports sur les erreurs et les mesures.</span><span class="sxs-lookup"><span data-stu-id="ce143-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="ce143-137">Événements génériques peuvent être utilisés pour hello détaillée journalisation qui est consommée par les ingénieurs de dépannage.</span><span class="sxs-lookup"><span data-stu-id="ce143-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="ce143-138">Journalisation ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ce143-138">ASP.NET Core logging</span></span>

<span data-ttu-id="ce143-139">Toocarefully important son plan vous serez comment instrumenter votre code.</span><span class="sxs-lookup"><span data-stu-id="ce143-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="ce143-140">plan d’instrumentation droite Hello peut vous aider à éviter potentiellement déstabiliser votre base de code et puis avoir besoin de code de hello tooreinstrument.</span><span class="sxs-lookup"><span data-stu-id="ce143-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="ce143-141">tooreduce risque, vous pouvez choisir une bibliothèque d’instrumentation, par exemple [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), qui fait partie de Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="ce143-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="ce143-142">ASP.NET Core a un [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que vous pouvez utiliser avec le fournisseur hello de votre choix, tout en réduisant les effets de hello sur du code existant.</span><span class="sxs-lookup"><span data-stu-id="ce143-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="ce143-143">Vous pouvez utiliser du code hello dans ASP.NET Core sur Windows et Linux et Bonjour complète .NET Framework, donc votre code d’instrumentation est normalisé.</span><span class="sxs-lookup"><span data-stu-id="ce143-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="ce143-144">Cette opération est examinée plus en détail ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ce143-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="ce143-145">Utilisation de Microsoft.Extensions.Logging dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ce143-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="ce143-146">Ajoutez hello Microsoft.Extensions.Logging NuGet package toohello projet tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="ce143-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="ce143-147">En outre, ajoutez tous les packages de fournisseur (pour un package tiers, consultez hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="ce143-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="ce143-148">Pour plus d’informations, consultez l’article [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging) (Journalisation dans ASP.NET Core).</span><span class="sxs-lookup"><span data-stu-id="ce143-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="ce143-149">Ajouter un **à l’aide de** directive Microsoft.Extensions.Logging tooyour fichier de service.</span><span class="sxs-lookup"><span data-stu-id="ce143-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="ce143-150">Définissez une variable privée dans votre classe de service.</span><span class="sxs-lookup"><span data-stu-id="ce143-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="ce143-151">Dans le constructeur de hello de votre classe de service, ajoutez ce code :</span><span class="sxs-lookup"><span data-stu-id="ce143-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="ce143-152">Démarrez l’instrumentation de votre code dans vos méthodes.</span><span class="sxs-lookup"><span data-stu-id="ce143-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="ce143-153">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="ce143-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="ce143-154">Utilisation d’autres fournisseurs de journalisation</span><span class="sxs-lookup"><span data-stu-id="ce143-154">Using other logging providers</span></span>

<span data-ttu-id="ce143-155">Certains fournisseurs tiers utilisent ETL hello hello précédant la section, y compris [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), et [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="ce143-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="ce143-156">Vous pouvez connecter chacun d’eux à la journalisation ASP.NET Core ou les utiliser séparément.</span><span class="sxs-lookup"><span data-stu-id="ce143-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="ce143-157">Serilog offre une fonctionnalité qui enrichit tous les messages envoyés par un enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="ce143-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="ce143-158">Cette fonctionnalité peut être utile toooutput hello nom, type et les informations de partition.</span><span class="sxs-lookup"><span data-stu-id="ce143-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="ce143-159">toouse cette fonctionnalité Bonjour infrastructure d’ASP.NET Core, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce143-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="ce143-160">Ajouter hello Serilog, Serilog.Extensions.Logging, et Serilog.Sinks.Observable NuGet packages toohello projet.</span><span class="sxs-lookup"><span data-stu-id="ce143-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="ce143-161">Par exemple suivant de hello, également ajouter Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="ce143-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="ce143-162">Une meilleure approche est présentée plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ce143-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="ce143-163">Dans Serilog, créez une instance de journal LoggerConfiguration et hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="ce143-164">Ajoutez un constructeur de service Serilog.ILogger argument toohello et passez hello nouvellement créé enregistreur d’événements.</span><span class="sxs-lookup"><span data-stu-id="ce143-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="ce143-165">Dans le constructeur du service hello, ajouter hello suivant le code qui crée hello enrichers de propriété pour hello **ServiceTypeName**, **ServiceName**, **PartitionId**et  **InstanceId** propriétés du service de hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="ce143-166">Il ajoute également un toohello enrichisseur de propriété fabrique de journalisation ASP.NET Core, vous pouvez donc utiliser Microsoft.Extensions.Logging.ILogger dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ce143-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="ce143-167">Code de hello instrument hello même que si vous utilisez ASP.NET Core sans Serilog.</span><span class="sxs-lookup"><span data-stu-id="ce143-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="ce143-168">Nous recommandons que vous n’utilisez pas hello statique Log.Logger avec hello précédent exemple.</span><span class="sxs-lookup"><span data-stu-id="ce143-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="ce143-169">L’infrastructure de service peut héberger plusieurs instances de hello même type dans un seul processus de service.</span><span class="sxs-lookup"><span data-stu-id="ce143-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="ce143-170">Si vous utilisez hello Log.Logger statique, l’enregistreur de dernière hello d’enrichers de propriété hello affichera les valeurs pour toutes les instances qui sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ce143-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="ce143-171">Il s’agit de l’une des raisons pour lesquelles hello _logger variable est un membre privé de la classe de service hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="ce143-172">En outre, vous devez vous code hello _logger toocommon disponibles, qui peut-être être utilisé entre les services.</span><span class="sxs-lookup"><span data-stu-id="ce143-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="ce143-173">Choix d’un fournisseur de journalisation</span><span class="sxs-lookup"><span data-stu-id="ce143-173">Choosing a logging provider</span></span>

<span data-ttu-id="ce143-174">Si votre application repose sur des performances élevées, **EventSource** constitue généralement une bonne approche.</span><span class="sxs-lookup"><span data-stu-id="ce143-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="ce143-175">**EventSource** *généralement* utilise moins de ressources et plus performante que ASP.NET Core journalisation ou l’une des solutions tierces disponibles de hello.</span><span class="sxs-lookup"><span data-stu-id="ce143-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="ce143-176">Cela ne représente pas un problème pour de nombreux services, mais si votre service est axé sur les performances, le recours à **EventSource** peut être plus judicieux.</span><span class="sxs-lookup"><span data-stu-id="ce143-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="ce143-177">Toutefois, tooget ces avantages de structuré journalisation, **EventSource** nécessite un plus grand investissement de votre équipe d’ingénieurs.</span><span class="sxs-lookup"><span data-stu-id="ce143-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="ce143-178">Si possible, effectuez un prototype rapide de quelques options de journalisation, puis choisissez hello qui répond le mieux à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ce143-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce143-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce143-179">Next steps</span></span>

<span data-ttu-id="ce143-180">Une fois que vous avez choisi vos tooinstrument de fournisseur de journalisation de vos applications et services, événements et les journaux doivent toobe agrégée avant de la plateforme d’analyse tooany peuvent être envoyées.</span><span class="sxs-lookup"><span data-stu-id="ce143-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="ce143-181">En savoir plus sur [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) et [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter comprendre certains des hello options recommandée.</span><span class="sxs-lookup"><span data-stu-id="ce143-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
