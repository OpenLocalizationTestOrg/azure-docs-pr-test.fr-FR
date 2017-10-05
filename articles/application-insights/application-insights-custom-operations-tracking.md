---
title: "Suivi des opérations personnalisées avec le kit SDK .NET d’Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="294ab-103">Suivi des opérations personnalisées avec le kit SDK .NET d’Application Insights</span><span class="sxs-lookup"><span data-stu-id="294ab-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="294ab-104">Les kits SDK d’Application Azure Insights effectuent automatiquement le suivi des appels et demandes HTTP entrants à des services dépendants, par exemple, des requêtes HTTP ou des requêtes SQL.</span><span class="sxs-lookup"><span data-stu-id="294ab-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="294ab-105">Le suivi et la corrélation des demandes et des dépendances vous offrent une meilleure visibilité de la réactivité et de la fiabilité de l’application entière sur l’ensemble des micro-services qui combinent cette application.</span><span class="sxs-lookup"><span data-stu-id="294ab-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="294ab-106">Il existe une classe de modèles d’application qui ne peuvent pas être pris en charge de façon générique.</span><span class="sxs-lookup"><span data-stu-id="294ab-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="294ab-107">La surveillance appropriée de ces modèles requiert une instrumentation manuelle du code.</span><span class="sxs-lookup"><span data-stu-id="294ab-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="294ab-108">Cet article traite de quelques modèles qui peuvent requérir une instrumentation manuelle, tels que le traitement de la file d’attente personnalisé et les tâches en arrière-plan à long terme en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="294ab-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="294ab-109">Ce document fournit des conseils sur la façon d’effectuer le suivi d’opérations personnalisées avec le kit SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="294ab-110">Cette documentation concerne :</span><span class="sxs-lookup"><span data-stu-id="294ab-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="294ab-111">Application Insights pour .NET (également appelé Kit SDK de base) version 2.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="294ab-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="294ab-112">Application Insights pour applications web (exécute ASP.NET) version 2.4 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="294ab-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="294ab-113">Application Insights pour ASP.NET Core version 2.1 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="294ab-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="294ab-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="294ab-114">Overview</span></span>
<span data-ttu-id="294ab-115">Une opération est un élément de travail logique exécuté par une application.</span><span class="sxs-lookup"><span data-stu-id="294ab-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="294ab-116">Il a un nom, une heure de début, une durée, un résultat et un contexte d’exécution tel qu’un nom d’utilisateur, des propriétés et un résultat.</span><span class="sxs-lookup"><span data-stu-id="294ab-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="294ab-117">Si l’opération A a été initiée par l’opération B, l’opération B est alors définie en tant que parent pour A. Une opération ne peut avoir qu’un seul parent, mais il peut avoir de nombreuses opérations enfants.</span><span class="sxs-lookup"><span data-stu-id="294ab-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="294ab-118">Pour plus d’informations sur les opérations et la corrélation de télémétrie, consultez [Corrélation de télémétrie d’Application Azure Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="294ab-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="294ab-119">Dans le kit SDK .NET d’Application Insights, l’opération est décrite par la classe abstraite [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) et par ses descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) et [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="294ab-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="294ab-120">Suivi des opérations entrantes</span><span class="sxs-lookup"><span data-stu-id="294ab-120">Incoming operations tracking</span></span> 
<span data-ttu-id="294ab-121">Le kit SDK web d’Application Insights collecte automatiquement des requêtes HTTP pour les applications ASP.NET qui s’exécutent dans un pipeline IIS et toutes les applications ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="294ab-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="294ab-122">Il existe des solutions prises en charge par la communauté pour les autres plateformes et infrastructures.</span><span class="sxs-lookup"><span data-stu-id="294ab-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="294ab-123">Toutefois, si l’application n’est prise en charge par aucune solution standard ni prise en charge par la communauté, vous pouvez l’instrumenter manuellement.</span><span class="sxs-lookup"><span data-stu-id="294ab-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="294ab-124">Un autre exemple nécessitant un suivi personnalisé est le Worker qui reçoit des éléments de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="294ab-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="294ab-125">Pour certaines files d’attente, l’appel visant à ajouter un message à cette file d’attente est comptabilisé en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="294ab-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="294ab-126">Toutefois, l’opération de haut niveau qui décrit le traitement des messages n’est pas collectée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="294ab-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="294ab-127">Voyons comment effectuer le suivi de telles opérations.</span><span class="sxs-lookup"><span data-stu-id="294ab-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="294ab-128">À un niveau élevé, la tâche consiste à créer `RequestTelemetry` et à définir les propriétés connues.</span><span class="sxs-lookup"><span data-stu-id="294ab-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="294ab-129">Une fois l’opération terminée, vous réalisez un suivi de la télémétrie.</span><span class="sxs-lookup"><span data-stu-id="294ab-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="294ab-130">L’exemple suivant illustre ce cas de figure.</span><span class="sxs-lookup"><span data-stu-id="294ab-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="294ab-131">Requête HTTP dans une application Owin auto-hébergée</span><span class="sxs-lookup"><span data-stu-id="294ab-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="294ab-132">Dans cet exemple, nous suivons le [protocole HTTP pour la corrélation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="294ab-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="294ab-133">Attendez-vous à recevoir les en-têtes décrites ici.</span><span class="sxs-lookup"><span data-stu-id="294ab-133">You should expect to receive headers that are described there.</span></span>

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

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
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

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="294ab-134">Le protocole HTTP pour la corrélation déclare également l’en-tête `Correlation-Context`.</span><span class="sxs-lookup"><span data-stu-id="294ab-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="294ab-135">Toutefois, il est omis ici par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="294ab-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="294ab-136">Instrumentation des files d’attente</span><span class="sxs-lookup"><span data-stu-id="294ab-136">Queue instrumentation</span></span>
<span data-ttu-id="294ab-137">Pour la communication HTTP, nous avons créé un protocole pour transmettre les détails de corrélation.</span><span class="sxs-lookup"><span data-stu-id="294ab-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="294ab-138">Avec certains protocoles de files d’attente, vous pouvez transmettre des métadonnées supplémentaires avec le message tandis que d’autres ne le permettent pas.</span><span class="sxs-lookup"><span data-stu-id="294ab-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="294ab-139">File d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="294ab-139">Service Bus queue</span></span>
<span data-ttu-id="294ab-140">Avec la [file d’attente Service Bus](../service-bus-messaging/index.md) Azure, vous pouvez envoyer un ensemble de propriétés avec le message.</span><span class="sxs-lookup"><span data-stu-id="294ab-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="294ab-141">Nous l’utilisons pour transmettre l’ID de corrélation.</span><span class="sxs-lookup"><span data-stu-id="294ab-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="294ab-142">La file d’attente Service Bus utilise des protocoles TCP.</span><span class="sxs-lookup"><span data-stu-id="294ab-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="294ab-143">Application Insights n’effectue pas automatiquement le suivi des opérations de file d’attente, et nous devons les suivre manuellement.</span><span class="sxs-lookup"><span data-stu-id="294ab-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="294ab-144">L’opération de retrait de file d’attente est une API de style push et nous ne sommes pas en mesure d’effectuer son suivi.</span><span class="sxs-lookup"><span data-stu-id="294ab-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="294ab-145">Enqueue (empiler)</span><span class="sxs-lookup"><span data-stu-id="294ab-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
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

#### <a name="process"></a><span data-ttu-id="294ab-146">Process</span><span class="sxs-lookup"><span data-stu-id="294ab-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="294ab-147">File d’attente de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="294ab-147">Azure Storage queue</span></span>
<span data-ttu-id="294ab-148">L’exemple suivant montre comment effectuer le suivi des opérations de [file d’attente de stockage Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) et mettre en corrélation la télémétrie entre le producteur, le consommateur et le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="294ab-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="294ab-149">La file d’attente de stockage dispose d’une API HTTP.</span><span class="sxs-lookup"><span data-stu-id="294ab-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="294ab-150">Tous les appels vers la file d’attente sont suivis par le collecteur de dépendance Application Insights pour les requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="294ab-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="294ab-151">Préparez-vous.Assurez-vous que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` se trouve dans `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="294ab-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="294ab-152">Si ce n’est pas le cas, ajoutez-le par programmation dans [Filtrage et prétraitement dans le kit SDK d’Application Azure Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="294ab-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="294ab-153">Si vous configurez manuellement Application Insights, assurez-vous de créer et d’initialiser `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de façon semblable au code suivant :</span><span class="sxs-lookup"><span data-stu-id="294ab-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="294ab-154">Vous pouvez également mettre en corrélation l’ID d’opération Application Insights avec l’ID de demande de stockage.</span><span class="sxs-lookup"><span data-stu-id="294ab-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="294ab-155">Pour plus d’informations sur la définition et obtention d’un client de demande de stockage et un ID de demande de serveur, consultez [Surveiller, diagnostiquer et dépanner Stockage Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="294ab-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="294ab-156">Enqueue (empiler)</span><span class="sxs-lookup"><span data-stu-id="294ab-156">Enqueue</span></span>
<span data-ttu-id="294ab-157">Étant donné que les files d’attente de stockage prennent en charge l’API HTTP, toutes les opérations mettant en jeu la file d’attente sont automatiquement suivies par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="294ab-158">Dans de nombreux cas, cette instrumentation doit être suffisante.</span><span class="sxs-lookup"><span data-stu-id="294ab-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="294ab-159">Toutefois, pour mettre en corrélation les traces côté client avec les traces du producteur, vous devez transmettre un contexte de corrélation de façon similaire à la manière utilisée dans le Protocole HTTP pour la corrélation.</span><span class="sxs-lookup"><span data-stu-id="294ab-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="294ab-160">Dans cet exemple, nous avons suivi l’opération facultative `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="294ab-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="294ab-161">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="294ab-161">You can:</span></span>

 - <span data-ttu-id="294ab-162">**Mettre en corrélation les nouvelles tentatives (le cas échéant)** : elles ont toutes un parent commun qui est l’opération `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="294ab-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="294ab-163">Dans le cas contraire, elles sont comptabilisées en tant qu’enfants de la demande entrante.</span><span class="sxs-lookup"><span data-stu-id="294ab-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="294ab-164">S’il existe plusieurs demandes logiques pour la file d’attente, il pourrait être difficile de trouver quel appel a généré de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="294ab-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="294ab-165">**Mettre en corrélation les journaux de stockage Azure (si nécessaire)** : elles sont mises en corrélation avec la télémétrie Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="294ab-166">L’opération `Enqueue` est l’enfant d’une opération parent (par exemple, une demande HTTP entrante).</span><span class="sxs-lookup"><span data-stu-id="294ab-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="294ab-167">L’appel de dépendance HTTP est l’enfant de l’opération `Enqueue` et le petit-enfant de la demande entrante :</span><span class="sxs-lookup"><span data-stu-id="294ab-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="294ab-168">Pour réduire la quantité de données de télémétrie que votre application signale ou si vous ne souhaitez pas suivre l’opération `Enqueue` pour d’autres raisons, utilisez directement l’API `Activity` :</span><span class="sxs-lookup"><span data-stu-id="294ab-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="294ab-169">Créez (et démarrez) une nouvelle opération `Activity` au lieu de démarrer l’opération Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="294ab-170">Il n’est *pas* nécessaire de lui assigner des propriétés à part le nom d’opération.</span><span class="sxs-lookup"><span data-stu-id="294ab-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="294ab-171">Sérialisez `yourActivity.Id` dans la charge utile du message à la place de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="294ab-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="294ab-172">Vous pouvez également utiliser `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="294ab-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="294ab-173">Dequeue (Enlever de la file d’attente)</span><span class="sxs-lookup"><span data-stu-id="294ab-173">Dequeue</span></span>
<span data-ttu-id="294ab-174">Comme avec `Enqueue`, une requête HTTP réelle à la file d’attente de stockage est automatiquement suivie par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="294ab-175">Toutefois, l’opération `Enqueue` se produit vraisemblablement dans le contexte parent, par exemple un contexte de demande entrant.</span><span class="sxs-lookup"><span data-stu-id="294ab-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="294ab-176">Les kits SDK d’Application Insights mettent automatiquement en corrélation cette opération (et sa partie HTTP) avec la demande parent et d’autres données de télémétrie signalées dans le même cadre.</span><span class="sxs-lookup"><span data-stu-id="294ab-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="294ab-177">L’opération `Dequeue` est compliquée.</span><span class="sxs-lookup"><span data-stu-id="294ab-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="294ab-178">Le kit SDK d’Application Insights effectue automatiquement le suivi des demandes HTTP.</span><span class="sxs-lookup"><span data-stu-id="294ab-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="294ab-179">Toutefois, il ne connait pas le contexte de corrélation avant que le message ne soit analysé.</span><span class="sxs-lookup"><span data-stu-id="294ab-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="294ab-180">Il n’est pas possible de mettre en corrélation la requête HTTP afin d’obtenir le message avec le reste des données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="294ab-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="294ab-181">Dans de nombreux cas, il peut être utile de mettre en corrélation la requête HTTP adressée à la file d’attente avec d’autres traces également.</span><span class="sxs-lookup"><span data-stu-id="294ab-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="294ab-182">L’exemple suivant illustre son fonctionnement :</span><span class="sxs-lookup"><span data-stu-id="294ab-182">The following example demonstrates how to do it:</span></span>

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

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
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

#### <a name="process"></a><span data-ttu-id="294ab-183">Process</span><span class="sxs-lookup"><span data-stu-id="294ab-183">Process</span></span>

<span data-ttu-id="294ab-184">Dans l’exemple suivant, nous traçons le message entrant de la même façon qu’une requête HTTP entrante :</span><span class="sxs-lookup"><span data-stu-id="294ab-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
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

<span data-ttu-id="294ab-185">De même, les autres opérations de file d’attente peuvent être instrumentées.</span><span class="sxs-lookup"><span data-stu-id="294ab-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="294ab-186">Une opération d’aperçu doit être instrumentée de façon similaire à un retrait de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="294ab-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="294ab-187">L’instrumentation des opérations de gestion de file d’attente n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="294ab-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="294ab-188">Application Insights effectue le suivi d’opérations telles que HTTP et, dans la plupart des cas, cela suffit.</span><span class="sxs-lookup"><span data-stu-id="294ab-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="294ab-189">Lors de l’instrumentation d’une suppression de message, assurez-vous de définir les identificateurs de l’opération (corrélation).</span><span class="sxs-lookup"><span data-stu-id="294ab-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="294ab-190">Vous pouvez également utiliser l’API `Activity`.</span><span class="sxs-lookup"><span data-stu-id="294ab-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="294ab-191">Vous n’avez alors pas besoin de définir des identificateurs d’opérations sur les éléments de télémétrie car Application Insights le fait pour vous :</span><span class="sxs-lookup"><span data-stu-id="294ab-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="294ab-192">Créez une nouvelle API `Activity` une fois que vous avez un élément à partir de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="294ab-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="294ab-193">Utilisez `Activity.SetParentId(message.ParentId)` pour mettre en corrélation les journaux du consommateur et du producteur.</span><span class="sxs-lookup"><span data-stu-id="294ab-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="294ab-194">Démarrez `Activity`.</span><span class="sxs-lookup"><span data-stu-id="294ab-194">Start the `Activity`.</span></span>
- <span data-ttu-id="294ab-195">Effectuez le suivi des opérations de retrait de file d’attente, de traitement et de suppression à l’aide des programmes d’assistance `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="294ab-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="294ab-196">Procédez à partir du même flux de contrôle asynchrone (contexte d’exécution).</span><span class="sxs-lookup"><span data-stu-id="294ab-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="294ab-197">De cette manière, elles sont correctement mises en corrélation.</span><span class="sxs-lookup"><span data-stu-id="294ab-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="294ab-198">Arrêtez `Activity`.</span><span class="sxs-lookup"><span data-stu-id="294ab-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="294ab-199">Utilisez `Start/StopOperation` ou appelez manuellement la télémétrie `Track`.</span><span class="sxs-lookup"><span data-stu-id="294ab-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="294ab-200">Traitement par lots</span><span class="sxs-lookup"><span data-stu-id="294ab-200">Batch processing</span></span>
<span data-ttu-id="294ab-201">Avec des files d’attente, vous pouvez retirer plusieurs messages de la file d’attente avec une seule demande.</span><span class="sxs-lookup"><span data-stu-id="294ab-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="294ab-202">Le traitement de ces messages est vraisemblablement indépendant et appartient à différentes opérations logiques.</span><span class="sxs-lookup"><span data-stu-id="294ab-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="294ab-203">Dans ce cas, il n’est pas possible de mettre en corrélation l’opération `Dequeue` avec un traitement de message particulier.</span><span class="sxs-lookup"><span data-stu-id="294ab-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="294ab-204">Chaque traitement de message doit être traité dans son propre flux de contrôle asynchrone.</span><span class="sxs-lookup"><span data-stu-id="294ab-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="294ab-205">Pour plus d’informations, consultez la section [Suivi des dépendances sortantes](#outgoing-dependencies-tracking).</span><span class="sxs-lookup"><span data-stu-id="294ab-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="294ab-206">Tâches en arrière-plan à long terme</span><span class="sxs-lookup"><span data-stu-id="294ab-206">Long-running background tasks</span></span>
<span data-ttu-id="294ab-207">Certaines applications démarrent des opérations à long terme qui peuvent être dues à des demandes de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="294ab-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="294ab-208">Du point de vue du traçage/de l’instrumentation, ce n’est pas différent de l’instrumentation des demandes ou des dépendances :</span><span class="sxs-lookup"><span data-stu-id="294ab-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process the task.
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

<span data-ttu-id="294ab-209">Dans cet exemple, nous utilisons `telemetryClient.StartOperation` pour créer `RequestTelemetry` et remplir le contexte de corrélation.</span><span class="sxs-lookup"><span data-stu-id="294ab-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="294ab-210">Supposons que vous avez une opération parent qui a été créée par les demandes entrantes qui ont planifié l’opération.</span><span class="sxs-lookup"><span data-stu-id="294ab-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="294ab-211">Tant que `BackgroundTask` démarre dans le même flux de contrôle asynchrone en tant que demande entrante, elle est mise en corrélation avec cette opération parent.</span><span class="sxs-lookup"><span data-stu-id="294ab-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="294ab-212">`BackgroundTask` et tous les éléments de télémétrie imbriqués sont automatiquement mis en corrélation avec la demande à son origine, même après la fin de la demande.</span><span class="sxs-lookup"><span data-stu-id="294ab-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="294ab-213">Lorsque la tâche démarre à partir du thread en arrière-plan qui n’a pas d’opération (`Activity`) associée, `BackgroundTask` n’a pas de parent.</span><span class="sxs-lookup"><span data-stu-id="294ab-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="294ab-214">Toutefois, il peut avoir plusieurs opérations imbriquées.</span><span class="sxs-lookup"><span data-stu-id="294ab-214">However, it can have nested operations.</span></span> <span data-ttu-id="294ab-215">Tous les éléments de télémétrie signalés à partir de la tâche sont mis en corrélation avec l’élément `RequestTelemetry` créé dans l’élément `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="294ab-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="294ab-216">Suivi des dépendances sortantes</span><span class="sxs-lookup"><span data-stu-id="294ab-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="294ab-217">Vous pouvez effectuer le suivi de votre propre genre de dépendance ou d’une opération qui n’est pas prise en charge par Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="294ab-218">La méthode `Enqueue` dans la file d’attente Service Bus ou la file d’attente de stockage peut servir d’exemples pour ce type de suivi personnalisé.</span><span class="sxs-lookup"><span data-stu-id="294ab-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="294ab-219">L’approche générale utilisée pour le suivi personnalisé des dépendances est la suivante :</span><span class="sxs-lookup"><span data-stu-id="294ab-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="294ab-220">Appelez la méthode `TelemetryClient.StartOperation` (extension) qui remplit les propriétés `DependencyTelemetry` nécessaires pour la corrélation et d’autres propriétés (heure de début, durée).</span><span class="sxs-lookup"><span data-stu-id="294ab-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="294ab-221">Définissez d’autres propriétés personnalisées sur l’élément `DependencyTelemetry`, comme le nom et tout autre contexte dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="294ab-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="294ab-222">Effectuez un appel de dépendance et attendez les résultats.</span><span class="sxs-lookup"><span data-stu-id="294ab-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="294ab-223">Arrêtez l’opération avec `StopOperation` lorsqu’elle est terminée.</span><span class="sxs-lookup"><span data-stu-id="294ab-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="294ab-224">Traitez les exceptions.</span><span class="sxs-lookup"><span data-stu-id="294ab-224">Handle exceptions.</span></span>

<span data-ttu-id="294ab-225">`StopOperation` ne peut arrêter que l’opération lancée.</span><span class="sxs-lookup"><span data-stu-id="294ab-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="294ab-226">Si l’opération en cours d’exécution actuelle ne correspond pas à celle que vous souhaitez arrêter, `StopOperation` ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="294ab-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="294ab-227">Cette situation peut se produire si vous démarrez plusieurs opérations en parallèle dans le même contexte d’exécution :</span><span class="sxs-lookup"><span data-stu-id="294ab-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="294ab-228">Assurez-vous de toujours appeler `StartOperation` et d’exécuter votre tâche dans son propre contexte :</span><span class="sxs-lookup"><span data-stu-id="294ab-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="294ab-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="294ab-229">Next steps</span></span>

- <span data-ttu-id="294ab-230">Découvrez les bases de la [corrélation de télémétrie](application-insights-correlation.md) dans Application Insights.</span><span class="sxs-lookup"><span data-stu-id="294ab-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="294ab-231">Pour connaître les types et les modèles de données Application Insights, consultez [Modèle de données](application-insights-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="294ab-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="294ab-232">Signalez les [événements et métriques](app-insights-api-custom-events-metrics.md) à Application Insights .</span><span class="sxs-lookup"><span data-stu-id="294ab-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="294ab-233">Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) standard de la collection de propriétés de contexte.</span><span class="sxs-lookup"><span data-stu-id="294ab-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="294ab-234">Consultez le [Guide de l’utilisateur System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) pour voir comment mettre en corrélation les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="294ab-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
