---
title: "Déclencheurs et liaisons Service Bus Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des déclencheurs et des liaisons Azure Service Bus dans Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="ccacc-104">Liaisons Service Bus Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ccacc-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ccacc-105">Cet article explique comment configurer et utiliser des liaisons Azure Service Bus dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ccacc-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="ccacc-106">Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente et les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ccacc-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="ccacc-107">Déclencheur Service Bus</span><span class="sxs-lookup"><span data-stu-id="ccacc-107">Service Bus trigger</span></span>
<span data-ttu-id="ccacc-108">Utilisez le déclencheur Service Bus pour répondre aux messages provenant d'une file d’attente ou d'une rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ccacc-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="ccacc-109">Les déclencheurs de file d’attente et de rubrique Service Bus sont définis par les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="ccacc-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="ccacc-110">Déclencheur de *file d’attente* :</span><span class="sxs-lookup"><span data-stu-id="ccacc-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="ccacc-111">Déclencheur de *rubrique* :</span><span class="sxs-lookup"><span data-stu-id="ccacc-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="ccacc-112">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="ccacc-112">Note the following:</span></span>

* <span data-ttu-id="ccacc-113">Pour `connection`, [créez un paramètre d’application dans votre application de fonction](functions-how-to-use-azure-function-app-settings.md) qui contient la chaîne de connexion à votre espace de noms Service Bus, puis spécifiez le nom du paramètre d’application dans la propriété `connection` de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="ccacc-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="ccacc-114">Vous obtenez la chaîne de connexion en suivant les étapes indiquées à la section [Obtenir les informations d’identification de gestion](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="ccacc-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="ccacc-115">La chaîne de connexion doit être destinée à un espace de noms Service Bus, et non limitée à une file d’attente ou une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="ccacc-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="ccacc-116">Si vous laissez `connection` vide, le déclencheur suppose qu’une chaîne de connexion Service Bus par défaut est spécifiée dans le paramètre d’application nommé `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="ccacc-117">Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="ccacc-118">La valeur par défaut est `manage`, ce qui indique que `connection` a l'autorisation **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="ccacc-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="ccacc-119">Si vous utilisez une chaîne de connexion qui n’a pas l'autorisation **Gérer**, définissez `accessRights` sur `listen`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="ccacc-120">Sinon, le runtime Functions pourrait échouer à effectuer des opérations qui nécessitent des droits de gestion.</span><span class="sxs-lookup"><span data-stu-id="ccacc-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="ccacc-121">Comportement du déclencheur</span><span class="sxs-lookup"><span data-stu-id="ccacc-121">Trigger behavior</span></span>
* <span data-ttu-id="ccacc-122">**Thread unique** - Par défaut, le runtime Functions traite plusieurs messages simultanément.</span><span class="sxs-lookup"><span data-stu-id="ccacc-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="ccacc-123">Pour que le runtime ne traite qu’un message de file d’attente ou de rubrique à la fois, définissez `serviceBus.maxConcurrentCalls` sur 1 dans *host.json*.</span><span class="sxs-lookup"><span data-stu-id="ccacc-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="ccacc-124">Pour plus d’informations sur *host.json*, consultez [Structure de dossiers](functions-reference.md#folder-structure) et [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="ccacc-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="ccacc-125">**Gestion des messages incohérents** - Service Bus assure sa propre gestion des messages incohérents. Il est impossible de la contrôler ou de la configurer dans la configuration ou le code d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ccacc-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="ccacc-126">**Comportement de PeekLock** - Le runtime Functions reçoit un message en mode [`PeekLock`](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) et appelle `Complete` sur le message si la fonction se termine correctement. Si la fonction échoue, il appelle `Abandon`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="ccacc-127">Si la fonction s’exécute au-delà du délai imparti à `PeekLock`, le verrou est automatiquement renouvelé.</span><span class="sxs-lookup"><span data-stu-id="ccacc-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="ccacc-128">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="ccacc-128">Trigger usage</span></span>
<span data-ttu-id="ccacc-129">Cette section vous montre comment utiliser votre déclencheur Service Bus dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="ccacc-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="ccacc-130">Dans C# and F#, le message du déclencheur Service Bus peut être désérialisé vers l’un des types d'entrée suivants :</span><span class="sxs-lookup"><span data-stu-id="ccacc-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="ccacc-131">`string` - utile pour les messages de type chaîne</span><span class="sxs-lookup"><span data-stu-id="ccacc-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="ccacc-132">`byte[]` - utile pour les données binaires</span><span class="sxs-lookup"><span data-stu-id="ccacc-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="ccacc-133">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données JSON sérialisées.</span><span class="sxs-lookup"><span data-stu-id="ccacc-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="ccacc-134">Si vous déclarez un type d’entrée personnalisé, comme `CustomType`, Azure Functions essaye de désérialiser les données JSON dans le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="ccacc-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="ccacc-135">`BrokeredMessage` - vous donne le message désérialisé avec la méthode [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccacc-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="ccacc-136">Dans Node.js, le message du déclencheur Service Bus est passé à la fonction en tant que chaîne ou en tant qu’objet JSON.</span><span class="sxs-lookup"><span data-stu-id="ccacc-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="ccacc-137">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="ccacc-137">Trigger sample</span></span>
<span data-ttu-id="ccacc-138">Supposons que vous avez le code function.json suivant :</span><span class="sxs-lookup"><span data-stu-id="ccacc-138">Suppose you have the following function.json:</span></span>

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="ccacc-139">Consultez l'exemple de code spécifique au langage qui traite un message de file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ccacc-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="ccacc-140">C#</span><span class="sxs-lookup"><span data-stu-id="ccacc-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ccacc-141">F#</span><span class="sxs-lookup"><span data-stu-id="ccacc-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="ccacc-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ccacc-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="ccacc-143">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="ccacc-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="ccacc-144">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="ccacc-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="ccacc-145">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="ccacc-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="ccacc-146">Liaison de sortie Service Bus</span><span class="sxs-lookup"><span data-stu-id="ccacc-146">Service Bus output binding</span></span>
<span data-ttu-id="ccacc-147">La sortie de file d’attente et de rubrique Service Bus utilise les objets JSON suivants dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="ccacc-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="ccacc-148">Sortie de *file d’attente* :</span><span class="sxs-lookup"><span data-stu-id="ccacc-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="ccacc-149">Sortie de *rubrique* :</span><span class="sxs-lookup"><span data-stu-id="ccacc-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="ccacc-150">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="ccacc-150">Note the following:</span></span>

* <span data-ttu-id="ccacc-151">Pour `connection`, [créez un paramètre d’application dans votre application de fonction](functions-how-to-use-azure-function-app-settings.md) qui contient la chaîne de connexion à votre espace de noms Service Bus, puis spécifiez le nom du paramètre d’application dans la propriété `connection` de votre liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="ccacc-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="ccacc-152">Vous obtenez la chaîne de connexion en suivant les étapes indiquées à la section [Obtenir les informations d’identification de gestion](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="ccacc-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="ccacc-153">La chaîne de connexion doit être destinée à un espace de noms Service Bus, et non limitée à une file d’attente ou une rubrique spécifique.</span><span class="sxs-lookup"><span data-stu-id="ccacc-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="ccacc-154">Si vous laissez `connection` vide, la liaison de sortie suppose qu’une chaîne de connexion Service Bus par défaut est spécifiée dans le paramètre d’application nommé `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="ccacc-155">Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="ccacc-156">La valeur par défaut est `manage`, ce qui indique que `connection` a l'autorisation **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="ccacc-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="ccacc-157">Si vous utilisez une chaîne de connexion qui n’a pas l'autorisation **Gérer**, définissez `accessRights` sur `listen`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="ccacc-158">Sinon, le runtime Functions pourrait échouer à effectuer des opérations qui nécessitent des droits de gestion.</span><span class="sxs-lookup"><span data-stu-id="ccacc-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="ccacc-159">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="ccacc-159">Output usage</span></span>
<span data-ttu-id="ccacc-160">Dans C# et F#, Azure Functions peut créer un message de file d’attente Service Bus à partir d’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="ccacc-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="ccacc-161">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) - la définition du paramètre ressemble à `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="ccacc-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="ccacc-162">Functions désérialise l’objet dans un message JSON.</span><span class="sxs-lookup"><span data-stu-id="ccacc-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="ccacc-163">Si la valeur de sortie est null lorsque la fonction se termine, Functions crée le message avec un objet null.</span><span class="sxs-lookup"><span data-stu-id="ccacc-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="ccacc-164">`string` - La définition du paramètre ressemble à `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="ccacc-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="ccacc-165">Si la valeur du paramètre n'est pas null lorsque la fonction se termine, Functions crée un message.</span><span class="sxs-lookup"><span data-stu-id="ccacc-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="ccacc-166">`byte[]` - La définition du paramètre ressemble à `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="ccacc-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="ccacc-167">Si la valeur du paramètre n'est pas null lorsque la fonction se termine, Functions crée un message.</span><span class="sxs-lookup"><span data-stu-id="ccacc-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="ccacc-168">`BrokeredMessage` - La définition du paramètre ressemble à `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="ccacc-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="ccacc-169">Si la valeur du paramètre n'est pas null lorsque la fonction se termine, Functions crée un message.</span><span class="sxs-lookup"><span data-stu-id="ccacc-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="ccacc-170">Pour créer plusieurs messages dans une fonction C#, vous pouvez utiliser `ICollector<T>` ou `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="ccacc-171">Un message est créé quand vous appelez la méthode `Add` .</span><span class="sxs-lookup"><span data-stu-id="ccacc-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="ccacc-172">Dans Node.js, vous pouvez affecter une chaîne, un tableau d’octets ou un objet Javascript (désérialisé dans JSON) à `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="ccacc-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="ccacc-173">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="ccacc-173">Output sample</span></span>
<span data-ttu-id="ccacc-174">Supposons le code function.json suivant, qui définit une sortie de file d'attente Service Bus :</span><span class="sxs-lookup"><span data-stu-id="ccacc-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

<span data-ttu-id="ccacc-175">Consultez l'exemple spécifique au langage qui envoie un message à la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ccacc-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="ccacc-176">C#</span><span class="sxs-lookup"><span data-stu-id="ccacc-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="ccacc-177">F#</span><span class="sxs-lookup"><span data-stu-id="ccacc-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="ccacc-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ccacc-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="ccacc-179">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="ccacc-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="ccacc-180">Ou, pour créer plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="ccacc-180">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="ccacc-181">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="ccacc-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="ccacc-182">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="ccacc-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="ccacc-183">Ou, pour créer plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="ccacc-183">Or, to create multiple messages:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ccacc-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ccacc-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

