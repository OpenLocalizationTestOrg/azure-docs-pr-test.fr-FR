---
title: "aaaCall, déclencheur, ou imbriquer des flux de travail avec des points de terminaison HTTP - Azure Logic Apps | Documents Microsoft"
description: "Configurer toocall de points de terminaison HTTP, le déclencheur ou imbriquer le flux de travail pour Azure Logic Apps"
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
ms.openlocfilehash: 072a314c3bff75ab7696f86bb063bb7c03c4ae89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="call-trigger-or-nest-workflows-with-http-endpoints-in-logic-apps"></a><span data-ttu-id="c222d-104">Appeler, déclencher ou imbriquer des workflows via des points de terminaison HTTP dans des applications logiques</span><span class="sxs-lookup"><span data-stu-id="c222d-104">Call, trigger, or nest workflows with HTTP endpoints in logic apps</span></span>

<span data-ttu-id="c222d-105">Vous pouvez exposer en mode natif les points de terminaison HTTP synchrones en tant que déclencheurs sur des applications logiques, afin que vous puissiez déclencher ou appeler vos applications logiques via une URL.</span><span class="sxs-lookup"><span data-stu-id="c222d-105">You can natively expose synchronous HTTP endpoints as triggers on logic apps so that you can trigger or call your logic apps through a URL.</span></span> <span data-ttu-id="c222d-106">Vous pouvez également imbriquer des workflows dans vos applications logiques à l’aide d’un modèle de points de terminaison pouvant être appelés.</span><span class="sxs-lookup"><span data-stu-id="c222d-106">You can also nest workflows in your logic apps by using a pattern of callable endpoints.</span></span>

<span data-ttu-id="c222d-107">points de terminaison HTTP toocreate, vous pouvez ajouter ces déclencheurs afin que vos applications logiques peuvent recevoir des demandes entrantes :</span><span class="sxs-lookup"><span data-stu-id="c222d-107">toocreate HTTP endpoints, you can add these triggers so that your logic apps can receive incoming requests:</span></span>

* [<span data-ttu-id="c222d-108">Requête</span><span class="sxs-lookup"><span data-stu-id="c222d-108">Request</span></span>](../connectors/connectors-native-reqres.md)

