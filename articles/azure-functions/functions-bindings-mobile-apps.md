---
title: liaisons des applications mobiles de fonctions aaaAzure | Documents Microsoft
description: "Comprendre comment les liaisons d’applications mobiles Azure toouse dans les fonctions d’Azure."
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
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="b5143-104">Liaisons Azure Mobile Apps Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5143-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b5143-105">Cet article explique comment tooconfigure et code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) liaisons dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b5143-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="b5143-106">Azure Functions prend en charge des liaisons d’entrée et de sortie pour Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="b5143-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="b5143-107">Hello applications mobiles d’entrée et sortie liaisons vous permettent de [lisent et écrivent des tables de toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) dans votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="b5143-108">Liaison d’entrée Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="b5143-108">Mobile Apps input binding</span></span>
<span data-ttu-id="b5143-109">Hello liaison d’entrée des applications mobiles charge un enregistrement à partir d’un point de terminaison de table mobile et le passe dans votre fonction.</span><span class="sxs-lookup"><span data-stu-id="b5143-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="b5143-110">Dans c# et F # fonctions, tout enregistrement toohello de modifications apportées sont automatiquement envoyés arrière toohello table lors de la fonction hello se termine avec succès.</span><span class="sxs-lookup"><span data-stu-id="b5143-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="b5143-111">Hello applications mobiles d’entrée tooa fonction utilise hello objet JSON Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="b5143-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="b5143-112">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5143-112">Note hello following:</span></span>

* <span data-ttu-id="b5143-113">`id`peut être statique, ou il peut être basée sur déclencheur hello qui appelle la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="b5143-114">Par exemple, si vous utilisez un [déclencheur de la file d’attente]() de votre fonction, puis `"id": "{queueTrigger}"` utilise hello la valeur de chaîne de message de file d’attente hello comme enregistrement ID tooretrieve de hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="b5143-115">`connection`doit contenir nom hello d’un paramètre d’application dans votre application de fonction, qui à son tour contient hello les URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="b5143-116">fonction Hello utilise cette URL tooconstruct hello requis des opérations de reste par rapport à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="b5143-117">Vous [créer un paramètre d’application dans votre application de la fonction]() qui contient les URL de votre application mobile (qui ressemble à `http://<appname>.azurewebsites.net`), puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre liaison d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b5143-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b5143-118">Vous devez toospecify `apiKey` si vous [implémenter une clé d’API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implémenter une clé d’API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b5143-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b5143-119">toodo, vous [créer un paramètre d’application dans votre application de la fonction]() qui contient la clé d’API de hello, puis ajoutez hello `apiKey` propriété dans votre liaison d’entrée par nom de hello du paramètre d’application hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b5143-120">Cette clé API ne doit pas être partagée avec vos clients d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b5143-121">Il ne doit être distribuées clients tooservice côté en toute sécurité, comme les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b5143-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b5143-122">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="b5143-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b5143-123">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="b5143-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="b5143-124">Utilisation en entrée</span><span class="sxs-lookup"><span data-stu-id="b5143-124">Input usage</span></span>
<span data-ttu-id="b5143-125">Cette section vous montre comment toouse vos applications mobiles d’entrée de liaison dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="b5143-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="b5143-126">Lors de l’enregistrement hello avec hello spécifié ID de table et d’enregistrement est trouvé, il est passé dans hello nommé [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) paramètre (ou, dans Node.js, il est passé dans hello `context.bindings.<name>` objet).</span><span class="sxs-lookup"><span data-stu-id="b5143-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="b5143-127">Lors de l’enregistrement de hello n’est pas trouvé, le paramètre hello est `null`.</span><span class="sxs-lookup"><span data-stu-id="b5143-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="b5143-128">Dans les fonctions de c# et F #, toute modification apportée toohello entrée enregistrement (paramètre d’entrée) est automatiquement envoyé arrière toohello table des applications mobiles lors de la fonction hello se termine avec succès.</span><span class="sxs-lookup"><span data-stu-id="b5143-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="b5143-129">Dans les fonctions de Node.js, utilisez `context.bindings.<name>` tooaccess hello enregistrement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b5143-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="b5143-130">Vous ne pouvez pas modifier un enregistrement dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="b5143-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="b5143-131">Exemple d’entrée</span><span class="sxs-lookup"><span data-stu-id="b5143-131">Input sample</span></span>
<span data-ttu-id="b5143-132">Supposez que vous avez hello suivant function.json, qui extrait un enregistrement de la table de l’application Mobile avec l’id de hello de message de déclenchement de file d’attente hello :</span><span class="sxs-lookup"><span data-stu-id="b5143-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

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

