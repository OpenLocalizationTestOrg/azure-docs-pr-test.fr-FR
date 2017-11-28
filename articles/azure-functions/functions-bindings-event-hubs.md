---
title: "liaisons de concentrateurs d’événements de fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment les liaisons d’Azure Event Hubs toouse dans les fonctions d’Azure."
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
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="0953d-104">Liaisons d’Event Hubs Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0953d-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0953d-105">Cet article explique comment tooconfigure et utiliser [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) liaisons pour les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0953d-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="0953d-106">Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0953d-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0953d-107">Si vous êtes nouveau tooAzure Event Hubs, consultez hello [vue d’ensemble des concentrateurs d’événements](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0953d-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="0953d-108">Déclencheur Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0953d-108">Event hub trigger</span></span>
<span data-ttu-id="0953d-109">Utilisez les concentrateurs d’événements hello déclencher l’événement de tooan de toorespond envoyé le flux d’événements tooan événement hub.</span><span class="sxs-lookup"><span data-stu-id="0953d-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="0953d-110">Vous devez avoir accès en lecture toohello événement hub tooset déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="0953d-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="0953d-111">déclencheur de fonction Hello Event Hubs utilise hello objet JSON Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0953d-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="0953d-112">`consumerGroup`est un hello tooset de propriété facultative utilisée [groupe de consommateurs](../event-hubs/event-hubs-features.md#event-consumers) utilisé toosubscribe tooevents dans le hub de hello.</span><span class="sxs-lookup"><span data-stu-id="0953d-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="0953d-113">Si omis, hello `$Default` groupe de consommateurs est utilisé.</span><span class="sxs-lookup"><span data-stu-id="0953d-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="0953d-114">`connection`doit être nom hello d’un paramètre d’application qui contient l’espace de noms hello connexion chaîne toohello du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0953d-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="0953d-115">Copier cette chaîne de connexion en cliquant sur hello **les informations de connexion** bouton pour hello *espace de noms*, pas les concentrateur d’événements hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="0953d-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="0953d-116">Cette chaîne de connexion doit avoir au moins lecture déclencheur de hello tooactivate autorisations.</span><span class="sxs-lookup"><span data-stu-id="0953d-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="0953d-117">[Paramètres supplémentaires](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) peut être fournie dans un host.json toofurther fichier fine paramétrer les concentrateurs d’événements déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="0953d-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="0953d-118">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="0953d-118">Trigger usage</span></span>
<span data-ttu-id="0953d-119">Lorsqu’une fonction de déclenchement de concentrateurs d’événements est déclenchée, message de type hello qui le déclenche est passé dans la fonction hello sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="0953d-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="0953d-120">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="0953d-120">Trigger sample</span></span>
<span data-ttu-id="0953d-121">Supposez que vous avez hello concentrateurs d’événements suivante se déclencher dans hello `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0953d-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="0953d-122">Voir exemple hello spécifiques au langage qui enregistre le corps du message hello du déclencheur de concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="0953d-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="0953d-123">C#</span><span class="sxs-lookup"><span data-stu-id="0953d-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="0953d-124">F#</span><span class="sxs-lookup"><span data-stu-id="0953d-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="0953d-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0953d-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="0953d-126">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="0953d-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="0953d-127">Vous pouvez également recevoir des événements hello comme un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objet, qui vous donne l’accès à toohello métadonnées d’événement.</span><span class="sxs-lookup"><span data-stu-id="0953d-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="0953d-128">événements tooreceive dans un lot, modifier la signature de méthode hello trop`string[]` ou `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="0953d-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="0953d-129">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="0953d-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="0953d-130">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="0953d-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="0953d-131">Liaison de sortie Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0953d-131">Event Hubs output binding</span></span>
<span data-ttu-id="0953d-132">Hello d’utiliser concentrateurs d’événements de sortie de flux d’événements liaison toowrite événements tooan événement hub.</span><span class="sxs-lookup"><span data-stu-id="0953d-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="0953d-133">Vous devez disposer d’envoi autorisation tooan événement hub toowrite événements tooit.</span><span class="sxs-lookup"><span data-stu-id="0953d-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="0953d-134">liaison de sortie Hello utilise hello objet JSON Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0953d-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="0953d-135">`connection`doit être nom hello d’un paramètre d’application qui contient l’espace de noms hello connexion chaîne toohello du concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0953d-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="0953d-136">Copier cette chaîne de connexion en cliquant sur hello **les informations de connexion** bouton pour hello *espace de noms*, pas les concentrateur d’événements hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="0953d-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="0953d-137">Cette chaîne de connexion doit avoir le flux d’événements envoi autorisations toosend hello message toohello.</span><span class="sxs-lookup"><span data-stu-id="0953d-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="0953d-138">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="0953d-138">Output usage</span></span>
<span data-ttu-id="0953d-139">Cette section vous montre comment toouse vos Hubs d’événements de sortie de liaison dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="0953d-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="0953d-140">Vous pouvez produire concentrateur d’événements de messages toohello configuré avec hello les types de paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0953d-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="0953d-141">`ICollector<string>`(toooutput plusieurs messages)</span><span class="sxs-lookup"><span data-stu-id="0953d-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="0953d-142">`IAsyncCollector<string>` (version asynchrone de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="0953d-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="0953d-143">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="0953d-143">Output sample</span></span>
<span data-ttu-id="0953d-144">Supposons que vous avez hello suivantes concentrateurs d’événements de sortie liaison Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="0953d-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="0953d-145">Consultez l’exemple de langage spécifiques hello qui écrit un flux même toohello d’événements.</span><span class="sxs-lookup"><span data-stu-id="0953d-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="0953d-146">C#</span><span class="sxs-lookup"><span data-stu-id="0953d-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="0953d-147">F#</span><span class="sxs-lookup"><span data-stu-id="0953d-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="0953d-148">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0953d-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="0953d-149">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="0953d-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="0953d-150">Ou, toocreate plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="0953d-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="0953d-151">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="0953d-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="0953d-152">Exemple de sortie pour Node.js</span><span class="sxs-lookup"><span data-stu-id="0953d-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="0953d-153">Ou, toosend plusieurs messages,</span><span class="sxs-lookup"><span data-stu-id="0953d-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0953d-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0953d-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
