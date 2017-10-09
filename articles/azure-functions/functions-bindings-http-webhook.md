---
title: les liaisons HTTP de fonctions et webhook aaaAzure | Documents Microsoft
description: "Comprendre comment toouse HTTP et webhook déclenche et les liaisons dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="2756d-104">Liaisons HTTP et webhook Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2756d-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="2756d-105">Cet article explique comment tooconfigure et utiliser HTTP déclenche et les liaisons dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2756d-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="2756d-106">Avec ces options, vous pouvez utiliser les toowebhooks de toobuild de fonctions d’Azure sans serveur de répondre et API.</span><span class="sxs-lookup"><span data-stu-id="2756d-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="2756d-107">Les fonctions Azure fournit hello suivant des liaisons :</span><span class="sxs-lookup"><span data-stu-id="2756d-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="2756d-108">Un [déclencheur HTTP](#httptrigger) vous permet d’appeler une fonction avec une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="2756d-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="2756d-109">Cela peut être trop personnalisé toorespond[webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="2756d-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="2756d-110">Un [liaison de sortie HTTP](#output) vous permet de toorespond toohello demande.</span><span class="sxs-lookup"><span data-stu-id="2756d-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="2756d-111">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="2756d-111">HTTP trigger</span></span>
<span data-ttu-id="2756d-112">déclencheur HTTP Hello exécutera votre fonction dans la demande de réponse tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="2756d-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="2756d-113">Vous pouvez le personnaliser URL de toorespond tooa particulière ou un ensemble de méthodes HTTP.</span><span class="sxs-lookup"><span data-stu-id="2756d-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="2756d-114">Un déclencheur HTTP peut également être configuré toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="2756d-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="2756d-115">Si vous utilisez le portail de fonctions hello, vous pouvez également commencer immédiatement à l’aide d’un modèle existant.</span><span class="sxs-lookup"><span data-stu-id="2756d-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="2756d-116">Sélectionnez **nouvelle fonction** et choisissez « Webhooks & de l’API » hello **scénario** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="2756d-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="2756d-117">Sélectionnez un des modèles de hello et cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="2756d-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="2756d-118">Par défaut, un déclencheur HTTP répondra demande toohello avec un code d’état HTTP 200 OK et un corps vide.</span><span class="sxs-lookup"><span data-stu-id="2756d-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="2756d-119">toomodify hello réponse, configurez un [liaison de sortie HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="2756d-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="2756d-120">Configuration d’un déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="2756d-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="2756d-121">Un déclencheur HTTP est défini en incluant un toohello similaire d’objet JSON suivant Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="2756d-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="2756d-122">liaison de Hello prend en charge hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2756d-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="2756d-123">**nom** : requise : nom de la variable hello utilisée dans le code de fonction de requête de hello ou de corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="2756d-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="2756d-124">Voir [Utilisation d’un déclencheur HTTP à partir d’un code](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="2756d-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="2756d-125">**type** : requise : doit être défini trop « httpTrigger ».</span><span class="sxs-lookup"><span data-stu-id="2756d-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="2756d-126">**direction** : requise : doit être défini trop « in ».</span><span class="sxs-lookup"><span data-stu-id="2756d-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="2756d-127">_authLevel_ : ce paramètre détermine les clés, le cas échéant, doivent toobe présent sur demande de hello dans la fonction d’ordre tooinvoke hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="2756d-128">Voir [Utilisation de clés](#keys) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2756d-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="2756d-129">valeur de Hello peut être hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2756d-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="2756d-130">_anonymous_ : aucune clé API n’est requise.</span><span class="sxs-lookup"><span data-stu-id="2756d-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="2756d-131">_function_ : une clé API spécifique de la fonction est requise.</span><span class="sxs-lookup"><span data-stu-id="2756d-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="2756d-132">Cela est hello par défaut si aucun n’est fourni.</span><span class="sxs-lookup"><span data-stu-id="2756d-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="2756d-133">_administrateur_ : hello la clé principale est requise.</span><span class="sxs-lookup"><span data-stu-id="2756d-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="2756d-134">**méthodes** : il s’agit d’un tableau de méthodes hello HTTP (fonction) hello toowhich répondra.</span><span class="sxs-lookup"><span data-stu-id="2756d-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="2756d-135">Si non spécifié, fonction hello répondra tooall HTTP méthodes.</span><span class="sxs-lookup"><span data-stu-id="2756d-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="2756d-136">Consultez [personnalisation de point de terminaison hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="2756d-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="2756d-137">**itinéraire** : modèle d’itinéraire hello, contrôle toowhich définit votre fonction répondra des URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="2756d-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="2756d-138">Bonjour valeur par défaut si aucun n’est fourni est `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="2756d-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="2756d-139">Consultez [personnalisation de point de terminaison hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="2756d-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="2756d-140">**webHookType** : Cela configure tooact de déclencheur hello HTTP comme un récepteur de webhook pour le fournisseur spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="2756d-141">Hello _méthodes_ propriété ne doit pas être définie si cela est choisi.</span><span class="sxs-lookup"><span data-stu-id="2756d-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="2756d-142">Consultez [réponse toowebhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="2756d-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="2756d-143">valeur de Hello peut être hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2756d-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="2756d-144">_genericJson_ : point de terminaison webhook à usage général sans logique pour un fournisseur spécifique.</span><span class="sxs-lookup"><span data-stu-id="2756d-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="2756d-145">_github_ : fonction hello répondra tooGitHub webhooks.</span><span class="sxs-lookup"><span data-stu-id="2756d-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="2756d-146">Hello _authLevel_ propriété ne doit pas être définie si cela est choisi.</span><span class="sxs-lookup"><span data-stu-id="2756d-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="2756d-147">_marge_ : fonction hello répondra tooSlack webhooks.</span><span class="sxs-lookup"><span data-stu-id="2756d-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="2756d-148">Hello _authLevel_ propriété ne doit pas être définie si cela est choisi.</span><span class="sxs-lookup"><span data-stu-id="2756d-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="2756d-149">Utilisation d’un déclencheur HTTP à partir d’un code</span><span class="sxs-lookup"><span data-stu-id="2756d-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="2756d-150">Pour les fonctions de c# et F #, vous pouvez déclarer type hello de votre toobe d’entrée de déclencheur soit `HttpRequestMessage` ou un type personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2756d-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="2756d-151">Si vous choisissez `HttpRequestMessage`, vous obtiendrez un objet de demande toohello un accès complet.</span><span class="sxs-lookup"><span data-stu-id="2756d-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="2756d-152">Pour un type personnalisé (par exemple, un POCO), les fonctions va tenter de corps de la demande tooparse hello en tant que propriétés de l’objet JSON toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="2756d-153">Pour les fonctions de Node.js hello fonctions runtime fournit des corps de la demande au lieu de l’objet de demande hello hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="2756d-154">Pour des exemples d’utilisation, voir [Exemples de déclencheur HTTP](#httptriggersample).</span><span class="sxs-lookup"><span data-stu-id="2756d-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="2756d-155">Liaison de sortie de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="2756d-155">HTTP response output binding</span></span>
<span data-ttu-id="2756d-156">Utilisez l’expéditeur de demande HTTP liaison toorespond toohello hello HTTP sortie.</span><span class="sxs-lookup"><span data-stu-id="2756d-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="2756d-157">Cette liaison requiert un déclencheur HTTP et vous permet de réponse de hello toocustomize associée demande du déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="2756d-158">Si aucune liaison de sortie HTTP n’est spécifiée, un déclencheur HTTP renvoie HTTP 200 OK avec un corps vide.</span><span class="sxs-lookup"><span data-stu-id="2756d-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="2756d-159">Configuration d’une liaison de sortie HTTP</span><span class="sxs-lookup"><span data-stu-id="2756d-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="2756d-160">Hello HTTP de la liaison est définie en incluant un toohello similaire d’objet JSON suivant Bonjour sortie `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="2756d-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="2756d-161">liaison de Hello contient hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="2756d-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="2756d-162">**nom** : requise : hello nom de la variable utilisée dans le code de fonction pour la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="2756d-163">Voir [Utilisation d’une liaison de sortie HTTP à partir d’un code](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="2756d-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="2756d-164">**type** : requise : doit être défini trop « http ».</span><span class="sxs-lookup"><span data-stu-id="2756d-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="2756d-165">**direction** : requise : doit être défini trop « sortie ».</span><span class="sxs-lookup"><span data-stu-id="2756d-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="2756d-166">Utilisation d’une liaison de sortie HTTP à partir d’un code</span><span class="sxs-lookup"><span data-stu-id="2756d-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="2756d-167">Vous pouvez utiliser hello sortie paramètre (par exemple, « res ») toorespond toohello http ou webhook appelant.</span><span class="sxs-lookup"><span data-stu-id="2756d-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="2756d-168">Vous pouvez également utiliser la norme `Request.CreateResponse()` (c#) ou `context.res` (Node.JS) modèle tooreturn votre réponse.</span><span class="sxs-lookup"><span data-stu-id="2756d-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="2756d-169">Pour des exemples qui illustrent comment toouse hello cette dernière méthode, consultez [exemples de déclencheur HTTP](#httptriggersample) et [exemples de déclencheurs de Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="2756d-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="2756d-170">Répondre toowebhooks</span><span class="sxs-lookup"><span data-stu-id="2756d-170">Responding toowebhooks</span></span>
<span data-ttu-id="2756d-171">Un déclencheur HTTP avec hello _webHookType_ propriété sera configuré toorespond trop[webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="2756d-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="2756d-172">configuration de base Hello utilise le paramètre de « genericJson » hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="2756d-173">Ce qui réduit les demandes tooonly celles de l’utilisation de HTTP POST et hello `application/json` le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="2756d-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="2756d-174">Hello déclencheur peut en outre être adaptés tooa webhook spécifique fournisseur (par exemple, [GitHub](https://developer.github.com/webhooks/) et [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="2756d-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="2756d-175">Si un fournisseur est spécifié, hello fonctions runtime peut prendre en charge la logique de validation du fournisseur hello pour vous.</span><span class="sxs-lookup"><span data-stu-id="2756d-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="2756d-176">Configurer GitHub en tant que fournisseur de webhooks</span><span class="sxs-lookup"><span data-stu-id="2756d-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="2756d-177">toorespond tooGitHub webhooks, commencez par créer votre fonction avec un déclencheur de HTTP et définir hello _webHookType_ propriété trop « github ».</span><span class="sxs-lookup"><span data-stu-id="2756d-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="2756d-178">Ensuite, copiez son [URL](#url) et sa [clé API](#keys) vers la page **Ajouter un Webhook** de votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="2756d-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="2756d-179">Pour plus d’informations, voir la documentation [Création de webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2756d-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="2756d-180">Configuration de Slack en tant que fournisseur de webhook</span><span class="sxs-lookup"><span data-stu-id="2756d-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="2756d-181">webhook de marge Hello génère un jeton au lieu de ce qui vous permet de spécifier, vous devez donc configurer une clé spécifiques à une fonction avec jeton hello à partir de la marge.</span><span class="sxs-lookup"><span data-stu-id="2756d-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="2756d-182">Voir [Utilisation de clés](#keys).</span><span class="sxs-lookup"><span data-stu-id="2756d-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="2756d-183">Personnalisation de point de terminaison HTTP hello</span><span class="sxs-lookup"><span data-stu-id="2756d-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="2756d-184">Par défaut, lorsque vous créez une fonction d’un déclencheur HTTP, ou WebHook, fonction hello est adressable avec un itinéraire de formulaire de hello :</span><span class="sxs-lookup"><span data-stu-id="2756d-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="2756d-185">Vous pouvez personnaliser cet itinéraire à l’aide de hello facultatif `route` propriété sur le déclencheur de hello HTTP d’entrée de liaison.</span><span class="sxs-lookup"><span data-stu-id="2756d-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="2756d-186">Par exemple, hello suivant *function.json* fichier définit un `route` propriétés d’un déclencheur HTTP :</span><span class="sxs-lookup"><span data-stu-id="2756d-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="2756d-187">À l’aide de cette configuration, fonction hello est maintenant adressable par hello suivant l’itinéraire au lieu de l’itinéraire d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="2756d-188">Cela permet au code de fonction hello toosupport deux des paramètres dans l’adresse de hello, « catégorie » et « id ».</span><span class="sxs-lookup"><span data-stu-id="2756d-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="2756d-189">Vous pouvez utiliser les [contraintes d’itinéraire des API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) de votre choix avec vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="2756d-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="2756d-190">Hello suivant le code de fonction c# utilise les deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="2756d-190">hello following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="2756d-191">Voici les paramètres d’itinéraire même hello de toouse code Node.js (fonction).</span><span class="sxs-lookup"><span data-stu-id="2756d-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="2756d-192">Par défaut, tous les itinéraires de fonction sont préfixés par *api*.</span><span class="sxs-lookup"><span data-stu-id="2756d-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="2756d-193">Vous pouvez également personnaliser ou supprimer le préfixe hello à l’aide de hello `http.routePrefix` propriété dans votre *host.json* fichier.</span><span class="sxs-lookup"><span data-stu-id="2756d-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="2756d-194">exemple Hello supprime hello *api* préfixe d’itinéraire à l’aide d’une chaîne vide pour le préfixe hello Bonjour *host.json* fichier.</span><span class="sxs-lookup"><span data-stu-id="2756d-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="2756d-195">Pour plus d’informations sur la façon de tooupdate hello *host.json* fichier de votre fonction, consultez [fonctionnement des fichiers de l’application tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="2756d-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="2756d-196">Pour plus d’informations sur les autres propriétés que vous pouvez configurer dans votre fichier *host.json*, consultez la [référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="2756d-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="2756d-197">Utilisation de clés</span><span class="sxs-lookup"><span data-stu-id="2756d-197">Working with keys</span></span>
<span data-ttu-id="2756d-198">HttpTriggers peut tirer parti des clés pour renforcer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="2756d-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="2756d-199">Un standard HttpTrigger pouvez les utiliser comme une clé d’API, nécessitant toobe de clé hello présent sur la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="2756d-200">Webhooks peut utiliser des clés tooauthorize demandes de plusieurs façons, selon le fournisseur hello prend en charge.</span><span class="sxs-lookup"><span data-stu-id="2756d-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="2756d-201">Les clés sont stockées dans votre Function App dans Azure, et chiffrées au repos.</span><span class="sxs-lookup"><span data-stu-id="2756d-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="2756d-202">tooview vos clés, créer de nouveaux ou toonew les valeurs de clés de restauration, accédez tooone de vos fonctions au sein du portail de hello et sélectionnez « Gérer ».</span><span class="sxs-lookup"><span data-stu-id="2756d-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="2756d-203">Il existe deux types de clés :</span><span class="sxs-lookup"><span data-stu-id="2756d-203">There are two types of keys:</span></span>
- <span data-ttu-id="2756d-204">**Clés d’hôtes**: ces clés sont partagés par toutes les fonctions de l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="2756d-205">Lorsqu’il est utilisé comme une clé d’API, permettent de fonction tooany d’accès au sein de l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="2756d-206">**Touches de fonction**: ces clés s’appliquent uniquement toohello des fonctions spécifiques dans lesquelles ils sont définis.</span><span class="sxs-lookup"><span data-stu-id="2756d-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="2756d-207">Lorsqu’il est utilisé comme une clé d’API, ils ne permettre access toothat (fonction).</span><span class="sxs-lookup"><span data-stu-id="2756d-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="2756d-208">Chaque clé est nommé pour référence et il existe une clé par défaut (nommée « default ») au niveau de fonction et l’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="2756d-209">Hello **clé principale de** est une clé d’hôte par défaut nommée « _master » qui est défini pour chaque application de la fonction et ne peuvent pas être révoqués.</span><span class="sxs-lookup"><span data-stu-id="2756d-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="2756d-210">Il fournit des API d’exécution d’un accès administratif toohello.</span><span class="sxs-lookup"><span data-stu-id="2756d-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="2756d-211">À l’aide de `"authLevel": "admin"` Bonjour JSON de liaison requiert cette clé toobe présenté à la demande de hello ; une autre clé entraîne un échec d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="2756d-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="2756d-212">Échéance toohello élevés des autorisations accordées par la clé principale de hello, vous ne devez pas partager cette clé avec des tiers ou le distribuer dans les applications clientes natives.</span><span class="sxs-lookup"><span data-stu-id="2756d-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="2756d-213">Faites preuve de prudence lorsque vous choisissez le niveau d’autorisation d’admin hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="2756d-214">Autorisation de clé API</span><span class="sxs-lookup"><span data-stu-id="2756d-214">API key authorization</span></span>
<span data-ttu-id="2756d-215">Par défaut, un HttpTrigger requiert une clé d’API dans la demande HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="2756d-216">Par conséquent, votre requête HTTP ressemble normalement à ceci :</span><span class="sxs-lookup"><span data-stu-id="2756d-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="2756d-217">clé de Hello peut être inclus dans une variable de chaîne de requête nommée `code`, comme indiqué ci-dessus, ou il peut être inclus dans un `x-functions-key` en-tête HTTP.</span><span class="sxs-lookup"><span data-stu-id="2756d-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="2756d-218">valeur de Hello de clé de hello peut être n’importe quelle touche de fonction définis pour la fonction de hello ou n’importe quelle touche de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="2756d-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="2756d-219">Vous pouvez choisir des demandes tooallow sans clés ou spécifier que la clé principale hello doit être utilisée en modifiant les hello `authLevel` propriété Bonjour liaison JSON (voir [déclencheur HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="2756d-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="2756d-220">Clés et webhooks</span><span class="sxs-lookup"><span data-stu-id="2756d-220">Keys and webhooks</span></span>
<span data-ttu-id="2756d-221">Autorisation de Webhook est gérée par le composant récepteur hello webhook, partie hello HttpTrigger et le mécanisme de hello varie selon le type de webhook hello.</span><span class="sxs-lookup"><span data-stu-id="2756d-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="2756d-222">Toutefois, chaque mécanisme dépend d’une clé.</span><span class="sxs-lookup"><span data-stu-id="2756d-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="2756d-223">Par défaut, touche de fonction hello nommée « default » est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2756d-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="2756d-224">Si vous le souhaitez toouse une autre clé, vous devez tooconfigure hello webhook fournisseur toosend hello nom de clé avec requête hello de hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="2756d-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="2756d-225">**Chaîne de requête**: fournisseur de hello transmet le nom de la clé hello Bonjour `clientid` le paramètre de chaîne de requête (par exemple, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="2756d-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="2756d-226">**En-tête de demande**: fournisseur de hello transmet le nom de la clé hello Bonjour `x-functions-clientid` en-tête.</span><span class="sxs-lookup"><span data-stu-id="2756d-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="2756d-227">Les clés de fonction prennent le pas sur les clés d’hôte.</span><span class="sxs-lookup"><span data-stu-id="2756d-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="2756d-228">Si deux clés sont définies avec le même nom, hello de hello touche de fonction sera utilisé.</span><span class="sxs-lookup"><span data-stu-id="2756d-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="2756d-229">Exemples de déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="2756d-229">HTTP trigger samples</span></span>
<span data-ttu-id="2756d-230">Supposez que vous avez hello suivant déclencheur HTTP Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="2756d-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="2756d-231">Consultez l’exemple hello spécifiques à une langue qui recherche un `name` paramètre dans la chaîne de requête hello ou corps hello de demande de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="2756d-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="2756d-232">C#</span><span class="sxs-lookup"><span data-stu-id="2756d-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="2756d-233">F#</span><span class="sxs-lookup"><span data-stu-id="2756d-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="2756d-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2756d-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="2756d-235">Exemple de déclencheur HTTP en C#</span><span class="sxs-lookup"><span data-stu-id="2756d-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="2756d-236">Vous pouvez également lier tooa POCO au lieu de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="2756d-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="2756d-237">Cela sera être intégré à partir du corps hello de demande hello, analysée au format JSON.</span><span class="sxs-lookup"><span data-stu-id="2756d-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="2756d-238">De même, un type peut être passé en sortie de réponse HTTP de toohello de liaison, et cela sera retourné en tant que corps de réponse hello, avec un code de 200 état.</span><span class="sxs-lookup"><span data-stu-id="2756d-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="2756d-239">Exemple de déclencheur HTTP en F#</span><span class="sxs-lookup"><span data-stu-id="2756d-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="2756d-240">Vous avez besoin une `project.json` fichier qui utilise NuGet tooreference hello `FSharp.Interop.Dynamic` et `Dynamitey` assemblys, comme suit :</span><span class="sxs-lookup"><span data-stu-id="2756d-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="2756d-241">Cette option NuGet toofetch les dépendances et les référencer dans votre script.</span><span class="sxs-lookup"><span data-stu-id="2756d-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="2756d-242">Exemple de déclencheur HTTP en Node.js</span><span class="sxs-lookup"><span data-stu-id="2756d-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="2756d-243">Exemples de webhook</span><span class="sxs-lookup"><span data-stu-id="2756d-243">Webhook samples</span></span>
<span data-ttu-id="2756d-244">Supposez que vous avez hello suivant déclencheur webhook Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="2756d-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="2756d-245">Voir exemple hello spécifiques au langage qui enregistre les commentaires de problème GitHub.</span><span class="sxs-lookup"><span data-stu-id="2756d-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="2756d-246">C#</span><span class="sxs-lookup"><span data-stu-id="2756d-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="2756d-247">F#</span><span class="sxs-lookup"><span data-stu-id="2756d-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="2756d-248">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2756d-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="2756d-249">Exemple de Webhook en C#</span><span class="sxs-lookup"><span data-stu-id="2756d-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="2756d-250">Exemple de Webhook en F#</span><span class="sxs-lookup"><span data-stu-id="2756d-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="2756d-251">Exemple de webhook en Node.js</span><span class="sxs-lookup"><span data-stu-id="2756d-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="2756d-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2756d-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

