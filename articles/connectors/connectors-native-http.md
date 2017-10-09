---
title: "aaaCommunicate avec n’importe quel point de terminaison via HTTP - Azure Logic Apps | Documents Microsoft"
description: "Créer des applications logiques qui peuvent communiquer avec n’importe quel point de terminaison via HTTP"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a><span data-ttu-id="df86d-103">Prise en main hello action HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-103">Get started with hello HTTP action</span></span>

<span data-ttu-id="df86d-104">Avec hello action HTTP, vous pouvez étendre le flux de travail pour votre organisation et communiquer un point de terminaison tooany via HTTP.</span><span class="sxs-lookup"><span data-stu-id="df86d-104">With hello HTTP action, you can extend workflows for your organization and communicate tooany endpoint over HTTP.</span></span>

<span data-ttu-id="df86d-105">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="df86d-105">You can:</span></span>

* <span data-ttu-id="df86d-106">Créez des workflows d’application logique qui s’activent (se déclenchent) lors d’une défaillance d’un site Web que vous gérez.</span><span class="sxs-lookup"><span data-stu-id="df86d-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="df86d-107">Communiquent tooany le point de terminaison via HTTP tooextend votre flux de travail à d’autres services.</span><span class="sxs-lookup"><span data-stu-id="df86d-107">Communicate tooany endpoint over HTTP tooextend your workflows into other services.</span></span>

