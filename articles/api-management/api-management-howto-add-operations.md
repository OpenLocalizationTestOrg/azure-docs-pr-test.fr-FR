---
title: "Comment ajouter des opérations à une API dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment ajouter des opérations à une API dans Gestion des API Azure."
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
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="4c9ea-103">Ajout d'opérations à une API dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="4c9ea-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="4c9ea-104">Pour qu'une API puisse être utilisée dans Gestion des API, vous devez ajouter des opérations.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="4c9ea-105">Ce guide présente comment ajouter et configurer différents types d'opérations pour une API dans Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="4c9ea-106"><a name="add-operation"> </a>Ajout d’une opération</span><span class="sxs-lookup"><span data-stu-id="4c9ea-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="4c9ea-107">Les opérations sont ajoutées et configurées dans une API sur le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="4c9ea-108">Pour accéder au portail des éditeurs, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portail des éditeurs][api-management-management-console]

> <span data-ttu-id="4c9ea-110">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4c9ea-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4c9ea-111">Sélectionnez l’API souhaitée dans le portail de publication, puis l’onglet **Opérations** .</span><span class="sxs-lookup"><span data-stu-id="4c9ea-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![Opérations][api-management-operations]

<span data-ttu-id="4c9ea-113">Cliquez sur **Ajouter une opération** pour ajouter une nouvelle opération.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="4c9ea-114">**Nouvelle opération** s’affiche et l’onglet **Signature** est sélectionné par défaut.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Ajouter une opération][api-management-add-operation]

