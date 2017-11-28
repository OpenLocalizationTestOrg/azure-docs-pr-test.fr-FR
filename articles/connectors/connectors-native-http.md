---
title: Communiquer avec un point de terminaison via HTTP - Azure Logic Apps | Microsoft Docs
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
ms.openlocfilehash: d422a07a27ffa62a673bd2d471ae4fc837251dee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-http-action"></a><span data-ttu-id="24dcb-103">Prise en main de l’action HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-103">Get started with the HTTP action</span></span>

<span data-ttu-id="24dcb-104">Avec l’action HTTP, vous pouvez étendre les workflows pour votre organisation et communiquer avec n’importe quel point de terminaison par le biais de HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-104">With the HTTP action, you can extend workflows for your organization and communicate to any endpoint over HTTP.</span></span>

<span data-ttu-id="24dcb-105">Vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="24dcb-105">You can:</span></span>

* <span data-ttu-id="24dcb-106">Créez des workflows d’application logique qui s’activent (se déclenchent) lors d’une défaillance d’un site Web que vous gérez.</span><span class="sxs-lookup"><span data-stu-id="24dcb-106">Create logic app workflows that activate (trigger) when a website that you manage goes down.</span></span>
* <span data-ttu-id="24dcb-107">Communiquez avec n’importe quel point de terminaison par le biais de HTTP afin d’étendre vos workflows à d’autres services.</span><span class="sxs-lookup"><span data-stu-id="24dcb-107">Communicate to any endpoint over HTTP to extend your workflows into other services.</span></span>

