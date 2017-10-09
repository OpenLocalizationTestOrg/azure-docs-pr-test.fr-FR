---
title: "Filtres d’aaaCreating avec l’API REST Azure Media Services | Documents Microsoft"
description: "Cette rubrique décrit comment toocreate filtre votre client peut utiliser les toostream des sections spécifiques d’un flux. Media Services crée les manifestes dynamique tooachieve cette diffusion sélective."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f7d23daf-7cd2-49c7-a195-ab902912ab3c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: d0b5af3b193b35f22ac70887963c2f0a06b60bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-rest-api"></a><span data-ttu-id="d7f6d-104">Création de filtres avec l’API REST Media Services Azure</span><span class="sxs-lookup"><span data-stu-id="d7f6d-104">Creating Filters with Azure Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7f6d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d7f6d-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="d7f6d-106">REST</span><span class="sxs-lookup"><span data-stu-id="d7f6d-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="d7f6d-107">À compter de version 2.11, Media Services vous permet toodefine des filtres pour vos ressources.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="d7f6d-108">Ces filtres sont des règles côté serveur qui permettent à vos clients toochoose toodo opérations : lecture uniquement une section d’une vidéo (au lieu de hello vidéo complètes), ou spécifiez uniquement un sous-ensemble de formats audio et vidéo que les appareils de votre client peuvent traiter () au lieu de tous les formats de hello qui sont associés les actifs hello).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="d7f6d-109">Ce filtrage de vos ressources est archivé via **manifeste dynamique**s qui sont créées lors de toostream de demande de votre client une vidéo en fonction de filtres spécifiées.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-109">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="d7f6d-110">Pour plus d’informations connexes toofilters et dynamique de manifeste, consultez [dynamique manifestes de vue d’ensemble](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="d7f6d-111">Cette rubrique montre comment toouse API REST toocreate, mettre à jour et supprimer des filtres.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-111">This topic shows how toouse REST APIs toocreate, update, and delete filters.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="d7f6d-112">Les types utilisés toocreate filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-112">Types used toocreate filters</span></span>
<span data-ttu-id="d7f6d-113">les types suivants Hello sont utilisées lors de la création de filtres :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-113">hello following types are used when creating filters:</span></span>  