<span data-ttu-id="4c9ea-116">Spécifiez le **verbe HTTP** en le choisissant dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![HTTP method][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="4c9ea-118">Définissez le modèle d'URL en tapant un fragment d'URL comprenant un ou plusieurs segments de chemin d'URL et aucun ou plusieurs paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="4c9ea-119">Le modèle d'URL, ajouté à l'URL de base de l'API, identifie de façon unique l'opération HTTP.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="4c9ea-120">Il peut contenir une ou plusieurs parties variables identifiées par des accolades.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="4c9ea-121">Ces parties variables sont appelées paramètres de modèle. Des valeurs leur sont affectées de façon dynamique à partir de l'URL de la demande lorsque la demande est traitée par la plateforme Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="4c9ea-122">Le modèle d’URL peut inclure des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="4c9ea-123">Par exemple, spécifiez `/*` pour transférer toutes les demandes de cette méthode HTTP vers le service principal.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![URL template][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="4c9ea-125">Si vous le souhaitez, spécifiez le **modèle de réécriture de l'URL**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="4c9ea-126">Ceci vous permet d'utiliser le modèle d'URL standard pour traiter les demandes entrantes dans la partie frontale, tout en faisant appel à la partie principale via une URL convertie selon le modèle de réécriture.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="4c9ea-127">Les paramètres du modèle d'URL doivent être utilisés dans le modèle de réécriture.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="4c9ea-128">L'exemple qui suit montre comment un type de contenu codé sous forme de segment de chemin dans le service web de l'exemple précédent peut être utilisé comme paramètre de requête dans l'API publiée via la plateforme Gestion des API à l'aide des modèles d'URL.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![URL template rewrite][api-management-url-template-rewrite]

<span data-ttu-id="4c9ea-130">Les appelants de l’opération utilisent le format `/customers?customerid=ALFKI`, qui est mappé sur `/Customers('ALFKI')` lors de l’appel du service principal.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="4c9ea-131">**Nom d’affichage** et **Description** fournissent une description de l’opération et offrent des informations aux développeurs utilisant cette API dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Description][api-management-description]

<span data-ttu-id="4c9ea-133">La description de l'opération peut être ajoutée en texte brut ou au format HTML dans la zone de texte **Description** .</span><span class="sxs-lookup"><span data-stu-id="4c9ea-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="4c9ea-134"><a name="operation-caching"> </a>Mise en cache de l’opération</span><span class="sxs-lookup"><span data-stu-id="4c9ea-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="4c9ea-135">La mise en cache de la réponse réduit le temps de latence perçu par les consommateurs de l'API, réduit la bande passante consommée et allège la charge sur le service web HTTP qui utilise l'API.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="4c9ea-136">Pour activer facilement et rapidement la mise en cache pour une opération, sélectionnez l’onglet **Mise en cache** et cochez la case **Activer**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Mise en cache][api-management-caching-tab]

<span data-ttu-id="4c9ea-138">**Durée** spécifie la durée pendant laquelle la réponse de l'opération reste dans le cache.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="4c9ea-139">La valeur par défaut est de 3600 secondes (1 heure).</span><span class="sxs-lookup"><span data-stu-id="4c9ea-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="4c9ea-140">Les clés de cache permettent de faire la distinction entre les réponses, afin que la réponse correspondant à chaque clé de cache obtienne sa propre valeur mise en cache.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="4c9ea-141">Vous pouvez également entrer des paramètres de chaîne de requête spécifiques et/ou des en-têtes HTTP à utiliser pour calculer les valeurs de clés de cache dans les zones de texte **Variation par paramètres de chaîne de requête** et **Variation par en-têtes**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="4c9ea-142">Si aucune valeur n’est spécifiée, l’URL complète de la demande et les valeurs d’en-tête HTTP suivantes sont utilisées pour générer la clé de cache : **Accept** et **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="4c9ea-143">Pour plus d’informations sur la mise en cache et les stratégies associée, consultez la page [Mise en cache des résultats d’opérations dans Gestion des API Azure][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4c9ea-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="4c9ea-144"><a name="request-parameters"> </a>Paramètres de la demande</span><span class="sxs-lookup"><span data-stu-id="4c9ea-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="4c9ea-145">Les paramètres de l'opération sont gérés dans l'onglet Paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="4c9ea-146">Les paramètres spécifiés dans **Modèle d’URL**, dans l’onglet **Signature**, sont automatiquement ajoutés et ne peuvent être changés qu’en modifiant le modèle d’URL.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="4c9ea-147">D'autres paramètres peuvent être ajoutés manuellement.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="4c9ea-148">Pour ajouter un nouveau paramètre de requête, cliquez sur **Ajouter des paramètres de requête** et entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c9ea-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="4c9ea-149">**Nom** : nom du paramètre.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="4c9ea-150">**Description** : courte description du paramètre (facultatif).</span><span class="sxs-lookup"><span data-stu-id="4c9ea-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="4c9ea-151">**Type** : type de paramètre, sélectionné dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="4c9ea-152">**Valeurs** : valeurs qui peuvent être affectées à ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="4c9ea-153">Une des valeurs peut être marquée comme valeur par défaut (facultatif).</span><span class="sxs-lookup"><span data-stu-id="4c9ea-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="4c9ea-154">**Obligatoire** : activez la case à cocher pour rendre le paramètre obligatoire.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![Paramètres de la demande][api-management-request-parameters]

## <span data-ttu-id="4c9ea-156"><a name="request-body"> </a>Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="4c9ea-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="4c9ea-157">Si l'opération l'autorise (par exemple PUT, POST) et qu'elle nécessite un corps, vous pouvez fournir un exemple dans un des formats pris en charge (JSON, XML, etc.).</span><span class="sxs-lookup"><span data-stu-id="4c9ea-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="4c9ea-158">Le corps de la demande est utilisé uniquement pour information et n'est pas validé.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="4c9ea-159">Pour entrer le corps de la demande, passez dans l'onglet **Corps** .</span><span class="sxs-lookup"><span data-stu-id="4c9ea-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="4c9ea-160">Cliquez sur **Ajouter une représentation**, tapez le nom du type de contenu (par exemple application/json), sélectionnez-le dans la liste déroulante, puis collez l'exemple souhaité au format sélectionné dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![Corps de la demande][api-management-request-body]

<span data-ttu-id="4c9ea-162">En plus des représentations, vous pouvez également spécifier une description dans la zone de texte **Description** .</span><span class="sxs-lookup"><span data-stu-id="4c9ea-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="4c9ea-163"><a name="responses"> </a>Réponses</span><span class="sxs-lookup"><span data-stu-id="4c9ea-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="4c9ea-164">Il est conseillé de fournir des exemples de réponses pour tous les codes d'état que l'opération peut produire.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="4c9ea-165">Chaque code d'état peut avoir plusieurs exemples de corps de réponse, un pour chacun des types de contenu pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="4c9ea-166">Pour ajouter une réponse, cliquez sur **Ajouter**, puis saisissez le code d’état souhaité.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="4c9ea-167">Dans cet exemple, le code d’état est **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="4c9ea-168">Une fois le code affiché dans la liste déroulante, sélectionnez-le. Le code de réponse est alors créé et ajouté à votre opération.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Response code][api-management-response-code]

<span data-ttu-id="4c9ea-170">Cliquez sur **Ajouter une représentation**, commencez à taper le nom du type de contenu (par exemple application/json), puis sélectionnez-le dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Body content type][api-management-response-body-content-type]

<span data-ttu-id="4c9ea-172">Collez l'exemple de corps de la réponse au format sélectionné dans la zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-172">Paste the response body example in the selected format into the text box.</span></span> 

![Response body][api-management-response-body]

<span data-ttu-id="4c9ea-174">Si vous le souhaitez, vous pouvez spécifier une description dans la zone de texte **Description** .</span><span class="sxs-lookup"><span data-stu-id="4c9ea-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="4c9ea-175">Une fois l'opération configurée, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="4c9ea-176"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c9ea-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="4c9ea-177">Une fois les opérations ajoutées à une API, l'étape suivante est l'association de l'API à un produit et sa publication, afin que les développeurs puissent appeler ses opérations.</span><span class="sxs-lookup"><span data-stu-id="4c9ea-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="4c9ea-178">[Création et publication d’un produit][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="4c9ea-178">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