<span data-ttu-id="24dcb-108">Pour commencer à utiliser l’action HTTP dans une application logique, consultez [Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="24dcb-108">To get started using the HTTP action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-http-trigger"></a><span data-ttu-id="24dcb-109">Utilisation du déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-109">Use the HTTP trigger</span></span>
<span data-ttu-id="24dcb-110">Un déclencheur est un événement qui peut être utilisé pour lancer le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="24dcb-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="24dcb-111">[En savoir plus sur les déclencheurs](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24dcb-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="24dcb-112">Voici un exemple de séquence de configuration du déclencheur HTTP dans le concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="24dcb-112">Here’s an example sequence of how to set up the HTTP trigger in the Logic App Designer.</span></span>

1. <span data-ttu-id="24dcb-113">Ajoutez le déclencheur HTTP dans votre application logique.</span><span class="sxs-lookup"><span data-stu-id="24dcb-113">Add the HTTP trigger in your logic app.</span></span>
2. <span data-ttu-id="24dcb-114">Renseignez les paramètres du point de terminaison HTTP que vous souhaitez interroger.</span><span class="sxs-lookup"><span data-stu-id="24dcb-114">Fill in the parameters for the HTTP endpoint that you want to poll.</span></span>
3. <span data-ttu-id="24dcb-115">Modifiez l’intervalle de périodicité sur la fréquence d’interrogation souhaitée.</span><span class="sxs-lookup"><span data-stu-id="24dcb-115">Modify the recurrence interval on how frequently it should poll.</span></span>

   <span data-ttu-id="24dcb-116">L’application logique se déclenche maintenant avec n’importe quel contenu retourné lors de chaque vérification.</span><span class="sxs-lookup"><span data-stu-id="24dcb-116">The logic app now fires with any content that is returned during each check.</span></span>

   ![Déclencheur HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-the-http-trigger-works"></a><span data-ttu-id="24dcb-118">Fonctionnement du déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-118">How the HTTP trigger works</span></span>

<span data-ttu-id="24dcb-119">Le déclencheur HTTP effectue un appel sur un point de terminaison HTTP selon un intervalle récurrent.</span><span class="sxs-lookup"><span data-stu-id="24dcb-119">The HTTP trigger sends a call to HTTP endpoint on a recurring interval.</span></span> <span data-ttu-id="24dcb-120">Par défaut, tout code de réponse HTTP inférieur à 300 entraîne l’exécution d’une application logique.</span><span class="sxs-lookup"><span data-stu-id="24dcb-120">By default, any HTTP response code that is lower than 300 causes a logic app to run.</span></span> <span data-ttu-id="24dcb-121">Pour spécifier si l’application logique doit se déclencher, vous pouvez modifier l’application logique en mode code et ajouter une condition qui prend une valeur donnée après l’appel HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-121">To specify whether the logic app should fire, you can edit the logic app in code view, and add a condition that evaluates after the HTTP call.</span></span> <span data-ttu-id="24dcb-122">Voici un exemple de déclencheur HTTP qui se déclenche chaque fois que le code d’état renvoyé est supérieur ou égal à `400`.</span><span class="sxs-lookup"><span data-stu-id="24dcb-122">Here's an example of an HTTP trigger that fires when the returned status code is greater than or equal to `400`.</span></span>

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

<span data-ttu-id="24dcb-123">Consultez [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger)pour obtenir des informations complètes sur les paramètres du déclencheur HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-123">Full details about the HTTP trigger parameters are available on [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).</span></span>

## <a name="use-the-http-action"></a><span data-ttu-id="24dcb-124">Utilisation de l’action HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-124">Use the HTTP action</span></span>

<span data-ttu-id="24dcb-125">Une action est une opération effectuée par le flux de travail défini dans une application logique.</span><span class="sxs-lookup"><span data-stu-id="24dcb-125">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> 
<span data-ttu-id="24dcb-126">[Apprenez-en davantage sur les actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24dcb-126">[Learn more about actions](connectors-overview.md).</span></span>

1. <span data-ttu-id="24dcb-127">Choisissez **Nouvelle étape** > **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="24dcb-127">Choose **New Step** > **Add an action**.</span></span>
3. <span data-ttu-id="24dcb-128">Dans la zone de recherche Action , **http** pour répertorier les actions HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-128">In the action search box, type **http** to list the HTTP actions.</span></span>
   
    ![Sélection de l’action HTTP](./media/connectors-native-http/using-action-1.png)

4. <span data-ttu-id="24dcb-130">Ajoutez tout paramètre nécessaire à l’appel HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-130">Add any required parameters for the HTTP call.</span></span>
   
    ![Exécution de l’action HTTP](./media/connectors-native-http/using-action-2.png)

5. <span data-ttu-id="24dcb-132">Dans la barre d’outils du concepteur, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="24dcb-132">On the designer toolbar, click **Save**.</span></span> <span data-ttu-id="24dcb-133">Votre application logique est enregistrée et publiée (activée) en même temps.</span><span class="sxs-lookup"><span data-stu-id="24dcb-133">Your logic app is saved and published (activated) at the same time.</span></span>

## <a name="http-trigger"></a><span data-ttu-id="24dcb-134">Déclencheur HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-134">HTTP trigger</span></span>
<span data-ttu-id="24dcb-135">Voici les détails du déclencheur que ce connecteur prend en charge.</span><span class="sxs-lookup"><span data-stu-id="24dcb-135">Here are the details for the trigger that this connector supports.</span></span> <span data-ttu-id="24dcb-136">Le connecteur HTTP possède un déclencheur.</span><span class="sxs-lookup"><span data-stu-id="24dcb-136">The HTTP connector has one trigger.</span></span>

| <span data-ttu-id="24dcb-137">Déclencheur</span><span class="sxs-lookup"><span data-stu-id="24dcb-137">Trigger</span></span> | <span data-ttu-id="24dcb-138">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24dcb-139">http</span><span class="sxs-lookup"><span data-stu-id="24dcb-139">HTTP</span></span> |<span data-ttu-id="24dcb-140">Exécute un appel HTTP et renvoie le contenu de la réponse.</span><span class="sxs-lookup"><span data-stu-id="24dcb-140">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-action"></a><span data-ttu-id="24dcb-141">Action HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-141">HTTP action</span></span>
<span data-ttu-id="24dcb-142">Voici les détails de l’action que ce connecteur prend en charge.</span><span class="sxs-lookup"><span data-stu-id="24dcb-142">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="24dcb-143">Le connecteur HTTP n’a qu’une seule action possible.</span><span class="sxs-lookup"><span data-stu-id="24dcb-143">The HTTP connector has one possible action.</span></span>

| <span data-ttu-id="24dcb-144">Action</span><span class="sxs-lookup"><span data-stu-id="24dcb-144">Action</span></span> | <span data-ttu-id="24dcb-145">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-145">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24dcb-146">http</span><span class="sxs-lookup"><span data-stu-id="24dcb-146">HTTP</span></span> |<span data-ttu-id="24dcb-147">Exécute un appel HTTP et renvoie le contenu de la réponse.</span><span class="sxs-lookup"><span data-stu-id="24dcb-147">Makes an HTTP call and returns the response content.</span></span> |

## <a name="http-details"></a><span data-ttu-id="24dcb-148">Détails HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-148">HTTP details</span></span>
<span data-ttu-id="24dcb-149">Les tableaux suivants décrivent les champs de saisie obligatoires et facultatifs pour l’action, ainsi que les détails des résultats correspondants associés à son utilisation.</span><span class="sxs-lookup"><span data-stu-id="24dcb-149">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

#### <a name="http-request"></a><span data-ttu-id="24dcb-150">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-150">HTTP request</span></span>
<span data-ttu-id="24dcb-151">Vous trouverez ci-dessous les champs de saisie de l’action permettant de générer une demande HTTP sortante.</span><span class="sxs-lookup"><span data-stu-id="24dcb-151">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="24dcb-152">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="24dcb-152">A * means that it is a required field.</span></span>

| <span data-ttu-id="24dcb-153">Nom complet</span><span class="sxs-lookup"><span data-stu-id="24dcb-153">Display name</span></span> | <span data-ttu-id="24dcb-154">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="24dcb-154">Property name</span></span> | <span data-ttu-id="24dcb-155">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24dcb-156">Method (Méthode)*</span><span class="sxs-lookup"><span data-stu-id="24dcb-156">Method*</span></span> |<span data-ttu-id="24dcb-157">statique</span><span class="sxs-lookup"><span data-stu-id="24dcb-157">method</span></span> |<span data-ttu-id="24dcb-158">Verbe HTTP à utiliser</span><span class="sxs-lookup"><span data-stu-id="24dcb-158">The HTTP verb to use</span></span> |
| <span data-ttu-id="24dcb-159">URI*</span><span class="sxs-lookup"><span data-stu-id="24dcb-159">URI*</span></span> |<span data-ttu-id="24dcb-160">URI</span><span class="sxs-lookup"><span data-stu-id="24dcb-160">uri</span></span> |<span data-ttu-id="24dcb-161">URI de la requête HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-161">The URI for the HTTP request</span></span> |
| <span data-ttu-id="24dcb-162">En-têtes</span><span class="sxs-lookup"><span data-stu-id="24dcb-162">Headers</span></span> |<span data-ttu-id="24dcb-163">En-têtes</span><span class="sxs-lookup"><span data-stu-id="24dcb-163">headers</span></span> |<span data-ttu-id="24dcb-164">Un objet JSON d’en-têtes HTTP à inclure</span><span class="sxs-lookup"><span data-stu-id="24dcb-164">A JSON object of HTTP headers to include</span></span> |
| <span data-ttu-id="24dcb-165">Corps</span><span class="sxs-lookup"><span data-stu-id="24dcb-165">Body</span></span> |<span data-ttu-id="24dcb-166">Corps</span><span class="sxs-lookup"><span data-stu-id="24dcb-166">body</span></span> |<span data-ttu-id="24dcb-167">Le texte de la requête HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-167">The HTTP request body</span></span> |
| <span data-ttu-id="24dcb-168">Authentification</span><span class="sxs-lookup"><span data-stu-id="24dcb-168">Authentication</span></span> |<span data-ttu-id="24dcb-169">Authentification</span><span class="sxs-lookup"><span data-stu-id="24dcb-169">authentication</span></span> |<span data-ttu-id="24dcb-170">Détails contenus dans la section [Authentification](#authentication)</span><span class="sxs-lookup"><span data-stu-id="24dcb-170">Details in the [Authentication](#authentication) section</span></span> |

<br>

#### <a name="output-details"></a><span data-ttu-id="24dcb-171">Détails des résultats</span><span class="sxs-lookup"><span data-stu-id="24dcb-171">Output details</span></span>
<span data-ttu-id="24dcb-172">Vous trouverez ci-dessous les détails de sortie correspondant à la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-172">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="24dcb-173">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="24dcb-173">Property name</span></span> | <span data-ttu-id="24dcb-174">Type de données</span><span class="sxs-lookup"><span data-stu-id="24dcb-174">Data type</span></span> | <span data-ttu-id="24dcb-175">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-175">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24dcb-176">headers</span><span class="sxs-lookup"><span data-stu-id="24dcb-176">Headers</span></span> |<span data-ttu-id="24dcb-177">objet</span><span class="sxs-lookup"><span data-stu-id="24dcb-177">object</span></span> |<span data-ttu-id="24dcb-178">En-têtes de réponse</span><span class="sxs-lookup"><span data-stu-id="24dcb-178">Response headers</span></span> |
| <span data-ttu-id="24dcb-179">Corps</span><span class="sxs-lookup"><span data-stu-id="24dcb-179">Body</span></span> |<span data-ttu-id="24dcb-180">objet</span><span class="sxs-lookup"><span data-stu-id="24dcb-180">object</span></span> |<span data-ttu-id="24dcb-181">Objet Réponse</span><span class="sxs-lookup"><span data-stu-id="24dcb-181">Response object</span></span> |
| <span data-ttu-id="24dcb-182">Code d’état</span><span class="sxs-lookup"><span data-stu-id="24dcb-182">Status Code</span></span> |<span data-ttu-id="24dcb-183">int</span><span class="sxs-lookup"><span data-stu-id="24dcb-183">int</span></span> |<span data-ttu-id="24dcb-184">Code d'état HTTP</span><span class="sxs-lookup"><span data-stu-id="24dcb-184">HTTP status code</span></span> |

## <a name="authentication"></a><span data-ttu-id="24dcb-185">Authentification</span><span class="sxs-lookup"><span data-stu-id="24dcb-185">Authentication</span></span>
<span data-ttu-id="24dcb-186">La fonctionnalité Logic Apps vous permet d’utiliser différents types d’authentification sur vos points de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dcb-186">The Logic Apps feature allows you to use different types of authentication against HTTP endpoints.</span></span> <span data-ttu-id="24dcb-187">Vous pouvez utiliser cette authentification avec les connecteurs **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)** et **[HTTP Webhook](connectors-native-webhook.md)**.</span><span class="sxs-lookup"><span data-stu-id="24dcb-187">You can use this authentication with the **HTTP**, **[HTTP + Swagger](connectors-native-http-swagger.md)**, and **[HTTP Webhook](connectors-native-webhook.md)** connectors.</span></span> <span data-ttu-id="24dcb-188">Les types d’authentification suivants sont configurables :</span><span class="sxs-lookup"><span data-stu-id="24dcb-188">The following types of authentication are configurable:</span></span>

* [<span data-ttu-id="24dcb-189">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="24dcb-189">Basic authentication</span></span>](#basic-authentication)
* [<span data-ttu-id="24dcb-190">Authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="24dcb-190">Client certificate authentication</span></span>](#client-certificate-authentication)
* [<span data-ttu-id="24dcb-191">Authentification OAuth Azure Active Directory (Azure AD)</span><span class="sxs-lookup"><span data-stu-id="24dcb-191">Azure Active Directory (Azure AD) OAuth authentication</span></span>](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a><span data-ttu-id="24dcb-192">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="24dcb-192">Basic authentication</span></span>

<span data-ttu-id="24dcb-193">L’objet d’authentification suivant est obligatoire pour l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="24dcb-193">The following authentication object is needed for basic authentication.</span></span>
<span data-ttu-id="24dcb-194">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="24dcb-194">A * means that it is a required field.</span></span>

| <span data-ttu-id="24dcb-195">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="24dcb-195">Property name</span></span> | <span data-ttu-id="24dcb-196">Type de données</span><span class="sxs-lookup"><span data-stu-id="24dcb-196">Data type</span></span> | <span data-ttu-id="24dcb-197">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24dcb-198">Entrez*</span><span class="sxs-lookup"><span data-stu-id="24dcb-198">Type*</span></span> |<span data-ttu-id="24dcb-199">type</span><span class="sxs-lookup"><span data-stu-id="24dcb-199">type</span></span> |<span data-ttu-id="24dcb-200">Type d’authentification (doit être `Basic` dans le cas d’une authentification de base)</span><span class="sxs-lookup"><span data-stu-id="24dcb-200">Type of authentication (must be `Basic` for basic authentication)</span></span> |
| <span data-ttu-id="24dcb-201">Nom d’utilisateur*</span><span class="sxs-lookup"><span data-stu-id="24dcb-201">Username*</span></span> |<span data-ttu-id="24dcb-202">username</span><span class="sxs-lookup"><span data-stu-id="24dcb-202">username</span></span> |<span data-ttu-id="24dcb-203">Nom d’utilisateur utilisé pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="24dcb-203">User name to authenticate</span></span> |
| <span data-ttu-id="24dcb-204">Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="24dcb-204">Password*</span></span> |<span data-ttu-id="24dcb-205">password</span><span class="sxs-lookup"><span data-stu-id="24dcb-205">password</span></span> |<span data-ttu-id="24dcb-206">Mot de passe à authentifier</span><span class="sxs-lookup"><span data-stu-id="24dcb-206">Password to authenticate</span></span> |

> [!TIP]
> <span data-ttu-id="24dcb-207">Si vous souhaitez utiliser un mot de passe qui ne peut pas être récupéré à partir de la définition, utilisez un paramètre `securestring` et la `@parameters()` 
> [fonction de définition de flux de travail](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="24dcb-207">If you want to use a password that cannot be retrieved from the definition, use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="24dcb-208">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="24dcb-208">For example:</span></span>

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a><span data-ttu-id="24dcb-209">Authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="24dcb-209">Client certificate authentication</span></span>

<span data-ttu-id="24dcb-210">L’objet d’authentification suivant est requis pour l’authentification du certificat client.</span><span class="sxs-lookup"><span data-stu-id="24dcb-210">The following authentication object is needed for client certificate authentication.</span></span> <span data-ttu-id="24dcb-211">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="24dcb-211">A * means that it is a required field.</span></span>

| <span data-ttu-id="24dcb-212">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="24dcb-212">Property name</span></span> | <span data-ttu-id="24dcb-213">Type de données</span><span class="sxs-lookup"><span data-stu-id="24dcb-213">Data type</span></span> | <span data-ttu-id="24dcb-214">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-214">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24dcb-215">Entrez*</span><span class="sxs-lookup"><span data-stu-id="24dcb-215">Type*</span></span> |<span data-ttu-id="24dcb-216">type</span><span class="sxs-lookup"><span data-stu-id="24dcb-216">type</span></span> |<span data-ttu-id="24dcb-217">Type d’authentification (doit être `ClientCertificate` pour les certificats client SSL)</span><span class="sxs-lookup"><span data-stu-id="24dcb-217">The type of authentication (must be `ClientCertificate` for SSL client certificates)</span></span> |
| <span data-ttu-id="24dcb-218">PFX*</span><span class="sxs-lookup"><span data-stu-id="24dcb-218">PFX*</span></span> |<span data-ttu-id="24dcb-219">pfx</span><span class="sxs-lookup"><span data-stu-id="24dcb-219">pfx</span></span> |<span data-ttu-id="24dcb-220">Contenu codé en Base64 du fichier Personal Information Exchange (PFX)</span><span class="sxs-lookup"><span data-stu-id="24dcb-220">The Base64-encoded contents of the Personal Information Exchange (PFX) file</span></span> |
| <span data-ttu-id="24dcb-221">Mot de passe*</span><span class="sxs-lookup"><span data-stu-id="24dcb-221">Password*</span></span> |<span data-ttu-id="24dcb-222">password</span><span class="sxs-lookup"><span data-stu-id="24dcb-222">password</span></span> |<span data-ttu-id="24dcb-223">Mot de passe d’accès au fichier PFX</span><span class="sxs-lookup"><span data-stu-id="24dcb-223">The password to access the PFX file</span></span> |

> [!TIP]
> <span data-ttu-id="24dcb-224">Pour utiliser un paramètre qui ne sera pas lisible dans la définition après l’enregistrement de votre application logique, vous pouvez utiliser un paramètre `securestring` et la `@parameters()` 
> [fonction de définition de flux de travail](http://aka.ms/logicappdocs).</span><span class="sxs-lookup"><span data-stu-id="24dcb-224">To use a parameter that won't be readable in the definition after saving the logic app, you can use a `securestring` parameter and the `@parameters()` 
> [workflow definition function](http://aka.ms/logicappdocs).</span></span>

<span data-ttu-id="24dcb-225">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="24dcb-225">For example:</span></span>

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a><span data-ttu-id="24dcb-226">Authentification OAuth Azure AD</span><span class="sxs-lookup"><span data-stu-id="24dcb-226">Azure AD OAuth authentication</span></span>
<span data-ttu-id="24dcb-227">L’objet d’authentification suivant est obligatoire pour l’authentification OAuth Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24dcb-227">The following authentication object is needed for Azure AD OAuth authentication.</span></span> <span data-ttu-id="24dcb-228">Le symbole * désigne est un champ obligatoire.</span><span class="sxs-lookup"><span data-stu-id="24dcb-228">A * means that it is a required field.</span></span>

| <span data-ttu-id="24dcb-229">Nom de la propriété</span><span class="sxs-lookup"><span data-stu-id="24dcb-229">Property name</span></span> | <span data-ttu-id="24dcb-230">Type de données</span><span class="sxs-lookup"><span data-stu-id="24dcb-230">Data type</span></span> | <span data-ttu-id="24dcb-231">Description</span><span class="sxs-lookup"><span data-stu-id="24dcb-231">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24dcb-232">Entrez*</span><span class="sxs-lookup"><span data-stu-id="24dcb-232">Type*</span></span> |<span data-ttu-id="24dcb-233">type</span><span class="sxs-lookup"><span data-stu-id="24dcb-233">type</span></span> |<span data-ttu-id="24dcb-234">Type d’authentification (doit être `ActiveDirectoryOAuth` dans le cas d’une authentification OAuth Azure AD)</span><span class="sxs-lookup"><span data-stu-id="24dcb-234">The type of authentication (must be `ActiveDirectoryOAuth` for Azure AD OAuth)</span></span> |
| <span data-ttu-id="24dcb-235">Locataire*</span><span class="sxs-lookup"><span data-stu-id="24dcb-235">Tenant*</span></span> |<span data-ttu-id="24dcb-236">locataire</span><span class="sxs-lookup"><span data-stu-id="24dcb-236">tenant</span></span> |<span data-ttu-id="24dcb-237">L’identifiant de locataire pour le locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="24dcb-237">The tenant identifier for the Azure AD tenant</span></span> |
| <span data-ttu-id="24dcb-238">Public ciblé*</span><span class="sxs-lookup"><span data-stu-id="24dcb-238">Audience*</span></span> |<span data-ttu-id="24dcb-239">audience</span><span class="sxs-lookup"><span data-stu-id="24dcb-239">audience</span></span> |<span data-ttu-id="24dcb-240">Ressource pour laquelle vous demandez une autorisation d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="24dcb-240">The resource you are requesting authorization to use.</span></span> <span data-ttu-id="24dcb-241">Par exemple : `https://management.core.windows.net/`</span><span class="sxs-lookup"><span data-stu-id="24dcb-241">For example: `https://management.core.windows.net/`</span></span> |
| <span data-ttu-id="24dcb-242">ID de client*</span><span class="sxs-lookup"><span data-stu-id="24dcb-242">Client ID*</span></span> |<span data-ttu-id="24dcb-243">clientId</span><span class="sxs-lookup"><span data-stu-id="24dcb-243">clientId</span></span> |<span data-ttu-id="24dcb-244">Identifiant client de l’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="24dcb-244">The client identifier for the Azure AD application</span></span> |
| <span data-ttu-id="24dcb-245">Secret*</span><span class="sxs-lookup"><span data-stu-id="24dcb-245">Secret*</span></span> |<span data-ttu-id="24dcb-246">secret</span><span class="sxs-lookup"><span data-stu-id="24dcb-246">secret</span></span> |<span data-ttu-id="24dcb-247">Phrase secrète du client qui demande le jeton</span><span class="sxs-lookup"><span data-stu-id="24dcb-247">The secret of the client that is requesting the token</span></span> |

> [!TIP]
> <span data-ttu-id="24dcb-248">Vous pouvez utiliser un paramètre `securestring` et la [fonction de définition de flux de travail](http://aka.ms/logicappdocs) `@parameters()` pour utiliser un paramètre qui ne sera pas lisible dans la définition après l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="24dcb-248">You can use a `securestring` parameter and the `@parameters()` [workflow definition function](http://aka.ms/logicappdocs) to use a parameter that won't be readable in the definition after saving.</span></span>
> 
> 

<span data-ttu-id="24dcb-249">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="24dcb-249">For example:</span></span>

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a><span data-ttu-id="24dcb-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24dcb-250">Next steps</span></span>
<span data-ttu-id="24dcb-251">Essayez maintenant la plateforme et [créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="24dcb-251">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="24dcb-252">Vous pouvez explorer les autres connecteurs disponibles dans les applications logiques en examinant notre [liste d’API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="24dcb-252">You can explore the other available connectors in Logic Apps by looking at our [APIs list](apis-list.md).</span></span>

