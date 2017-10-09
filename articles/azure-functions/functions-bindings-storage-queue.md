---
title: "liaisons de stockage de file d’attente de fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment toouse le stockage Azure déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="54d06-104">Liaisons de stockage de file d’attente d’Azure Functions</span><span class="sxs-lookup"><span data-stu-id="54d06-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="54d06-105">Cet article décrit comment tooconfigure et code liaisons de stockage de file d’attente Azure dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="54d06-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="54d06-106">Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="54d06-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="54d06-107">Pour les fonctionnalités qui sont disponibles dans toutes les liaisons, consultez [Concepts des déclencheurs et liaisons Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="54d06-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="54d06-108">Déclencheur de stockage de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-108">Queue storage trigger</span></span>
<span data-ttu-id="54d06-109">déclencheur de stockage de file d’attente Azure Hello permet toomonitor un stockage de file d’attente pour les nouveaux messages et réagit toothem.</span><span class="sxs-lookup"><span data-stu-id="54d06-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="54d06-110">Définir un déclencheur de la file d’attente à l’aide de hello **intégrer** portail de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="54d06-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="54d06-111">portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="54d06-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="54d06-112">Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="54d06-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="54d06-113">Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54d06-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="54d06-114">Paramètres supplémentaires peuvent être fournies dans un [host.json fichier](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther affiner les déclencheurs de stockage de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54d06-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="54d06-115">Par exemple, vous pouvez modifier la fréquence d’interrogation de file d’attente de hello en host.json.</span><span class="sxs-lookup"><span data-stu-id="54d06-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="54d06-116">Utilisation d’un déclencheur de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-116">Using a queue trigger</span></span>
<span data-ttu-id="54d06-117">Dans les fonctions de Node.js, accéder à l’aide des données de file d’attente hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="54d06-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="54d06-118">Dans les fonctions de .NET, accéder à l’aide d’un paramètre de méthode comme charge utile de file d’attente hello `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="54d06-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="54d06-119">Ici, `paramName` est la valeur hello spécifiée Bonjour [configuration du déclencheur](#trigger).</span><span class="sxs-lookup"><span data-stu-id="54d06-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="54d06-120">message de file d’attente d’appel peut être désérialisé tooany Hello les types suivants :</span><span class="sxs-lookup"><span data-stu-id="54d06-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="54d06-121">Objet POCO.</span><span class="sxs-lookup"><span data-stu-id="54d06-121">POCO object.</span></span> <span data-ttu-id="54d06-122">Utilisez si la charge utile de file d’attente hello est un objet JSON.</span><span class="sxs-lookup"><span data-stu-id="54d06-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="54d06-123">Hello fonctions runtime désérialise la charge utile de hello en objet POCO hello.</span><span class="sxs-lookup"><span data-stu-id="54d06-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="54d06-124">Métadonnées de déclencheur de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-124">Queue trigger metadata</span></span>
<span data-ttu-id="54d06-125">déclencheur de file d’attente Hello fournit plusieurs propriétés de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="54d06-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="54d06-126">Ces propriétés peuvent être utilisées dans les expressions de liaison dans d’autres liaisons ou en tant que paramètres dans votre code.</span><span class="sxs-lookup"><span data-stu-id="54d06-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="54d06-127">les valeurs Hello ont hello même sémantique que [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="54d06-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="54d06-128">**QueueTrigger** : charge utile de la file d’attente (s’il s’agit d’une chaîne valide)</span><span class="sxs-lookup"><span data-stu-id="54d06-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="54d06-129">**DequeueCount** : type `int`.</span><span class="sxs-lookup"><span data-stu-id="54d06-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="54d06-130">Bonjour le nombre de fois où que ce message a été dépilé.</span><span class="sxs-lookup"><span data-stu-id="54d06-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="54d06-131">**ExpirationTime** : type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="54d06-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="54d06-132">temps de Hello ce message hello expire.</span><span class="sxs-lookup"><span data-stu-id="54d06-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="54d06-133">**Id**:type `string`.</span><span class="sxs-lookup"><span data-stu-id="54d06-133">**Id** - Type `string`.</span></span> <span data-ttu-id="54d06-134">ID de message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54d06-134">Queue message ID.</span></span>
* <span data-ttu-id="54d06-135">**InsertionTime** : type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="54d06-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="54d06-136">temps de Hello ce message de type hello a été ajouté à la file d’attente de toohello.</span><span class="sxs-lookup"><span data-stu-id="54d06-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="54d06-137">**NextVisibleTime** : tapez `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="54d06-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="54d06-138">temps de Hello ce message de type hello sera de nouveau visible.</span><span class="sxs-lookup"><span data-stu-id="54d06-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="54d06-139">**PopReceipt** : type `string`.</span><span class="sxs-lookup"><span data-stu-id="54d06-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="54d06-140">accusé de réception pop du message de type Hello.</span><span class="sxs-lookup"><span data-stu-id="54d06-140">hello message's pop receipt.</span></span>

<span data-ttu-id="54d06-141">Consultez Comment toouse hello dans les métadonnées de file d’attente [exemple de déclencheur](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="54d06-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="54d06-142">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="54d06-142">Trigger sample</span></span>
<span data-ttu-id="54d06-143">Supposons que vous avez hello suivant function.json qui définit un déclencheur de la file d’attente :</span><span class="sxs-lookup"><span data-stu-id="54d06-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

<span data-ttu-id="54d06-144">Consultez l’exemple de langage spécifiques hello qui Récupère et enregistre les métadonnées de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="54d06-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="54d06-145">C#</span><span class="sxs-lookup"><span data-stu-id="54d06-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="54d06-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="54d06-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="54d06-147">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="54d06-147">Trigger sample in C#</span></span> #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="54d06-148">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="54d06-148">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="54d06-149">Gestion des messages de file d’attente incohérents</span><span class="sxs-lookup"><span data-stu-id="54d06-149">Handling poison queue messages</span></span>
<span data-ttu-id="54d06-150">En cas d’échec d’une fonction de déclenchement de file d’attente, les fonctions de Azure essaie de nouveau cette fonction des toofive heures pour un message de la file d’attente donnée, y compris hello tout d’abord essayer.</span><span class="sxs-lookup"><span data-stu-id="54d06-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="54d06-151">Si toutes les cinq tentatives échouent, hello fonctions runtime ajoute un stockage de file d’attente message tooa nommé  *&lt;originalqueuename >-incohérents*.</span><span class="sxs-lookup"><span data-stu-id="54d06-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="54d06-152">Vous pouvez écrire une fonction tooprocess messages de file d’attente de messages incohérents hello par les enregistrer ou de l’envoi d’une notification qu’attention manuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="54d06-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="54d06-153">les messages incohérents toohandle vérifier manuellement, hello `dequeueCount` de message de file d’attente hello (consultez [métadonnées de file d’attente déclencheur](#meta)).</span><span class="sxs-lookup"><span data-stu-id="54d06-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="54d06-154">Liaison de sortie de stockage de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-154">Queue storage output binding</span></span>
<span data-ttu-id="54d06-155">liaison vous permet de file d’attente de tooa toowrite messages de sortie Hello stockage de file d’attente Azure.</span><span class="sxs-lookup"><span data-stu-id="54d06-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="54d06-156">Définir une file d’attente de liaison de sortie à l’aide de hello **intégrer** portail de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="54d06-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="54d06-157">portail Hello crée hello définition Bonjour **liaisons** section de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="54d06-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="54d06-158">Hello `connection` propriété doit contenir le nom hello d’un paramètre d’application qui contient une chaîne de connexion de stockage.</span><span class="sxs-lookup"><span data-stu-id="54d06-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="54d06-159">Bonjour portail Azure, hello éditeur standard Bonjour **intégrer** onglet configure ce paramètre d’application pour vous lorsque vous sélectionnez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="54d06-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="54d06-160">Utilisation d’une liaison de sortie de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-160">Using a queue output binding</span></span>
<span data-ttu-id="54d06-161">Dans les fonctions de Node.js, vous accédez à l’aide de file d’attente de sortie hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="54d06-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="54d06-162">Dans les fonctions de .NET, vous pouvez produire tooany Hello les types suivants.</span><span class="sxs-lookup"><span data-stu-id="54d06-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="54d06-163">Lorsqu’il existe un paramètre de type `T`, `T` doit être un des types de sortie hello pris en charge, tel que `string` ou un POCO.</span><span class="sxs-lookup"><span data-stu-id="54d06-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="54d06-164">`out T` (sérialisé au format JSON)</span><span class="sxs-lookup"><span data-stu-id="54d06-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="54d06-165">`out`[`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="54d06-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="54d06-166">Vous pouvez également utiliser le type de retour de méthode hello comme hello liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="54d06-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="54d06-167">Exemple de sortie de file d’attente</span><span class="sxs-lookup"><span data-stu-id="54d06-167">Queue output sample</span></span>
<span data-ttu-id="54d06-168">suivant de Hello *function.json* définit un déclencheur HTTP avec une file d’attente de liaison de sortie :</span><span class="sxs-lookup"><span data-stu-id="54d06-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

<span data-ttu-id="54d06-169">Consultez l’exemple hello spécifiques au langage qui génère un message de la file d’attente avec une charge utile HTTP entrant hello.</span><span class="sxs-lookup"><span data-stu-id="54d06-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="54d06-170">C#</span><span class="sxs-lookup"><span data-stu-id="54d06-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="54d06-171">Node.JS</span><span class="sxs-lookup"><span data-stu-id="54d06-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="54d06-172">Exemple de sortie de file d’attente en C#</span><span class="sxs-lookup"><span data-stu-id="54d06-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

<span data-ttu-id="54d06-173">utilisation de plusieurs messages, toosend un `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="54d06-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="54d06-174">Exemple de sortie de file d’attente en Node.js</span><span class="sxs-lookup"><span data-stu-id="54d06-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="54d06-175">Ou, toosend plusieurs messages,</span><span class="sxs-lookup"><span data-stu-id="54d06-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="54d06-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54d06-176">Next steps</span></span>

<span data-ttu-id="54d06-177">Pour obtenir un exemple d’une fonction qui utilise des déclencheurs de stockage de file d’attente et les liaisons, consultez [créer un service Azure de tooan fonction Azure connecté](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="54d06-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