<span data-ttu-id="df86d-108">tooget démarré à l’aide d’action de hello HTTP dans une application logique, consultez [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="df86d-108">tooget started using hello HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-http-trigger"></a><span data-ttu-id="df86d-109">Utilisez le déclencheur de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-109">Use hello HTTP trigger</span></span>
<span data-ttu-id="df86d-110">Un déclencheur est un événement qui peut être utilisé toostart hello flux de travail qui est défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="df86d-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="df86d-111">[En savoir plus sur les déclencheurs](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df86d-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="df86d-112">Voici un exemple de séquence de comment déclencher des tooset des hello HTTP Bonjour Concepteur de logique d’application.</span><span class="sxs-lookup"><span data-stu-id="df86d-112">Here’s an example sequence of how tooset up hello HTTP trigger in hello Logic App Designer.</span></span>

1. <span data-ttu-id="df86d-113">Ajouter le déclencheur HTTP hello dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="df86d-113">Add hello HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="df86d-114">Renseignez les paramètres pour le point de terminaison hello HTTP que vous souhaitez toopoll hello.</span><span class="sxs-lookup"><span data-stu-id="df86d-114">Fill in hello parameters for hello HTTP endpoint that you want toopoll.</span></span>
3. <span data-ttu-id="df86d-115">Modifier l’intervalle de périodicité hello sur la fréquence à laquelle il doit interroger.</span><span class="sxs-lookup"><span data-stu-id="df86d-115">Modify hello recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="df86d-116">application de la logique de Hello déclenche maintenant dont le contenu est renvoyée lors de chaque vérification.</span><span class="sxs-lookup"><span data-stu-id="df86d-116">hello logic app now fires with any content that is returned during each check.</span></span>

   ![Déclencheur HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a><span data-ttu-id="df86d-118">Fonctionne de déclencheur HTTP hello</span><span class="sxs-lookup"><span data-stu-id="df86d-118">How hello HTTP trigger works</span></span>

<span data-ttu-id="df86d-119">déclencheur HTTP Hello envoie un point de terminaison tooHTTP appel sur un intervalle périodique.</span><span class="sxs-lookup"><span data-stu-id="df86d-119">hello HTTP trigger sends a call tooHTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="df86d-120">Par défaut, tout code de réponse HTTP qui est inférieur à 300 entraîne un toorun d’application logique.</span><span class="sxs-lookup"><span data-stu-id="df86d-120">By default, any HTTP response code that is lower than 300 causes a logic app toorun.</span></span> <span data-ttu-id="df86d-121">toospecify si l’application logique de hello doit être activé, vous pouvez modifier l’application de la logique de hello en mode code et ajouter une condition qui prend la valeur hello après l’appel HTTP.</span><span class="sxs-lookup"><span data-stu-id="df86d-121">toospecify whether hello logic app should fire, you can edit hello logic app in code view, and add a condition that evaluates after hello HTTP call.</span></span> <span data-ttu-id="df86d-122">Voici un exemple d’un déclencheur HTTP qui se déclenche lorsque hello retourné le code d’état est supérieur ou égal à trop`400`.</span><span class="sxs-lookup"><span data-stu-id="df86d-122">Here's an example of an HTTP trigger that fires when hello returned status code is greater than or equal too`400`.</span></span>

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

<span data-ttu-id="df86d-123">En savoir plus sur les paramètres de déclencheur hello HTTP sont disponibles sur [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span><span class="sxs-lookup"><span data-stu-id="df86d-123">Full details about hello HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-hello-http-action"></a><span data-ttu-id="df86d-124">Utilisez l’action de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-124">Use hello HTTP action</span></span>

<span data-ttu-id="df86d-125">Une action est une opération est effectuée par le flux de travail hello défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="df86d-125">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="df86d-126">[En savoir plus sur les actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df86d-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="df86d-127">Choisissez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="df86d-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="df86d-128">Dans la zone de recherche action hello, tapez **http** actions de hello HTTP toolist.</span><span class="sxs-lookup"><span data-stu-id="df86d-128">In hello action search box, type **http** toolist hello HTTP actions.</span></span>
   
    ![Sélectionnez l’action de hello HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="df86d-130">Ajoutez tous les paramètres requis pour l’appel de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="df86d-130">Add any required parameters for hello HTTP call.</span></span>
   
    ![Hello complète action HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="df86d-132">Dans la barre d’outils Concepteur hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="df86d-132">On hello designer toolbar, click **Save**.</span></span> <span data-ttu-id="df86d-133">Votre application logique est enregistrée et publiée (activée) à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="df86d-133">Your logic app is saved and published (activated) at hello same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="df86d-134">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-134">HTTP trigger</span></span>
<span data-ttu-id="df86d-135">Voici les détails de hello pour déclencheur hello qui prend en charge par ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="df86d-135">Here are hello details for hello trigger that this connector supports.</span></span> <span data-ttu-id="df86d-136">connecteur HTTP Hello a un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="df86d-136">hello HTTP connector has one trigger.</span></span>

| <span data-ttu-id="df86d-137">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="df86d-137">Trigger</span></span> | <span data-ttu-id="df86d-138">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df86d-139">HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-139">HTTP</span></span> |<span data-ttu-id="df86d-140">Effectue un appel HTTP et retourne le contenu de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="df86d-140">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="df86d-141">Action HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-141">HTTP action</span></span>
<span data-ttu-id="df86d-142">Voici les détails de hello pour action hello qui prend en charge par ce connecteur.</span><span class="sxs-lookup"><span data-stu-id="df86d-142">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="df86d-143">connecteur de Hello HTTP a une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="df86d-143">hello HTTP connector has one possible action.</span></span>

| <span data-ttu-id="df86d-144">Action</span><span class="sxs-lookup"><span data-stu-id="df86d-144">Action</span></span> | <span data-ttu-id="df86d-145">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="df86d-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-146">HTTP</span></span> |<span data-ttu-id="df86d-147">Effectue un appel HTTP et retourne le contenu de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="df86d-147">Makes an HTTP call and returns hello response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="df86d-148">Détails HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-148">HTTP details</span></span>
<span data-ttu-id="df86d-149">Hello tableaux suivants décrivent hello requis et les champs d’entrée facultatifs pour action de hello et détails sortie correspondants hello qui sont associés à l’aide d’action de hello.</span><span class="sxs-lookup"><span data-stu-id="df86d-149">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="df86d-150">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-150">HTTP request</span></span>
<span data-ttu-id="df86d-151">Hello Voici les champs d’entrée pour l’action hello, qui effectue une requête de sortie HTTP.</span><span class="sxs-lookup"><span data-stu-id="df86d-151">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="df86d-152">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="df86d-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="df86d-153">Nom complet</span><span class="sxs-lookup"><span data-stu-id="df86d-153">Display name</span></span> | <span data-ttu-id="df86d-154">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="df86d-154">Property name</span></span> | <span data-ttu-id="df86d-155">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df86d-156">Method (Méthode)*</span><span class="sxs-lookup"><span data-stu-id="df86d-156">Method*</span></span> |<span data-ttu-id="df86d-157">method</span><span class="sxs-lookup"><span data-stu-id="df86d-157">method</span></span> |<span data-ttu-id="df86d-158">Hello HTTP verbe toouse</span><span class="sxs-lookup"><span data-stu-id="df86d-158">hello HTTP verb toouse</span></span> |
| <span data-ttu-id="df86d-159">URI*</span><span class="sxs-lookup"><span data-stu-id="df86d-159">URI*</span></span> |<span data-ttu-id="df86d-160">URI</span><span class="sxs-lookup"><span data-stu-id="df86d-160">uri</span></span> |<span data-ttu-id="df86d-161">Hello URI de demande de hello HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-161">hello URI for hello HTTP request</span></span> |
| <span data-ttu-id="df86d-162">headers</span><span class="sxs-lookup"><span data-stu-id="df86d-162">Headers</span></span> |<span data-ttu-id="df86d-163">headers</span><span class="sxs-lookup"><span data-stu-id="df86d-163">headers</span></span> |<span data-ttu-id="df86d-164">Un objet JSON de tooinclude des en-têtes HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-164">A JSON object of HTTP headers tooinclude</span></span> |
| <span data-ttu-id="df86d-165">Corps</span><span class="sxs-lookup"><span data-stu-id="df86d-165">Body</span></span> |<span data-ttu-id="df86d-166">body</span><span class="sxs-lookup"><span data-stu-id="df86d-166">body</span></span> |<span data-ttu-id="df86d-167">Hello corps de la demande HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-167">hello HTTP request body</span></span> |
| <span data-ttu-id="df86d-168">Authentification</span><span class="sxs-lookup"><span data-stu-id="df86d-168">Authentication</span></span> |<span data-ttu-id="df86d-169">authentication</span><span class="sxs-lookup"><span data-stu-id="df86d-169">authentication</span></span> |<span data-ttu-id="df86d-170">Détails Bonjour [authentification](#authentication) section</span><span class="sxs-lookup"><span data-stu-id="df86d-170">Details in hello [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="df86d-171">Détails des résultats</span><span class="sxs-lookup"><span data-stu-id="df86d-171">Output details</span></span>
<span data-ttu-id="df86d-172">Hello Voici les détails de sortie de réponse HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="df86d-172">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="df86d-173">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="df86d-173">Property name</span></span> | <span data-ttu-id="df86d-174">Type de données</span><span class="sxs-lookup"><span data-stu-id="df86d-174">Data type</span></span> | <span data-ttu-id="df86d-175">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df86d-176">headers</span><span class="sxs-lookup"><span data-stu-id="df86d-176">Headers</span></span> |<span data-ttu-id="df86d-177">objet</span><span class="sxs-lookup"><span data-stu-id="df86d-177">object</span></span> |<span data-ttu-id="df86d-178">En-têtes de réponse</span><span class="sxs-lookup"><span data-stu-id="df86d-178">Response headers</span></span> |
| <span data-ttu-id="df86d-179">Corps</span><span class="sxs-lookup"><span data-stu-id="df86d-179">Body</span></span> |<span data-ttu-id="df86d-180">objet</span><span class="sxs-lookup"><span data-stu-id="df86d-180">object</span></span> |<span data-ttu-id="df86d-181">Objet Réponse</span><span class="sxs-lookup"><span data-stu-id="df86d-181">Response object</span></span> |
| <span data-ttu-id="df86d-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="df86d-182">Status Code</span></span> |<span data-ttu-id="df86d-183">int</span><span class="sxs-lookup"><span data-stu-id="df86d-183">int</span></span> |<span data-ttu-id="df86d-184">Code d'état HTTP</span><span class="sxs-lookup"><span data-stu-id="df86d-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="df86d-185">Authentification</span><span class="sxs-lookup"><span data-stu-id="df86d-185">Authentication</span></span>
<span data-ttu-id="df86d-186">fonctionnalité de Logic Apps Hello permet toouse différents types d’authentification par rapport aux points de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="df86d-186">hello Logic Apps feature allows you toouse different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="df86d-187">Vous pouvez utiliser cette authentification avec hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, et  **[HTTP Webhook](connectors-native-webhook.md)**  connecteurs.</span><span class="sxs-lookup"><span data-stu-id="df86d-187">You can use this authentication with hello **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="df86d-188">Hello, les types d’authentification suivants est configurable :</span><span class="sxs-lookup"><span data-stu-id="df86d-188">hello following types of authentication are configurable:</span></span>

* [<span data-ttu-id="df86d-189">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="df86d-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="df86d-190">Authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="df86d-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="df86d-191">Authentification OAuth Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="df86d-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="df86d-192">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="df86d-192">Basic authentication</span></span>

<span data-ttu-id="df86d-193">Hello suivant l’objet d’authentification est nécessaire pour l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="df86d-193">hello following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="df86d-194">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="df86d-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="df86d-195">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="df86d-195">Property name</span></span> | <span data-ttu-id="df86d-196">Type de données</span><span class="sxs-lookup"><span data-stu-id="df86d-196">Data type</span></span> | <span data-ttu-id="df86d-197">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df86d-198">Entrez*</span><span class="sxs-lookup"><span data-stu-id="df86d-198">Type*</span></span> |<span data-ttu-id="df86d-199">type</span><span class="sxs-lookup"><span data-stu-id="df86d-199">type</span></span> |<span data-ttu-id="df86d-200">Type d’authentification (doit être `Basic` dans le cas d’une authentification de base)</span><span class="sxs-lookup"><span data-stu-id="df86d-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="df86d-201">Nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="df86d-201">Username*</span></span> |<span data-ttu-id="df86d-202">username</span><span class="sxs-lookup"><span data-stu-id="df86d-202">username</span></span> |<span data-ttu-id="df86d-203">Tooauthenticate de nom d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="df86d-203">User name tooauthenticate</span></span> |
| <span data-ttu-id="df86d-204">Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="df86d-204">Password*</span></span> |<span data-ttu-id="df86d-205">password</span><span class="sxs-lookup"><span data-stu-id="df86d-205">password</span></span> |<span data-ttu-id="df86d-206">Mot de passe tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="df86d-206">Password tooauthenticate</span></span> |

> [!TIP]
> <span data-ttu-id="df86d-207">Si vous souhaitez toouse un mot de passe ne peut pas être récupérée à partir de la définition de hello, utilisez un `securestring` paramètre et hello `@parameters()`  
>  [fonction de définition de flux de travail](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="df86d-207">If you want toouse a password that cannot be retrieved from hello definition, use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="df86d-208">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="df86d-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="df86d-209">Authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="df86d-209">Client certificate authentication</span></span>

<span data-ttu-id="df86d-210">Hello objet suivant de l’authentification est nécessaire pour l’authentification par certificat client.</span><span class="sxs-lookup"><span data-stu-id="df86d-210">hello following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="df86d-211">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="df86d-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="df86d-212">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="df86d-212">Property name</span></span> | <span data-ttu-id="df86d-213">Type de données</span><span class="sxs-lookup"><span data-stu-id="df86d-213">Data type</span></span> | <span data-ttu-id="df86d-214">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df86d-215">Entrez*</span><span class="sxs-lookup"><span data-stu-id="df86d-215">Type*</span></span> |<span data-ttu-id="df86d-216">type</span><span class="sxs-lookup"><span data-stu-id="df86d-216">type</span></span> |<span data-ttu-id="df86d-217">type d’authentification de Hello (doit être `ClientCertificate` pour les certificats clients SSL)</span><span class="sxs-lookup"><span data-stu-id="df86d-217">hello type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="df86d-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="df86d-218">PFX*</span></span> |<span data-ttu-id="df86d-219">pfx</span><span class="sxs-lookup"><span data-stu-id="df86d-219">pfx</span></span> |<span data-ttu-id="df86d-220">contenu de codée en Base64 Hello du fichier d’informations Exchange PFX (Personal) hello</span><span class="sxs-lookup"><span data-stu-id="df86d-220">hello Base64-encoded contents of hello Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="df86d-221">Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="df86d-221">Password*</span></span> |<span data-ttu-id="df86d-222">password</span><span class="sxs-lookup"><span data-stu-id="df86d-222">password</span></span> |<span data-ttu-id="df86d-223">tooaccess de mot de passe Hello hello fichier PFX</span><span class="sxs-lookup"><span data-stu-id="df86d-223">hello password tooaccess hello PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="df86d-224">toouse un paramètre qui ne sont pas lisible dans la définition de hello après avoir enregistré l’application logique de hello, vous pouvez utiliser un `securestring` paramètre et hello `@parameters()`  
>  [fonction de définition de flux de travail](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="df86d-224">toouse a parameter that won't be readable in hello definition after saving hello logic app, you can use a `securestring` parameter and hello `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="df86d-225">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="df86d-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="df86d-226">Authentification OAuth Azure AD</span><span class="sxs-lookup"><span data-stu-id="df86d-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="df86d-227">Hello suivant l’objet d’authentification est nécessaire pour l’authentification Azure AD OAuth.</span><span class="sxs-lookup"><span data-stu-id="df86d-227">hello following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="df86d-228">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="df86d-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="df86d-229">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="df86d-229">Property name</span></span> | <span data-ttu-id="df86d-230">Type de données</span><span class="sxs-lookup"><span data-stu-id="df86d-230">Data type</span></span> | <span data-ttu-id="df86d-231">Description</span><span class="sxs-lookup"><span data-stu-id="df86d-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df86d-232">Entrez*</span><span class="sxs-lookup"><span data-stu-id="df86d-232">Type*</span></span> |<span data-ttu-id="df86d-233">type</span><span class="sxs-lookup"><span data-stu-id="df86d-233">type</span></span> |<span data-ttu-id="df86d-234">type d’authentification de Hello (doit être `ActiveDirectoryOAuth` pour Azure AD OAuth)</span><span class="sxs-lookup"><span data-stu-id="df86d-234">hello type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="df86d-235">Locataire*</span><span class="sxs-lookup"><span data-stu-id="df86d-235">Tenant*</span></span> |<span data-ttu-id="df86d-236">locataire</span><span class="sxs-lookup"><span data-stu-id="df86d-236">tenant</span></span> |<span data-ttu-id="df86d-237">Identificateur du locataire Hello pour le client de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="df86d-237">hello tenant identifier for hello Azure AD tenant</span></span> |
| <span data-ttu-id="df86d-238">Public ciblé*</span><span class="sxs-lookup"><span data-stu-id="df86d-238">Audience*</span></span> |<span data-ttu-id="df86d-239">audience</span><span class="sxs-lookup"><span data-stu-id="df86d-239">audience</span></span> |<span data-ttu-id="df86d-240">ressource Hello vous demande d’autorisation toouse.</span><span class="sxs-lookup"><span data-stu-id="df86d-240">hello resource you are requesting authorization toouse.</span></span> <span data-ttu-id="df86d-241">Par exemple : `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="df86d-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="df86d-242">ID de client*</span><span class="sxs-lookup"><span data-stu-id="df86d-242">Client ID*</span></span> |<span data-ttu-id="df86d-243">clientId</span><span class="sxs-lookup"><span data-stu-id="df86d-243">clientId</span></span> |<span data-ttu-id="df86d-244">Hello d’identificateur de client pour l’application hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="df86d-244">hello client identifier for hello Azure AD application</span></span> |
| <span data-ttu-id="df86d-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="df86d-245">Secret*</span></span> |<span data-ttu-id="df86d-246">secret</span><span class="sxs-lookup"><span data-stu-id="df86d-246">secret</span></span> |<span data-ttu-id="df86d-247">secret Hello du client hello qui demande hello jeton</span><span class="sxs-lookup"><span data-stu-id="df86d-247">hello secret of hello client that is requesting hello token</span></span> |

> [!TIP]
> <span data-ttu-id="df86d-248">Vous pouvez utiliser un `securestring` paramètre et hello `@parameters()` [fonction de définition de workflow](http://aka.ms/logicappdocs) toouse un paramètre qui ne sont pas lisible dans la définition de hello après l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="df86d-248">You can use a `securestring` parameter and hello `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) toouse a parameter that won't be readable in hello definition after saving.</span></span>
> 
> 

<span data-ttu-id="df86d-249">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="df86d-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="df86d-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df86d-250">Next steps</span></span>
<span data-ttu-id="df86d-251">Maintenant, essayez de plate-forme de hello et [créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="df86d-251">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="df86d-252">Vous pouvez Explorer hello tous les autres connecteurs disponibles dans les applications de la logique en consultant notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="df86d-252">You can explore hello other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