<span data-ttu-id="b5143-133">Voir l’exemple hello spécifiques à une langue qui utilise l’enregistrement d’entrée de hello à partir de la liaison de hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="b5143-134">les exemples c# et F # Hello également modifier l’enregistrement hello `text` propriété.</span><span class="sxs-lookup"><span data-stu-id="b5143-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="b5143-135">C#</span><span class="sxs-lookup"><span data-stu-id="b5143-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="b5143-136">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b5143-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="b5143-137">Exemple d’entrée en C#</span><span class="sxs-lookup"><span data-stu-id="b5143-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="b5143-138">Exemple d’entrée en Node.js</span><span class="sxs-lookup"><span data-stu-id="b5143-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="b5143-139">Liaison de sortie Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="b5143-139">Mobile Apps output binding</span></span>
<span data-ttu-id="b5143-140">Utilisez hello Mobile Apps sortie liaison toowrite un enregistrement tooa Mobile Apps table point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="b5143-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="b5143-141">Hello des applications mobiles de sortie pour une fonction utilise hello objet JSON Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="b5143-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="b5143-142">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5143-142">Note hello following:</span></span>

* <span data-ttu-id="b5143-143">`connection`doit contenir nom hello d’un paramètre d’application dans votre application de fonction, qui à son tour contient hello les URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="b5143-144">fonction Hello utilise cette URL tooconstruct hello requis des opérations de reste par rapport à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="b5143-145">Vous [créer un paramètre d’application dans votre application de la fonction]() qui contient les URL de votre application mobile (qui ressemble à `http://<appname>.azurewebsites.net`), puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre liaison d’entrée.</span><span class="sxs-lookup"><span data-stu-id="b5143-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="b5143-146">Vous devez toospecify `apiKey` si vous [implémenter une clé d’API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implémenter une clé d’API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="b5143-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="b5143-147">toodo, vous [créer un paramètre d’application dans votre application de la fonction]() qui contient la clé d’API de hello, puis ajoutez hello `apiKey` propriété dans votre liaison d’entrée par nom de hello du paramètre d’application hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="b5143-148">Cette clé API ne doit pas être partagée avec vos clients d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="b5143-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="b5143-149">Il ne doit être distribuées clients tooservice côté en toute sécurité, comme les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b5143-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="b5143-150">Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="b5143-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="b5143-151">Ceci protège vos informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="b5143-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="b5143-152">Utilisation en sortie</span><span class="sxs-lookup"><span data-stu-id="b5143-152">Output usage</span></span>
<span data-ttu-id="b5143-153">Cette section vous montre comment toouse vos applications mobiles de sortie de liaison dans votre code de fonction.</span><span class="sxs-lookup"><span data-stu-id="b5143-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="b5143-154">Dans les fonctions de c#, utilisez un paramètre de sortie nommés de type `out object` tooaccess hello sortie d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="b5143-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="b5143-155">Dans les fonctions de Node.js, utilisez `context.bindings.<name>` tooaccess hello sortie d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="b5143-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b5143-156">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="b5143-156">Output sample</span></span>
<span data-ttu-id="b5143-157">Supposons que vous avez hello suivant function.json, qui définit un déclencheur de la file d’attente et une sortie d’applications mobiles :</span><span class="sxs-lookup"><span data-stu-id="b5143-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="b5143-158">Voir exemple hello spécifiques au langage qui crée un enregistrement de point de terminaison de table hello applications mobiles avec le contenu du message de file d’attente hello hello.</span><span class="sxs-lookup"><span data-stu-id="b5143-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="b5143-159">C#</span><span class="sxs-lookup"><span data-stu-id="b5143-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b5143-160">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b5143-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b5143-161">Exemple de sortie en C#</span><span class="sxs-lookup"><span data-stu-id="b5143-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="b5143-162">Exemple de sortie en Node.js</span><span class="sxs-lookup"><span data-stu-id="b5143-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b5143-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5143-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

