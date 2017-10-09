---
title: "référence du développeur pour les fonctions Azure aaaJavaScript | Documents Microsoft"
description: "Comprendre le fonctionnement de toodevelop à l’aide de JavaScript."
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="40489-104">Guide des développeurs JavaScript sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40489-105">Script C#</span><span class="sxs-lookup"><span data-stu-id="40489-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="40489-106">Script F#</span><span class="sxs-lookup"><span data-stu-id="40489-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="40489-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="40489-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="40489-108">Hello JavaScript expérience pour les fonctions Azure rend facile tooexport une fonction qui est passée comme un `context` objet permettant de communiquer avec le runtime de hello et pour recevoir et envoyer des données via les liaisons.</span><span class="sxs-lookup"><span data-stu-id="40489-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="40489-109">Cet article suppose que vous avez déjà lu hello [référence du développeur Azure fonctions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="40489-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="40489-110">Exporter une fonction</span><span class="sxs-lookup"><span data-stu-id="40489-110">Exporting a function</span></span>
<span data-ttu-id="40489-111">Toutes les fonctions JavaScript doivent exporter un seul `function` via `module.exports` pour hello runtime toofind hello fonction et l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="40489-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="40489-112">Cette fonction doit toujours inclure un objet `context` .</span><span class="sxs-lookup"><span data-stu-id="40489-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="40489-113">Liaisons de `direction === "in"` sont passés comme arguments de fonction, ce qui signifie que vous pouvez utiliser [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically gérer de nouvelles entrées (par exemple, à l’aide de `arguments.length` tooiterate sur toutes vos entrées).</span><span class="sxs-lookup"><span data-stu-id="40489-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="40489-114">Cette fonctionnalité est pratique si vous ne disposez que d’un déclencheur sans entrée supplémentaire, dans la mesure où vous pouvez accéder de manière prévisible aux données de votre déclencheur sans faire référence à votre objet `context`.</span><span class="sxs-lookup"><span data-stu-id="40489-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="40489-115">arguments de Hello sont toujours passées le long de la fonction toohello dans l’ordre de hello dans lequel ils apparaissent dans *function.json*, même si vous ne les spécifiez dans votre instruction d’exportations.</span><span class="sxs-lookup"><span data-stu-id="40489-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="40489-116">Par exemple, si vous avez `function(context, a, b)` et modifiez-le trop`function(context, a)`, vous pouvez toujours obtenir les valeur hello `b` dans le code de fonction en vous reportant trop`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="40489-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="40489-117">Toutes les liaisons, quelle que soit la direction, sont également transmis sur hello `context` (voir hello script suivant) de l’objet.</span><span class="sxs-lookup"><span data-stu-id="40489-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="40489-118">Objet de contexte</span><span class="sxs-lookup"><span data-stu-id="40489-118">context object</span></span>
<span data-ttu-id="40489-119">Hello runtime utilise un `context` objet toopass données tooand à partir de votre fonction et le toolet vous communiquez avec le runtime de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="40489-120">Hello objet de contexte est toujours première fonction de tooa paramètre hello et doit être inclus, car il possède des méthodes telles que `context.done` et `context.log`, qui sont requis toouse hello runtime correctement.</span><span class="sxs-lookup"><span data-stu-id="40489-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="40489-121">Vous pouvez nommer les objets hello ce que vous voulez (par exemple, `ctx` ou `c`).</span><span class="sxs-lookup"><span data-stu-id="40489-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="40489-122">Propriété context.bindings</span><span class="sxs-lookup"><span data-stu-id="40489-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="40489-123">Retourne un objet nommé qui contient toutes vos données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="40489-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="40489-124">Par exemple, hello après la définition de la liaison dans votre *function.json* permet d’accéder à hello le contenu de la file d’attente de hello de hello `context.bindings.myInput` objet.</span><span class="sxs-lookup"><span data-stu-id="40489-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="40489-125">Méthode context.done</span><span class="sxs-lookup"><span data-stu-id="40489-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="40489-126">Informe le runtime hello que votre code est terminée.</span><span class="sxs-lookup"><span data-stu-id="40489-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="40489-127">Vous devez appeler `context.done`, ou autre hello runtime jamais sait que votre fonction est terminée et l’exécution de hello va expirer.</span><span class="sxs-lookup"><span data-stu-id="40489-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="40489-128">Hello `context.done` méthode permet de vous toopass sauvegarder un runtime de toohello d’erreur définis par l’utilisateur et un sac de propriétés qui remplacent les propriétés de hello sur hello `context.bindings` objet.</span><span class="sxs-lookup"><span data-stu-id="40489-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="40489-129">Méthode context.log</span><span class="sxs-lookup"><span data-stu-id="40489-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="40489-130">Vous permet de toowrite toohello diffusion en continu journaux de la console au niveau de trace par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="40489-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="40489-131">Sur `context.log`, d’autres méthodes de journalisation qui vous permettre d’écrire le journal de la console toohello à d’autres niveaux de trace :</span><span class="sxs-lookup"><span data-stu-id="40489-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="40489-132">Méthode</span><span class="sxs-lookup"><span data-stu-id="40489-132">Method</span></span>                 | <span data-ttu-id="40489-133">Description</span><span class="sxs-lookup"><span data-stu-id="40489-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="40489-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="40489-134">**error(_message_)**</span></span>   | <span data-ttu-id="40489-135">Écrit tooerror au niveau de journalisation, ou inférieure.</span><span class="sxs-lookup"><span data-stu-id="40489-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="40489-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="40489-136">**warn(_message_)**</span></span>    | <span data-ttu-id="40489-137">Écrit toowarning au niveau de journalisation, ou inférieure.</span><span class="sxs-lookup"><span data-stu-id="40489-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="40489-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="40489-138">**info(_message_)**</span></span>    | <span data-ttu-id="40489-139">Écrit tooinfo au niveau de journalisation, ou inférieure.</span><span class="sxs-lookup"><span data-stu-id="40489-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="40489-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="40489-140">**verbose(_message_)**</span></span> | <span data-ttu-id="40489-141">Écrit la journalisation au niveau du tooverbose.</span><span class="sxs-lookup"><span data-stu-id="40489-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="40489-142">Hello exemple suivant écrit console toohello au niveau de trace d’avertissement hello :</span><span class="sxs-lookup"><span data-stu-id="40489-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="40489-143">Vous pouvez définir le seuil de niveau de trace hello pour l’enregistrement dans le fichier de host.json hello ou mettez-le hors tension.</span><span class="sxs-lookup"><span data-stu-id="40489-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="40489-144">Pour plus d’informations sur le fonctionnement des journaux toowrite toohello, consultez la section de suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="40489-145">Type de données d’une liaison</span><span class="sxs-lookup"><span data-stu-id="40489-145">Binding data type</span></span>

<span data-ttu-id="40489-146">toodefine type de données de hello pour une liaison d’entrée, utilisez hello `dataType` propriété dans la définition de la liaison hello.</span><span class="sxs-lookup"><span data-stu-id="40489-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="40489-147">Par exemple, tooread hello contenu d’une requête HTTP au format binaire, utilisez le type de hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="40489-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="40489-148">Les autres options pour `dataType` sont `stream` et `string`.</span><span class="sxs-lookup"><span data-stu-id="40489-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="40489-149">Console de toohello de sortie de trace en écriture</span><span class="sxs-lookup"><span data-stu-id="40489-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="40489-150">Dans les fonctions, vous utilisez hello `context.log` console toohello de méthodes toowrite trace sortie.</span><span class="sxs-lookup"><span data-stu-id="40489-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="40489-151">À ce stade, vous ne pouvez pas utiliser `console.log` toowrite toohello console.</span><span class="sxs-lookup"><span data-stu-id="40489-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="40489-152">Lorsque vous appelez `context.log()`, votre message est écrit console toohello au niveau de trace par défaut de hello, qui est hello _info_ niveau de suivi.</span><span class="sxs-lookup"><span data-stu-id="40489-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="40489-153">Hello de code suivant écrit console toohello au niveau de trace hello info :</span><span class="sxs-lookup"><span data-stu-id="40489-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="40489-154">Bonjour code précédent est équivalent toohello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="40489-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="40489-155">Hello de code suivant écrit console toohello au niveau d’erreur hello :</span><span class="sxs-lookup"><span data-stu-id="40489-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="40489-156">Étant donné que _erreur_ est hello de trace la plus élevée au niveau, cette trace est écrite sortie toohello à tous les niveaux de trace tant que la journalisation est activée.</span><span class="sxs-lookup"><span data-stu-id="40489-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="40489-157">Tous les `context.log` méthodes prennent en charge hello même format de paramètre est pris en charge par hello Node.js [util.format méthode](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="40489-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="40489-158">Tenez compte des hello suivant de code, qui écrit toohello console à l’aide du niveau de trace par défaut hello :</span><span class="sxs-lookup"><span data-stu-id="40489-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="40489-159">Vous pouvez également hello écriture même code Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="40489-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="40489-160">Configurer le niveau de trace hello pour la journalisation de console</span><span class="sxs-lookup"><span data-stu-id="40489-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="40489-161">Fonctions vous permet de définir le niveau de trace hello seuil pour l’écriture de console toohello, ce qui rend la façon de hello toocontrol facilement les traces sont écrites toohello console à partir de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="40489-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="40489-162">seuil de hello tooset pour toutes les traces écrites toohello console, utilisez hello `tracing.consoleLevel` propriété dans le fichier de host.json hello.</span><span class="sxs-lookup"><span data-stu-id="40489-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="40489-163">Ce paramètre s’applique à des fonctions de tooall dans votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="40489-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="40489-164">Hello exemple suivant définit la journalisation documentée hello trace seuil tooenable :</span><span class="sxs-lookup"><span data-stu-id="40489-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="40489-165">Les valeurs de **consoleLevel** correspondent toohello les noms de hello `context.log` méthodes.</span><span class="sxs-lookup"><span data-stu-id="40489-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="40489-166">le jeu de la trace de toutes les journalisation toohello console, toodisable **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="40489-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="40489-167">Pour plus d’informations sur le fichier de host.json hello, consultez hello [rubrique de référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="40489-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="40489-168">Déclencheurs et liaisons HTTP</span><span class="sxs-lookup"><span data-stu-id="40489-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="40489-169">De sortie HTTP et les déclencheurs de webhook et HTTP liaisons utilisent la demande et messages de réponse objets toorepresent hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="40489-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="40489-170">Objet Requête</span><span class="sxs-lookup"><span data-stu-id="40489-170">Request object</span></span>

<span data-ttu-id="40489-171">Hello `request` objet a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="40489-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="40489-172">Propriété</span><span class="sxs-lookup"><span data-stu-id="40489-172">Property</span></span>      | <span data-ttu-id="40489-173">Description</span><span class="sxs-lookup"><span data-stu-id="40489-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="40489-174">_body_</span><span class="sxs-lookup"><span data-stu-id="40489-174">_body_</span></span>        | <span data-ttu-id="40489-175">Objet qui contient le corps hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="40489-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="40489-176">_headers_</span></span>     | <span data-ttu-id="40489-177">Objet qui contient les en-têtes de demande hello.</span><span class="sxs-lookup"><span data-stu-id="40489-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="40489-178">_method_</span><span class="sxs-lookup"><span data-stu-id="40489-178">_method_</span></span>      | <span data-ttu-id="40489-179">Bonjour la méthode HTTP de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="40489-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="40489-180">_originalUrl_</span></span> | <span data-ttu-id="40489-181">Hello l’URL de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="40489-182">_params_</span><span class="sxs-lookup"><span data-stu-id="40489-182">_params_</span></span>      | <span data-ttu-id="40489-183">Objet qui contient les paramètres de routage hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="40489-184">_query_</span><span class="sxs-lookup"><span data-stu-id="40489-184">_query_</span></span>       | <span data-ttu-id="40489-185">Objet qui contient des paramètres de requête hello.</span><span class="sxs-lookup"><span data-stu-id="40489-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="40489-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="40489-186">_rawBody_</span></span>     | <span data-ttu-id="40489-187">corps de Hello du message de type hello en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="40489-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="40489-188">Objet Réponse</span><span class="sxs-lookup"><span data-stu-id="40489-188">Response object</span></span>

<span data-ttu-id="40489-189">Hello `response` objet a hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="40489-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="40489-190">Propriété</span><span class="sxs-lookup"><span data-stu-id="40489-190">Property</span></span>  | <span data-ttu-id="40489-191">Description</span><span class="sxs-lookup"><span data-stu-id="40489-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="40489-192">_body_</span><span class="sxs-lookup"><span data-stu-id="40489-192">_body_</span></span>    | <span data-ttu-id="40489-193">Objet qui contient le corps de réponse de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="40489-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="40489-194">_headers_</span></span> | <span data-ttu-id="40489-195">Objet qui contient les en-têtes de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="40489-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="40489-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="40489-196">_isRaw_</span></span>   | <span data-ttu-id="40489-197">Indique que la mise en forme est ignorée pour la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="40489-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="40489-198">_statut_</span><span class="sxs-lookup"><span data-stu-id="40489-198">_status_</span></span>  | <span data-ttu-id="40489-199">code d’état HTTP de la réponse de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="40489-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="40489-200">L’accès à la demande de hello et de réponse</span><span class="sxs-lookup"><span data-stu-id="40489-200">Accessing hello request and response</span></span> 

<span data-ttu-id="40489-201">Lorsque vous travaillez avec des déclencheurs HTTP, vous pouvez accéder aux objets de demande et de réponse HTTP dans une des trois manières hello :</span><span class="sxs-lookup"><span data-stu-id="40489-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="40489-202">Hello nommé d’entrée et de sortie des liaisons.</span><span class="sxs-lookup"><span data-stu-id="40489-202">From hello named input and output bindings.</span></span> <span data-ttu-id="40489-203">De cette façon, le déclencheur HTTP hello et liaisons fonctionnent hello même comme toute autre liaison.</span><span class="sxs-lookup"><span data-stu-id="40489-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="40489-204">Hello exemple suivant définit l’objet de réponse hello aide portant un nom `response` liaison :</span><span class="sxs-lookup"><span data-stu-id="40489-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="40489-205">À partir de `req` et `res` propriétés hello `context` objet.</span><span class="sxs-lookup"><span data-stu-id="40489-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="40489-206">De cette façon, vous pouvez utiliser les données de tooaccess HTTP de modèle classique de hello à partir de l’objet de contexte hello, au lieu d’avoir hello toouse complète `context.bindings.name` modèle.</span><span class="sxs-lookup"><span data-stu-id="40489-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="40489-207">Hello suivant montre l’exemple de comment tooaccess hello `req` et `res` objets hello `context`:</span><span class="sxs-lookup"><span data-stu-id="40489-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="40489-208">En appelant `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="40489-208">By calling `context.done()`.</span></span> <span data-ttu-id="40489-209">Un type spécial de liaison HTTP renvoie la réponse hello passé toohello `context.done()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="40489-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="40489-210">Hello suivant HTTP sortie liaison définit un `$return` paramètre de sortie :</span><span class="sxs-lookup"><span data-stu-id="40489-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="40489-211">Cette liaison de sortie attend réponse de hello toosupply lorsque vous appelez `done()`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="40489-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="40489-212">Version du nœud et gestion des packages</span><span class="sxs-lookup"><span data-stu-id="40489-212">Node version and Package Management</span></span>
<span data-ttu-id="40489-213">version du nœud Hello est actuellement verrouillée à `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="40489-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="40489-214">Nous examinons la prise en charge d’autres versions ainsi que le fait de la rendre configurable.</span><span class="sxs-lookup"><span data-stu-id="40489-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="40489-215">Hello suit vous permettre d’inclure des packages dans votre application de fonction :</span><span class="sxs-lookup"><span data-stu-id="40489-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="40489-216">Accédez trop`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="40489-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="40489-217">Cliquez sur **Console de débogage** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="40489-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="40489-218">Accédez trop`D:\home\site\wwwroot`, puis faites glisser votre toohello de fichier package.json **wwwroot** dossier au niveau de la partie supérieure de la page de hello hello.</span><span class="sxs-lookup"><span data-stu-id="40489-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="40489-219">Vous pouvez télécharger les fichiers tooyour fonction application autrement également.</span><span class="sxs-lookup"><span data-stu-id="40489-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="40489-220">Pour plus d’informations, consultez [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="40489-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="40489-221">Une fois hello package.json fichier est chargé, exécutez hello `npm install` commande hello **console de l’exécution à distance Kudu**.</span><span class="sxs-lookup"><span data-stu-id="40489-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="40489-222">Cette action télécharge les packages hello indiqués dans le fichier de package.json hello et redémarre l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="40489-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="40489-223">Une fois hello packages dont vous avez besoin sont installés, vous importez les tooyour fonction en appelant `require('packagename')`, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="40489-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="40489-224">Vous devez définir un `package.json` fichier à votre application de la fonction hello racine.</span><span class="sxs-lookup"><span data-stu-id="40489-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="40489-225">Fichier de définition hello permet à toutes les fonctions de partage d’application hello hello mêmes packages mis en cache, ce qui donne de meilleurs hello.</span><span class="sxs-lookup"><span data-stu-id="40489-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="40489-226">Si un conflit de version, vous pouvez le résoudre en ajoutant un `package.json` fichier dans le dossier hello d’une fonction spécifique.</span><span class="sxs-lookup"><span data-stu-id="40489-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="40489-227">Variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="40489-227">Environment variables</span></span>
<span data-ttu-id="40489-228">tooget une variable d’environnement ou une valeur de paramètre d’application, utilisez `process.env`, comme indiqué dans l’exemple de code suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="40489-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="40489-229">Considérations relatives aux fonctions JavaScript</span><span class="sxs-lookup"><span data-stu-id="40489-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="40489-230">Lorsque vous travaillez avec les fonctions JavaScript, tenez compte des considérations hello Bonjour les deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="40489-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="40489-231">Choisir des plans App Service à cœur unique</span><span class="sxs-lookup"><span data-stu-id="40489-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="40489-232">Lorsque vous créez une application de fonction qui utilise hello plan App Service, nous vous recommandons de sélectionner un plan à cœur unique au lieu d’un plan à plusieurs cœurs.</span><span class="sxs-lookup"><span data-stu-id="40489-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="40489-233">Aujourd'hui, les fonctions exécute les fonctions JavaScript plus efficacement sur des machines virtuelles à cœur unique, et à l’aide de machines virtuelles plus grandes ne produit pas les améliorations des performances hello attendu.</span><span class="sxs-lookup"><span data-stu-id="40489-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="40489-234">Le cas échéant, vous pouvez faire une mise à l’échelle horizontale manuellement en ajoutant des instances de machine virtuelle à cœur unique, ou vous pouvez activer la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="40489-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="40489-235">Pour plus d’informations, consultez [Mettre à l’échelle le nombre d’instances manuellement ou automatiquement](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40489-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="40489-236">Prise en charge de typeScript et CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="40489-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="40489-237">Étant donné que la prise en charge directe n’existe pas encore de TypeScript ou CoffeeScript de compilation automatique via l’exécution de hello, cette prise en charge doit toobe gérée en dehors de l’exécution de hello, au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="40489-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40489-238">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40489-238">Next steps</span></span>
<span data-ttu-id="40489-239">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="40489-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="40489-240">Meilleures pratiques pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="40489-241">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="40489-242">Informations de référence pour les développeurs C# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="40489-243">Informations de référence pour les développeurs F# sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="40489-244">Déclencheurs et liaisons Azure Functions</span><span class="sxs-lookup"><span data-stu-id="40489-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

