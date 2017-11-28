---
title: "vue d’ensemble des API REST opérations Services aaaMedia | Documents Microsoft"
description: "Vue d’ensemble de l’API REST Media Services"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a><span data-ttu-id="2b920-103">Vue d’ensemble de l’API REST Media Services Operations</span><span class="sxs-lookup"><span data-stu-id="2b920-103">Media Services operations REST API overview</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="2b920-104">Hello **opérations REST de Media Services** API est utilisée pour la création de travaux, ressources, les stratégies d’accès et autres opérations sur des objets dans un compte de Service de support.</span><span class="sxs-lookup"><span data-stu-id="2b920-104">hello **Media Services Operations REST** API is used for creating jobs, assets, access policies, and other operations on objects in a Media Service account.</span></span> <span data-ttu-id="2b920-105">Pour plus d’informations, consultez [Référence de l’API REST Media Services Operations](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="2b920-105">For more information, see [Media Services Operations REST API reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).</span></span>

<span data-ttu-id="2b920-106">Microsoft Azure Media Services est un service qui accepte les demandes HTTP OData et peut répondre dans les formats JSON ou atom+pub détaillés.</span><span class="sxs-lookup"><span data-stu-id="2b920-106">Microsoft Azure Media Services is a service that accepts OData-based HTTP requests and can respond back in verbose JSON or atom+pub.</span></span> <span data-ttu-id="2b920-107">Étant donné que Media Services sont conformes aux règles de conception tooAzure, il existe un ensemble d’en-têtes HTTP obligatoires que chaque client doit utiliser lors de la connexion des Services de tooMedia, ainsi que d’un ensemble d’en-têtes facultatifs qui peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="2b920-107">Because Media Services conforms tooAzure design guidelines, there is a set of required HTTP headers that each client must use when connecting tooMedia Services, as well as a set of optional headers that can be used.</span></span> <span data-ttu-id="2b920-108">Hello sections suivantes décrivent les en-têtes hello et verbes HTTP que vous pouvez utiliser lorsque la création de demandes et recevoir des réponses à partir des Services de support.</span><span class="sxs-lookup"><span data-stu-id="2b920-108">hello following sections describe hello headers and HTTP verbs you can use when creating requests and receiving responses from Media Services.</span></span>

<span data-ttu-id="2b920-109">Cette rubrique donne une vue d’ensemble de la façon v2 REST toouse avec Media Services.</span><span class="sxs-lookup"><span data-stu-id="2b920-109">This topic gives an overview of how toouse REST v2 with Media Services.</span></span>

## <a name="considerations"></a><span data-ttu-id="2b920-110">Considérations</span><span class="sxs-lookup"><span data-stu-id="2b920-110">Considerations</span></span>

<span data-ttu-id="2b920-111">Hello suivant considérations s’appliquent lors de l’utilisation de REST.</span><span class="sxs-lookup"><span data-stu-id="2b920-111">hello following considerations apply when using REST.</span></span>

* <span data-ttu-id="2b920-112">Lors de l’interrogation des entités, il existe une limite de 1000 entités retournées à la fois, car il est public reste v2 limite les résultats de too1000 de résultats de requête.</span><span class="sxs-lookup"><span data-stu-id="2b920-112">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="2b920-113">Vous devez toouse **ignorer** et **prendre** (.NET) / **haut** (REST), comme décrit dans [cet exemple .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) et [cette API REST exemple](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities).</span><span class="sxs-lookup"><span data-stu-id="2b920-113">You need toouse **Skip** and **Take** (.NET)/ **top** (REST) as described in [this .NET example](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) and [this REST API example](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities).</span></span> 
* <span data-ttu-id="2b920-114">Lors de l’utilisation de JSON et en spécifiant toouse hello **__metadata** mot clé dans la demande de hello (par exemple, un objet lié tooreferences) vous devez définir hello **accepter** en-tête trop[format JSON détaillé ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (voir hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="2b920-114">When using JSON and specifying toouse hello **__metadata** keyword in hello request (for example, tooreferences a linked object) you MUST set hello **Accept** header too[JSON Verbose format](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (see hello following example).</span></span> <span data-ttu-id="2b920-115">OData ne comprend pas hello **__metadata** propriété Bonjour demander, sauf si vous lui affectez tooverbose.</span><span class="sxs-lookup"><span data-stu-id="2b920-115">Odata does not understand hello **__metadata** property in hello request, unless you set it tooverbose.</span></span>  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a><span data-ttu-id="2b920-116">En-têtes de requête HTTP standard pris en charge par Media Services</span><span class="sxs-lookup"><span data-stu-id="2b920-116">Standard HTTP request headers supported by Media Services</span></span>
<span data-ttu-id="2b920-117">Pour chaque appel que vous apportez dans Media Services, il existe un ensemble d’en-têtes obligatoires, vous devez inclure dans votre demande et un ensemble d’en-têtes facultatifs vous pouvez également tooinclude.</span><span class="sxs-lookup"><span data-stu-id="2b920-117">For every call you make into Media Services, there is a set of required headers you must include in your request and also a set of optional headers you may want tooinclude.</span></span> <span data-ttu-id="2b920-118">Hello suivant table listes hello requis en-têtes :</span><span class="sxs-lookup"><span data-stu-id="2b920-118">hello following table lists hello required headers:</span></span>

| <span data-ttu-id="2b920-119">En-tête</span><span class="sxs-lookup"><span data-stu-id="2b920-119">Header</span></span> | <span data-ttu-id="2b920-120">Type</span><span class="sxs-lookup"><span data-stu-id="2b920-120">Type</span></span> | <span data-ttu-id="2b920-121">Valeur</span><span class="sxs-lookup"><span data-stu-id="2b920-121">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b920-122">Autorisation</span><span class="sxs-lookup"><span data-stu-id="2b920-122">Authorization</span></span> |<span data-ttu-id="2b920-123">Support</span><span class="sxs-lookup"><span data-stu-id="2b920-123">Bearer</span></span> |<span data-ttu-id="2b920-124">Le support est hello acceptées uniquement le mécanisme d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="2b920-124">Bearer is hello only accepted authorization mechanism.</span></span> <span data-ttu-id="2b920-125">valeur de Hello doit également inclure hello accès jeton fourni par ACS.</span><span class="sxs-lookup"><span data-stu-id="2b920-125">hello value must also include hello access token provided by ACS.</span></span> |
| <span data-ttu-id="2b920-126">x-ms-version</span><span class="sxs-lookup"><span data-stu-id="2b920-126">x-ms-version</span></span> |<span data-ttu-id="2b920-127">Décimal</span><span class="sxs-lookup"><span data-stu-id="2b920-127">Decimal</span></span> |<span data-ttu-id="2b920-128">2.11</span><span class="sxs-lookup"><span data-stu-id="2b920-128">2.11</span></span> |
| <span data-ttu-id="2b920-129">DataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="2b920-129">DataServiceVersion</span></span> |<span data-ttu-id="2b920-130">Décimal</span><span class="sxs-lookup"><span data-stu-id="2b920-130">Decimal</span></span> |<span data-ttu-id="2b920-131">3.0</span><span class="sxs-lookup"><span data-stu-id="2b920-131">3.0</span></span> |
| <span data-ttu-id="2b920-132">MaxDataServiceVersion</span><span class="sxs-lookup"><span data-stu-id="2b920-132">MaxDataServiceVersion</span></span> |<span data-ttu-id="2b920-133">Décimal</span><span class="sxs-lookup"><span data-stu-id="2b920-133">Decimal</span></span> |<span data-ttu-id="2b920-134">3.0</span><span class="sxs-lookup"><span data-stu-id="2b920-134">3.0</span></span> |

> [!NOTE]
> <span data-ttu-id="2b920-135">Étant donné que Media Services utilise OData tooexpose son référentiel de métadonnées asset sous-jacent via les API REST, hello DataServiceVersion et MaxDataServiceVersion en-têtes doit être inclus dans une demande ; Toutefois, si elles ne sont pas, puis Media Services suppose valeur DataServiceVersion de hello à utiliser est 3.0.</span><span class="sxs-lookup"><span data-stu-id="2b920-135">Because Media Services uses OData tooexpose its underlying asset metadata repository through REST APIs, hello DataServiceVersion and MaxDataServiceVersion headers should be included in any request; however, if they are not, then currently Media Services assumes hello DataServiceVersion value in use is 3.0.</span></span>
> 
> 

<span data-ttu-id="2b920-136">Hello Voici un ensemble d’en-têtes facultatifs :</span><span class="sxs-lookup"><span data-stu-id="2b920-136">hello following is a set of optional headers:</span></span>

| <span data-ttu-id="2b920-137">En-tête</span><span class="sxs-lookup"><span data-stu-id="2b920-137">Header</span></span> | <span data-ttu-id="2b920-138">Type</span><span class="sxs-lookup"><span data-stu-id="2b920-138">Type</span></span> | <span data-ttu-id="2b920-139">Valeur</span><span class="sxs-lookup"><span data-stu-id="2b920-139">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b920-140">Date</span><span class="sxs-lookup"><span data-stu-id="2b920-140">Date</span></span> |<span data-ttu-id="2b920-141">Date RFC 1123</span><span class="sxs-lookup"><span data-stu-id="2b920-141">RFC 1123 date</span></span> |<span data-ttu-id="2b920-142">Horodatage de la demande de hello</span><span class="sxs-lookup"><span data-stu-id="2b920-142">Timestamp of hello request</span></span> |
| <span data-ttu-id="2b920-143">Acceptation</span><span class="sxs-lookup"><span data-stu-id="2b920-143">Accept</span></span> |<span data-ttu-id="2b920-144">Type de contenu</span><span class="sxs-lookup"><span data-stu-id="2b920-144">Content type</span></span> |<span data-ttu-id="2b920-145">Hello demandé le type de contenu de réponse hello tels que les suivants hello :</span><span class="sxs-lookup"><span data-stu-id="2b920-145">hello requested content type for hello response such as hello following:</span></span><p> <span data-ttu-id="2b920-146">-application/json;odata=verbose</span><span class="sxs-lookup"><span data-stu-id="2b920-146">-application/json;odata=verbose</span></span><p> <span data-ttu-id="2b920-147">- application/atom+xml</span><span class="sxs-lookup"><span data-stu-id="2b920-147">- application/atom+xml</span></span><p> <span data-ttu-id="2b920-148">Les réponses peuvent avoir un type de contenu différents, comme une extraction d’objets blob, où une réponse correcte contient le flux d’objets blob hello comme charge utile de hello.</span><span class="sxs-lookup"><span data-stu-id="2b920-148">Responses may have a different content type, such as a blob fetch, where a successful response will contain hello blob stream as hello payload.</span></span> |
| <span data-ttu-id="2b920-149">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="2b920-149">Accept-Encoding</span></span> |<span data-ttu-id="2b920-150">Gzip, deflate</span><span class="sxs-lookup"><span data-stu-id="2b920-150">Gzip, deflate</span></span> |<span data-ttu-id="2b920-151">Codage GZIP et DEFLATE, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="2b920-151">GZIP and DEFLATE encoding, when applicable.</span></span> <span data-ttu-id="2b920-152">Remarque : pour les ressources volumineuses, Media Services peut ignorer cet en-tête et retourner des données non compressées.</span><span class="sxs-lookup"><span data-stu-id="2b920-152">Note: For large resources, Media Services may ignore this header and return noncompressed data.</span></span> |
| <span data-ttu-id="2b920-153">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="2b920-153">Accept-Language</span></span> |<span data-ttu-id="2b920-154">« en », « es » et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2b920-154">"en", "es", and so on.</span></span> |<span data-ttu-id="2b920-155">Spécifie la langue de hello préféré pour la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="2b920-155">Specifies hello preferred language for hello response.</span></span> |
| <span data-ttu-id="2b920-156">Accept-Charset</span><span class="sxs-lookup"><span data-stu-id="2b920-156">Accept-Charset</span></span> |<span data-ttu-id="2b920-157">Type de jeu de caractères comme « UTF-8 »</span><span class="sxs-lookup"><span data-stu-id="2b920-157">Charset type like “UTF-8”</span></span> |<span data-ttu-id="2b920-158">La valeur par défaut est UTF-8.</span><span class="sxs-lookup"><span data-stu-id="2b920-158">Default is UTF-8.</span></span> |
| <span data-ttu-id="2b920-159">X-HTTP-Method</span><span class="sxs-lookup"><span data-stu-id="2b920-159">X-HTTP-Method</span></span> |<span data-ttu-id="2b920-160">Méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="2b920-160">HTTP Method</span></span> |<span data-ttu-id="2b920-161">Permet aux clients ou un pare-feu qui ne prennent pas en charge les méthodes HTTP telles que PUT ou DELETE toouse ces méthodes, tunnel établis via un appel GET.</span><span class="sxs-lookup"><span data-stu-id="2b920-161">Allows clients or firewalls that do not support HTTP methods like PUT or DELETE toouse these methods, tunneled via a GET call.</span></span> |
| <span data-ttu-id="2b920-162">Content-Type</span><span class="sxs-lookup"><span data-stu-id="2b920-162">Content-Type</span></span> |<span data-ttu-id="2b920-163">Type de contenu</span><span class="sxs-lookup"><span data-stu-id="2b920-163">Content type</span></span> |<span data-ttu-id="2b920-164">Contenu de type hello du corps de demande dans les demandes PUT ou POST.</span><span class="sxs-lookup"><span data-stu-id="2b920-164">Content type of hello request body in PUT or POST requests.</span></span> |
| <span data-ttu-id="2b920-165">client-request-id</span><span class="sxs-lookup"><span data-stu-id="2b920-165">client-request-id</span></span> |<span data-ttu-id="2b920-166">String</span><span class="sxs-lookup"><span data-stu-id="2b920-166">String</span></span> |<span data-ttu-id="2b920-167">Une valeur défini par l’appelant qui identifie hello donnée de demande.</span><span class="sxs-lookup"><span data-stu-id="2b920-167">A caller-defined value that identifies hello given request.</span></span> <span data-ttu-id="2b920-168">Si spécifié, cette valeur sera incluse dans le message de réponse hello en tant que moyen toomap hello demande.</span><span class="sxs-lookup"><span data-stu-id="2b920-168">If specified, this value will be included in hello response message as a way toomap hello request.</span></span> <p><p><span data-ttu-id="2b920-169">**Important**</span><span class="sxs-lookup"><span data-stu-id="2b920-169">**Important**</span></span><p><span data-ttu-id="2b920-170">Les valeurs doivent être limitées à 2096 b (2k).</span><span class="sxs-lookup"><span data-stu-id="2b920-170">Values should be capped at 2096b (2k).</span></span> |

## <a name="standard-http-response-headers-supported-by-media-services"></a><span data-ttu-id="2b920-171">En-têtes de réponse HTTP standard pris en charge par Media Services</span><span class="sxs-lookup"><span data-stu-id="2b920-171">Standard HTTP response headers supported by Media Services</span></span>
<span data-ttu-id="2b920-172">Hello Voici un ensemble d’en-têtes qui peuvent être retournées tooyou en fonction de la ressource hello demandée et hello action que vous vouliez tooperform.</span><span class="sxs-lookup"><span data-stu-id="2b920-172">hello following is a set of headers that may be returned tooyou depending on hello resource you were requesting and hello action you intended tooperform.</span></span>

| <span data-ttu-id="2b920-173">En-tête</span><span class="sxs-lookup"><span data-stu-id="2b920-173">Header</span></span> | <span data-ttu-id="2b920-174">Type</span><span class="sxs-lookup"><span data-stu-id="2b920-174">Type</span></span> | <span data-ttu-id="2b920-175">Valeur</span><span class="sxs-lookup"><span data-stu-id="2b920-175">Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2b920-176">request-id</span><span class="sxs-lookup"><span data-stu-id="2b920-176">request-id</span></span> |<span data-ttu-id="2b920-177">String</span><span class="sxs-lookup"><span data-stu-id="2b920-177">String</span></span> |<span data-ttu-id="2b920-178">Identificateur unique pour l’opération en cours hello, générés par le service.</span><span class="sxs-lookup"><span data-stu-id="2b920-178">A unique identifier for hello current operation, service generated.</span></span> |
| <span data-ttu-id="2b920-179">client-request-id</span><span class="sxs-lookup"><span data-stu-id="2b920-179">client-request-id</span></span> |<span data-ttu-id="2b920-180">String</span><span class="sxs-lookup"><span data-stu-id="2b920-180">String</span></span> |<span data-ttu-id="2b920-181">Un identificateur spécifié par l’appelant hello dans la demande d’origine hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="2b920-181">An identifier specified by hello caller in hello original request, if present.</span></span> |
| <span data-ttu-id="2b920-182">Date</span><span class="sxs-lookup"><span data-stu-id="2b920-182">Date</span></span> |<span data-ttu-id="2b920-183">Date RFC 1123</span><span class="sxs-lookup"><span data-stu-id="2b920-183">RFC 1123 date</span></span> |<span data-ttu-id="2b920-184">date de Hello cette demande hello a été traitée.</span><span class="sxs-lookup"><span data-stu-id="2b920-184">hello date that hello request was processed.</span></span> |
| <span data-ttu-id="2b920-185">Content-Type</span><span class="sxs-lookup"><span data-stu-id="2b920-185">Content-Type</span></span> |<span data-ttu-id="2b920-186">Varie</span><span class="sxs-lookup"><span data-stu-id="2b920-186">Varies</span></span> |<span data-ttu-id="2b920-187">type de contenu Hello hello du corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="2b920-187">hello content type of hello response body.</span></span> |
| <span data-ttu-id="2b920-188">Content-Encoding</span><span class="sxs-lookup"><span data-stu-id="2b920-188">Content-Encoding</span></span> |<span data-ttu-id="2b920-189">Varie</span><span class="sxs-lookup"><span data-stu-id="2b920-189">Varies</span></span> |<span data-ttu-id="2b920-190">Gzip ou deflate, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="2b920-190">Gzip or deflate, as appropriate.</span></span> |

## <a name="standard-http-verbs-supported-by-media-services"></a><span data-ttu-id="2b920-191">Verbes HTTP standard pris en charge par Media Services</span><span class="sxs-lookup"><span data-stu-id="2b920-191">Standard HTTP verbs supported by Media Services</span></span>
<span data-ttu-id="2b920-192">Hello Voici une liste complète des verbes HTTP qui peuvent être utilisés lors des demandes HTTP :</span><span class="sxs-lookup"><span data-stu-id="2b920-192">hello following is a complete list of HTTP verbs that can be used when making HTTP requests:</span></span>

| <span data-ttu-id="2b920-193">Verbe</span><span class="sxs-lookup"><span data-stu-id="2b920-193">Verb</span></span> | <span data-ttu-id="2b920-194">Description</span><span class="sxs-lookup"><span data-stu-id="2b920-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b920-195">GET</span><span class="sxs-lookup"><span data-stu-id="2b920-195">GET</span></span> |<span data-ttu-id="2b920-196">Retourne hello la valeur actuelle d’un objet.</span><span class="sxs-lookup"><span data-stu-id="2b920-196">Returns hello current value of an object.</span></span> |
| <span data-ttu-id="2b920-197">POST</span><span class="sxs-lookup"><span data-stu-id="2b920-197">POST</span></span> |<span data-ttu-id="2b920-198">Crée un objet basé sur les données hello fournies, ou envoie une commande.</span><span class="sxs-lookup"><span data-stu-id="2b920-198">Creates an object based on hello data provided, or submits a command.</span></span> |
| <span data-ttu-id="2b920-199">PUT</span><span class="sxs-lookup"><span data-stu-id="2b920-199">PUT</span></span> |<span data-ttu-id="2b920-200">Remplace un objet ou crée un objet nommé (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="2b920-200">Replaces an object, or creates a named object (when applicable).</span></span> |
| <span data-ttu-id="2b920-201">SUPPRIMER</span><span class="sxs-lookup"><span data-stu-id="2b920-201">DELETE</span></span> |<span data-ttu-id="2b920-202">Supprime un objet.</span><span class="sxs-lookup"><span data-stu-id="2b920-202">Deletes an object.</span></span> |
| <span data-ttu-id="2b920-203">MERGE</span><span class="sxs-lookup"><span data-stu-id="2b920-203">MERGE</span></span> |<span data-ttu-id="2b920-204">Met à jour un objet existant avec des modifications de propriété nommées.</span><span class="sxs-lookup"><span data-stu-id="2b920-204">Updates an existing object with named property changes.</span></span> |
| <span data-ttu-id="2b920-205">HEAD</span><span class="sxs-lookup"><span data-stu-id="2b920-205">HEAD</span></span> |<span data-ttu-id="2b920-206">Retourne les métadonnées d’un objet d’une réponse GET.</span><span class="sxs-lookup"><span data-stu-id="2b920-206">Returns metadata of an object for a GET response.</span></span> |

## <a name="discover-media-services-model"></a><span data-ttu-id="2b920-207">Découvrir le modèle Media Services</span><span class="sxs-lookup"><span data-stu-id="2b920-207">Discover Media Services model</span></span>
<span data-ttu-id="2b920-208">entités de Media Services toomake plus détectables, opération de hello $metadata peuvent être utilisées.</span><span class="sxs-lookup"><span data-stu-id="2b920-208">toomake Media Services entities more discoverable, hello $metadata operation can be used.</span></span> <span data-ttu-id="2b920-209">Il vous permet de tooretrieve tous les types d’entité valide, les propriétés d’entité, associations, fonctions, actions et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2b920-209">It allows you tooretrieve all valid entity types, entity properties, associations, functions, actions, and so on.</span></span> <span data-ttu-id="2b920-210">Hello suivant montre comment tooconstruct hello URI : https://media.windows.net/API/$ métadonnées.</span><span class="sxs-lookup"><span data-stu-id="2b920-210">hello following example shows how tooconstruct hello URI: https://media.windows.net/API/$metadata.</span></span>

<span data-ttu-id="2b920-211">Vous devez ajouter « ? api-version=2.x « fin toohello Hello URI si vous souhaitez que les métadonnées de hello tooview dans un navigateur, n’incluez pas d’en-tête x-ms-version de hello dans votre demande.</span><span class="sxs-lookup"><span data-stu-id="2b920-211">You should append "?api-version=2.x" toohello end of hello URI if you want tooview hello metadata in a browser, or do not include hello x-ms-version header in your request.</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="2b920-212">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="2b920-212">Connect tooMedia Services</span></span>

<span data-ttu-id="2b920-213">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="2b920-213">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="2b920-214">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="2b920-214">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="2b920-215">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="2b920-215">You must make subsequent calls toohello new URI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b920-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2b920-216">Next steps</span></span>

<span data-ttu-id="2b920-217">tooaccess AMS APIs avec REST, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec REST](media-services-rest-connect-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="2b920-217">tooaccess AMS APIs with REST, see [Use Azure AD authentication tooaccess hello Azure Media Services API with REST](media-services-rest-connect-with-aad.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2b920-218">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="2b920-218">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2b920-219">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2b920-219">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
