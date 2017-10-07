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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Suivi des opérations personnalisées avec le kit SDK .NET d’Application Insights

Azure SDK Application Insights automatiquement suivi HTTP entrant demande et appelle toodependent services, tels que les requêtes HTTP et les requêtes SQL. Le suivi et la corrélation des demandes et des dépendances vous offrent une visibilité en réactivité et la fiabilité de l’application hello entier entre tous les microservices qui combinent cette application. 

Il existe une classe de modèles d’application qui ne peuvent pas être pris en charge de façon générique. La surveillance appropriée de ces modèles requiert une instrumentation manuelle du code. Cet article traite de quelques modèles qui peuvent requérir une instrumentation manuelle, tels que le traitement de la file d’attente personnalisé et les tâches en arrière-plan à long terme en cours d’exécution.

Ce document fournit des conseils sur la tootrack des opérations personnalisées avec hello Application Insights SDK. Cette documentation concerne :

- Application Insights pour .NET (également appelé Kit SDK de base) version 2.4 et versions ultérieures.
- Application Insights pour applications web (exécute ASP.NET) version 2.4 et versions ultérieures.
- Application Insights pour ASP.NET Core version 2.1 et versions ultérieures.

## <a name="overview"></a>Vue d'ensemble
Une opération est un élément de travail logique exécuté par une application. Il a un nom, une heure de début, une durée, un résultat et un contexte d’exécution tel qu’un nom d’utilisateur, des propriétés et un résultat. Si l’opération A a été initiée par l’opération B, l’opération B est alors définie en tant que parent pour A. Une opération ne peut avoir qu’un seul parent, mais il peut avoir de nombreuses opérations enfants. Pour plus d’informations sur les opérations et la corrélation de télémétrie, consultez [Corrélation de télémétrie d’Application Azure Insights](application-insights-correlation.md).