* [<span data-ttu-id="c222d-109">Déclencheur ApiConnectionWebhook</span><span class="sxs-lookup"><span data-stu-id="c222d-109">API Connection Webhook</span></span>](logic-apps-workflow-actions-triggers.md#api-connection-trigger)

* [<span data-ttu-id="c222d-110">Déclencheur HTTPWebhook</span><span class="sxs-lookup"><span data-stu-id="c222d-110">HTTP Webhook</span></span>](../connectors/connectors-native-webhook.md)

   > [!NOTE]
   > <span data-ttu-id="c222d-111">Bien que nos exemples utilisent hello **demande** déclencheur, vous pouvez utiliser une des hello répertoriés déclencheurs HTTP, et tous les principes de façon identique s’appliquent toohello autres types de déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="c222d-111">Although our examples use hello **Request** trigger, you can use any of hello listed HTTP triggers, and all principles identically apply toohello other trigger types.</span></span>

## <a name="set-up-an-http-endpoint-for-your-logic-app"></a><span data-ttu-id="c222d-112">Configurer un point de terminaison HTTP pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="c222d-112">Set up an HTTP endpoint for your logic app</span></span>

<span data-ttu-id="c222d-113">toocreate un point de terminaison HTTP, ajoutez un déclencheur qui peut recevoir des demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="c222d-113">toocreate an HTTP endpoint, add a trigger that can receive incoming requests.</span></span>

1. <span data-ttu-id="c222d-114">Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="c222d-114">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="c222d-115">Accédez tooyour logique application et ouvrez le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="c222d-115">Go tooyour logic app, and open Logic App Designer.</span></span>

2. <span data-ttu-id="c222d-116">Ajoutez un déclencheur qui permet à votre application logique de recevoir des requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="c222d-116">Add a trigger that lets your logic app receive incoming requests.</span></span> <span data-ttu-id="c222d-117">Par exemple, ajouter hello **demande** application logique de tooyour déclencheur.</span><span class="sxs-lookup"><span data-stu-id="c222d-117">For example, add hello **Request** trigger tooyour logic app.</span></span>

3.  <span data-ttu-id="c222d-118">Sous **demander un schéma JSON corps**, vous pouvez éventuellement entrer un schéma JSON pour la charge utile de la hello (données) que vous attendez hello déclencheur tooreceive.</span><span class="sxs-lookup"><span data-stu-id="c222d-118">Under **Request Body JSON Schema**, you can optionally enter a JSON schema for hello payload (data) that you expect hello trigger tooreceive.</span></span>

    <span data-ttu-id="c222d-119">le Concepteur de Hello utilise ce schéma pour générer des jetons que votre application de la logique peut utiliser tooconsume, parse et passer les données à partir de déclencheur hello via votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="c222d-119">hello designer uses this schema for generating tokens that your logic app can use tooconsume, parse, and pass data from hello trigger through your workflow.</span></span> 
    <span data-ttu-id="c222d-120">Cliquez sur le lien renvoyant à la section [Jetons générés à partir de schémas JSON pour votre application logique](#generated-tokens) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="c222d-120">More about [tokens generated from JSON schemas](#generated-tokens).</span></span>

    <span data-ttu-id="c222d-121">Pour cet exemple, entrez le schéma hello indiqué dans le Concepteur de hello :</span><span class="sxs-lookup"><span data-stu-id="c222d-121">For this example, enter hello schema shown in hello designer:</span></span>

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

    ![Ajouter une action de demande hello][1]

    > [!TIP]
    > 
    > <span data-ttu-id="c222d-123">Vous pouvez générer un schéma pour une charge utile JSON d’exemple à partir d’un outil tel que [jsonschema.net](http://jsonschema.net/), ou Bonjour **demande** déclencheur en choisissant **utilisez exemple charge utile toogenerate de schéma**.</span><span class="sxs-lookup"><span data-stu-id="c222d-123">You can generate a schema for a sample JSON payload from a tool like [jsonschema.net](http://jsonschema.net/), or in hello **Request** trigger by choosing **Use sample payload toogenerate schema**.</span></span> 
    > <span data-ttu-id="c222d-124">Entrez votre exemple de charge utile et choisissez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c222d-124">Enter your sample payload, and choose **Done**.</span></span>

    <span data-ttu-id="c222d-125">Par exemple, cet exemple de charge utile :</span><span class="sxs-lookup"><span data-stu-id="c222d-125">For example, this sample payload:</span></span>

    ```json
    {
       "address": "21 2nd Street, New York, New York"
    }
    ```

    <span data-ttu-id="c222d-126">génère ce schéma :</span><span class="sxs-lookup"><span data-stu-id="c222d-126">generates this schema:</span></span>

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

4.  <span data-ttu-id="c222d-127">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="c222d-127">Save your logic app.</span></span> <span data-ttu-id="c222d-128">Sous **HTTP POST toothis URL**, vous devez maintenant rechercher une URL de rappel généré, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c222d-128">Under **HTTP POST toothis URL**, you should now find a generated callback URL, like this example:</span></span>

    ![URL de rappel générée pour le point de terminaison](./media/logic-apps-http-endpoint/generated-endpoint-url.png)

    <span data-ttu-id="c222d-130">Cette URL contient une clé de Signature d’accès partagé (SAS) dans les paramètres de requête hello qui sont utilisés pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="c222d-130">This URL contains a Shared Access Signature (SAS) key in hello query parameters that are used for authentication.</span></span> 
    <span data-ttu-id="c222d-131">Vous pouvez également obtenir l’URL de point de terminaison HTTP hello à partir de votre présentation de l’application logique Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c222d-131">You can also get hello HTTP endpoint URL from your logic app overview in hello Azure portal.</span></span> <span data-ttu-id="c222d-132">Sous **Historique du déclencheur**, sélectionnez votre déclencheur :</span><span class="sxs-lookup"><span data-stu-id="c222d-132">Under **Trigger History**, select your trigger:</span></span>

    ![Obtenir l’URL de point de terminaison HTTP à partir du portail Azure][2]

    <span data-ttu-id="c222d-134">Ou vous pouvez obtenir les URL de hello par cet appel :</span><span class="sxs-lookup"><span data-stu-id="c222d-134">Or you can get hello URL by making this call:</span></span>

    ```
    POST https://management.azure.com/{logic-app-resourceID}/triggers/{myendpointtrigger}/listCallbackURL?api-version=2016-06-01
    ```

## <a name="change-hello-http-method-for-your-trigger"></a><span data-ttu-id="c222d-135">Modifier la méthode HTTP de hello pour votre déclencheur</span><span class="sxs-lookup"><span data-stu-id="c222d-135">Change hello HTTP method for your trigger</span></span>

<span data-ttu-id="c222d-136">Par défaut, hello **demande** déclencheur attend une demande HTTP POST, mais vous pouvez utiliser une méthode HTTP différente.</span><span class="sxs-lookup"><span data-stu-id="c222d-136">By default, hello **Request** trigger expects an HTTP POST request, but you can use a different HTTP method.</span></span> 

> [!NOTE]
> <span data-ttu-id="c222d-137">Vous pouvez spécifier un seul type de méthode.</span><span class="sxs-lookup"><span data-stu-id="c222d-137">You can specify only one method type.</span></span>

1. <span data-ttu-id="c222d-138">Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="c222d-138">On your **Request** trigger, choose **Show advanced options**.</span></span>

2. <span data-ttu-id="c222d-139">Ouvrez hello **méthode** liste.</span><span class="sxs-lookup"><span data-stu-id="c222d-139">Open hello **Method** list.</span></span> <span data-ttu-id="c222d-140">Dans cet exemple, sélectionnez **GET** pour pouvoir tester ultérieurement l’URL de votre point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="c222d-140">For this example, select **GET** so that you can test your HTTP endpoint's URL later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c222d-141">Vous pouvez sélectionner n’importe quelle autre méthode HTTP, ou spécifier une méthode personnalisée pour votre propre application logique.</span><span class="sxs-lookup"><span data-stu-id="c222d-141">You can select any other HTTP method, or specify a custom method for your own logic app.</span></span>

    ![Changer de méthode HTTP](./media/logic-apps-http-endpoint/change-method.png)

## <a name="accept-parameters-through-your-http-endpoint-url"></a><span data-ttu-id="c222d-143">Accepter les paramètres via votre URL de point de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="c222d-143">Accept parameters through your HTTP endpoint URL</span></span>

<span data-ttu-id="c222d-144">Lorsque vous souhaitez que vos paramètres de tooaccept de URL de point de terminaison HTTP, personnaliser les chemin d’accès relatif de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="c222d-144">When you want your HTTP endpoint URL tooaccept parameters, customize your trigger's relative path.</span></span>

1. <span data-ttu-id="c222d-145">Sur votre déclencheur de **requête**, choisissez **Afficher les options avancées**.</span><span class="sxs-lookup"><span data-stu-id="c222d-145">On your **Request** trigger, choose **Show advanced options**.</span></span> 

2. <span data-ttu-id="c222d-146">Sous **méthode**, spécifiez la méthode hello HTTP que vous souhaitez toouse de votre demande.</span><span class="sxs-lookup"><span data-stu-id="c222d-146">Under **Method**, specify hello HTTP method that you want your request toouse.</span></span> <span data-ttu-id="c222d-147">Dans cet exemple, sélectionnez hello **obtenir** méthode, si vous n’avez pas déjà fait, afin que vous puissiez tester URL du votre point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="c222d-147">For this example, select hello **GET** method, if you haven't already, so that you can test your HTTP endpoint's URL.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c222d-148">Lorsque vous spécifiez un chemin d’accès relatif pour votre déclencheur, vous devez également spécifier explicitement une méthode HTTP pour votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="c222d-148">When you specify a relative path for your trigger, you must also explicitly specify an HTTP method for your trigger.</span></span>

3. <span data-ttu-id="c222d-149">Sous **chemin d’accès relatif**, spécifiez le chemin d’accès relatif de hello pour le paramètre hello que votre URL doit accepter, par exemple, `customers/{customerID}`.</span><span class="sxs-lookup"><span data-stu-id="c222d-149">Under **Relative path**, specify hello relative path for hello parameter that your URL should accept, for example, `customers/{customerID}`.</span></span>

    ![Spécifiez la méthode HTTP de hello et chemin d’accès relatif pour le paramètre](./media/logic-apps-http-endpoint/relativeurl.png)

4. <span data-ttu-id="c222d-151">toouse hello paramètre, ajoutez un **réponse** action tooyour logique application.</span><span class="sxs-lookup"><span data-stu-id="c222d-151">toouse hello parameter, add a **Response** action tooyour logic app.</span></span> <span data-ttu-id="c222d-152">(Sous votre déclencheur, choisissez **Nouvelle étape** > **Ajouter une action** > **Response**)</span><span class="sxs-lookup"><span data-stu-id="c222d-152">(Under your trigger, choose **New step** > **Add an action** > **Response**)</span></span> 

5. <span data-ttu-id="c222d-153">Dans votre réponse **corps**, incluent le jeton hello pour le paramètre hello que vous avez spécifié dans le chemin d’accès relatif de votre déclencheur.</span><span class="sxs-lookup"><span data-stu-id="c222d-153">In your response's **Body**, include hello token for hello parameter that you specified in your trigger's relative path.</span></span>

    <span data-ttu-id="c222d-154">Par exemple, tooreturn `Hello {customerID}`, mettre à jour de votre réponse **corps** avec `Hello {customerID token}`.</span><span class="sxs-lookup"><span data-stu-id="c222d-154">For example, tooreturn `Hello {customerID}`, update your response's **Body** with `Hello {customerID token}`.</span></span> 
    <span data-ttu-id="c222d-155">liste de contenu dynamique Hello doit apparaître et afficher hello `customerID` jeton pour vous tooselect.</span><span class="sxs-lookup"><span data-stu-id="c222d-155">hello dynamic content list should appear and show hello `customerID` token for you tooselect.</span></span>

    ![Ajoutez paramètre tooresponse corps](./media/logic-apps-http-endpoint/relativeurlresponse.png)

    <span data-ttu-id="c222d-157">Votre valeur **Corps** doit ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c222d-157">Your **Body** should look like this example:</span></span>

    ![Corps de la réponse avec le paramètre](./media/logic-apps-http-endpoint/relative-url-with-parameter.png)

6. <span data-ttu-id="c222d-159">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="c222d-159">Save your logic app.</span></span> 

    <span data-ttu-id="c222d-160">Votre URL de point de terminaison HTTP inclut désormais les chemin d’accès relatif hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c222d-160">Your HTTP endpoint URL now includes hello relative path, for example:</span></span> 

    <span data-ttu-id="c222d-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span><span class="sxs-lookup"><span data-stu-id="c222d-161">https&#58;//prod-00.southcentralus.logic.azure.com/workflows/f90cb66c52ea4e9cabe0abf4e197deff/triggers/manual/paths/invoke/customers/{customerID}...</span></span>

7. <span data-ttu-id="c222d-162">tootest votre point de terminaison HTTP, copier- coller hello URL mise à jour dans une autre fenêtre de navigateur, mais remplacent `{customerID}` avec `123456`, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="c222d-162">tootest your HTTP endpoint, copy and paste hello updated URL into another browser window, but replace `{customerID}` with `123456`, and press Enter.</span></span>

    <span data-ttu-id="c222d-163">Votre navigateur doit afficher le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="c222d-163">Your browser should show this text:</span></span> 

    `Hello 123456`

<a name="generated-tokens"></a>
### <a name="tokens-generated-from-json-schemas-for-your-logic-app"></a><span data-ttu-id="c222d-164">Jetons générés à partir de schémas JSON pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="c222d-164">Tokens generated from JSON schemas for your logic app</span></span>

<span data-ttu-id="c222d-165">Lorsque vous fournissez un schéma JSON dans votre **demande** déclencher, hello Concepteur de logique d’application génère des jetons pour les propriétés de ce schéma.</span><span class="sxs-lookup"><span data-stu-id="c222d-165">When you provide a JSON schema in your **Request** trigger, hello Logic App Designer generates tokens for properties in that schema.</span></span> <span data-ttu-id="c222d-166">Vous pouvez ensuite utiliser ces jetons pour transmettre des données au workflow de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="c222d-166">You can then use those tokens for passing data through your logic app workflow.</span></span>

<span data-ttu-id="c222d-167">Pour cet exemple, si vous ajoutez hello `title` et `name` de schéma de propriété tooyour JSON, leurs jetons sont désormais disponible toouse dans les étapes ultérieures de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="c222d-167">For this example, if you add hello `title` and `name` properties tooyour JSON schema, their tokens are now available toouse in later workflow steps.</span></span> 

<span data-ttu-id="c222d-168">Voici le schéma JSON hello complet :</span><span class="sxs-lookup"><span data-stu-id="c222d-168">Here is hello complete JSON schema:</span></span>

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

## <a name="create-nested-workflows-for-logic-apps"></a><span data-ttu-id="c222d-169">Créer des workflows imbriqués pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="c222d-169">Create nested workflows for logic apps</span></span>

<span data-ttu-id="c222d-170">Vous pouvez imbriquer des workflows dans votre application logique en ajoutant d’autres applications logiques qui peuvent recevoir des requêtes.</span><span class="sxs-lookup"><span data-stu-id="c222d-170">You can nest workflows in your logic app by adding other logic apps that can receive requests.</span></span> <span data-ttu-id="c222d-171">tooinclude ces applications logique, ajouter hello **Azure Logic Apps - choisissez un flux de travail Logic Apps** déclencheur tooyour d’action.</span><span class="sxs-lookup"><span data-stu-id="c222d-171">tooinclude these logic apps, add hello **Azure Logic Apps - Choose a Logic Apps workflow** action tooyour trigger.</span></span> <span data-ttu-id="c222d-172">Vous pouvez ensuite choisir entre des applications logiques éligibles.</span><span class="sxs-lookup"><span data-stu-id="c222d-172">You can then select from eligible logic apps.</span></span>

![Ajouter une autre application logique](./media/logic-apps-http-endpoint/choose-logic-apps-workflow.png)

## <a name="call-or-trigger-logic-apps-through-http-endpoints"></a><span data-ttu-id="c222d-174">Appeler ou déclencher des applications logiques via des points de terminaison HTTP</span><span class="sxs-lookup"><span data-stu-id="c222d-174">Call or trigger logic apps through HTTP endpoints</span></span>

<span data-ttu-id="c222d-175">Après avoir créé votre point de terminaison HTTP, vous pouvez déclencher votre application logique via un `POST` méthode toohello une URL complète.</span><span class="sxs-lookup"><span data-stu-id="c222d-175">After you create your HTTP endpoint, you can trigger your logic app through a `POST` method toohello full URL.</span></span> <span data-ttu-id="c222d-176">Les applications logiques ont une prise en charge intégrée pour les points de terminaison à accès direct.</span><span class="sxs-lookup"><span data-stu-id="c222d-176">Logic apps have built-in support for direct-access endpoints.</span></span>

## <a name="reference-content-from-an-incoming-request"></a><span data-ttu-id="c222d-177">Référencer le contenu à partir d’une requête entrante</span><span class="sxs-lookup"><span data-stu-id="c222d-177">Reference content from an incoming request</span></span>

<span data-ttu-id="c222d-178">Si le contenu de hello de type est `application/json`, vous pouvez référencer des propriétés à partir de la demande entrante de hello.</span><span class="sxs-lookup"><span data-stu-id="c222d-178">If hello content's type is `application/json`, you can reference properties from hello incoming request.</span></span> <span data-ttu-id="c222d-179">Sinon, le contenu est traité comme une seule unité binaire que vous pouvez passer tooother API.</span><span class="sxs-lookup"><span data-stu-id="c222d-179">Otherwise, content is treated as a single binary unit that you can pass tooother APIs.</span></span> <span data-ttu-id="c222d-180">tooreference ce contenu à l’intérieur du flux de travail hello, vous devez convertir ce contenu.</span><span class="sxs-lookup"><span data-stu-id="c222d-180">tooreference this content inside hello workflow, you must convert that content.</span></span> <span data-ttu-id="c222d-181">Par exemple, si vous passez `application/xml` contenu, vous pouvez utiliser `@xpath()` pour l’extraction de XPath, ou `@json()` pour la conversion XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c222d-181">For example, if you pass `application/xml` content, you can use `@xpath()` for an XPath extraction, or `@json()` for converting XML tooJSON.</span></span> <span data-ttu-id="c222d-182">Découvrez plus en détail comment [utiliser les types de contenu](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="c222d-182">Learn about [working with content types](../logic-apps/logic-apps-content-type.md).</span></span>

<span data-ttu-id="c222d-183">tooget hello la sortie à partir d’une demande entrante, vous pouvez utiliser hello `@triggerOutputs()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="c222d-183">tooget hello output from an incoming request, you can use hello `@triggerOutputs()` function.</span></span> <span data-ttu-id="c222d-184">sortie de Hello peut ressembler à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="c222d-184">hello output might look like this example:</span></span>

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

<span data-ttu-id="c222d-185">tooaccess hello `body` propriété en particulier, vous pouvez utiliser hello `@triggerBody()` contextuel.</span><span class="sxs-lookup"><span data-stu-id="c222d-185">tooaccess hello `body` property specifically, you can use hello `@triggerBody()` shortcut.</span></span> 

## <a name="respond-toorequests"></a><span data-ttu-id="c222d-186">Répondre toorequests</span><span class="sxs-lookup"><span data-stu-id="c222d-186">Respond toorequests</span></span>

<span data-ttu-id="c222d-187">Vous souhaiterez peut-être toorespond toocertain demandes qui démarre une application logique en retournant du contenu toohello appelant.</span><span class="sxs-lookup"><span data-stu-id="c222d-187">You might want toorespond toocertain requests that start a logic app by returning content toohello caller.</span></span> <span data-ttu-id="c222d-188">code d’état tooconstruct hello, en-tête et corps de réponse, vous pouvez utiliser hello **réponse** action.</span><span class="sxs-lookup"><span data-stu-id="c222d-188">tooconstruct hello status code, header, and body for your response, you can use hello **Response** action.</span></span> <span data-ttu-id="c222d-189">Cette action peut apparaître n’importe où dans votre application logique, pas seulement à la fin de hello de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="c222d-189">This action can appear anywhere in your logic app, not just at hello end of your workflow.</span></span>

> [!NOTE] 
> <span data-ttu-id="c222d-190">Si votre application logique n’inclut pas un **réponse**, point de terminaison hello HTTP répond *immédiatement* avec un **202 accepté** état.</span><span class="sxs-lookup"><span data-stu-id="c222d-190">If your logic app doesn't include a **Response**, hello HTTP endpoint responds *immediately* with a **202 Accepted** status.</span></span> <span data-ttu-id="c222d-191">En outre, pour hello d’origine demande tooget hello réponse, toutes les étapes nécessaires pour la réponse de hello doivent se terminer en hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md) sauf si vous appelez workflow hello comme application logique imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c222d-191">Also, for hello original request tooget hello response, all steps required for hello response must finish within hello [request timeout limit](./logic-apps-limits-and-config.md) unless you call hello workflow as a nested logic app.</span></span> <span data-ttu-id="c222d-192">Si aucune réponse se produit au sein de cette limite, la demande entrante de hello arrive à expiration et reçoit la réponse de hello HTTP **408 délai d’expiration du Client**.</span><span class="sxs-lookup"><span data-stu-id="c222d-192">If no response happens within this limit, hello incoming request times out and receives hello HTTP response **408 Client timeout**.</span></span> <span data-ttu-id="c222d-193">Pour les applications de la logique imbriquées, hello parent logique application continue toowait d’une réponse jusqu'à la fin, quel que soit le temps est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c222d-193">For nested logic apps, hello parent logic app continues toowait for a response until completed, regardless of how much time is required.</span></span>

### <a name="construct-hello-response"></a><span data-ttu-id="c222d-194">Construire la réponse de hello</span><span class="sxs-lookup"><span data-stu-id="c222d-194">Construct hello response</span></span>

<span data-ttu-id="c222d-195">Vous pouvez inclure plusieurs en-têtes et tout type de contenu dans le corps de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="c222d-195">You can include more than one header and any type of content in hello response body.</span></span> <span data-ttu-id="c222d-196">Dans notre exemple de réponse, l’en-tête de hello Spécifie que réponse de hello possède le type de contenu `application/json`.</span><span class="sxs-lookup"><span data-stu-id="c222d-196">In our example response, hello header specifies that hello response has content type `application/json`.</span></span> <span data-ttu-id="c222d-197">et hello corps contient `title` et `name`, basé sur un schéma JSON hello mis à jour pour hello **demande** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="c222d-197">and hello body contains `title` and `name`, based on hello JSON schema updated previously for hello **Request** trigger.</span></span>

![Action HTTP Response][3]

<span data-ttu-id="c222d-199">Les réponses ont ces propriétés :</span><span class="sxs-lookup"><span data-stu-id="c222d-199">Responses have these properties:</span></span>

| <span data-ttu-id="c222d-200">Propriété</span><span class="sxs-lookup"><span data-stu-id="c222d-200">Property</span></span> | <span data-ttu-id="c222d-201">Description</span><span class="sxs-lookup"><span data-stu-id="c222d-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c222d-202">statusCode</span><span class="sxs-lookup"><span data-stu-id="c222d-202">statusCode</span></span> |<span data-ttu-id="c222d-203">Spécifie le code d’état HTTP de hello pour la demande entrante si toohello ne répond.</span><span class="sxs-lookup"><span data-stu-id="c222d-203">Specifies hello HTTP status code for responding toohello incoming request.</span></span> <span data-ttu-id="c222d-204">Ce code peut être tout code d’état valide commençant par 2xx, 4xx ou 5xx.</span><span class="sxs-lookup"><span data-stu-id="c222d-204">This code can be any valid status code that starts with 2xx, 4xx, or 5xx.</span></span> <span data-ttu-id="c222d-205">Cependant, les codes d’état 3xx ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="c222d-205">However, 3xx status codes are not permitted.</span></span> |
| <span data-ttu-id="c222d-206">headers</span><span class="sxs-lookup"><span data-stu-id="c222d-206">headers</span></span> |<span data-ttu-id="c222d-207">Définit un nombre quelconque de tooinclude d’en-têtes dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="c222d-207">Defines any number of headers tooinclude in hello response.</span></span> |
| <span data-ttu-id="c222d-208">body</span><span class="sxs-lookup"><span data-stu-id="c222d-208">body</span></span> |<span data-ttu-id="c222d-209">Indique un objet corps qui peut être une chaîne, un objet JSON ou même du contenu binaire référencé à partir d’une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c222d-209">Specifies a body object that can be a string, a JSON object, or even binary content referenced from a previous step.</span></span> |

<span data-ttu-id="c222d-210">Voici le schéma JSON hello ressemble maintenant pour hello **réponse** action :</span><span class="sxs-lookup"><span data-stu-id="c222d-210">Here's what hello JSON schema looks like now for hello **Response** action:</span></span>

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
> <span data-ttu-id="c222d-211">définition complète JSON tooview hello pour votre application logique, sur hello Concepteur de logique d’application, choisissez **mode Code**.</span><span class="sxs-lookup"><span data-stu-id="c222d-211">tooview hello complete JSON definition for your logic app, on hello Logic App Designer, choose **Code view**.</span></span>

## <a name="q--a"></a><span data-ttu-id="c222d-212">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="c222d-212">Q & A</span></span>

#### <a name="q-what-about-url-security"></a><span data-ttu-id="c222d-213">Q : Qu’en est-il de la sécurité de l’URL ?</span><span class="sxs-lookup"><span data-stu-id="c222d-213">Q: What about URL security?</span></span>

<span data-ttu-id="c222d-214">R : Les URL de rappel de l’application logique sont générées de façon sécurisée par Azure via une signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="c222d-214">A: Azure securely generates logic app callback URLs using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="c222d-215">Cette signature est transmise directement comme paramètre de requête et doit être validée avant que votre application logique puisse être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="c222d-215">This signature passes through as a query parameter and must be validated before your logic app can fire.</span></span> <span data-ttu-id="c222d-216">Azure génère la signature hello à l’aide d’une combinaison unique d’une clé secrète par application logique, le nom de déclencheur hello et opération hello qui est effectuée.</span><span class="sxs-lookup"><span data-stu-id="c222d-216">Azure generates hello signature using a unique combination of a secret key per logic app, hello trigger name, and hello operation that's performed.</span></span> <span data-ttu-id="c222d-217">Par conséquent, sauf si une personne a la clé d’application logique secrète accès toohello, ils ne peut pas générer une signature valide.</span><span class="sxs-lookup"><span data-stu-id="c222d-217">So unless someone has access toohello secret logic app key, they cannot generate a valid signature.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c222d-218">Systèmes sécurisés et de production, il est fortement recommandé par rapport à l’appel de votre application logique directement à partir de navigateur de hello, car :</span><span class="sxs-lookup"><span data-stu-id="c222d-218">For production and secure systems, we strongly recommend against calling your logic app directly from hello browser because:</span></span>
   > 
   > * <span data-ttu-id="c222d-219">clé d’accès partagé Hello s’affiche dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="c222d-219">hello shared access key appears in hello URL.</span></span>
   > * <span data-ttu-id="c222d-220">Vous ne peut pas gérer les stratégies de contenu sécurisées en raison des domaines tooshared entre les clients de l’application logique.</span><span class="sxs-lookup"><span data-stu-id="c222d-220">You can't manage secure content policies due tooshared domains across Logic App customers.</span></span>

#### <a name="q-can-i-configure-http-endpoints-further"></a><span data-ttu-id="c222d-221">Q : Puis-je configurer des points de terminaison HTTP de façon plus poussée ?</span><span class="sxs-lookup"><span data-stu-id="c222d-221">Q: Can I configure HTTP endpoints further?</span></span>

<span data-ttu-id="c222d-222">R : Oui, les points de terminaison HTTP prennent en charge une configuration plus avancée via [**Gestion des API**](../api-management/api-management-key-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="c222d-222">A: Yes, HTTP endpoints support more advanced configuration through [**API Management**](../api-management/api-management-key-concepts.md).</span></span> <span data-ttu-id="c222d-223">Ce service offre également la possibilité de hello pour tooconsistently vous gérez toutes les API, y compris les applications de la logique, paramétrer des noms de domaine personnalisé, utiliser plusieurs méthodes d’authentification et plus d’informations, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c222d-223">This service also offers hello capability for you tooconsistently manage all your APIs, including logic apps, set up custom domain names, use more authentication methods, and more, for example:</span></span>

* [<span data-ttu-id="c222d-224">Méthode de demande de modification hello</span><span class="sxs-lookup"><span data-stu-id="c222d-224">Change hello request method</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#SetRequestMethod)
* [<span data-ttu-id="c222d-225">Modifier les segments d’URL hello de demande de hello</span><span class="sxs-lookup"><span data-stu-id="c222d-225">Change hello URL segments of hello request</span></span>](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#RewriteURL)
* <span data-ttu-id="c222d-226">Configurer vos domaines de la gestion des API Bonjour [portail Azure](https://portal.azure.com/ "portail Azure")</span><span class="sxs-lookup"><span data-stu-id="c222d-226">Set up your API Management domains in hello [Azure portal](https://portal.azure.com/ "Azure portal")</span></span>
* <span data-ttu-id="c222d-227">Configurer toocheck de stratégie pour l’authentification de base</span><span class="sxs-lookup"><span data-stu-id="c222d-227">Set up policy toocheck for Basic authentication</span></span>

#### <a name="q-what-changed-when-hello-schema-migrated-from-hello-december-1-2014-preview"></a><span data-ttu-id="c222d-228">Q : qu’est changé lorsque le schéma de hello migré à partir de la version préliminaire du 1er décembre 2014 hello ?</span><span class="sxs-lookup"><span data-stu-id="c222d-228">Q: What changed when hello schema migrated from hello December 1, 2014 preview?</span></span>

<span data-ttu-id="c222d-229">R : Voici un résumé des modifications apportées :</span><span class="sxs-lookup"><span data-stu-id="c222d-229">A: Here's a summary about these changes:</span></span>

| <span data-ttu-id="c222d-230">Version préliminaire du 1er décembre 2014</span><span class="sxs-lookup"><span data-stu-id="c222d-230">December 1, 2014 preview</span></span> | <span data-ttu-id="c222d-231">1er juin 2016</span><span class="sxs-lookup"><span data-stu-id="c222d-231">June 1, 2016</span></span> |
| --- | --- |
| <span data-ttu-id="c222d-232">Cliquez sur l’application API **Écouteur HTTP**</span><span class="sxs-lookup"><span data-stu-id="c222d-232">Click **HTTP Listener** API App</span></span> |<span data-ttu-id="c222d-233">Cliquez sur **Déclenchement manuel** (aucune application API nécessaire)</span><span class="sxs-lookup"><span data-stu-id="c222d-233">Click **Manual trigger** (no API App required)</span></span> |
| <span data-ttu-id="c222d-234">Paramètre d’écouteur HTTP «*Envoie une réponse automatiquement*»</span><span class="sxs-lookup"><span data-stu-id="c222d-234">HTTP Listener setting "*Sends response automatically*"</span></span> |<span data-ttu-id="c222d-235">Soit inclure un **réponse** action ou pas dans la définition de workflow hello</span><span class="sxs-lookup"><span data-stu-id="c222d-235">Either include a **Response** action or not in hello workflow definition</span></span> |
| <span data-ttu-id="c222d-236">Configurez l’authentification de base ou OAuth</span><span class="sxs-lookup"><span data-stu-id="c222d-236">Configure Basic or OAuth authentication</span></span> |<span data-ttu-id="c222d-237">via la gestion des API</span><span class="sxs-lookup"><span data-stu-id="c222d-237">via API Management</span></span> |
| <span data-ttu-id="c222d-238">Configurer la méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="c222d-238">Configure HTTP method</span></span> |<span data-ttu-id="c222d-239">Sous **Afficher les options avancées**, choisissez une méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="c222d-239">Under **Show advanced options**, choose an HTTP method</span></span> |
| <span data-ttu-id="c222d-240">Configurer le chemin d’accès relatif</span><span class="sxs-lookup"><span data-stu-id="c222d-240">Configure relative path</span></span> |<span data-ttu-id="c222d-241">Sous **Afficher les options avancées**, ajoutez un chemin d’accès relatif</span><span class="sxs-lookup"><span data-stu-id="c222d-241">Under **Show advanced options**, add a relative path</span></span> |
| <span data-ttu-id="c222d-242">Corps d’entrants hello référence via`@triggerOutputs().body.Content`</span><span class="sxs-lookup"><span data-stu-id="c222d-242">Reference hello incoming body through `@triggerOutputs().body.Content`</span></span> |<span data-ttu-id="c222d-243">Référencez via `@triggerOutputs().body`</span><span class="sxs-lookup"><span data-stu-id="c222d-243">Reference through `@triggerOutputs().body`</span></span> |
| <span data-ttu-id="c222d-244">**Envoyer la réponse HTTP** action sur hello écouteur HTTP</span><span class="sxs-lookup"><span data-stu-id="c222d-244">**Send HTTP response** action on hello HTTP Listener</span></span> |<span data-ttu-id="c222d-245">Cliquez sur **répondre tooHTTP demande** (aucune application API n’obligatoire)</span><span class="sxs-lookup"><span data-stu-id="c222d-245">Click **Respond tooHTTP request** (no API App required)</span></span> |

## <a name="get-help"></a><span data-ttu-id="c222d-246">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="c222d-246">Get help</span></span>

<span data-ttu-id="c222d-247">tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="c222d-247">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="c222d-248">toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="c222d-248">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c222d-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c222d-249">Next steps</span></span>

* [<span data-ttu-id="c222d-250">Créer des définitions d’application logique</span><span class="sxs-lookup"><span data-stu-id="c222d-250">Author logic app definitions</span></span>](./logic-apps-author-definitions.md)
* [<span data-ttu-id="c222d-251">Gérer les erreurs et exceptions</span><span class="sxs-lookup"><span data-stu-id="c222d-251">Handle errors and exceptions</span></span>](./logic-apps-exception-handling.md)

[1]: ./media/logic-apps-http-endpoint/manualtrigger.png
[2]: ./media/logic-apps-http-endpoint/manualtriggerurl.png
[3]: ./media/logic-apps-http-endpoint/response.png
