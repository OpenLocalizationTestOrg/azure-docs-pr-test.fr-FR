---
title: "Liaisons d’Event Hubs Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des liaisons Azure Event Hubs dans Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="2d92d-104">Liaisons d’Event Hubs Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2d92d-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="2d92d-105">Cet article explique comment configurer et utiliser des liaisons [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) pour Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="2d92d-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="2d92d-106">Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2d92d-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="2d92d-107">Si vous débutez avec Azure Event Hubs, consultez la [vue d’ensemble d’Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2d92d-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="2d92d-108">Déclencheur Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2d92d-108">Event hub trigger</span></span>
<span data-ttu-id="2d92d-109">Utilisez le déclencheur Event Hubs pour répondre à un événement envoyé à un flux d’événements d’un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="2d92d-110">Vous devez disposer de l’accès en lecture au hub d’événements pour configurer le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="2d92d-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="2d92d-111">Le déclencheur Event Hubs d’une fonction utilise l’objet JSON suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="2d92d-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="2d92d-112">`consumerGroup` est une propriété facultative utilisée pour définir le [groupe de consommateurs](../event-hubs/event-hubs-features.md#event-consumers) utilisé pour l’abonnement à des événements dans le hub.</span><span class="sxs-lookup"><span data-stu-id="2d92d-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="2d92d-113">En cas d’omission, le groupe de consommateurs `$Default` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2d92d-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="2d92d-114">`connection` doit être le nom d’un paramètre d’application qui contient la chaîne de connexion à l’espace de noms du hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="2d92d-115">Copiez cette chaîne de connexion en cliquant sur le bouton **Informations de connexion** pour *l’espace de noms*, et non pour le hub d’événements lui-même.</span><span class="sxs-lookup"><span data-stu-id="2d92d-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="2d92d-116">Cette chaîne de connexion doit avoir au moins des droits de lecture pour activer le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="2d92d-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="2d92d-117">Vous pouvez fournir des [paramètres supplémentaires](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) dans un fichier host.json pour affiner les déclencheurs Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2d92d-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="2d92d-118">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="2d92d-118">Trigger usage</span></span>
<span data-ttu-id="2d92d-119">Quand une fonction de déclenchement Event Hubs est déclenchée, le message qui le déclenche est passé à la fonction en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="2d92d-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="2d92d-120">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="2d92d-120">Trigger sample</span></span>
<span data-ttu-id="2d92d-121">Supposez que le tableau `bindings` de function.json contient le déclencheur Event Hubs suivant :</span><span class="sxs-lookup"><span data-stu-id="2d92d-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="2d92d-122">Consultez l’exemple dans le langage de votre choix pour voir comment enregistrer le corps du message du déclencheur de hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="2d92d-123">C#</span><span class="sxs-lookup"><span data-stu-id="2d92d-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="2d92d-124">F#</span><span class="sxs-lookup"><span data-stu-id="2d92d-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="2d92d-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2d92d-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="2d92d-126">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="2d92d-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="2d92d-127">Vous pouvez également recevoir l’événement en tant qu’objet [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata), qui vous permet d’accéder aux métadonnées de l’événement.</span><span class="sxs-lookup"><span data-stu-id="2d92d-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="2d92d-128">Pour recevoir les événements dans un lot, modifiez la signature de méthode sur `string[]` ou `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="2d92d-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="2d92d-129">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="2d92d-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="2d92d-130">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="2d92d-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="2d92d-131">Liaison de sortie Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2d92d-131">Event Hubs output binding</span></span>
<span data-ttu-id="2d92d-132">Utilisez la liaison de sortie Event Hubs pour écrire des événements dans un flux d’événements du hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="2d92d-133">Vous devez disposer de l’autorisation d’envoi à un hub d’événements pour y écrire les événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="2d92d-134">La liaison de sortie utilise l’objet JSON suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="2d92d-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="2d92d-135">`connection` doit être le nom d’un paramètre d’application qui contient la chaîne de connexion à l’espace de noms du hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="2d92d-136">Copiez cette chaîne de connexion en cliquant sur le bouton **Informations de connexion** pour *l’espace de noms*, et non pour le hub d’événements lui-même.</span><span class="sxs-lookup"><span data-stu-id="2d92d-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="2d92d-137">Cette chaîne de connexion doit disposer d’autorisations d’envoi pour envoyer le message au flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="2d92d-138">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="2d92d-138">Output usage</span></span>
<span data-ttu-id="2d92d-139">Cette section vous montre comment utiliser la liaison de sortie Event Hubs dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="2d92d-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="2d92d-140">Vous pouvez générer des messages au concentrateur d’événements configuré avec les types de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="2d92d-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="2d92d-141">`ICollector<string>`(pour envoyer plusieurs messages)</span><span class="sxs-lookup"><span data-stu-id="2d92d-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="2d92d-142">`IAsyncCollector<string>` (version asynchrone de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="2d92d-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="2d92d-143">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="2d92d-143">Output sample</span></span>
<span data-ttu-id="2d92d-144">Supposez que le tableau `bindings` de function.json contient la liaison de sortie Event Hubs suivante :</span><span class="sxs-lookup"><span data-stu-id="2d92d-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="2d92d-145">Consultez l’exemple dans le langage de votre choix pour voir comment écrire un événement dans le flux d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d92d-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="2d92d-146">C#</span><span class="sxs-lookup"><span data-stu-id="2d92d-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="2d92d-147">F#</span><span class="sxs-lookup"><span data-stu-id="2d92d-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="2d92d-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2d92d-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="2d92d-149">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="2d92d-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="2d92d-150">Ou, pour créer plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="2d92d-150">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="2d92d-151">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="2d92d-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="2d92d-152">Exemple de sortie pour Node.js</span><span class="sxs-lookup"><span data-stu-id="2d92d-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="2d92d-153">Ou, pour envoyer plusieurs messages,</span><span class="sxs-lookup"><span data-stu-id="2d92d-153">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="2d92d-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d92d-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
