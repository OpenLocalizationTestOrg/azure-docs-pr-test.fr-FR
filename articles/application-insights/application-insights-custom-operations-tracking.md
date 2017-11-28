---
title: "aaaTrack des opérations personnalisées avec Azure Application Insights .NET SDK | Documents Microsoft"
description: "Suivi des opérations personnalisées avec le kit SDK .NET d’Azure Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="0b674-103">Suivi des opérations personnalisées avec le kit SDK .NET d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="0b674-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="0b674-104">Azure SDK Application Insights automatiquement suivi HTTP entrant demande et appelle toodependent services, tels que les requêtes HTTP et les requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="0b674-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="0b674-105">Le suivi et la corrélation des demandes et des dépendances vous offrent une visibilité en réactivité et la fiabilité de l’application hello entier entre tous les microservices qui combinent cette application.</span><span class="sxs-lookup"><span data-stu-id="0b674-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="0b674-106">Il existe une classe de modèles d’application qui ne peuvent pas être pris en charge de façon générique.</span><span class="sxs-lookup"><span data-stu-id="0b674-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="0b674-107">La surveillance appropriée de ces modèles requiert une instrumentation manuelle du code.</span><span class="sxs-lookup"><span data-stu-id="0b674-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="0b674-108">Cet article traite de quelques modèles qui peuvent requérir une instrumentation manuelle, tels que le traitement de la file d’attente personnalisé et les tâches en arrière-plan à long terme en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0b674-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="0b674-109">Ce document fournit des conseils sur la tootrack des opérations personnalisées avec hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="0b674-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="0b674-110">Cette documentation concerne :</span><span class="sxs-lookup"><span data-stu-id="0b674-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="0b674-111">Application Insights pour .NET (également appelé Kit SDK de base) version 2.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0b674-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="0b674-112">Application Insights pour applications web (exécute ASP.NET) version 2.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0b674-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="0b674-113">Application Insights pour ASP.NET Core version 2.1 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="0b674-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="0b674-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0b674-114">Overview</span></span>
<span data-ttu-id="0b674-115">Une opération est un élément de travail logique exécuté par une application.</span><span class="sxs-lookup"><span data-stu-id="0b674-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="0b674-116">Il a un nom, une heure de début, une durée, un résultat et un contexte d’exécution tel qu’un nom d’utilisateur, des propriétés et un résultat.</span><span class="sxs-lookup"><span data-stu-id="0b674-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="0b674-117">Si l’opération A a été initiée par l’opération B, l’opération B est alors définie en tant que parent pour A. Une opération ne peut avoir qu’un seul parent, mais il peut avoir de nombreuses opérations enfants.</span><span class="sxs-lookup"><span data-stu-id="0b674-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="0b674-118">Pour plus d’informations sur les opérations et la corrélation de télémétrie, consultez [Corrélation de télémétrie d’Application Azure Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="0b674-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="0b674-119">Bonjour Application Insights .NET SDK, opération de hello est décrite par la classe abstraite de hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) et de ses descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) et [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="0b674-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="0b674-120">Suivi des opérations entrantes</span><span class="sxs-lookup"><span data-stu-id="0b674-120">Incoming operations tracking</span></span> 
<span data-ttu-id="0b674-121">Hello web Application Insights que SDK collecte automatiquement des requêtes HTTP pour les applications ASP.NET qui s’exécutent dans un pipeline d’IIS et toutes les applications ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0b674-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="0b674-122">Il existe des solutions prises en charge par la communauté pour les autres plateformes et infrastructures.</span><span class="sxs-lookup"><span data-stu-id="0b674-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="0b674-123">Toutefois, si l’application hello n’est pas pris en charge par les standard de hello ou pris en charge par une Communauté de solutions, vous pouvez l’instrumenter manuellement.</span><span class="sxs-lookup"><span data-stu-id="0b674-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="0b674-124">Un autre exemple nécessitant un suivi personnalisé est travail hello qui reçoit les éléments de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="0b674-125">Pour des files d’attente, hello appeler tooadd un message de file d’attente toothis est suivie en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="0b674-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="0b674-126">Toutefois, opération de haut niveau hello qui décrit le traitement des messages n’est pas collectée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0b674-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="0b674-127">Voyons comment effectuer le suivi de telles opérations.</span><span class="sxs-lookup"><span data-stu-id="0b674-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="0b674-128">Sur un niveau élevé, tâche hello est toocreate `RequestTelemetry` et définir des propriétés connues.</span><span class="sxs-lookup"><span data-stu-id="0b674-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="0b674-129">Une fois hello terminé, les données de télémétrie hello effectuer le suivi.</span><span class="sxs-lookup"><span data-stu-id="0b674-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="0b674-130">Bonjour à l’exemple suivant illustre cette tâche.</span><span class="sxs-lookup"><span data-stu-id="0b674-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="0b674-131">Requête HTTP dans une application Owin auto-hébergée</span><span class="sxs-lookup"><span data-stu-id="0b674-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="0b674-132">Dans cet exemple, nous suivons hello [le protocole HTTP pour la corrélation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="0b674-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="0b674-133">Attendez-vous à ce que les en-têtes tooreceive décrits il.</span><span class="sxs-lookup"><span data-stu-id="0b674-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="0b674-134">le protocole HTTP pour la corrélation de Hello déclare également hello `Correlation-Context` en-tête.</span><span class="sxs-lookup"><span data-stu-id="0b674-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="0b674-135">Toutefois, il est omis ici par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="0b674-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="0b674-136">Instrumentation des files d’attente</span><span class="sxs-lookup"><span data-stu-id="0b674-136">Queue instrumentation</span></span>
<span data-ttu-id="0b674-137">Pour les communications HTTP, nous avons créé un protocole toopass détails de la corrélation.</span><span class="sxs-lookup"><span data-stu-id="0b674-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="0b674-138">Avec les protocoles de certaines files d’attente, vous pouvez passer des métadonnées supplémentaires avec le message de type hello et avec d’autres que vous ne pouvez pas.</span><span class="sxs-lookup"><span data-stu-id="0b674-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="0b674-139">File d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="0b674-139">Service Bus queue</span></span>
<span data-ttu-id="0b674-140">Avec hello Azure [file d’attente Service Bus](../service-bus-messaging/index.md), vous pouvez passer un jeu de propriétés, ainsi que le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="0b674-141">Nous les utilisons ID de corrélation hello toopass.</span><span class="sxs-lookup"><span data-stu-id="0b674-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="0b674-142">file d’attente du Service Bus Hello utilise des protocoles TCP.</span><span class="sxs-lookup"><span data-stu-id="0b674-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="0b674-143">Application Insights n’effectue pas automatiquement le suivi des opérations de file d’attente, et nous devons les suivre manuellement.</span><span class="sxs-lookup"><span data-stu-id="0b674-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="0b674-144">Hello dequeue opération est une API de style push, et nous sommes tootrack Impossible d’elle.</span><span class="sxs-lookup"><span data-stu-id="0b674-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="0b674-145">Enqueue (empiler)</span><span class="sxs-lookup"><span data-stu-id="0b674-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="0b674-146">Process</span><span class="sxs-lookup"><span data-stu-id="0b674-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="0b674-147">File d’attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0b674-147">Azure Storage queue</span></span>
<span data-ttu-id="0b674-148">Hello suivant montre l’exemple de comment tootrack hello [file d’attente de stockage Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) opérations et mettre en corrélation télémétrie entre le producteur de hello, hello consommateur et le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0b674-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="0b674-149">file d’attente de stockage Hello a une API HTTP.</span><span class="sxs-lookup"><span data-stu-id="0b674-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="0b674-150">File d’attente de tous les appels toohello sont suivies par hello Application Insights dépendance collecteur pour les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="0b674-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="0b674-151">Préparez-vous.Assurez-vous que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` se trouve dans `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="0b674-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="0b674-152">Si vous n’est pas installé, l’ajouter par programmation, comme décrit dans [de filtrage et de prétraitement Bonjour Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="0b674-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="0b674-153">Si vous configurez manuellement Application Insights, assurez-vous de créer et d’initialiser `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de façon semblable au code suivant :</span><span class="sxs-lookup"><span data-stu-id="0b674-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="0b674-154">Vous pouvez aussi hello toocorrelate Application Insights l’ID d’opération avec l’ID de demande de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="0b674-155">Pour plus d’informations sur comment tooset et obtenir un stockage de demande client et un ID de demande de serveur, consultez [moniteur, diagnostiquer et résoudre les problèmes de stockage Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="0b674-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="0b674-156">Enqueue (empiler)</span><span class="sxs-lookup"><span data-stu-id="0b674-156">Enqueue</span></span>
<span data-ttu-id="0b674-157">Les files d’attente de stockage prenant en charge les API HTTP de hello, toutes les opérations de file d’attente hello sont automatiquement suivies par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="0b674-158">Dans de nombreux cas, cette instrumentation doit être suffisante.</span><span class="sxs-lookup"><span data-stu-id="0b674-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="0b674-159">Toutefois, toocorrelate effectue le suivi sur le côté du consommateur hello avec les traces producteur, vous devez passer un contexte de corrélation de même toohow nous faire Bonjour le protocole HTTP pour la corrélation.</span><span class="sxs-lookup"><span data-stu-id="0b674-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="0b674-160">Dans cet exemple, nous avons suivi hello facultatif `Enqueue` opération.</span><span class="sxs-lookup"><span data-stu-id="0b674-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="0b674-161">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="0b674-161">You can:</span></span>

 - <span data-ttu-id="0b674-162">**Mettre en corrélation des nouvelles tentatives (le cas échéant)**: ils ont tous un parent commun qui est hello `Enqueue` opération.</span><span class="sxs-lookup"><span data-stu-id="0b674-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="0b674-163">Dans le cas contraire, elles sont suivies en tant qu’enfants de la demande entrante de hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="0b674-164">S’il existe de file d’attente de plusieurs demandes logique toohello, il peut être difficile toofind quel appel a généré de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="0b674-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="0b674-165">**Mettre en corrélation les journaux de stockage Azure (si nécessaire)** : elles sont mises en corrélation avec la télémétrie Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="0b674-166">Hello `Enqueue` opération est enfant hello d’une opération de parent (par exemple, une demande HTTP entrante).</span><span class="sxs-lookup"><span data-stu-id="0b674-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="0b674-167">appel de dépendance Hello HTTP est enfant hello hello `Enqueue` opération et hello petits-enfants de demande entrante de hello :</span><span class="sxs-lookup"><span data-stu-id="0b674-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="0b674-168">quantité de hello tooreduce de télémétrie signale de votre application ou si vous ne souhaitez pas tootrack hello `Enqueue` opération pour d’autres raisons, utilisez hello `Activity` directement les API :</span><span class="sxs-lookup"><span data-stu-id="0b674-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="0b674-169">Créer (et démarrer) un nouveau `Activity` au lieu de démarrer l’opération d’Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="0b674-170">Vous faire *pas* devez tooassign toutes les propriétés sur celui-ci, à l’exception du nom de l’opération hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="0b674-171">Sérialiser `yourActivity.Id` dans la charge utile du message hello au lieu de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="0b674-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="0b674-172">Vous pouvez également utiliser `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="0b674-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="0b674-173">Dequeue (Enlever de la file d’attente)</span><span class="sxs-lookup"><span data-stu-id="0b674-173">Dequeue</span></span>
<span data-ttu-id="0b674-174">De même trop`Enqueue`, une file d’attente de stockage toohello réel HTTP demande automatiquement suivi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="0b674-175">Toutefois, hello `Enqueue` vraisemblablement, opération qui se produit dans le contexte parent hello, par exemple un contexte de demande entrant.</span><span class="sxs-lookup"><span data-stu-id="0b674-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="0b674-176">SDK application Insights mettre en corrélation automatiquement une telle opération (et sa partie HTTP) avec la demande de parent hello et autres données de télémétrie signalé Bonjour même étendue.</span><span class="sxs-lookup"><span data-stu-id="0b674-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="0b674-177">Hello `Dequeue` opération est difficile.</span><span class="sxs-lookup"><span data-stu-id="0b674-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="0b674-178">Hello Application Insights SDK effectue automatiquement le suivi des demandes HTTP.</span><span class="sxs-lookup"><span data-stu-id="0b674-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="0b674-179">Toutefois, il ne sait pas contexte de corrélation hello jusqu'à ce que le message de type hello est analysé.</span><span class="sxs-lookup"><span data-stu-id="0b674-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="0b674-180">Il n’est pas possible de toocorrelate hello HTTP demande tooget message de type hello avec rest hello de télémétrie de hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="0b674-181">Dans de nombreux cas, il peut être utile toocorrelate hello HTTP toohello file d’attente avec d’autres traces ainsi.</span><span class="sxs-lookup"><span data-stu-id="0b674-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="0b674-182">Hello exemple suivant montre comment toodo il :</span><span class="sxs-lookup"><span data-stu-id="0b674-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="0b674-183">Process</span><span class="sxs-lookup"><span data-stu-id="0b674-183">Process</span></span>

<span data-ttu-id="0b674-184">Bonjour l’exemple suivant, nous avons un message entrant de trace d’une manière de même demander toohow nous trace HTTP entrant :</span><span class="sxs-lookup"><span data-stu-id="0b674-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="0b674-185">De même, les autres opérations de file d’attente peuvent être instrumentées.</span><span class="sxs-lookup"><span data-stu-id="0b674-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="0b674-186">Une opération d’aperçu doit être instrumentée de façon similaire à un retrait de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="0b674-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="0b674-187">L’instrumentation des opérations de gestion de file d’attente n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0b674-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="0b674-188">Application Insights effectue le suivi d’opérations telles que HTTP et, dans la plupart des cas, cela suffit.</span><span class="sxs-lookup"><span data-stu-id="0b674-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="0b674-189">Lorsque vous instrumentez la suppression du message, assurez-vous que vous définissez les opération hello les identificateurs (corrélation).</span><span class="sxs-lookup"><span data-stu-id="0b674-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="0b674-190">Vous pouvez également utiliser hello `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="0b674-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="0b674-191">Vous ne devez pas les identificateurs d’opération tooset sur les éléments de télémétrie hello, car l’Application Insights fait pour vous :</span><span class="sxs-lookup"><span data-stu-id="0b674-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="0b674-192">Créer un nouveau `Activity` une fois que vous avez un élément de file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="0b674-193">Utilisez `Activity.SetParentId(message.ParentId)` toocorrelate les journaux producteur et consommateur.</span><span class="sxs-lookup"><span data-stu-id="0b674-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="0b674-194">Démarrer hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="0b674-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="0b674-195">Effectuez le suivi des opérations de retrait de file d’attente, de traitement et de suppression à l’aide des programmes d’assistance `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="0b674-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="0b674-196">Le faire à partir de hello asynchrone même contrôler les flux (contexte d’exécution).</span><span class="sxs-lookup"><span data-stu-id="0b674-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="0b674-197">De cette manière, elles sont correctement mises en corrélation.</span><span class="sxs-lookup"><span data-stu-id="0b674-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="0b674-198">Arrêt hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="0b674-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="0b674-199">Utilisez `Start/StopOperation` ou appelez manuellement la télémétrie `Track`.</span><span class="sxs-lookup"><span data-stu-id="0b674-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="0b674-200">Traitement par lots</span><span class="sxs-lookup"><span data-stu-id="0b674-200">Batch processing</span></span>
<span data-ttu-id="0b674-201">Avec des files d’attente, vous pouvez retirer plusieurs messages de la file d’attente avec une seule demande.</span><span class="sxs-lookup"><span data-stu-id="0b674-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="0b674-202">Traitement des messages de ce type est sans doute indépendant et appartient toohello les opérations logiques différents.</span><span class="sxs-lookup"><span data-stu-id="0b674-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="0b674-203">Dans ce cas, il n’est pas possible de toocorrelate hello `Dequeue` le traitement des messages tooparticular opération.</span><span class="sxs-lookup"><span data-stu-id="0b674-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="0b674-204">Chaque traitement de message doit être traité dans son propre flux de contrôle asynchrone.</span><span class="sxs-lookup"><span data-stu-id="0b674-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="0b674-205">Pour plus d’informations, consultez hello [dépendances sortantes suivi](#outgoing-dependencies-tracking) section.</span><span class="sxs-lookup"><span data-stu-id="0b674-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="0b674-206">Tâches en arrière-plan à long terme</span><span class="sxs-lookup"><span data-stu-id="0b674-206">Long-running background tasks</span></span>
<span data-ttu-id="0b674-207">Certaines applications démarrent des opérations à long terme qui peuvent être dues à des demandes de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0b674-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="0b674-208">Hello/instrumentation de traçage du point de vue, il n’est pas différente de l’instrumentation de demande ou la dépendance :</span><span class="sxs-lookup"><span data-stu-id="0b674-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="0b674-209">Dans cet exemple, nous utilisons `telemetryClient.StartOperation` toocreate `RequestTelemetry` et le contexte de corrélation de remplissage hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="0b674-210">Supposons que vous avez une opération parent qui a été créée par les demandes entrantes qui hello opération planifiée.</span><span class="sxs-lookup"><span data-stu-id="0b674-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="0b674-211">Tant que `BackgroundTask` commence dans hello même flux de contrôle asynchrone en tant qu’une demande entrante, il est mis en corrélation avec cette opération parent.</span><span class="sxs-lookup"><span data-stu-id="0b674-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="0b674-212">`BackgroundTask`et tous les éléments de télémétrie imbriquées sont automatiquement mis en corrélation avec demande hello à l’origine, même après la fin de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="0b674-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="0b674-213">Démarrage de la tâche hello à partir du thread d’arrière-plan hello n’a aucune opération (`Activity`) associé, `BackgroundTask` dépourvu de tout parent.</span><span class="sxs-lookup"><span data-stu-id="0b674-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="0b674-214">Toutefois, il peut avoir plusieurs opérations imbriquées.</span><span class="sxs-lookup"><span data-stu-id="0b674-214">However, it can have nested operations.</span></span> <span data-ttu-id="0b674-215">Tous les éléments de télémétrie signalées à partir de la tâche hello sont corrélé toohello `RequestTelemetry` créé dans `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="0b674-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="0b674-216">Suivi des dépendances sortantes</span><span class="sxs-lookup"><span data-stu-id="0b674-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="0b674-217">Vous pouvez effectuer le suivi de votre propre genre de dépendance ou d’une opération qui n’est pas prise en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="0b674-218">Hello `Enqueue` méthode dans la file d’attente du Service Bus hello ou file d’attente de stockage hello peut servir d’exemples pour ce type de suivi personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0b674-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="0b674-219">Bonjour général personnalisé suivi des dépendances consiste à :</span><span class="sxs-lookup"><span data-stu-id="0b674-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="0b674-220">Appelez hello `TelemetryClient.StartOperation` (méthode) (extension) qui remplit hello `DependencyTelemetry` propriétés qui sont nécessaires pour la corrélation et d’autres propriétés (heure de début de marqueur, la durée).</span><span class="sxs-lookup"><span data-stu-id="0b674-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="0b674-221">Définir d’autres propriétés personnalisées sur hello `DependencyTelemetry`, tels que le nom de hello et un autre contexte que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="0b674-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="0b674-222">Effectuez un appel de dépendance et attendez les résultats.</span><span class="sxs-lookup"><span data-stu-id="0b674-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="0b674-223">Arrêter l’opération hello avec `StopOperation` quand elle est terminée.</span><span class="sxs-lookup"><span data-stu-id="0b674-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="0b674-224">Traitez les exceptions.</span><span class="sxs-lookup"><span data-stu-id="0b674-224">Handle exceptions.</span></span>

<span data-ttu-id="0b674-225">`StopOperation`uniquement interrompt hello qui a été démarrée.</span><span class="sxs-lookup"><span data-stu-id="0b674-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="0b674-226">Si opération en cours d’exécution en cours de hello ne correspond pas hello une souhaité toostop, `StopOperation` n’exécute aucune opération.</span><span class="sxs-lookup"><span data-stu-id="0b674-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="0b674-227">Cette situation peut se produire si vous démarrez plusieurs opérations en parallèle dans hello même contexte d’exécution :</span><span class="sxs-lookup"><span data-stu-id="0b674-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="0b674-228">Assurez-vous de toujours appeler `StartOperation` et d’exécuter votre tâche dans son propre contexte :</span><span class="sxs-lookup"><span data-stu-id="0b674-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0b674-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b674-229">Next steps</span></span>

- <span data-ttu-id="0b674-230">Principes fondamentaux de hello [corrélation de télémétrie](application-insights-correlation.md) dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="0b674-231">Consultez hello [modèle de données](application-insights-data-model.md) pour le modèle de données et les types d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="0b674-232">Rapport personnalisé [événements et métriques](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="0b674-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="0b674-233">Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) standard de la collection de propriétés de contexte.</span><span class="sxs-lookup"><span data-stu-id="0b674-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="0b674-234">Vérifiez hello [Guide de l’utilisateur System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee comment nous mettre en corrélation les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="0b674-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
