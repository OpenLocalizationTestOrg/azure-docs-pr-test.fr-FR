---
title: "Liaisons HTTP et webhook d’Azure Functions | Microsoft Docs"
description: "Découvrez comment utiliser des déclencheurs et des liaisons HTTP et webhook dans Azure Functions."
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
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="b5f75-104">Liaisons HTTP et webhook Azure Functions</span><span class="sxs-lookup"><span data-stu-id="b5f75-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b5f75-105">Cet article explique comment configurer et utiliser des déclencheurs et liaisons HTTP dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b5f75-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="b5f75-106">Ces éléments vous permettent d’utiliser Azure Functions pour générer des API sans serveur et répondre aux webhooks.</span><span class="sxs-lookup"><span data-stu-id="b5f75-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="b5f75-107">Fonctions Azure fournit les liaisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="b5f75-108">Un [déclencheur HTTP](#httptrigger) vous permet d’appeler une fonction avec une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="b5f75-109">Vous pouvez personnaliser cela pour répondre aux [webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="b5f75-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="b5f75-110">Un [liaison de sortie HTTP](#output) permet de répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="b5f75-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="b5f75-111">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-111">HTTP trigger</span></span>
<span data-ttu-id="b5f75-112">Le déclencheur HTTP exécute votre fonction en réponse à une requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="b5f75-113">Vous pouvez personnaliser la fonction pour répondre à une URL particulière ou à un ensemble de méthodes HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="b5f75-114">Vous pouvez également configurer un déclencheur HTTP pour répondre aux webhooks.</span><span class="sxs-lookup"><span data-stu-id="b5f75-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="b5f75-115">Si vous utilisez le portail des fonctions, vous pouvez également commencer immédiatement à utiliser un modèle existant.</span><span class="sxs-lookup"><span data-stu-id="b5f75-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="b5f75-116">Sélectionnez **Nouvelle fonction**, puis choisissez « API et webhooks » dans la liste déroulante **Scénario**.</span><span class="sxs-lookup"><span data-stu-id="b5f75-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="b5f75-117">Sélectionnez un des modèles, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b5f75-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="b5f75-118">Par défaut, un déclencheur HTTP répondra à la demande avec un code d’état HTTP 200 OK et un corps vide.</span><span class="sxs-lookup"><span data-stu-id="b5f75-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="b5f75-119">Pour modifier la réponse, configurez une [liaison de sortie HTTP](#output).</span><span class="sxs-lookup"><span data-stu-id="b5f75-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="b5f75-120">Configuration d’un déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="b5f75-121">Pour définir un déclencheur HTTP, incluez un objet JSON similaire au suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="b5f75-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="b5f75-122">La liaison prend en charge les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="b5f75-123">**name** : obligatoire - nom de variable utilisé dans le code de la fonction pour la demande ou dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="b5f75-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="b5f75-124">Voir [Utilisation d’un déclencheur HTTP à partir d’un code](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="b5f75-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="b5f75-125">**type** : obligatoire - doit être « httpTrigger ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="b5f75-126">**direction** : obligatoire - doit être « in ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="b5f75-127">_authLevel_ : détermine, le cas échéant, les clés qui doivent être présentes dans la demande pour appeler la fonction.</span><span class="sxs-lookup"><span data-stu-id="b5f75-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="b5f75-128">Voir [Utilisation de clés](#keys) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b5f75-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="b5f75-129">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="b5f75-130">_anonymous_ : aucune clé API n’est requise.</span><span class="sxs-lookup"><span data-stu-id="b5f75-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="b5f75-131">_function_ : une clé API spécifique de la fonction est requise.</span><span class="sxs-lookup"><span data-stu-id="b5f75-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="b5f75-132">Il s’agit de la valeur par défaut si aucune valeur n’est fournie.</span><span class="sxs-lookup"><span data-stu-id="b5f75-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="b5f75-133">_admin_ : la clé principale est requise.</span><span class="sxs-lookup"><span data-stu-id="b5f75-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="b5f75-134">**methods** : il s’agit d’un tableau des méthodes HTTP auxquelles la fonction répond.</span><span class="sxs-lookup"><span data-stu-id="b5f75-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="b5f75-135">À défaut de spécification, la fonction répond à toutes les méthodes HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="b5f75-136">Voir [Personnalisation du point de terminaison HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="b5f75-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b5f75-137">**route** : définit le modèle de routage, en contrôlant les URL de demande auxquelles votre fonction répond.</span><span class="sxs-lookup"><span data-stu-id="b5f75-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="b5f75-138">La valeur par défaut est `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="b5f75-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="b5f75-139">Voir [Personnalisation du point de terminaison HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="b5f75-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="b5f75-140">**webHookType** : configure le déclencheur HTTP pour qu’il agisse en tant que récepteur de webhook pour le fournisseur spécifié.</span><span class="sxs-lookup"><span data-stu-id="b5f75-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="b5f75-141">Si cette valeur est choisie, la propriété _methods_ ne doit pas être définie.</span><span class="sxs-lookup"><span data-stu-id="b5f75-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="b5f75-142">Voir [Réponse aux webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="b5f75-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="b5f75-143">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="b5f75-144">_genericJson_ : point de terminaison webhook à usage général sans logique pour un fournisseur spécifique.</span><span class="sxs-lookup"><span data-stu-id="b5f75-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="b5f75-145">_github_ : la fonction répond aux webhooks GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5f75-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="b5f75-146">Si cette valeur est choisie, la propriété _authLevel_ ne doit pas être définie.</span><span class="sxs-lookup"><span data-stu-id="b5f75-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="b5f75-147">_slack_ : la fonction répond aux webhooks Slack.</span><span class="sxs-lookup"><span data-stu-id="b5f75-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="b5f75-148">Si cette valeur est choisie, la propriété _authLevel_ ne doit pas être définie.</span><span class="sxs-lookup"><span data-stu-id="b5f75-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="b5f75-149">Utilisation d’un déclencheur HTTP à partir d’un code</span><span class="sxs-lookup"><span data-stu-id="b5f75-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="b5f75-150">Pour les fonctions C# et F #, vous pouvez déclarer le type de votre entrée de déclenchement en tant que `HttpRequestMessage` ou type personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b5f75-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="b5f75-151">Si vous choisissez `HttpRequestMessage`, vous obtenez un accès complet à l’objet de la demande.</span><span class="sxs-lookup"><span data-stu-id="b5f75-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="b5f75-152">Pour un type personnalisé (par exemple, un objet CLR traditionnel), Functions tente d’analyser le corps de la demande en tant que JSON pour compléter les propriétés de l’objet.</span><span class="sxs-lookup"><span data-stu-id="b5f75-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="b5f75-153">Dans le cas des fonctions Node.js, le runtime Functions fournit le corps de requête plutôt que l’objet de requête.</span><span class="sxs-lookup"><span data-stu-id="b5f75-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="b5f75-154">Pour des exemples d’utilisation, voir [Exemples de déclencheur HTTP](#httptriggersample).</span><span class="sxs-lookup"><span data-stu-id="b5f75-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="b5f75-155">Liaison de sortie de réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-155">HTTP response output binding</span></span>
<span data-ttu-id="b5f75-156">Utilisez la liaison de sortie HTTP pour répondre à l’expéditeur de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="b5f75-157">Cette liaison requiert un déclencheur HTTP, et vous permet de personnaliser la réponse associée à la demande du déclencheur.</span><span class="sxs-lookup"><span data-stu-id="b5f75-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="b5f75-158">Si aucune liaison de sortie HTTP n’est spécifiée, un déclencheur HTTP renvoie HTTP 200 OK avec un corps vide.</span><span class="sxs-lookup"><span data-stu-id="b5f75-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="b5f75-159">Configuration d’une liaison de sortie HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="b5f75-160">La liaison de sortie HTTP est définie en incluant dans le tableau `bindings` de function.json un objet JSON similaire à celui-ci :</span><span class="sxs-lookup"><span data-stu-id="b5f75-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="b5f75-161">La liaison contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="b5f75-162">**name** : obligatoire - nom de variable utilisé dans le code de fonction pour la réponse.</span><span class="sxs-lookup"><span data-stu-id="b5f75-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="b5f75-163">Voir [Utilisation d’une liaison de sortie HTTP à partir d’un code](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="b5f75-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="b5f75-164">**type** : obligatoire - doit être « http ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="b5f75-165">**direction** : obligatoire - doit être « out ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="b5f75-166">Utilisation d’une liaison de sortie HTTP à partir d’un code</span><span class="sxs-lookup"><span data-stu-id="b5f75-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="b5f75-167">Vous pouvez utiliser le paramètre de sortie (par exemple, « res ») pour répondre à l’appelant HTTP ou webhook.</span><span class="sxs-lookup"><span data-stu-id="b5f75-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="b5f75-168">Vous pouvez également utiliser le modèle `Request.CreateResponse()` (C#) ou `context.res` (Node.JS) standard pour retourner votre réponse.</span><span class="sxs-lookup"><span data-stu-id="b5f75-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="b5f75-169">Pour des exemples d’utilisation de cette dernière méthode, voir [Exemples de déclencheurs HTTP](#httptriggersample) et [Exemples de déclencheurs webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="b5f75-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="b5f75-170">Réponse aux webhooks</span><span class="sxs-lookup"><span data-stu-id="b5f75-170">Responding to webhooks</span></span>
<span data-ttu-id="b5f75-171">Un déclencheur HTTP avec la propriété _webHookType_ sera configuré pour répondre aux [webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="b5f75-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="b5f75-172">La configuration de base utilise le paramètre « genericJson ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="b5f75-173">Cela limite les demandes à celles utilisant HTTP Post et le type de contenu `application/json`.</span><span class="sxs-lookup"><span data-stu-id="b5f75-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="b5f75-174">Le déclencheur peut en outre être adapté à un fournisseur de webhook spécifique (par exemple, [GitHub](https://developer.github.com/webhooks/) et [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="b5f75-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="b5f75-175">Si un fournisseur est spécifié, le runtime Functions peut se charger de la logique de validation du fournisseur à votre place.</span><span class="sxs-lookup"><span data-stu-id="b5f75-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="b5f75-176">Configurer GitHub en tant que fournisseur de webhooks</span><span class="sxs-lookup"><span data-stu-id="b5f75-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="b5f75-177">Pour répondre aux webhooks GitHub, commencez par créer votre fonction avec un déclencheur HTTP, et définir la propriété _webHookType_ sur « github ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="b5f75-178">Ensuite, copiez son [URL](#url) et sa [clé API](#keys) vers la page **Ajouter un Webhook** de votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5f75-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="b5f75-179">Pour plus d’informations, voir la documentation [Création de webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b5f75-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="b5f75-180">Configuration de Slack en tant que fournisseur de webhook</span><span class="sxs-lookup"><span data-stu-id="b5f75-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="b5f75-181">La webhook de Slack génère un jeton à votre place au lieu de vous laisser le spécifier. Vous devez donc configurer une clé spécifique de la fonction avec le jeton reçu de Slack.</span><span class="sxs-lookup"><span data-stu-id="b5f75-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="b5f75-182">Voir [Utilisation de clés](#keys).</span><span class="sxs-lookup"><span data-stu-id="b5f75-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="b5f75-183">Personnalisation du point de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="b5f75-184">Par défaut, lorsque vous créez une fonction pour un déclencheur HTTP ou un WebHook, la fonction est adressable avec un itinéraire de la forme :</span><span class="sxs-lookup"><span data-stu-id="b5f75-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="b5f75-185">Vous pouvez personnaliser cet itinéraire en utilisant la propriété facultative `route` sur la liaison d’entrée du déclencheur HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="b5f75-186">Par exemple, le fichier *function.json* suivant définit une propriété `route` pour un déclencheur HTTP :</span><span class="sxs-lookup"><span data-stu-id="b5f75-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="b5f75-187">Avec cette configuration, la fonction est désormais adressable avec l’itinéraire suivant au lieu de l’itinéraire d’origine.</span><span class="sxs-lookup"><span data-stu-id="b5f75-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="b5f75-188">Cela permet au code de la fonction de prendre en charge deux paramètres dans l’adresse, « category » et « id ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="b5f75-189">Vous pouvez utiliser les [contraintes d’itinéraire des API Web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) de votre choix avec vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="b5f75-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="b5f75-190">Le code de la fonction C# suivant utilise les deux paramètres.</span><span class="sxs-lookup"><span data-stu-id="b5f75-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="b5f75-191">Voici le code de la fonction Node.js qui utilise les mêmes paramètres d’itinéraire.</span><span class="sxs-lookup"><span data-stu-id="b5f75-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="b5f75-192">Par défaut, tous les itinéraires de fonction sont préfixés par *api*.</span><span class="sxs-lookup"><span data-stu-id="b5f75-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="b5f75-193">Vous pouvez également personnaliser ou supprimer le préfixe avec la propriété `http.routePrefix` dans votre fichier *host.json*.</span><span class="sxs-lookup"><span data-stu-id="b5f75-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="b5f75-194">L’exemple suivant supprime le préfixe d’itinéraire *api* en sélectionnant une chaîne vide pour le préfixe dans le fichier *host.json*.</span><span class="sxs-lookup"><span data-stu-id="b5f75-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="b5f75-195">Pour plus d’informations sur la mise à jour du fichier *host.json* de votre fonction, consultez [Mettre à jour les fichiers Function App](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="b5f75-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="b5f75-196">Pour plus d’informations sur les autres propriétés que vous pouvez configurer dans votre fichier *host.json*, consultez la [référence host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="b5f75-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="b5f75-197">Utilisation de clés</span><span class="sxs-lookup"><span data-stu-id="b5f75-197">Working with keys</span></span>
<span data-ttu-id="b5f75-198">HttpTriggers peut tirer parti des clés pour renforcer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="b5f75-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="b5f75-199">Un HttpTrigger standard peut les utiliser en tant que clés API, en exigeant que la clé soit présente dans la requête.</span><span class="sxs-lookup"><span data-stu-id="b5f75-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="b5f75-200">Les webhooks peuvent utiliser des clés pour autoriser des demandes de plusieurs façons, selon ce que le fournisseur prend en charge.</span><span class="sxs-lookup"><span data-stu-id="b5f75-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="b5f75-201">Les clés sont stockées dans votre Function App dans Azure, et chiffrées au repos.</span><span class="sxs-lookup"><span data-stu-id="b5f75-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="b5f75-202">Pour afficher vos clés, créez des clés, ou restaurez des clés avec de nouvelles valeurs, accédez à l’une de vos fonctions au sein du portail, puis sélectionnez « Gérer ».</span><span class="sxs-lookup"><span data-stu-id="b5f75-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="b5f75-203">Il existe deux types de clés :</span><span class="sxs-lookup"><span data-stu-id="b5f75-203">There are two types of keys:</span></span>
- <span data-ttu-id="b5f75-204">**Clés d’hôte** : ces clés sont partagées par toutes les fonctions au sein de la Function App.</span><span class="sxs-lookup"><span data-stu-id="b5f75-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="b5f75-205">Utilisées en tant que clés API, elles permettent d’accéder à toute fonction au sein de la Function App.</span><span class="sxs-lookup"><span data-stu-id="b5f75-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="b5f75-206">**Clés de fonction** : ces clés s’appliquent uniquement aux fonctions spécifiques sous lesquelles elles sont définies.</span><span class="sxs-lookup"><span data-stu-id="b5f75-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="b5f75-207">Utilisées en tant que clés API, elles permettent d’accéder uniquement à ces fonctions.</span><span class="sxs-lookup"><span data-stu-id="b5f75-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="b5f75-208">Chaque clé est nommée pour référence et il existe une clé par défaut (nommée « default ») au niveau fonction et hôte.</span><span class="sxs-lookup"><span data-stu-id="b5f75-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="b5f75-209">Le **clé principale** est une clé d’hôte par défaut nommée « _master » qui est définie pour chaque Function App et qui ne peut pas être révoquée.</span><span class="sxs-lookup"><span data-stu-id="b5f75-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="b5f75-210">Elle fournit un accès administratif aux API de runtime.</span><span class="sxs-lookup"><span data-stu-id="b5f75-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="b5f75-211">L’utilisation de `"authLevel": "admin"` dans le JSON de liaison nécessite que cette clé soit présentée à la demande. Une autre clé entraînerait un échec d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="b5f75-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="b5f75-212">En raison des autorisations élevées qu’accorde la clé principale, vous ne devez pas partager celle-ci avec des tiers, ou la distribuer dans des applications clientes natives.</span><span class="sxs-lookup"><span data-stu-id="b5f75-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="b5f75-213">Faites preuve de prudence lors du choix du niveau d’autorisation administrateur.</span><span class="sxs-lookup"><span data-stu-id="b5f75-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="b5f75-214">Autorisation de clé API</span><span class="sxs-lookup"><span data-stu-id="b5f75-214">API key authorization</span></span>
<span data-ttu-id="b5f75-215">Par défaut, un HttpTrigger requiert une clé API dans la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="b5f75-216">Par conséquent, votre requête HTTP ressemble normalement à ceci :</span><span class="sxs-lookup"><span data-stu-id="b5f75-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="b5f75-217">Cette clé peut être incluse dans une variable de chaîne de requête nommée `code` ou dans un en-tête HTTP `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="b5f75-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="b5f75-218">La valeur de la clé peut être toute clé de fonction définie pour la fonction, ou toute clé d’hôte.</span><span class="sxs-lookup"><span data-stu-id="b5f75-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="b5f75-219">Vous pouvez autoriser des demandes sans clé ou spécifier que la clé principale doit être utilisée en modifiant la propriété `authLevel` dans le JSON de liaison (voir [Déclencheur HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="b5f75-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="b5f75-220">Clés et webhooks</span><span class="sxs-lookup"><span data-stu-id="b5f75-220">Keys and webhooks</span></span>
<span data-ttu-id="b5f75-221">Une autorisation de webhook est gérée par le composant récepteur de webhook, qui fait partie du HttpTrigger, et le mécanisme varie en fonction du type de webhook.</span><span class="sxs-lookup"><span data-stu-id="b5f75-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="b5f75-222">Toutefois, chaque mécanisme dépend d’une clé.</span><span class="sxs-lookup"><span data-stu-id="b5f75-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="b5f75-223">Par défaut, la clé de fonction nommée « default » est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b5f75-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="b5f75-224">Si vous souhaitez utiliser une autre clé, vous devez configurer le fournisseur de webhook pour envoyer le nom de clé avec la demande de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5f75-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="b5f75-225">**Chaîne de requête** : le fournisseur transmet le nom de clé dans le paramètre de chaîne de requête `clientid` (par exemple, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="b5f75-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="b5f75-226">**En-tête de demande** : le fournisseur transmet le nom de clé dans l’en-tête `x-functions-clientid`.</span><span class="sxs-lookup"><span data-stu-id="b5f75-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="b5f75-227">Les clés de fonction prennent le pas sur les clés d’hôte.</span><span class="sxs-lookup"><span data-stu-id="b5f75-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="b5f75-228">Si les deux clés portent le même nom, la clé de fonction est utilisée.</span><span class="sxs-lookup"><span data-stu-id="b5f75-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="b5f75-229">Exemples de déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="b5f75-229">HTTP trigger samples</span></span>
<span data-ttu-id="b5f75-230">Supposons que le tableau `bindings` de function.json contient le déclencheur HTTP suivant :</span><span class="sxs-lookup"><span data-stu-id="b5f75-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="b5f75-231">Voir l’exemple spécifique du langage qui recherche un paramètre `name` dans la chaîne de requête ou dans le corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5f75-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="b5f75-232">C#</span><span class="sxs-lookup"><span data-stu-id="b5f75-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="b5f75-233">F#</span><span class="sxs-lookup"><span data-stu-id="b5f75-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="b5f75-234">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b5f75-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="b5f75-235">Exemple de déclencheur HTTP en C#</span><span class="sxs-lookup"><span data-stu-id="b5f75-235">HTTP trigger sample in C#</span></span> #
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

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="b5f75-236">Vous pouvez également lier à un POCO au lieu de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="b5f75-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="b5f75-237">Ceci est alimenté à partir du corps de la demande, analysé en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="b5f75-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="b5f75-238">De même, un type peut être passé à la sortie de réponse HTTP qui lie, et ceci est retourné en tant que corps de la réponse, avec un code d’état 200.</span><span class="sxs-lookup"><span data-stu-id="b5f75-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="b5f75-239">Exemple de déclencheur HTTP en F#</span><span class="sxs-lookup"><span data-stu-id="b5f75-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="b5f75-240">Vous avez besoin d’un fichier `project.json` qui utilise NuGet pour référencer les assemblys `FSharp.Interop.Dynamic` et `Dynamitey`, comme suit :</span><span class="sxs-lookup"><span data-stu-id="b5f75-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="b5f75-241">Ce code utilisera NuGet pour extraire vos dépendances et les référencera dans votre script.</span><span class="sxs-lookup"><span data-stu-id="b5f75-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="b5f75-242">Exemple de déclencheur HTTP en Node.js</span><span class="sxs-lookup"><span data-stu-id="b5f75-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="b5f75-243">Exemples de webhook</span><span class="sxs-lookup"><span data-stu-id="b5f75-243">Webhook samples</span></span>
<span data-ttu-id="b5f75-244">Supposons que le tableau `bindings` de function.json contient le déclencheur de webhook suivant :</span><span class="sxs-lookup"><span data-stu-id="b5f75-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="b5f75-245">Voir l’exemple spécifique du langage qui journalise les commentaires de problème GitHub.</span><span class="sxs-lookup"><span data-stu-id="b5f75-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="b5f75-246">C#</span><span class="sxs-lookup"><span data-stu-id="b5f75-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="b5f75-247">F#</span><span class="sxs-lookup"><span data-stu-id="b5f75-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="b5f75-248">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b5f75-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="b5f75-249">Exemple de Webhook en C#</span><span class="sxs-lookup"><span data-stu-id="b5f75-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="b5f75-250">Exemple de Webhook en F#</span><span class="sxs-lookup"><span data-stu-id="b5f75-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="b5f75-251">Exemple de webhook en Node.js</span><span class="sxs-lookup"><span data-stu-id="b5f75-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="b5f75-252">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5f75-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

