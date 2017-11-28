---
title: "Information de référence pour les développeurs JavaScript sur Azure Functions | Microsoft Docs"
description: "Découvrez comment développer des fonctions à l’aide de JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="3e878-104">Guide des développeurs JavaScript sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e878-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="3e878-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="3e878-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="3e878-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="3e878-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3e878-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="3e878-108">L’expérience JavaScript pour Azure Functions facilite l’exportation d’une fonction qui reçoit un objet `context` pour communiquer avec le runtime et pour recevoir et envoyer des données par le biais des liaisons.</span><span class="sxs-lookup"><span data-stu-id="3e878-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="3e878-109">Cet article suppose que vous ayez déjà lu l’article [Informations de référence pour les développeurs sur Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="3e878-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="3e878-110">Exporter une fonction</span><span class="sxs-lookup"><span data-stu-id="3e878-110">Exporting a function</span></span>
<span data-ttu-id="3e878-111">Toutes les fonctions JavaScript doivent exporter un seul `function` par le biais de `module.exports` pour que le runtime trouve la fonction et l’exécute.</span><span class="sxs-lookup"><span data-stu-id="3e878-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="3e878-112">Cette fonction doit toujours inclure un objet `context` .</span><span class="sxs-lookup"><span data-stu-id="3e878-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="3e878-113">Les liaisons de `direction === "in"` sont transmises en tant qu’arguments de fonction, ce qui signifie que vous pouvez utiliser [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) pour gérer de manière dynamique les nouvelles entrées (par exemple, en utilisant `arguments.length` pour effectuer une itération sur toutes vos entrées).</span><span class="sxs-lookup"><span data-stu-id="3e878-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="3e878-114">Cette fonctionnalité est pratique si vous ne disposez que d’un déclencheur sans entrée supplémentaire, dans la mesure où vous pouvez accéder de manière prévisible aux données de votre déclencheur sans faire référence à votre objet `context`.</span><span class="sxs-lookup"><span data-stu-id="3e878-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="3e878-115">Les arguments sont toujours transmis à la fonction dans leur ordre d’apparition dans *function.json*, même si vous ne les spécifiez pas dans votre instruction d’exportation.</span><span class="sxs-lookup"><span data-stu-id="3e878-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="3e878-116">Par exemple, si vous avez `function(context, a, b)` et le remplacez par `function(context, a)`, vous pouvez toujours obtenir la valeur `b` dans le code de fonction en faisant référence à `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="3e878-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="3e878-117">Toutes les liaisons, quelle que soit leur direction, sont également transmises sur l’objet `context` (voir le script ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="3e878-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="3e878-118">Objet de contexte</span><span class="sxs-lookup"><span data-stu-id="3e878-118">context object</span></span>
<span data-ttu-id="3e878-119">Le runtime utilise un objet `context` pour transmettre des données vers et à partir de votre fonction et vous permettre de communiquer avec le runtime.</span><span class="sxs-lookup"><span data-stu-id="3e878-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="3e878-120">L’objet de contexte est toujours le premier paramètre d’une fonction et doit toujours être inclus, car il possède des méthodes telles que `context.done` et `context.log` nécessaires pour utiliser correctement le runtime.</span><span class="sxs-lookup"><span data-stu-id="3e878-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="3e878-121">Vous pouvez nommer l’objet comme vous le souhaitez (par exemple, `ctx` ou `c`).</span><span class="sxs-lookup"><span data-stu-id="3e878-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="3e878-122">Propriété context.bindings</span><span class="sxs-lookup"><span data-stu-id="3e878-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="3e878-123">Retourne un objet nommé qui contient toutes vos données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="3e878-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="3e878-124">Par exemple, la définition de liaison suivante dans votre *function.json* vous permet d’accéder au contenu de la file d’attente à partir de l’objet `context.bindings.myInput`.</span><span class="sxs-lookup"><span data-stu-id="3e878-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="3e878-125">Méthode context.done</span><span class="sxs-lookup"><span data-stu-id="3e878-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="3e878-126">Informe le runtime que votre code est terminé.</span><span class="sxs-lookup"><span data-stu-id="3e878-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="3e878-127">Vous devez appeler `context.done`. Sinon, le runtime ne sait pas que votre fonction est terminée et que l’exécution va expirer.</span><span class="sxs-lookup"><span data-stu-id="3e878-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="3e878-128">La méthode `context.done` permet de transmettre une erreur définie par l’utilisateur au runtime ainsi qu’un conteneur de propriétés, qui remplaceront les propriétés de l’objet `context.bindings`.</span><span class="sxs-lookup"><span data-stu-id="3e878-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="3e878-129">Méthode context.log</span><span class="sxs-lookup"><span data-stu-id="3e878-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="3e878-130">Vous permet d’écrire dans les journaux de console de streaming au niveau de trace par défaut.</span><span class="sxs-lookup"><span data-stu-id="3e878-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="3e878-131">Des méthodes de journalisation supplémentaires sont disponibles sur `context.log` pour vous permettre d’écrire dans le journal de console à d’autres niveaux de trace :</span><span class="sxs-lookup"><span data-stu-id="3e878-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="3e878-132">Méthode</span><span class="sxs-lookup"><span data-stu-id="3e878-132">Method</span></span>                 | <span data-ttu-id="3e878-133">Description</span><span class="sxs-lookup"><span data-stu-id="3e878-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="3e878-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3e878-134">**error(_message_)**</span></span>   | <span data-ttu-id="3e878-135">Écrit dans la journalisation du niveau d’erreur, ou à un niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="3e878-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="3e878-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3e878-136">**warn(_message_)**</span></span>    | <span data-ttu-id="3e878-137">Écrit dans la journalisation du niveau d’avertissement, ou à un niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="3e878-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="3e878-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3e878-138">**info(_message_)**</span></span>    | <span data-ttu-id="3e878-139">Écrit dans la journalisation du niveau d’information, ou à un niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="3e878-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="3e878-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="3e878-140">**verbose(_message_)**</span></span> | <span data-ttu-id="3e878-141">Écrit dans la journalisation du niveau détaillé.</span><span class="sxs-lookup"><span data-stu-id="3e878-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="3e878-142">L’exemple suivant écrit dans la console au niveau de trace d’avertissement :</span><span class="sxs-lookup"><span data-stu-id="3e878-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="3e878-143">Vous pouvez définir le seuil du niveau de trace pour la journalisation dans le fichier host.json, ou le désactiver.</span><span class="sxs-lookup"><span data-stu-id="3e878-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="3e878-144">Pour plus d’informations sur l’écriture dans les journaux, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="3e878-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="3e878-145">Type de données d’une liaison</span><span class="sxs-lookup"><span data-stu-id="3e878-145">Binding data type</span></span>

<span data-ttu-id="3e878-146">Pour définir le type de données pour une liaison d’entrée, utilisez la propriété `dataType` dans la définition de la liaison.</span><span class="sxs-lookup"><span data-stu-id="3e878-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="3e878-147">Par exemple, pour lire le contenu d’une requête HTTP au format binaire, utilisez le type `binary` :</span><span class="sxs-lookup"><span data-stu-id="3e878-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="3e878-148">Les autres options pour `dataType` sont `stream` et `string`.</span><span class="sxs-lookup"><span data-stu-id="3e878-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="3e878-149">Écrire la sortie de trace dans la console</span><span class="sxs-lookup"><span data-stu-id="3e878-149">Writing trace output to the console</span></span> 

<span data-ttu-id="3e878-150">Dans Functions, vous utilisez les méthodes `context.log` pour écrire la sortie de trace dans la console.</span><span class="sxs-lookup"><span data-stu-id="3e878-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="3e878-151">À ce stade, vous ne pouvez pas utiliser `console.log` pour écrire dans la console.</span><span class="sxs-lookup"><span data-stu-id="3e878-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="3e878-152">Lorsque vous appelez `context.log()`, votre message est écrit dans la console au niveau de trace par défaut, qui est le niveau de trace d’_informations_.</span><span class="sxs-lookup"><span data-stu-id="3e878-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="3e878-153">Le code suivant écrit dans la console au niveau de trace d’informations :</span><span class="sxs-lookup"><span data-stu-id="3e878-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="3e878-154">Il équivaut à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="3e878-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="3e878-155">Le code suivant écrit dans la console au niveau de trace d’erreur :</span><span class="sxs-lookup"><span data-stu-id="3e878-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="3e878-156">Étant donné que le niveau d’_erreur_ constitue le niveau de trace le plus élevé, cette trace est écrite dans la sortie à tous les niveaux de trace tant que la journalisation est activée.</span><span class="sxs-lookup"><span data-stu-id="3e878-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="3e878-157">Toutes les méthodes `context.log` prennent en charge le même format de paramètre que celui pris en charge par la [méthode util.format](https://nodejs.org/api/util.html#util_util_format_format) Node.js.</span><span class="sxs-lookup"><span data-stu-id="3e878-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="3e878-158">Prenons le code suivant qui écrit dans la console en utilisant le niveau de trace par défaut :</span><span class="sxs-lookup"><span data-stu-id="3e878-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="3e878-159">Vous pouvez écrire ce même code au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3e878-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="3e878-160">Configurer le niveau de trace pour la journalisation de la console</span><span class="sxs-lookup"><span data-stu-id="3e878-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="3e878-161">Functions vous permet de définir le niveau de trace du seuil pour écrire dans la console, ce qui facilite le contrôle de l’écriture des traces dans la console à partir de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="3e878-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="3e878-162">Utilisez la propriété `tracing.consoleLevel` dans le fichier host.json pour définir le seuil de toutes les traces écrites dans la console.</span><span class="sxs-lookup"><span data-stu-id="3e878-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="3e878-163">Ce paramètre s’applique à toutes les fonctions dans votre Function App.</span><span class="sxs-lookup"><span data-stu-id="3e878-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="3e878-164">L’exemple suivant définit le seuil de trace permettant d’activer la journalisation détaillée :</span><span class="sxs-lookup"><span data-stu-id="3e878-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="3e878-165">Les valeurs de **consoleLevel** correspondent aux noms des méthodes `context.log`.</span><span class="sxs-lookup"><span data-stu-id="3e878-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="3e878-166">Pour désactiver toutes les journalisations de trace dans la console, définissez **consoleLevel** sur _désactivé_.</span><span class="sxs-lookup"><span data-stu-id="3e878-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="3e878-167">Pour plus d’informations sur le fichier host.json, consultez la [rubrique de référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="3e878-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="3e878-168">Déclencheurs et liaisons HTTP</span><span class="sxs-lookup"><span data-stu-id="3e878-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="3e878-169">Les déclencheurs HTTP et webhook ainsi que les liaisons de sortie HTTP utilisent les objets de requête et de réponse pour représenter la messagerie HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e878-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="3e878-170">Objet Requête</span><span class="sxs-lookup"><span data-stu-id="3e878-170">Request object</span></span>

<span data-ttu-id="3e878-171">L’objet `request` dispose des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e878-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="3e878-172">Propriété</span><span class="sxs-lookup"><span data-stu-id="3e878-172">Property</span></span>      | <span data-ttu-id="3e878-173">Description</span><span class="sxs-lookup"><span data-stu-id="3e878-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="3e878-174">_body_</span><span class="sxs-lookup"><span data-stu-id="3e878-174">_body_</span></span>        | <span data-ttu-id="3e878-175">Objet qui contient le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="3e878-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="3e878-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="3e878-176">_headers_</span></span>     | <span data-ttu-id="3e878-177">Objet qui contient les en-têtes de la demande.</span><span class="sxs-lookup"><span data-stu-id="3e878-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="3e878-178">_method_</span><span class="sxs-lookup"><span data-stu-id="3e878-178">_method_</span></span>      | <span data-ttu-id="3e878-179">Méthode HTTP de la demande.</span><span class="sxs-lookup"><span data-stu-id="3e878-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="3e878-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="3e878-180">_originalUrl_</span></span> | <span data-ttu-id="3e878-181">URL de la demande.</span><span class="sxs-lookup"><span data-stu-id="3e878-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="3e878-182">_params_</span><span class="sxs-lookup"><span data-stu-id="3e878-182">_params_</span></span>      | <span data-ttu-id="3e878-183">Objet qui contient les paramètres de routage de la demande.</span><span class="sxs-lookup"><span data-stu-id="3e878-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="3e878-184">_query_</span><span class="sxs-lookup"><span data-stu-id="3e878-184">_query_</span></span>       | <span data-ttu-id="3e878-185">Objet qui contient les paramètres de la requête.</span><span class="sxs-lookup"><span data-stu-id="3e878-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="3e878-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="3e878-186">_rawBody_</span></span>     | <span data-ttu-id="3e878-187">Corps du message en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="3e878-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="3e878-188">Objet Réponse</span><span class="sxs-lookup"><span data-stu-id="3e878-188">Response object</span></span>

<span data-ttu-id="3e878-189">L’objet `response` dispose des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e878-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="3e878-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="3e878-190">Property</span></span>  | <span data-ttu-id="3e878-191">Description</span><span class="sxs-lookup"><span data-stu-id="3e878-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="3e878-192">_body_</span><span class="sxs-lookup"><span data-stu-id="3e878-192">_body_</span></span>    | <span data-ttu-id="3e878-193">Objet qui contient le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="3e878-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="3e878-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="3e878-194">_headers_</span></span> | <span data-ttu-id="3e878-195">Objet qui contient les en-têtes de la réponse.</span><span class="sxs-lookup"><span data-stu-id="3e878-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="3e878-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="3e878-196">_isRaw_</span></span>   | <span data-ttu-id="3e878-197">Indique que la mise en forme est ignorée pour la réponse.</span><span class="sxs-lookup"><span data-stu-id="3e878-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="3e878-198">_statut_</span><span class="sxs-lookup"><span data-stu-id="3e878-198">_status_</span></span>  | <span data-ttu-id="3e878-199">Code d’état HTTP de la réponse.</span><span class="sxs-lookup"><span data-stu-id="3e878-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="3e878-200">Accès à la demande et à la réponse</span><span class="sxs-lookup"><span data-stu-id="3e878-200">Accessing the request and response</span></span> 

<span data-ttu-id="3e878-201">Lorsque vous travaillez avec des déclencheurs HTTP, trois méthodes vous permettent d’accéder à des objets de demande et de réponse HTTP :</span><span class="sxs-lookup"><span data-stu-id="3e878-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="3e878-202">À partir de des liaisons dites d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="3e878-202">From the named input and output bindings.</span></span> <span data-ttu-id="3e878-203">Avec cette méthode, le déclencheur HTTP et les liaisons fonctionnent de la même manière que toute autre liaison.</span><span class="sxs-lookup"><span data-stu-id="3e878-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="3e878-204">L’exemple suivant définit l’objet de réponse en utilisant une liaison nommée `response` :</span><span class="sxs-lookup"><span data-stu-id="3e878-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="3e878-205">À partir des propriétés `req` et `res` sur l’objet `context`.</span><span class="sxs-lookup"><span data-stu-id="3e878-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="3e878-206">Avec cette méthode, vous pouvez utiliser le modèle classique pour accéder aux données HTTP à partir de l’objet de contexte, au lieu d’utiliser le modèle `context.bindings.name` complet.</span><span class="sxs-lookup"><span data-stu-id="3e878-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="3e878-207">L’exemple suivant montre comment accéder aux objets `req` et `res` sur `context` :</span><span class="sxs-lookup"><span data-stu-id="3e878-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="3e878-208">En appelant `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="3e878-208">By calling `context.done()`.</span></span> <span data-ttu-id="3e878-209">Un type spécial de liaison HTTP renvoie la réponse transmise à la méthode `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="3e878-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="3e878-210">La liaison de sortie HTTP suivante définit un paramètre de sortie `$return` :</span><span class="sxs-lookup"><span data-stu-id="3e878-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="3e878-211">Cette liaison de sortie suppose que vous fournissiez la réponse lorsque vous appelez `done()` comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e878-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="3e878-212">Version du nœud et gestion des packages</span><span class="sxs-lookup"><span data-stu-id="3e878-212">Node version and Package Management</span></span>
<span data-ttu-id="3e878-213">La version de Node est actuellement verrouillée sur `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="3e878-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="3e878-214">Nous examinons la prise en charge d’autres versions ainsi que le fait de la rendre configurable.</span><span class="sxs-lookup"><span data-stu-id="3e878-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="3e878-215">Les étapes suivantes vous permettent d’inclure des packages dans votre Function App :</span><span class="sxs-lookup"><span data-stu-id="3e878-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="3e878-216">Accédez à `https://<function_app_name>.scm.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="3e878-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="3e878-217">Cliquez sur **Console de débogage** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="3e878-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="3e878-218">Accédez à `D:\home\site\wwwroot`, puis faites glisser le fichier package.json vers le dossier **wwwroot** dans la partie supérieure de la page.</span><span class="sxs-lookup"><span data-stu-id="3e878-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="3e878-219">Il existe d’autres manières de télécharger des fichiers dans votre Function App.</span><span class="sxs-lookup"><span data-stu-id="3e878-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="3e878-220">Pour plus d’informations, consultez [Comment mettre à jour les fichiers du conteneur de fonctions](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="3e878-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="3e878-221">Une fois le fichier package.json chargé, exécutez la commande `npm install` dans la **console d’exécution à distance Kudu**.</span><span class="sxs-lookup"><span data-stu-id="3e878-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="3e878-222">Les packages d’actions indiqués dans le fichier package.json sont téléchargés et Function App redémarre.</span><span class="sxs-lookup"><span data-stu-id="3e878-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="3e878-223">Une fois les packages nécessaires installés, vous pouvez les importer dans votre fonction en appelant `require('packagename')`, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3e878-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="3e878-224">Vous devez définir un fichier `package.json` à la racine de votre Function App.</span><span class="sxs-lookup"><span data-stu-id="3e878-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="3e878-225">Cela permet à toutes les fonctions de l’application de partager les mêmes packages mis en cache, pour des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="3e878-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="3e878-226">En cas de conflit de version, vous pouvez ajouter un fichier `package.json` dans le dossier d’une fonction spécifique pour le résoudre.</span><span class="sxs-lookup"><span data-stu-id="3e878-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="3e878-227">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="3e878-227">Environment variables</span></span>
<span data-ttu-id="3e878-228">Pour obtenir une variable d’environnement ou une valeur de paramètre d’application, utilisez `process.env`, comme illustré dans l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="3e878-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="3e878-229">Considérations relatives aux fonctions JavaScript</span><span class="sxs-lookup"><span data-stu-id="3e878-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="3e878-230">Lorsque vous utilisez des fonctions JavaScript, tenez compte des considérations décrites dans les deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="3e878-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="3e878-231">Choisir des plans App Service à cœur unique</span><span class="sxs-lookup"><span data-stu-id="3e878-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="3e878-232">Lorsque vous créez une Function App qui utilise le plan App Service, nous vous recommandons de sélectionner un plan à cœur unique plutôt qu’un plan à plusieurs cœurs.</span><span class="sxs-lookup"><span data-stu-id="3e878-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="3e878-233">À l’heure actuelle, Functions exécute les fonctions JavaScript plus efficacement sur des machines virtuelles à cœur unique. Le recours à de plus grandes machines virtuelles ne produit pas les améliorations de performances attendues.</span><span class="sxs-lookup"><span data-stu-id="3e878-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="3e878-234">Le cas échéant, vous pouvez faire une mise à l’échelle horizontale manuellement en ajoutant des instances de machine virtuelle à cœur unique, ou vous pouvez activer la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="3e878-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="3e878-235">Pour plus d’informations, consultez [Mettre à l’échelle le nombre d’instances manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e878-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="3e878-236">Prise en charge de typeScript et CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="3e878-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="3e878-237">Comme il n’existe encore aucune prise en charge directe pour l’auto-compilation de TypeScript/CoffeeScript via le runtime, cela nécessite une gestion externe au runtime, au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="3e878-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3e878-238">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e878-238">Next steps</span></span>
<span data-ttu-id="3e878-239">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e878-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="3e878-240">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="3e878-241">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="3e878-242">Informations de référence pour les développeurs C# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="3e878-243">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="3e878-244">Déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3e878-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