Bonjour Application Insights .NET SDK, opération de hello est décrite par la classe abstraite de hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) et de ses descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) et [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Suivi des opérations entrantes 
Hello web Application Insights que SDK collecte automatiquement des requêtes HTTP pour les applications ASP.NET qui s’exécutent dans un pipeline d’IIS et toutes les applications ASP.NET Core. Il existe des solutions prises en charge par la communauté pour les autres plateformes et infrastructures. Toutefois, si l’application hello n’est pas pris en charge par les standard de hello ou pris en charge par une Communauté de solutions, vous pouvez l’instrumenter manuellement.

Un autre exemple nécessitant un suivi personnalisé est travail hello qui reçoit les éléments de file d’attente hello. Pour des files d’attente, hello appeler tooadd un message de file d’attente toothis est suivie en tant que dépendance. Toutefois, opération de haut niveau hello qui décrit le traitement des messages n’est pas collectée automatiquement.

Voyons comment effectuer le suivi de telles opérations.

Sur un niveau élevé, tâche hello est toocreate `RequestTelemetry` et définir des propriétés connues. Une fois hello terminé, les données de télémétrie hello effectuer le suivi. Bonjour à l’exemple suivant illustre cette tâche.

### <a name="http-request-in-owin-self-hosted-app"></a>Requête HTTP dans une application Owin auto-hébergée
Dans cet exemple, nous suivons hello [le protocole HTTP pour la corrélation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Attendez-vous à ce que les en-têtes tooreceive décrits il.

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

le protocole HTTP pour la corrélation de Hello déclare également hello `Correlation-Context` en-tête. Toutefois, il est omis ici par souci de simplicité.

## <a name="queue-instrumentation"></a>Instrumentation des files d’attente
Pour les communications HTTP, nous avons créé un protocole toopass détails de la corrélation. Avec les protocoles de certaines files d’attente, vous pouvez passer des métadonnées supplémentaires avec le message de type hello et avec d’autres que vous ne pouvez pas.

### <a name="service-bus-queue"></a>File d’attente Service Bus
Avec hello Azure [file d’attente Service Bus](../service-bus-messaging/index.md), vous pouvez passer un jeu de propriétés, ainsi que le message de type hello. Nous les utilisons ID de corrélation hello toopass.

file d’attente du Service Bus Hello utilise des protocoles TCP. Application Insights n’effectue pas automatiquement le suivi des opérations de file d’attente, et nous devons les suivre manuellement. Hello dequeue opération est une API de style push, et nous sommes tootrack Impossible d’elle.

#### <a name="enqueue"></a>Enqueue (empiler)

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

#### <a name="process"></a>Process
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

### <a name="azure-storage-queue"></a>File d’attente de stockage Azure
Hello suivant montre l’exemple de comment tootrack hello [file d’attente de stockage Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) opérations et mettre en corrélation télémétrie entre le producteur de hello, hello consommateur et le stockage Azure. 

file d’attente de stockage Hello a une API HTTP. File d’attente de tous les appels toohello sont suivies par hello Application Insights dépendance collecteur pour les requêtes HTTP.
Préparez-vous.Assurez-vous que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` se trouve dans `applicationInsights.config`. Si vous n’est pas installé, l’ajouter par programmation, comme décrit dans [de filtrage et de prétraitement Bonjour Azure Application Insights SDK](app-insights-api-filtering-sampling.md).

Si vous configurez manuellement Application Insights, assurez-vous de créer et d’initialiser `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de façon semblable au code suivant :
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Vous pouvez aussi hello toocorrelate Application Insights l’ID d’opération avec l’ID de demande de stockage hello. Pour plus d’informations sur comment tooset et obtenir un stockage de demande client et un ID de demande de serveur, consultez [moniteur, diagnostiquer et résoudre les problèmes de stockage Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Enqueue (empiler)
Les files d’attente de stockage prenant en charge les API HTTP de hello, toutes les opérations de file d’attente hello sont automatiquement suivies par Application Insights. Dans de nombreux cas, cette instrumentation doit être suffisante. Toutefois, toocorrelate effectue le suivi sur le côté du consommateur hello avec les traces producteur, vous devez passer un contexte de corrélation de même toohow nous faire Bonjour le protocole HTTP pour la corrélation. 

Dans cet exemple, nous avons suivi hello facultatif `Enqueue` opération. Vous pouvez :

 - **Mettre en corrélation des nouvelles tentatives (le cas échéant)**: ils ont tous un parent commun qui est hello `Enqueue` opération. Dans le cas contraire, elles sont suivies en tant qu’enfants de la demande entrante de hello. S’il existe de file d’attente de plusieurs demandes logique toohello, il peut être difficile toofind quel appel a généré de nouvelles tentatives.
 - **Mettre en corrélation les journaux de stockage Azure (si nécessaire)** : elles sont mises en corrélation avec la télémétrie Application Insights.

Hello `Enqueue` opération est enfant hello d’une opération de parent (par exemple, une demande HTTP entrante). appel de dépendance Hello HTTP est enfant hello hello `Enqueue` opération et hello petits-enfants de demande entrante de hello :

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

quantité de hello tooreduce de télémétrie signale de votre application ou si vous ne souhaitez pas tootrack hello `Enqueue` opération pour d’autres raisons, utilisez hello `Activity` directement les API :

- Créer (et démarrer) un nouveau `Activity` au lieu de démarrer l’opération d’Application Insights hello. Vous faire *pas* devez tooassign toutes les propriétés sur celui-ci, à l’exception du nom de l’opération hello.
- Sérialiser `yourActivity.Id` dans la charge utile du message hello au lieu de `operation.Telemetry.Id`. Vous pouvez également utiliser `Activity.Current.Id`.


#### <a name="dequeue"></a>Dequeue (Enlever de la file d’attente)
De même trop`Enqueue`, une file d’attente de stockage toohello réel HTTP demande automatiquement suivi Application Insights. Toutefois, hello `Enqueue` vraisemblablement, opération qui se produit dans le contexte parent hello, par exemple un contexte de demande entrant. SDK application Insights mettre en corrélation automatiquement une telle opération (et sa partie HTTP) avec la demande de parent hello et autres données de télémétrie signalé Bonjour même étendue.

Hello `Dequeue` opération est difficile. Hello Application Insights SDK effectue automatiquement le suivi des demandes HTTP. Toutefois, il ne sait pas contexte de corrélation hello jusqu'à ce que le message de type hello est analysé. Il n’est pas possible de toocorrelate hello HTTP demande tooget message de type hello avec rest hello de télémétrie de hello.

Dans de nombreux cas, il peut être utile toocorrelate hello HTTP toohello file d’attente avec d’autres traces ainsi. Hello exemple suivant montre comment toodo il :

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

#### <a name="process"></a>Process

Bonjour l’exemple suivant, nous avons un message entrant de trace d’une manière de même demander toohow nous trace HTTP entrant :

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

De même, les autres opérations de file d’attente peuvent être instrumentées. Une opération d’aperçu doit être instrumentée de façon similaire à un retrait de la file d’attente. L’instrumentation des opérations de gestion de file d’attente n’est pas nécessaire. Application Insights effectue le suivi d’opérations telles que HTTP et, dans la plupart des cas, cela suffit.

Lorsque vous instrumentez la suppression du message, assurez-vous que vous définissez les opération hello les identificateurs (corrélation). Vous pouvez également utiliser hello `Activity` API. Vous ne devez pas les identificateurs d’opération tooset sur les éléments de télémétrie hello, car l’Application Insights fait pour vous :

- Créer un nouveau `Activity` une fois que vous avez un élément de file d’attente hello.
- Utilisez `Activity.SetParentId(message.ParentId)` toocorrelate les journaux producteur et consommateur.
- Démarrer hello `Activity`.
- Effectuez le suivi des opérations de retrait de file d’attente, de traitement et de suppression à l’aide des programmes d’assistance `Start/StopOperation`. Le faire à partir de hello asynchrone même contrôler les flux (contexte d’exécution). De cette manière, elles sont correctement mises en corrélation.
- Arrêt hello `Activity`.
- Utilisez `Start/StopOperation` ou appelez manuellement la télémétrie `Track`.

### <a name="batch-processing"></a>Traitement par lots
Avec des files d’attente, vous pouvez retirer plusieurs messages de la file d’attente avec une seule demande. Traitement des messages de ce type est sans doute indépendant et appartient toohello les opérations logiques différents. Dans ce cas, il n’est pas possible de toocorrelate hello `Dequeue` le traitement des messages tooparticular opération.

Chaque traitement de message doit être traité dans son propre flux de contrôle asynchrone. Pour plus d’informations, consultez hello [dépendances sortantes suivi](#outgoing-dependencies-tracking) section.

## <a name="long-running-background-tasks"></a>Tâches en arrière-plan à long terme
Certaines applications démarrent des opérations à long terme qui peuvent être dues à des demandes de l’utilisateur. Hello/instrumentation de traçage du point de vue, il n’est pas différente de l’instrumentation de demande ou la dépendance : 

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

Dans cet exemple, nous utilisons `telemetryClient.StartOperation` toocreate `RequestTelemetry` et le contexte de corrélation de remplissage hello. Supposons que vous avez une opération parent qui a été créée par les demandes entrantes qui hello opération planifiée. Tant que `BackgroundTask` commence dans hello même flux de contrôle asynchrone en tant qu’une demande entrante, il est mis en corrélation avec cette opération parent. `BackgroundTask`et tous les éléments de télémétrie imbriquées sont automatiquement mis en corrélation avec demande hello à l’origine, même après la fin de la demande hello.

Démarrage de la tâche hello à partir du thread d’arrière-plan hello n’a aucune opération (`Activity`) associé, `BackgroundTask` dépourvu de tout parent. Toutefois, il peut avoir plusieurs opérations imbriquées. Tous les éléments de télémétrie signalées à partir de la tâche hello sont corrélé toohello `RequestTelemetry` créé dans `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Suivi des dépendances sortantes
Vous pouvez effectuer le suivi de votre propre genre de dépendance ou d’une opération qui n’est pas prise en charge par Application Insights.

Hello `Enqueue` méthode dans la file d’attente du Service Bus hello ou file d’attente de stockage hello peut servir d’exemples pour ce type de suivi personnalisé.

Bonjour général personnalisé suivi des dépendances consiste à :

- Appelez hello `TelemetryClient.StartOperation` (méthode) (extension) qui remplit hello `DependencyTelemetry` propriétés qui sont nécessaires pour la corrélation et d’autres propriétés (heure de début de marqueur, la durée).
- Définir d’autres propriétés personnalisées sur hello `DependencyTelemetry`, tels que le nom de hello et un autre contexte que vous avez besoin.
- Effectuez un appel de dépendance et attendez les résultats.
- Arrêter l’opération hello avec `StopOperation` quand elle est terminée.
- Traitez les exceptions.

`StopOperation`uniquement interrompt hello qui a été démarrée. Si opération en cours d’exécution en cours de hello ne correspond pas hello une souhaité toostop, `StopOperation` n’exécute aucune opération. Cette situation peut se produire si vous démarrez plusieurs opérations en parallèle dans hello même contexte d’exécution :

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

Assurez-vous de toujours appeler `StartOperation` et d’exécuter votre tâche dans son propre contexte :
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

## <a name="next-steps"></a>Étapes suivantes

- Principes fondamentaux de hello [corrélation de télémétrie](application-insights-correlation.md) dans Application Insights.
- Consultez hello [modèle de données](application-insights-data-model.md) pour le modèle de données et les types d’Application Insights.
- Rapport personnalisé [événements et métriques](app-insights-api-custom-events-metrics.md) tooApplication Insights.
- Découvrez la [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) standard de la collection de propriétés de contexte.
- Vérifiez hello [Guide de l’utilisateur System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee comment nous mettre en corrélation les données de télémétrie.
