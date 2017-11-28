---
title: aaaHow tooadd operations tooan API de gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooadd opérations tooan API de gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="bc325-103">Comment tooadd opérations tooan API de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="bc325-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="bc325-104">Pour qu'une API puisse être utilisée dans Gestion des API, vous devez ajouter des opérations.</span><span class="sxs-lookup"><span data-stu-id="bc325-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="bc325-105">Ce guide montre comment tooadd et configurer les différents types d’opérations tooan API de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bc325-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="bc325-106"><a name="add-operation"></a>Ajout d’une opération</span><span class="sxs-lookup"><span data-stu-id="bc325-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="bc325-107">Les opérations sont ajoutées et configurés tooan API dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="bc325-108">tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="bc325-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="bc325-110">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bc325-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="bc325-111">Sélectionnez hello souhaité API dans le portail de publication hello et puis sélectionnez hello **Operations** onglet.</span><span class="sxs-lookup"><span data-stu-id="bc325-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![Opérations][api-management-operations]

<span data-ttu-id="bc325-113">Cliquez sur **ajouter une opération** tooadd une nouvelle opération.</span><span class="sxs-lookup"><span data-stu-id="bc325-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="bc325-114">Hello **nouvelle opération** s’affichera et hello **Signature** est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="bc325-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Ajouter une opération][api-management-add-operation]

