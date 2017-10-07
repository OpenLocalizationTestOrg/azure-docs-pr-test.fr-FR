---
title: "aaaAzure fonctions Service Bus déclencheurs et les liaisons | Documents Microsoft"
description: "Comprendre comment toouse Azure Service Bus déclenche et les liaisons dans les fonctions d’Azure."
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
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="a32b5-104">Liaisons Service Bus Azure Functions</span><span class="sxs-lookup"><span data-stu-id="a32b5-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a32b5-105">Cet article explique comment tooconfigure et de travailler avec des liaisons de Service Bus de Azure dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="a32b5-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="a32b5-106">Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente et les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a32b5-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="a32b5-107">Déclencheur Service Bus</span><span class="sxs-lookup"><span data-stu-id="a32b5-107">Service Bus trigger</span></span>
<span data-ttu-id="a32b5-108">Utilisez hello Service Bus déclencheur toorespond toomessages à partir d’une file d’attente du Bus de Service ou une rubrique.</span><span class="sxs-lookup"><span data-stu-id="a32b5-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="a32b5-109">déclencheurs de file d’attente et rubrique Service Bus Hello sont définis par hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="a32b5-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="a32b5-110">Déclencheur de *file d’attente* :</span><span class="sxs-lookup"><span data-stu-id="a32b5-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="a32b5-111">Déclencheur de *rubrique* :</span><span class="sxs-lookup"><span data-stu-id="a32b5-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="a32b5-112">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a32b5-112">Note hello following:</span></span>

