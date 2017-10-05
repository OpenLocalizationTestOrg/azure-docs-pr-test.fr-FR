---
title: Liaisons Mobile Apps Azure Functions| Microsoft Docs
description: "Découvrez comment utiliser des liaisons Azure Mobile Apps dans Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="08081-104">Liaisons Azure Mobile Apps Azure Functions</span><span class="sxs-lookup"><span data-stu-id="08081-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="08081-105">Cet article explique comment configurer et coder des liaisons [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="08081-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="08081-106">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="08081-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="08081-107">Les liaisons d’entrée et de sortie Mobile Apps vous permettent d’effectuer des opérations de [lecture et écriture dans des tables de données](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations), dans votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="08081-108">Liaison d’entrée Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="08081-108">Mobile Apps input binding</span></span>
<span data-ttu-id="08081-109">La liaison d’entrée Mobile Apps charge un enregistrement à partir d’un point de terminaison de table mobile et le transmet à votre fonction.</span><span class="sxs-lookup"><span data-stu-id="08081-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="08081-110">Dans des fonctions C# et F#, toutes les modifications apportées à l’enregistrement sont automatiquement renvoyées à la table une fois que la fonction s’est correctement terminée.</span><span class="sxs-lookup"><span data-stu-id="08081-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="08081-111">L’entrée Mobile Apps d’une fonction utilise l’objet JSON suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="08081-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="08081-112">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="08081-112">Note the following:</span></span>

* <span data-ttu-id="08081-113">L’élément `id` peut être statique ou basé sur le déclencheur qui appelle la fonction.</span><span class="sxs-lookup"><span data-stu-id="08081-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="08081-114">Par exemple, si vous utilisez un [déclencheur de file d’attente]() pour votre fonction, `"id": "{queueTrigger}"` utilise la valeur de chaîne du message de file d’attente en tant qu’ID de l’enregistrement à récupérer.</span><span class="sxs-lookup"><span data-stu-id="08081-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="08081-115">`connection` doit contenir le nom d’un paramètre d’application de votre application de fonction, comportant l’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="08081-116">La fonction utilise cette URL pour construire les opérations REST requises par rapport à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="08081-117">Vous [créez un paramètre d’application dans votre application de fonction](), contenant l’URL de votre application mobile (de type `http://<appname>.azurewebsites.net`), puis spécifiez le nom du paramètre d’application dans la propriété `connection` de votre liaison d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08081-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="08081-118">Vous devez spécifier `apiKey` si vous [implémentez une clé API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) ou [implémentez une clé API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="08081-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="08081-119">Pour ce faire, vous [créez un paramètre d’application dans votre application de fonction](), contenant la clé API, puis ajoutez la propriété `apiKey` dans votre liaison d’entrée avec le nom du paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="08081-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="08081-120">Cette clé API ne doit pas être partagée avec vos clients d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="08081-121">Elle doit uniquement être distribuée de façon sécurisée aux clients côté service, comme Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="08081-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="08081-122">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="08081-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="08081-123">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="08081-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="08081-124">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="08081-124">Input usage</span></span>
<span data-ttu-id="08081-125">Cette section vous montre comment utiliser la liaison d’entrée Mobile Apps dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="08081-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="08081-126">Lorsque l’enregistrement correspondant à la table et à l’ID d’enregistrement spécifiés est trouvé, il est transmis au paramètre [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) nommé (ou, dans Node.js, à l’objet `context.bindings.<name>`).</span><span class="sxs-lookup"><span data-stu-id="08081-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="08081-127">Si l’enregistrement est introuvable, le paramètre présente la valeur `null`.</span><span class="sxs-lookup"><span data-stu-id="08081-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="08081-128">Dans les fonctions C# et F#, toutes les modifications apportées à l’enregistrement d’entrée (paramètre d’entrée) sont automatiquement renvoyées à la table Mobile Apps une fois que la fonction s’est correctement terminée.</span><span class="sxs-lookup"><span data-stu-id="08081-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="08081-129">Dans les fonctions Node.js, utilisez `context.bindings.<name>` pour accéder à l’enregistrement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08081-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="08081-130">Vous ne pouvez pas modifier un enregistrement dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="08081-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="08081-131">Exemple d’entrée</span><span class="sxs-lookup"><span data-stu-id="08081-131">Input sample</span></span>
<span data-ttu-id="08081-132">Supposons le code function.json suivant, qui récupère un enregistrement de table Mobile Apps avec l’ID du message de déclenchement de file d’attente :</span><span class="sxs-lookup"><span data-stu-id="08081-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="08081-133">Consultez l’exemple dans le langage de votre choix pour voir comment utiliser l’enregistrement d’entrée à partir de la liaison.</span><span class="sxs-lookup"><span data-stu-id="08081-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="08081-134">Les exemples en C# et F# modifient également la propriété `text` de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="08081-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="08081-135">C#</span><span class="sxs-lookup"><span data-stu-id="08081-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="08081-136">Node.JS</span><span class="sxs-lookup"><span data-stu-id="08081-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="08081-137">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="08081-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="08081-138">Exemple d’entrée en Node.js</span><span class="sxs-lookup"><span data-stu-id="08081-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="08081-139">Liaison de sortie Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="08081-139">Mobile Apps output binding</span></span>
<span data-ttu-id="08081-140">Utilisez la liaison de sortie Mobile Apps pour écrire un nouvel enregistrement dans un point de terminaison de table Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="08081-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="08081-141">La sortie Mobile Apps d’une fonction utilise l’objet JSON suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="08081-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="08081-142">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="08081-142">Note the following:</span></span>

* <span data-ttu-id="08081-143">`connection` doit contenir le nom d’un paramètre d’application de votre application de fonction, comportant l’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="08081-144">La fonction utilise cette URL pour construire les opérations REST requises par rapport à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="08081-145">Vous [créez un paramètre d’application dans votre application de fonction](), contenant l’URL de votre application mobile (de type `http://<appname>.azurewebsites.net`), puis spécifiez le nom du paramètre d’application dans la propriété `connection` de votre liaison d’entrée.</span><span class="sxs-lookup"><span data-stu-id="08081-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="08081-146">Vous devez spécifier `apiKey` si vous [implémentez une clé API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) ou [implémentez une clé API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="08081-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="08081-147">Pour ce faire, vous [créez un paramètre d’application dans votre application de fonction](), contenant la clé API, puis ajoutez la propriété `apiKey` dans votre liaison d’entrée avec le nom du paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="08081-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="08081-148">Cette clé API ne doit pas être partagée avec vos clients d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="08081-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="08081-149">Elle doit uniquement être distribuée de façon sécurisée aux clients côté service, comme Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="08081-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="08081-150">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="08081-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="08081-151">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="08081-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="08081-152">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="08081-152">Output usage</span></span>
<span data-ttu-id="08081-153">Cette section vous montre comment utiliser la liaison de sortie Mobile Apps dans le code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="08081-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="08081-154">Dans les fonctions C#, utilisez un paramètre de sortie nommé de type `out object` pour accéder à l’enregistrement de sortie.</span><span class="sxs-lookup"><span data-stu-id="08081-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="08081-155">Dans les fonctions Node.js, utilisez `context.bindings.<name>` pour accéder à l’enregistrement de sortie.</span><span class="sxs-lookup"><span data-stu-id="08081-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="08081-156">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="08081-156">Output sample</span></span>
<span data-ttu-id="08081-157">Supposons le code function.json suivant, qui définit un déclencheur de file d’attente et une sortie Mobile Apps :</span><span class="sxs-lookup"><span data-stu-id="08081-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="08081-158">Consultez l’exemple dans le langage de votre choix pour voir comment créer un enregistrement dans le point de terminaison de la table Mobile Apps avec le contenu du message de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="08081-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="08081-159">C#</span><span class="sxs-lookup"><span data-stu-id="08081-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="08081-160">Node.JS</span><span class="sxs-lookup"><span data-stu-id="08081-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="08081-161">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="08081-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="08081-162">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="08081-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="08081-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08081-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