* [<span data-ttu-id="d7f6d-114">Filter</span><span class="sxs-lookup"><span data-stu-id="d7f6d-114">Filter</span></span>](https://docs.microsoft.com/rest/api/media/operations/filter)
* [<span data-ttu-id="d7f6d-115">AssetFilter</span><span class="sxs-lookup"><span data-stu-id="d7f6d-115">AssetFilter</span></span>](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* [<span data-ttu-id="d7f6d-116">PresentationTimeRange</span><span class="sxs-lookup"><span data-stu-id="d7f6d-116">PresentationTimeRange</span></span>](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* [<span data-ttu-id="d7f6d-117">FilterTrackSelect et FilterTrackPropertyCondition</span><span class="sxs-lookup"><span data-stu-id="d7f6d-117">FilterTrackSelect and FilterTrackPropertyCondition</span></span>](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

>[!NOTE]

><span data-ttu-id="d7f6d-118">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-118">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="d7f6d-119">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-119">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="d7f6d-120">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="d7f6d-120">Connect tooMedia Services</span></span>

<span data-ttu-id="d7f6d-121">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-121">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="d7f6d-122">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-122">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="d7f6d-123">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-123">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-filters"></a><span data-ttu-id="d7f6d-124">Création de filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-124">Create filters</span></span>
### <a name="create-global-filters"></a><span data-ttu-id="d7f6d-125">Création de filtres globaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-125">Create global Filters</span></span>
<span data-ttu-id="d7f6d-126">toocreate un filtre global, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-126">toocreate a global Filter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="d7f6d-127">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-127">HTTP Request</span></span>
<span data-ttu-id="d7f6d-128">En-têtes de demande</span><span class="sxs-lookup"><span data-stu-id="d7f6d-128">Request Headers</span></span>

    POST https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host:media.windows.net 

<span data-ttu-id="d7f6d-129">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="d7f6d-129">Request body</span></span> 

    {  
       "Name":"GlobalFilter",
       "PresentationTimeRange":{  
          "StartTimestamp":"0",
          "EndTimestamp":"9223372036854775807",
          "PresentationWindowDuration":"12000000000",
          "LiveBackoffDuration":"0",
          "Timescale":"10000000"
       },
       "Tracks":[  
          {  
             "PropertyConditions":
                  [  
                {  
                   "Property":"Type",
                   "Value":"audio",
                   "Operator":"Equal"
                },
                {  
                   "Property":"Bitrate",
                   "Value":"0-2147483647",
                   "Operator":"Equal"
                }
             ]
          }
       ]
    }




#### <a name="http-response"></a><span data-ttu-id="d7f6d-130">Réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-130">HTTP Response</span></span>
    HTTP/1.1 201 Created 

### <a name="create-local-assetfilters"></a><span data-ttu-id="d7f6d-131">Création d'AssetFilters locaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-131">Create local AssetFilters</span></span>
<span data-ttu-id="d7f6d-132">toocreate un AssetFilter local, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-132">toocreate a local AssetFilter, use hello following HTTP requests:</span></span>  

#### <a name="http-request"></a><span data-ttu-id="d7f6d-133">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-133">HTTP Request</span></span>
<span data-ttu-id="d7f6d-134">En-têtes de demande</span><span class="sxs-lookup"><span data-stu-id="d7f6d-134">Request Headers</span></span>

    POST https://media.windows.net/API/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net  

<span data-ttu-id="d7f6d-135">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="d7f6d-135">Request body</span></span> 

    {   
       "Name":"AssetFilter", 
       "ParentAssetId":"nb:cid:UUID:536e555d-1500-80c3-92dc-f1e4fdc6c592", 
       "PresentationTimeRange":{   
          "StartTimestamp":"0", 
          "EndTimestamp":"9223372036854775807", 
          "PresentationWindowDuration":"12000000000", 
          "LiveBackoffDuration":"0", 
          "Timescale":"10000000" 
       }, 
       "Tracks":[   
          {   
             "PropertyConditions": 
                  [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

#### <a name="http-response"></a><span data-ttu-id="d7f6d-136">Réponse HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-136">HTTP Response</span></span>
    HTTP/1.1 201 Created 
    . . . 

## <a name="list-filters"></a><span data-ttu-id="d7f6d-137">Liste des filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-137">List filters</span></span>
### <a name="get-all-global-filters-in-hello-ams-account"></a><span data-ttu-id="d7f6d-138">Obtenir tous les global **filtre**s dans le compte de hello AMS</span><span class="sxs-lookup"><span data-stu-id="d7f6d-138">Get all global **Filter**s in hello AMS account</span></span>
<span data-ttu-id="d7f6d-139">filtres de toolist, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-139">toolist filters, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d7f6d-140">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-140">HTTP Request</span></span>
    GET https://media.windows.net/API/Filters HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

### <a name="get-assetfilters-associated-with-an-asset"></a><span data-ttu-id="d7f6d-141">Obtention des **AssetFilter**s associés à un élément multimédia</span><span class="sxs-lookup"><span data-stu-id="d7f6d-141">Get **AssetFilter**s associated with an asset</span></span>
#### <a name="http-request"></a><span data-ttu-id="d7f6d-142">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-142">HTTP Request</span></span>
    GET https://media.windows.net/API/Assets('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592')/AssetFilters HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

### <a name="get-an-assetfilter-based-on-its-id"></a><span data-ttu-id="d7f6d-143">Obtention d'un **AssetFilter** en fonction de son ID</span><span class="sxs-lookup"><span data-stu-id="d7f6d-143">Get an **AssetFilter** based on its Id</span></span>
#### <a name="http-request"></a><span data-ttu-id="d7f6d-144">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-144">HTTP Request</span></span>
    GET https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000


## <a name="update-filters"></a><span data-ttu-id="d7f6d-145">Mise à jour des filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-145">Update filters</span></span>
<span data-ttu-id="d7f6d-146">Utilisez PATCH, PUT ou fusion tooupdate un filtre avec les nouvelles valeurs de propriété.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-146">Use PATCH, PUT or MERGE tooupdate a filter with new property values.</span></span>  <span data-ttu-id="d7f6d-147">Pour plus d'informations sur ces opérations, consultez [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-147">For more information about these operations, see [PATCH, PUT, MERGE](http://msdn.microsoft.com/library/dd541276.aspx).</span></span>

<span data-ttu-id="d7f6d-148">Si vous mettez à jour un filtre, peut prendre jusqu'à minutes too2 de règles de hello toorefresh de point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-148">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="d7f6d-149">Si le contenu hello a été traitée à l’aide de ce filtre (et mises en cache proxys et CDN caches), mise à jour de ce filtre peut entraîner des échecs de lecteur.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-149">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="d7f6d-150">Il est recommandé de cache de hello tooclear après la mise à jour de filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-150">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="d7f6d-151">Si cette option n'est pas possible, envisagez d'utiliser un filtre différent.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-151">If this option is not possible, consider using a different filter.</span></span>  

### <a name="update-global-filters"></a><span data-ttu-id="d7f6d-152">Mise à jour de filtres globaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-152">Update global Filters</span></span>
<span data-ttu-id="d7f6d-153">tooupdate un filtre global, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-153">tooupdate a global filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d7f6d-154">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-154">HTTP Request</span></span>
<span data-ttu-id="d7f6d-155">En-têtes de requête :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-155">Request headers:</span></span> 

    MERGE https://media.windows.net/API/Filters('filterName') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 
    Content-Length: 384

<span data-ttu-id="d7f6d-156">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-156">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 

### <a name="update-local-assetfilters"></a><span data-ttu-id="d7f6d-157">Mise à jour d’AssetFilters locaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-157">Update local AssetFilters</span></span>
<span data-ttu-id="d7f6d-158">tooupdate un filtre local, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-158">tooupdate a local filter, use hello following HTTP requests:</span></span> 

#### <a name="http-request"></a><span data-ttu-id="d7f6d-159">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-159">HTTP Request</span></span>
<span data-ttu-id="d7f6d-160">En-têtes de requête :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-160">Request headers:</span></span> 

    MERGE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__TestFilter')  HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Content-Type: application/json 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000 
    Host: media.windows.net 

<span data-ttu-id="d7f6d-161">Corps de la requête :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-161">Request body:</span></span> 

    { 
       "Tracks":[   
          {   
             "PropertyConditions": 
             [   
                {   
                   "Property":"Type", 
                   "Value":"audio", 
                   "Operator":"Equal" 
                }, 
                {   
                   "Property":"Bitrate", 
                   "Value":"0-2147483647", 
                   "Operator":"Equal" 
                } 
             ] 
          } 
       ] 
    } 


## <a name="delete-filters"></a><span data-ttu-id="d7f6d-162">Suppression de filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-162">Delete filters</span></span>
### <a name="delete-global-filters"></a><span data-ttu-id="d7f6d-163">Suppression de filtres globaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-163">Delete global Filters</span></span>
<span data-ttu-id="d7f6d-164">toodelete un filtre global, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-164">toodelete a global Filter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="d7f6d-165">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-165">HTTP Request</span></span>
    DELETE https://media.windows.net/api/Filters('GlobalFilter') HTTP/1.1 
    DataServiceVersion:3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 


### <a name="delete-local-assetfilters"></a><span data-ttu-id="d7f6d-166">Suppression d'AssetFilters locaux</span><span class="sxs-lookup"><span data-stu-id="d7f6d-166">Delete local AssetFilters</span></span>
<span data-ttu-id="d7f6d-167">toodelete un AssetFilter local, utilisez hello suivant des requêtes HTTP :</span><span class="sxs-lookup"><span data-stu-id="d7f6d-167">toodelete a local AssetFilter, use hello following HTTP requests:</span></span>

#### <a name="http-request"></a><span data-ttu-id="d7f6d-168">Demande HTTP</span><span class="sxs-lookup"><span data-stu-id="d7f6d-168">HTTP Request</span></span>
    DELETE https://media.windows.net/API/AssetFilters('nb%3Acid%3AUUID%3A536e555d-1500-80c3-92dc-f1e4fdc6c592__%23%23%23__LocalFilter') HTTP/1.1 
    DataServiceVersion: 3.0 
    MaxDataServiceVersion: 3.0 
    Accept: application/json 
    Accept-Charset: UTF-8 
    Authorization: Bearer <token value> 
    x-ms-version: 2.11 
    Host: media.windows.net 

## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="d7f6d-169">Création d'URL de diffusion qui utilisent des filtres</span><span class="sxs-lookup"><span data-stu-id="d7f6d-169">Build streaming URLs that use filters</span></span>
<span data-ttu-id="d7f6d-170">Pour plus d’informations sur comment toopublish et proposer vos éléments multimédias, consultez [tooCustomers de fourniture de contenu vue d’ensemble](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7f6d-170">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="d7f6d-171">Hello exemples suivants montrent comment tooadd filtre tooyour URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="d7f6d-171">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="d7f6d-172">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="d7f6d-172">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="d7f6d-173">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="d7f6d-173">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="d7f6d-174">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="d7f6d-174">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="d7f6d-175">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="d7f6d-175">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)

    
## <a name="media-services-learning-paths"></a><span data-ttu-id="d7f6d-176">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d7f6d-176">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d7f6d-177">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d7f6d-177">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d7f6d-178">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d7f6d-178">See Also</span></span>
[<span data-ttu-id="d7f6d-179">Vue d'ensemble des manifestes dynamiques</span><span class="sxs-lookup"><span data-stu-id="d7f6d-179">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