<span data-ttu-id="bc325-116">Spécifiez hello **verbe HTTP** en choisissant dans la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![HTTP method][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="bc325-118">Définir le modèle d’URL hello en tapant dans un fragment d’URL consistant en un ou plusieurs segments de chemin d’accès d’URL et zéro ou plusieurs paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="bc325-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="bc325-119">modèle d’URL Hello, URL de base toohello ajouté de hello API, identifie une seule opération HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc325-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="bc325-120">Il peut contenir une ou plusieurs parties variables identifiées par des accolades.</span><span class="sxs-lookup"><span data-stu-id="bc325-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="bc325-121">Ces parties variables sont appelées des paramètres de modèle et sont affectés dynamiquement les valeurs extraites à partir de l’URL de la demande hello lors de la demande de hello est traitée par la plateforme de gestion des API hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="bc325-122">modèle d’URL Hello peut inclure des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="bc325-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="bc325-123">Par exemple, la spécification `/*` par progression toutes les demandes de nouveau ce toohello de méthode HTTP ne pourront service.</span><span class="sxs-lookup"><span data-stu-id="bc325-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="bc325-125">Si vous le souhaitez, spécifier hello **modèle de réécrire les URL**.</span><span class="sxs-lookup"><span data-stu-id="bc325-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="bc325-126">Cela vous permet de modèle d’URL standard toouse hello pour le traitement des demandes entrantes sur hello frontal, lors de l’appel hello principal via une URL convertie selon toohello Réécrivez le modèle.</span><span class="sxs-lookup"><span data-stu-id="bc325-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="bc325-127">Paramètres de modèle à partir du modèle d’URL hello doivent être utilisés dans le modèle de réécriture hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="bc325-128">Hello suivant montre comment le contenu type encodé comme segment de chemin d’accès dans le service web pour hello hello précédent exemple peut être fourni comme paramètre de requête Bonjour API publiés via hello plateforme de gestion des API à l’aide de modèles d’URL hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![URL template rewrite][api-management-url-template-rewrite]

<span data-ttu-id="bc325-130">Opération de toohello appelants utilisent hello format `/customers?customerid=ALFKI` et il sera mappé trop`/Customers('ALFKI')` lorsque le service principal de hello est appelé.</span><span class="sxs-lookup"><span data-stu-id="bc325-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="bc325-131">**Affichage** nom et **Description** fournissent une description de l’opération de hello et est utilisés tooprovide documentation toohello les développeurs utilisant cette API dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Description][api-management-description]

<span data-ttu-id="bc325-133">description de l’opération Hello peut être spécifiée en tant que texte brut ou HTML Bonjour **Description** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bc325-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="bc325-134"><a name="operation-caching"></a>Mise en cache de l’opération</span><span class="sxs-lookup"><span data-stu-id="bc325-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="bc325-135">Réponse mise en cache réduit la latence perçue par les consommateurs hello API, permet de réduire la consommation de bande passante et la charge de hello diminue sur l’implémentation du service web hello HTTP hello API.</span><span class="sxs-lookup"><span data-stu-id="bc325-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="bc325-136">tooeasily et d’activer rapidement la mise en cache pour l’opération de hello, sélectionnez hello **mise en cache** et vérifiez hello **activer** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="bc325-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Mise en cache][api-management-caching-tab]

<span data-ttu-id="bc325-138">**Durée** spécifie hello laps de temps pendant le hello réponse d’opération reste dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="bc325-139">Hello par défaut est 3 600 secondes ou 1 heure.</span><span class="sxs-lookup"><span data-stu-id="bc325-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="bc325-140">Les clés de cache sont toodifferentiate utilisé entre les réponses afin que la réponse hello correspondant de clé de cache différents tooeach obtiendra sa propre valeur de mise en cache distinct.</span><span class="sxs-lookup"><span data-stu-id="bc325-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="bc325-141">Si vous le souhaitez, entrez les paramètres de chaîne de requête spécifique et/ou toobe d’en-têtes HTTP utilisés dans le calcul de valeurs de clé de cache Bonjour **variation par paramètres de chaîne de requête** et **variation par en-têtes** respectivement des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="bc325-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="bc325-142">Lorsque aucun sont des URL de demande spécifié, complète et hello valeurs d’en-tête HTTP suivantes est utilisée dans la génération de clé de cache : **accepter** et **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="bc325-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="bc325-143">Pour plus d’informations sur la mise en cache et la mise en cache des stratégies, consultez [affichage des résultats dans la gestion des API Azure toocache opération][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="bc325-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="bc325-144"><a name="request-parameters"></a>Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="bc325-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="bc325-145">Paramètres de l’opération sont gérés sur l’onglet Paramètres de hello. Paramètres spécifiés dans hello **modèle d’URL** sur hello **Signature** onglet sont ajoutés automatiquement et peut être modifiée qu’en modifiant le modèle d’URL hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="bc325-146">D'autres paramètres peuvent être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="bc325-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="bc325-147">tooadd un nouveau paramètre de requête, cliquez sur **ajouter un paramètre de requête** et entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bc325-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="bc325-148">**Nom** : nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="bc325-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="bc325-149">**Description** -une brève description du paramètre hello (facultatif).</span><span class="sxs-lookup"><span data-stu-id="bc325-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="bc325-150">**Type** -type de paramètre, sélectionné dans la liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="bc325-151">**Valeurs** -valeurs pouvant être affectées toothis paramètre.</span><span class="sxs-lookup"><span data-stu-id="bc325-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="bc325-152">Une des valeurs de hello peut être marquée comme valeur par défaut (facultative).</span><span class="sxs-lookup"><span data-stu-id="bc325-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="bc325-153">**Requis** -que le paramètre hello obligatoire en activant la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![Paramètres de la demande][api-management-request-parameters]

## <span data-ttu-id="bc325-155"><a name="request-body"></a>Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="bc325-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="bc325-156">Si l’opération de hello permet (par exemple, PUT, POST) et nécessite un corps, vous pouvez fournir un exemple de celui-ci dans toutes les hello pris en charge les formats de représentation (par exemple, au format json, XML).</span><span class="sxs-lookup"><span data-stu-id="bc325-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="bc325-157">corps de la demande Hello est utilisé uniquement à des fins de documentation et n’est pas validé.</span><span class="sxs-lookup"><span data-stu-id="bc325-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="bc325-158">tooenter un corps de demande, basculez toohello **corps** onglet.</span><span class="sxs-lookup"><span data-stu-id="bc325-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="bc325-159">Cliquez sur **ajouter la représentation sous forme**, commencez à taper le nom du type de contenu de votre choix (par exemple, application/json), sélectionnez-le dans la liste déroulante de hello et coller hello souhaité d’exemple de corps de demande dans le format sélectionné de hello dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![Corps de la demande][api-management-request-body]

<span data-ttu-id="bc325-161">Dans toorepresentations supplémentaires, vous pouvez également spécifier une description facultative dans hello **Description** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bc325-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="bc325-162"><a name="responses"></a>Réponses</span><span class="sxs-lookup"><span data-stu-id="bc325-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="bc325-163">Il s’agit d’une bonne pratique tooprovide obtenir des exemples de réponses pour tous les codes d’état hello opération risque de générer.</span><span class="sxs-lookup"><span data-stu-id="bc325-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="bc325-164">Chaque code d’état peut avoir plus d’un exemple de corps de réponse, une pour chaque hello pris en charge les types de contenu.</span><span class="sxs-lookup"><span data-stu-id="bc325-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="bc325-165">tooadd une réponse, cliquez sur **ajouter** et commencez à taper le code d’état hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="bc325-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="bc325-166">Dans cet exemple hello d’état est code **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="bc325-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="bc325-167">Une fois que le code de hello s’affiche dans hello de liste déroulante, sélectionnez-la et code de réponse hello est créé et ajouté tooyour opération.</span><span class="sxs-lookup"><span data-stu-id="bc325-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Response code][api-management-response-code]

<span data-ttu-id="bc325-169">Cliquez sur **ajouter la représentation sous forme**, commencez à taper le nom de type de contenu souhaité hello (par exemple, application/json) et sélectionnez dans hello déroulante.</span><span class="sxs-lookup"><span data-stu-id="bc325-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Body content type][api-management-response-body-content-type]

<span data-ttu-id="bc325-171">Collez l’exemple de corps de réponse hello dans le format sélectionné de hello dans la zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="bc325-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Response body][api-management-response-body]

<span data-ttu-id="bc325-173">Si vous le souhaitez, ajoutez une description facultative dans hello **Description** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bc325-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="bc325-174">Une fois l’opération de hello est configurée, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bc325-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="bc325-175"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc325-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="bc325-176">Une fois les opérations de hello ajoutées tooan API, étape suivante de hello est tooassociate hello API avec un produit et la publier afin que les développeurs peuvent appeler ses opérations.</span><span class="sxs-lookup"><span data-stu-id="bc325-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="bc325-177">[Comment toocreate et publier un produit][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="bc325-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
