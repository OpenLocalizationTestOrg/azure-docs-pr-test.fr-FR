---
title: "Appeler, déclencher ou imbriquer des workflows via des points de terminaison HTTP - Azure Logic Apps | Microsoft Docs"
description: "Configurer des points de terminaison HTTP pour appeler, déclencher ou imbriquer des workflows pour Azure Logic Apps"
services: logic-apps
keywords: workflows, points de terminaison HTTP
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 73ba2a70-03e9-4982-bfc8-ebfaad798bc2
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 03/31/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: c92692db23ac59f67890e26cce6b2d3272e8901d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="4c8a5-104">Appeler, déclencher ou imbriquer des workflows via des points de terminaison HTTP dans des applications logiques</span><span class="sxs-lookup"><span data-stu-id="4c8a5-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="4c8a5-105">Vous pouvez exposer en mode natif les points de terminaison HTTP synchrones en tant que déclencheurs sur des applications logiques, afin que vous puissiez déclencher ou appeler vos applications logiques via une URL.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="4c8a5-106">Vous pouvez également imbriquer des workflows dans vos applications logiques à l’aide d’un modèle de points de terminaison pouvant être appelés.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="4c8a5-107">Pour créer des points de terminaison HTTP, vous pouvez ajouter ces déclencheurs afin que vos applications logiques puissent recevoir des requêtes entrantes :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-107">To create HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="4c8a5-108">Requête</span><span class="sxs-lookup"><span data-stu-id="4c8a5-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="4c8a5-109">Déclencheur ApiConnectionWebhook</span><span class="sxs-lookup"><span data-stu-id="4c8a5-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="4c8a5-110">Déclencheur HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="4c8a5-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="4c8a5-111">Bien que nos exemples utilisent le déclencheur de **requête**, vous pouvez utiliser l’un des déclencheurs HTTP répertoriés, et tous les principes s’appliquent de la même façon aux autres types de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-111">Although our examples use the **Request** trigger, you can use any of the listed HTTP triggers, and all principles identically apply to the other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="4c8a5-112">Configurer un point de terminaison HTTP pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="4c8a5-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="4c8a5-113">Pour créer un point de terminaison HTTP, ajoutez un déclencheur qui peut recevoir des requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-113">To create an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="4c8a5-114">Connectez-vous au [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="4c8a5-114">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="4c8a5-115">Accédez à votre application logique et ouvrez le Concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-115">Go to your logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="4c8a5-116">Ajoutez un déclencheur qui permet à votre application logique de recevoir des requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="4c8a5-117">Par exemple, ajoutez le déclencheur **Requête** à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-117">For example, add the **Request** trigger to your logic app.</span></span>

3.  <span data-ttu-id="4c8a5-118">Sous **Schéma JSON du corps de la requête**, vous pouvez éventuellement entrer un schéma JSON pour la charge utile (données) que le déclencheur est susceptible de recevoir.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for the payload (data) that you expect the trigger to receive.</span></span>

    <span data-ttu-id="4c8a5-119">Le concepteur utilise ce schéma pour générer des jetons que votre application logique peut utiliser pour consommer, analyser et transmettre des données à partir du déclencheur via votre workflow.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-119">The designer uses this schema for generating tokens that your logic app can use to consume, parse, and pass data from the trigger through your workflow.</span></span> 
    <span data-ttu-id="4c8a5-120">Cliquez sur le lien renvoyant à la section [Jetons générés à partir de schémas JSON pour votre application logique](#generated-tokens) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="4c8a5-121">Pour cet exemple, entrez le schéma affiché dans le concepteur :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-121">For this example, enter the schema shown in the designer:</span></span>

    ```json
    {
      "type": "object",
      "properties": {
        "address": {
          "type": "string"
        }
      },
      "required": [
        "address"
      ]
    }
    ```

    ![Ajouter l’action de la requête][1]

    > [!TIP]
    > 
    > <span data-ttu-id="4c8a5-123">Vous pouvez générer un schéma pour un exemple de charge utile JSON à partir d’un outil tel que [jsonschema.net](http://jsonschema.net/), ou dans le déclencheur de **requête** en choisissant **Utiliser l’exemple de charge utile pour générer le schéma**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in the **Request** trigger by choosing **Use sample payload to generate schema**.</span></span> 
    > <span data-ttu-id="4c8a5-124">Entrez votre exemple de charge utile et choisissez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="4c8a5-125">Par exemple, cet exemple de charge utile :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="4c8a5-126">génère ce schéma :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-126">generates this schema:</span></span>

    ```json
    }
       "type": "object",
       "properties": {
          "address": {
             "type": "string" 
          }
       }
    }
    ```

4.  <span data-ttu-id="4c8a5-127">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-127">Save your logic app.</span></span> <span data-ttu-id="4c8a5-128">Sous **POST HTTP pour cette URL**, vous devez maintenant rechercher une URL de rappel générée, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-128">Under **HTTP POST to this URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL de rappel générée pour le point de terminaison](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="4c8a5-130">Cette URL contient une clé de signature d’accès partagé (SAP) dans les paramètres de requête utilisés pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-130">This URL contains a Shared Access Signature (SAS) key in the query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="4c8a5-131">Vous pouvez également obtenir l’URL de point de terminaison HTTP à partir de la vue d’ensemble de votre application logique dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-131">You can also get the HTTP endpoint URL from your logic app overview in the Azure portal.</span></span> <span data-ttu-id="4c8a5-132">Sous **Historique du déclencheur**, sélectionnez votre déclencheur :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obtenir l’URL de point de terminaison HTTP à partir du portail Azure][2]

    <span data-ttu-id="4c8a5-134">Ou vous pouvez obtenir l’URL en appelant :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-134">Or you can get the URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-the-http-method-for-your-trigger"></a><span data-ttu-id="4c8a5-135">Modifier la méthode HTTP pour votre déclencheur</span><span class="sxs-lookup"><span data-stu-id="4c8a5-135">Change the HTTP method for your trigger</span></span>

<span data-ttu-id="4c8a5-136">Par défaut, le déclencheur de **requête** attend une requête HTTP POST, mais vous pouvez utiliser une méthode HTTP différente.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-136">By default, the **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="4c8a5-137">Vous pouvez spécifier un seul type de méthode.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="4c8a5-138">Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="4c8a5-139">Ouvrez la liste **Méthode**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-139">Open the **Method** list.</span></span> <span data-ttu-id="4c8a5-140">Dans cet exemple, sélectionnez **GET** pour pouvoir tester ultérieurement l’URL de votre point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c8a5-141">Vous pouvez sélectionner n’importe quelle autre méthode HTTP, ou spécifier une méthode personnalisée pour votre propre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Changer de méthode HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="4c8a5-143">Accepter les paramètres via votre URL de point de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="4c8a5-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="4c8a5-144">Lorsque vous souhaitez que votre URL de point de terminaison HTTP accepte des paramètres, personnalisez le chemin d’accès relatif de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-144">When you want your HTTP endpoint URL to accept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="4c8a5-145">Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="4c8a5-146">Sous **Méthode**, spécifiez la méthode HTTP que vous souhaitez que votre requête utilise.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-146">Under **Method**, specify the HTTP method that you want your request to use.</span></span> <span data-ttu-id="4c8a5-147">Dans cet exemple, sélectionnez la méthode **GET**, si vous ne l’avez pas déjà fait, pour pouvoir tester l’URL de votre point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-147">For this example, select the **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="4c8a5-148">Lorsque vous spécifiez un chemin d’accès relatif pour votre déclencheur, vous devez également spécifier explicitement une méthode HTTP pour votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="4c8a5-149">Sous **Chemin d’accès relatif**, spécifiez le chemin d’accès relatif du paramètre que votre URL doit accepter, par exemple `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-149">Under **Relative path**, specify the relative path for the parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Spécifier la méthode HTTP et le chemin d’accès relatif pour le paramètre](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="4c8a5-151">Pour utiliser le paramètre, ajoutez une action **Response** à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-151">To use the parameter, add a **Response** action to your logic app.</span></span> <span data-ttu-id="4c8a5-152">(Sous votre déclencheur, choisissez **Nouvelle étape** > **Ajouter une action** > **Response**)</span><span class="sxs-lookup"><span data-stu-id="4c8a5-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="4c8a5-153">Pour la valeur **Corps** de votre réponse, incluez le jeton pour le paramètre que vous avez spécifié dans le chemin d’accès relatif de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-153">In your response's **Body**, include the token for the parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="4c8a5-154">Par exemple, pour renvoyer `Hello {customerID}`, mettez à jour la valeur **Corps** de votre réponse avec `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-154">For example, to return `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="4c8a5-155">La liste de contenu dynamique doit apparaître et afficher le `customerID` jeton pour la sélectionner.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-155">The dynamic content list should appear and show the `customerID` token for you to select.</span></span>

    ![Ajouter un paramètre au corps de la réponse](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="4c8a5-157">Votre valeur **Corps** doit ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-157">Your **Body** should look like this example:</span></span>

    ![Corps de la réponse avec le paramètre](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="4c8a5-159">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-159">Save your logic app.</span></span> 

    <span data-ttu-id="4c8a5-160">Votre URL de point de terminaison HTTP inclut désormais le chemin d’accès relatif, par exemple :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-160">Your HTTP endpoint URL now includes the relative path, for example:</span></span> 

    <span data-ttu-id="4c8a5-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="4c8a5-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="4c8a5-162">Pour tester votre point de terminaison HTTP, copiez et collez l’URL mise à jour dans une autre fenêtre de navigateur, mais remplacez `{customerID}` par `123456`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-162">To test your HTTP endpoint, copy and paste the updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="4c8a5-163">Votre navigateur doit afficher le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="4c8a5-164">Jetons générés à partir de schémas JSON pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="4c8a5-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="4c8a5-165">Lorsque vous fournissez un schéma JSON dans votre déclencheur de **requête**, le Concepteur d’application logique génère des jetons pour les propriétés de ce schéma.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-165">When you provide a JSON schema in your **Request** trigger, the Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="4c8a5-166">Vous pouvez ensuite utiliser ces jetons pour transmettre des données au workflow de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="4c8a5-167">Pour cet exemple, si vous ajoutez les propriétés `title` et `name` à votre schéma JSON, leurs jetons sont désormais disponibles pour être utilisés dans les étapes ultérieures du workflow.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-167">For this example, if you add the `title` and `name` properties to your JSON schema, their tokens are now available to use in later workflow steps.</span></span> 

<span data-ttu-id="4c8a5-168">Voici le schéma JSON complet :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-168">Here is the complete JSON schema:</span></span>

```json
{
   "type": "object",
   "properties": {
      "address": {
         "type": "string"
      },
      "title": {
         "type": "string"
      },
      "name": {
         "type": "string"
      }
   },
   "required": [
      "address",
      "title",
      "name"
   ]
}
```

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="4c8a5-169">Créer des workflows imbriqués pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="4c8a5-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="4c8a5-170">Vous pouvez imbriquer des workflows dans votre application logique en ajoutant d’autres applications logiques qui peuvent recevoir des requêtes.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="4c8a5-171">Pour inclure ces applications logiques, ajoutez l’action **Azure Logic Apps - Choisir un workflow Logic Apps** à votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-171">To include these logic apps, add the **Azure Logic Apps - Choose a Logic Apps workflow** action to your trigger.</span></span> <span data-ttu-id="4c8a5-172">Vous pouvez ensuite choisir entre des applications logiques éligibles.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-172">You can then select from eligible logic apps.</span></span>

![Ajouter une autre application logique](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="4c8a5-174">Appeler ou déclencher des applications logiques via des points de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="4c8a5-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="4c8a5-175">Une fois que vous avez créé votre point de terminaison HTTP, vous pouvez déclencher votre application logique via une méthode `POST` vers l’URL complète.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method to the full URL.</span></span> <span data-ttu-id="4c8a5-176">Les applications logiques ont une prise en charge intégrée pour les points de terminaison à accès direct.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="4c8a5-177">Référencer le contenu à partir d’une requête entrante</span><span class="sxs-lookup"><span data-stu-id="4c8a5-177">Reference content from an incoming request</span></span>

<span data-ttu-id="4c8a5-178">Si le type de contenu est `application/json`, vous pouvez référencer des propriétés à partir de la requête entrante.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-178">If the content's type is `application/json`, you can reference properties from the incoming request.</span></span> <span data-ttu-id="4c8a5-179">Sinon, le contenu est traité comme une seule unité binaire que vous pouvez transmettre à d’autres API.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-179">Otherwise, content is treated as a single binary unit that you can pass to other APIs.</span></span> <span data-ttu-id="4c8a5-180">Pour référencer ce contenu dans le workflow, vous devez le convertir.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-180">To reference this content inside the workflow, you must convert that content.</span></span> <span data-ttu-id="4c8a5-181">Par exemple, si vous transmettez le contenu `application/xml`, vous pouvez utiliser `@xpath()` pour une extraction XPath, ou `@json()` pour effectuer la conversion de XML vers JSON.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML to JSON.</span></span> <span data-ttu-id="4c8a5-182">Découvrez plus en détail comment [utiliser les types de contenu](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="4c8a5-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="4c8a5-183">Pour obtenir la sortie à partir d’une requête entrante, vous pouvez utiliser la fonction `@triggerOutputs()`.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-183">To get the output from an incoming request, you can use the `@triggerOutputs()` function.</span></span> <span data-ttu-id="4c8a5-184">La sortie peut ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-184">The output might look like this example:</span></span>

```json
{
    "headers": {
        "content-type" : "application/json"
    },
    "body": {
        "myProperty" : "property value"
    }
}
```

<span data-ttu-id="4c8a5-185">Pour accéder à la propriété `body`, vous pouvez utiliser le raccourci `@triggerBody()`.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-185">To access the `body` property specifically, you can use the `@triggerBody()` shortcut.</span></span> 

## <a name="respond-to-requests"></a><span data-ttu-id="4c8a5-186">Répondre aux requêtes</span><span class="sxs-lookup"><span data-stu-id="4c8a5-186">Respond to requests</span></span>

<span data-ttu-id="4c8a5-187">Vous souhaitez peut-être répondre à certaines requêtes qui démarrent une application logique en renvoyant du contenu à l’appelant.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-187">You might want to respond to certain requests that start a logic app by returning content to the caller.</span></span> <span data-ttu-id="4c8a5-188">Pour créer le code d’état, l’en-tête et le corps de votre réponse, vous pouvez utiliser l’action **Response**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-188">To construct the status code, header, and body for your response, you can use the **Response** action.</span></span> <span data-ttu-id="4c8a5-189">Cette action peut apparaître n’importe où dans votre application logique, et pas seulement à la fin de votre workflow.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-189">This action can appear anywhere in your logic app, not just at the end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="4c8a5-190">Si votre application logique n’inclut pas d’action **Response**, le point de terminaison HTTP répond *immédiatement* avec un état **202 - Accepté**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-190">If your logic app doesn't include a **Response**, the HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="4c8a5-191">En outre, pour que la requête d’origine obtienne la réponse, toutes les étapes nécessaires pour la réponse doivent être terminées avant la [limite du délai d’expiration de la requête](./logic-apps-limits-and-config.md), sauf si vous appelez le workflow en tant qu’application logique imbriquée.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-191">Also, for the original request to get the response, all steps required for the response must finish within the [request timeout limit](./logic-apps-limits-and-config.md) unless you call the workflow as a nested logic app.</span></span> <span data-ttu-id="4c8a5-192">Si aucune réponse n’est produite avant cette limite, la requête entrante expire et reçoit la réponse HTTP **408 - Dépassement du délai d’expiration par le client**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-192">If no response happens within this limit, the incoming request times out and receives the HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="4c8a5-193">Pour les applications logiques imbriquées, l’application logique parente continue à attendre une réponse jusqu’à ce qu’elle se termine, quelle que soit la durée de l’opération.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-193">For nested logic apps, the parent logic app continues to wait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-the-response"></a><span data-ttu-id="4c8a5-194">Construire la réponse</span><span class="sxs-lookup"><span data-stu-id="4c8a5-194">Construct the response</span></span>

<span data-ttu-id="4c8a5-195">Vous pouvez inclure plusieurs en-têtes et n’importe quel type de contenu dans le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-195">You can include more than one header and any type of content in the response body.</span></span> <span data-ttu-id="4c8a5-196">Dans notre exemple de réponse, l’en-tête spécifie que la réponse a le type de contenu `application/json`.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-196">In our example response, the header specifies that the response has content type `application/json`.</span></span> <span data-ttu-id="4c8a5-197">et que le corps contient `title` et `name`, selon le schéma JSON mis à jour précédemment pour le déclencheur de **requête**.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-197">and the body contains `title` and `name`, based on the JSON schema updated previously for the **Request** trigger.</span></span>

![Action HTTP Response][3]

<span data-ttu-id="4c8a5-199">Les réponses ont ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-199">Responses have these properties:</span></span>

| <span data-ttu-id="4c8a5-200">Propriété</span><span class="sxs-lookup"><span data-stu-id="4c8a5-200">Property</span></span> | <span data-ttu-id="4c8a5-201">Description</span><span class="sxs-lookup"><span data-stu-id="4c8a5-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c8a5-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="4c8a5-202">statusCode</span></span> |<span data-ttu-id="4c8a5-203">Indique le code d’état HTTP pour répondre à la requête entrante.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-203">Specifies the HTTP status code for responding to the incoming request.</span></span> <span data-ttu-id="4c8a5-204">Ce code peut être tout code d’état valide commençant par 2xx, 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="4c8a5-205">Cependant, les codes d’état 3xx ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="4c8a5-206">headers</span><span class="sxs-lookup"><span data-stu-id="4c8a5-206">headers</span></span> |<span data-ttu-id="4c8a5-207">Définit un nombre quelconque d’en-têtes à inclure dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-207">Defines any number of headers to include in the response.</span></span> |
| <span data-ttu-id="4c8a5-208">body</span><span class="sxs-lookup"><span data-stu-id="4c8a5-208">body</span></span> |<span data-ttu-id="4c8a5-209">Indique un objet corps qui peut être une chaîne, un objet JSON ou même du contenu binaire référencé à partir d’une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="4c8a5-210">Voici à quoi ressemble désormais le schéma JSON pour l’action **Response** :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-210">Here's what the JSON schema looks like now for the **Response** action:</span></span>

``` json
"Response": {
   "inputs": {
      "body": {
         "title": "@{triggerBody()?['title']}",
         "name": "@{triggerBody()?['name']}"
      },
      "headers": {
           "content-type": "application/json"
      },
      "statusCode": 200
   },
   "runAfter": {},
   "type": "Response"
}
```

> [!TIP]
> <span data-ttu-id="4c8a5-211">Pour afficher la définition JSON complète de votre application logique, choisissez **mode Code** dans le Concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-211">To view the complete JSON definition for your logic app, on the Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="4c8a5-212">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="4c8a5-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="4c8a5-213">Q : Qu’en est-il de la sécurité de l’URL ?</span><span class="sxs-lookup"><span data-stu-id="4c8a5-213">Q: What about URL security?</span></span>

<span data-ttu-id="4c8a5-214">R : Les URL de rappel de l’application logique sont générées de façon sécurisée par Azure via une signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="4c8a5-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="4c8a5-215">Cette signature est transmise directement comme paramètre de requête et doit être validée avant que votre application logique puisse être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="4c8a5-216">Azure génère cette signature via la combinaison unique d’une clé secrète par application logique, du nom du déclencheur et de l’opération qui est effectuée.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-216">Azure generates the signature using a unique combination of a secret key per logic app, the trigger name, and the operation that's performed.</span></span> <span data-ttu-id="4c8a5-217">Ainsi, à moins que quelqu’un ait accès à la clé secrète de l’application logique, personne ne peut générer de signature valide.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-217">So unless someone has access to the secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4c8a5-218">Pour les systèmes de production et sécurisés, nous vous déconseillons fortement d’appeler votre application logique directement à partir du navigateur, car :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-218">For production and secure systems, we strongly recommend against calling your logic app directly from the browser because:</span></span>
   > 
   > * <span data-ttu-id="4c8a5-219">la clé d’accès partagé s’affiche dans l’URL ;</span><span class="sxs-lookup"><span data-stu-id="4c8a5-219">The shared access key appears in the URL.</span></span>
   > * <span data-ttu-id="4c8a5-220">vous ne pouvez pas gérer de stratégies de contenu sécurisé en raison du partage de domaines entre les clients de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="4c8a5-220">You can't manage secure content policies due to shared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="4c8a5-221">Q : Puis-je configurer des points de terminaison HTTP de façon plus poussée ?</span><span class="sxs-lookup"><span data-stu-id="4c8a5-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="4c8a5-222">R : Oui, les points de terminaison HTTP prennent en charge une configuration plus avancée via [**Gestion des API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="4c8a5-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="4c8a5-223">Ce service vous offre également la possibilité de gérer toutes vos API de façon systématique, y compris les applications logiques, de configurer les noms de domaines personnalisés, d’utiliser plus de méthodes d’authentification et bien plus encore, comme par exemple :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-223">This service also offers the capability for you to consistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="4c8a5-224">Modification de la méthode de la requête</span><span class="sxs-lookup"><span data-stu-id="4c8a5-224">Change the request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="4c8a5-225">Modification des segments d’URL de la requête</span><span class="sxs-lookup"><span data-stu-id="4c8a5-225">Change the URL segments of the request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="4c8a5-226">Configuration de vos domaines Gestion des API dans le [portail Azure](https://portal.azure.com/ "portail Azure")</span><span class="sxs-lookup"><span data-stu-id="4c8a5-226">Set up your API Management domains in the [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="4c8a5-227">Configuration d’une stratégie pour vérifier l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="4c8a5-227">Set up policy to check for Basic authentication</span></span>

#### <a name="q-what-changed-when-the-schema-migrated-from-the-december-1-2014-preview"></a><span data-ttu-id="4c8a5-228">Q : Qu’est-ce qui a changé suite à la migration du schéma depuis la version préliminaire du 1er décembre 2014 ?</span><span class="sxs-lookup"><span data-stu-id="4c8a5-228">Q: What changed when the schema migrated from the December 1, 2014 preview?</span></span>

<span data-ttu-id="4c8a5-229">R : Voici un résumé des modifications apportées :</span><span class="sxs-lookup"><span data-stu-id="4c8a5-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="4c8a5-230">Version préliminaire du 1er décembre 2014</span><span class="sxs-lookup"><span data-stu-id="4c8a5-230">December 1, 2014 preview</span></span> | <span data-ttu-id="4c8a5-231">1er juin 2016</span><span class="sxs-lookup"><span data-stu-id="4c8a5-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="4c8a5-232">Cliquez sur l’application API **Écouteur HTTP**</span><span class="sxs-lookup"><span data-stu-id="4c8a5-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="4c8a5-233">Cliquez sur **Déclenchement manuel** (aucune application API nécessaire)</span><span class="sxs-lookup"><span data-stu-id="4c8a5-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="4c8a5-234">Paramètre d’écouteur HTTP «*Envoie une réponse automatiquement*»</span><span class="sxs-lookup"><span data-stu-id="4c8a5-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="4c8a5-235">Incluez ou non une action **Response** dans la définition du workflow</span><span class="sxs-lookup"><span data-stu-id="4c8a5-235">Either include a **Response** action or not in the workflow definition</span></span> |
| <span data-ttu-id="4c8a5-236">Configurez l’authentification de base ou OAuth</span><span class="sxs-lookup"><span data-stu-id="4c8a5-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="4c8a5-237">via la gestion des API</span><span class="sxs-lookup"><span data-stu-id="4c8a5-237">via API Management</span></span> |
| <span data-ttu-id="4c8a5-238">Configurer la méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="4c8a5-238">Configure HTTP method</span></span> |<span data-ttu-id="4c8a5-239">Sous **Afficher les options avancées**, choisissez une méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="4c8a5-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="4c8a5-240">Configurer le chemin d’accès relatif</span><span class="sxs-lookup"><span data-stu-id="4c8a5-240">Configure relative path</span></span> |<span data-ttu-id="4c8a5-241">Sous **Afficher les options avancées**, ajoutez un chemin d’accès relatif</span><span class="sxs-lookup"><span data-stu-id="4c8a5-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="4c8a5-242">Référencez le corps entrant par le biais de `@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="4c8a5-242">Reference the incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="4c8a5-243">Référencez via `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="4c8a5-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="4c8a5-244">**Envoyer une réponse HTTP** sur l’écouteur HTTP</span><span class="sxs-lookup"><span data-stu-id="4c8a5-244">**Send HTTP response** action on the HTTP Listener</span></span> |<span data-ttu-id="4c8a5-245">Cliquez sur **Répondre à la requête HTTP** (aucune application API nécessaire)</span><span class="sxs-lookup"><span data-stu-id="4c8a5-245">Click **Respond to HTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="4c8a5-246">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="4c8a5-246">Get help</span></span>

<span data-ttu-id="4c8a5-247">Pour poser des questions ou y répondre et voir ce que font les autres utilisateurs d’Azure Logic Apps, visitez le [Forum Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="4c8a5-247">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="4c8a5-248">Afin d’améliorer Azure Logic Apps ainsi que les connecteurs, votez pour des idées ou soumettez-en sur le [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="4c8a5-248">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c8a5-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c8a5-249">Next steps</span></span>

* [<span data-ttu-id="4c8a5-250">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="4c8a5-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="4c8a5-251">Gérer les erreurs et exceptions</span><span class="sxs-lookup"><span data-stu-id="4c8a5-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