* <span data-ttu-id="a32b5-113">Pour `connection`, [créer un paramètre d’application dans votre application de la fonction](functions-how-to-use-azure-function-app-settings.md) qui contient l’espace de noms de Service Bus hello connexion chaîne tooyour, puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="a32b5-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="a32b5-114">Obtenir de chaîne de connexion hello en suivant les étapes de hello présentés au [obtenir des informations d’identification de gestion hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="a32b5-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="a32b5-115">chaîne de connexion Hello doit être d’un espace de noms Service Bus, tooa non limité, la file d’attente spécifique ou une rubrique.</span><span class="sxs-lookup"><span data-stu-id="a32b5-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="a32b5-116">Si vous laissez `connection` vide, le déclencheur de hello part du principe qu’une chaîne de connexion de Service Bus par défaut est spécifiée dans une application de paramètre nommé `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="a32b5-117">Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="a32b5-118">valeur par défaut Hello est `manage`, ce qui signifie que hello `connection` a hello **gérer** autorisation.</span><span class="sxs-lookup"><span data-stu-id="a32b5-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="a32b5-119">Si vous utilisez une chaîne de connexion qui n’a pas de hello **gérer** de jeu d’autorisations, `accessRights` trop`listen`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="a32b5-120">Dans le cas contraire, les fonctions hello runtime risque d’échouer lors de la tentative toodo les opérations qui nécessitent les droits de gestion.</span><span class="sxs-lookup"><span data-stu-id="a32b5-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="a32b5-121">Comportement du déclencheur</span><span class="sxs-lookup"><span data-stu-id="a32b5-121">Trigger behavior</span></span>
* <span data-ttu-id="a32b5-122">**Modèle de thread unique** - par défaut, le processus d’exécution de fonctions hello plusieurs messages simultanément.</span><span class="sxs-lookup"><span data-stu-id="a32b5-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="a32b5-123">toodirect hello runtime tooprocess uniquement une file d’attente ou rubrique message unique à la fois, définissez `serviceBus.maxConcurrentCalls` too1 dans *host.json*.</span><span class="sxs-lookup"><span data-stu-id="a32b5-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="a32b5-124">Pour plus d’informations sur *host.json*, consultez [Structure de dossiers](functions-reference.md#folder-structure) et [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="a32b5-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="a32b5-125">**Gestion des messages incohérents** - Service Bus assure sa propre gestion des messages incohérents. Il est impossible de la contrôler ou de la configurer dans la configuration ou le code d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a32b5-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="a32b5-126">**Comportement de PeekLock** -hello fonctions runtime reçoit un message dans [ `PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) et appelle `Complete` sur le message de type hello si hello est terminée avec succès, ou des appels `Abandon` si hello Échec de la fonction.</span><span class="sxs-lookup"><span data-stu-id="a32b5-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="a32b5-127">Si la fonction hello s’exécute plus longtemps que hello `PeekLock` délai d’attente, les verrous hello est automatiquement renouvelée.</span><span class="sxs-lookup"><span data-stu-id="a32b5-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="a32b5-128">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="a32b5-128">Trigger usage</span></span>
<span data-ttu-id="a32b5-129">Cette section vous montre comment toouse votre Service Bus déclencher dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="a32b5-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="a32b5-130">En c# et F #, message d’appel du déclencheur Service Bus peut être désérialisé tooany Hello les types d’entrée suivants :</span><span class="sxs-lookup"><span data-stu-id="a32b5-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="a32b5-131">`string` - utile pour les messages de type chaîne</span><span class="sxs-lookup"><span data-stu-id="a32b5-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="a32b5-132">`byte[]` - utile pour les données binaires</span><span class="sxs-lookup"><span data-stu-id="a32b5-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="a32b5-133">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) : utile pour les données JSON sérialisées.</span><span class="sxs-lookup"><span data-stu-id="a32b5-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="a32b5-134">Si vous déclarez un type d’entrée personnalisé, tel que `CustomType`, les fonctions Azure essaie de données JSON de hello toodeserialize vers le type spécifié.</span><span class="sxs-lookup"><span data-stu-id="a32b5-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="a32b5-135">`BrokeredMessage`-permet de vous hello désérialisé message avec hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="a32b5-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="a32b5-136">Dans Node.js, message d’appel du déclencheur Service Bus est passé dans la fonction hello comme une chaîne ou un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="a32b5-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="a32b5-137">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="a32b5-137">Trigger sample</span></span>
<span data-ttu-id="a32b5-138">Supposons que vous avez hello suivant function.json :</span><span class="sxs-lookup"><span data-stu-id="a32b5-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="a32b5-139">Voir exemple hello spécifiques au langage qui traite un message de la file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a32b5-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="a32b5-140">C#</span><span class="sxs-lookup"><span data-stu-id="a32b5-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="a32b5-141">F#</span><span class="sxs-lookup"><span data-stu-id="a32b5-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="a32b5-142">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a32b5-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="a32b5-143">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="a32b5-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="a32b5-144">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="a32b5-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="a32b5-145">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="a32b5-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="a32b5-146">Liaison de sortie Service Bus</span><span class="sxs-lookup"><span data-stu-id="a32b5-146">Service Bus output binding</span></span>
<span data-ttu-id="a32b5-147">Hello sortie de file d’attente et rubrique Service Bus pour une fonction utiliser hello objets JSON Bonjour suivants `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="a32b5-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="a32b5-148">Sortie de *file d’attente* :</span><span class="sxs-lookup"><span data-stu-id="a32b5-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="a32b5-149">Sortie de *rubrique* :</span><span class="sxs-lookup"><span data-stu-id="a32b5-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="a32b5-150">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="a32b5-150">Note hello following:</span></span>

* <span data-ttu-id="a32b5-151">Pour `connection`, [créer un paramètre d’application dans votre application de la fonction](functions-how-to-use-azure-function-app-settings.md) qui contient l’espace de noms de Service Bus hello connexion chaîne tooyour, puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre sortie. liaison.</span><span class="sxs-lookup"><span data-stu-id="a32b5-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="a32b5-152">Obtenir de chaîne de connexion hello en suivant les étapes de hello présentés au [obtenir des informations d’identification de gestion hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="a32b5-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="a32b5-153">chaîne de connexion Hello doit être d’un espace de noms Service Bus, tooa non limité, la file d’attente spécifique ou une rubrique.</span><span class="sxs-lookup"><span data-stu-id="a32b5-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="a32b5-154">Si vous laissez `connection` vide, hello liaison de sortie suppose qu’une chaîne de connexion de Service Bus par défaut est spécifiée dans une application de paramètre nommé `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="a32b5-155">Pour `accessRights`, les valeurs disponibles sont `manage` et `listen`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="a32b5-156">valeur par défaut Hello est `manage`, ce qui signifie que hello `connection` a hello **gérer** autorisation.</span><span class="sxs-lookup"><span data-stu-id="a32b5-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="a32b5-157">Si vous utilisez une chaîne de connexion qui n’a pas de hello **gérer** de jeu d’autorisations, `accessRights` trop`listen`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="a32b5-158">Dans le cas contraire, les fonctions hello runtime risque d’échouer lors de la tentative toodo les opérations qui nécessitent les droits de gestion.</span><span class="sxs-lookup"><span data-stu-id="a32b5-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="a32b5-159">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="a32b5-159">Output usage</span></span>
<span data-ttu-id="a32b5-160">En c# et F #, les fonctions Azure peut créer un message de la file d’attente Service Bus à partir d’un des types suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="a32b5-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="a32b5-161">N’importe quel [objet](https://msdn.microsoft.com/library/system.object.aspx) - la définition du paramètre ressemble à `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="a32b5-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="a32b5-162">Fonctions désérialise un objet de hello dans un message JSON.</span><span class="sxs-lookup"><span data-stu-id="a32b5-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="a32b5-163">Si la valeur de sortie hello est null lorsque hello fonction s’arrête, fonctions crée le message de salutation avec un objet null.</span><span class="sxs-lookup"><span data-stu-id="a32b5-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="a32b5-164">`string` - La définition du paramètre ressemble à `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="a32b5-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="a32b5-165">Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.</span><span class="sxs-lookup"><span data-stu-id="a32b5-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="a32b5-166">`byte[]` - La définition du paramètre ressemble à `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="a32b5-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="a32b5-167">Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.</span><span class="sxs-lookup"><span data-stu-id="a32b5-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="a32b5-168">`BrokeredMessage` - La définition du paramètre ressemble à `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="a32b5-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="a32b5-169">Si la valeur du paramètre hello est non null lorsque hello fonction s’arrête, fonctions crée un message.</span><span class="sxs-lookup"><span data-stu-id="a32b5-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="a32b5-170">Pour créer plusieurs messages dans une fonction C#, vous pouvez utiliser `ICollector<T>` ou `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="a32b5-171">Un message est créé lorsque vous appelez hello `Add` (méthode).</span><span class="sxs-lookup"><span data-stu-id="a32b5-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="a32b5-172">Dans Node.js, vous pouvez affecter une chaîne, un tableau d’octets ou un objet de Javascript (désérialisé dans JSON) trop`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="a32b5-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="a32b5-173">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="a32b5-173">Output sample</span></span>
<span data-ttu-id="a32b5-174">Supposons que vous avez hello suivant function.json, qui définit une sortie de la file d’attente Service Bus :</span><span class="sxs-lookup"><span data-stu-id="a32b5-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="a32b5-175">Voir exemple hello spécifiques au langage qui envoie une file d’attente service bus de messages toohello.</span><span class="sxs-lookup"><span data-stu-id="a32b5-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="a32b5-176">C#</span><span class="sxs-lookup"><span data-stu-id="a32b5-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="a32b5-177">F#</span><span class="sxs-lookup"><span data-stu-id="a32b5-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="a32b5-178">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a32b5-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="a32b5-179">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="a32b5-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="a32b5-180">Ou, toocreate plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="a32b5-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="a32b5-181">Exemple de sortie en F#</span><span class="sxs-lookup"><span data-stu-id="a32b5-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="a32b5-182">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="a32b5-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="a32b5-183">Ou, toocreate plusieurs messages :</span><span class="sxs-lookup"><span data-stu-id="a32b5-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a32b5-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a32b5-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

