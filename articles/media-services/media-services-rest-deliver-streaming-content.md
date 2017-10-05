---
title: "Publier du contenu Azure Media Services à l’aide de REST"
description: "Apprenez à créer un localisateur utilisé pour générer une URL de diffusion en continu. Le code utilise l’API REST."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: ff332c30-30c6-4ed1-99d0-5fffd25d4f23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: d1e0a112040f6aa4cfa9e8c323507b1c0a223f3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="210e0-104">Publier du contenu Azure Media Services à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="210e0-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="210e0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="210e0-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="210e0-106">REST</span><span class="sxs-lookup"><span data-stu-id="210e0-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="210e0-107">Portail</span><span class="sxs-lookup"><span data-stu-id="210e0-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="210e0-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="210e0-108">Overview</span></span>
<span data-ttu-id="210e0-109">Vous pouvez diffuser un MP4 à débit adaptatif défini par la création d’un localisateur de diffusion en continu à la demande et la création d’une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="210e0-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="210e0-110">La rubrique [Encodage d’un élément multimédia](media-services-rest-encode-asset.md) indique comment encoder un ensemble de fichiers MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="210e0-110">The [encoding an asset](media-services-rest-encode-asset.md) topic shows how to encode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="210e0-111">Si votre contenu est chiffré, configurez la stratégie de livraison d’éléments multimédias (comme décrit dans [cette](media-services-rest-configure-asset-delivery-policy.md) rubrique) avant de créer un localisateur.</span><span class="sxs-lookup"><span data-stu-id="210e0-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="210e0-112">Vous pouvez également utiliser un localisateur de diffusion en continu à la demande pour créer des URL qui pointent vers les fichiers MP4 pouvant être téléchargés progressivement.</span><span class="sxs-lookup"><span data-stu-id="210e0-112">You can also use an OnDemand streaming locator to build URLs that point to MP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="210e0-113">Cette rubrique montre comment créer un localisateur de streaming à la demande pour publier votre élément multimédia et créer des URL de diffusion en continu Smooth, MPEG DASH et HLS.</span><span class="sxs-lookup"><span data-stu-id="210e0-113">This topic shows how to create an OnDemand streaming locator in order to publish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="210e0-114">Elle explique également la création d’URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="210e0-114">It also shows hot to build progressive download URLs.</span></span>

<span data-ttu-id="210e0-115">La section [suivante](#types) indique les types d’énumération dont les valeurs sont utilisées dans les appels REST.</span><span class="sxs-lookup"><span data-stu-id="210e0-115">The [following](#types) section shows the enum types whose values are used in the REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="210e0-116">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="210e0-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="210e0-117">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="210e0-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-to-media-services"></a><span data-ttu-id="210e0-118">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="210e0-118">Connect to Media Services</span></span>

<span data-ttu-id="210e0-119">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="210e0-119">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="210e0-120">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="210e0-120">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="210e0-121">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="210e0-121">You must make subsequent calls to the new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="210e0-122">Création d’un localisateur de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="210e0-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="210e0-123">Pour créer le localisateur de diffusion en continu à la demande et obtenir les URL, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="210e0-123">To create the OnDemand streaming locator and get URLs you need to do the following:</span></span>

1. <span data-ttu-id="210e0-124">Si le contenu est chiffré, définissez une stratégie d'accès.</span><span class="sxs-lookup"><span data-stu-id="210e0-124">If the content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="210e0-125">Création d’un localisateur de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="210e0-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="210e0-126">Si vous envisagez de diffuser en continu, obtenez le fichier manifeste de diffusion en continu (.ism) dans la ressource.</span><span class="sxs-lookup"><span data-stu-id="210e0-126">If you plan to stream, get the streaming manifest file (.ism) in the asset.</span></span> 
   
   <span data-ttu-id="210e0-127">Si vous souhaitez télécharger progressivement, obtenez les noms des fichiers MP4 dans la ressource.</span><span class="sxs-lookup"><span data-stu-id="210e0-127">If you plan to progressively download, get the names of MP4 files in the asset.</span></span> 
4. <span data-ttu-id="210e0-128">Création d’URL vers le fichier manifeste ou les fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="210e0-128">Build URLs to the manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="210e0-129">Notez que vous ne pouvez créer un localisateur de diffusion en continu en utilisant une stratégie d’accès qui inclut des autorisations d’écriture ou de suppression.</span><span class="sxs-lookup"><span data-stu-id="210e0-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="210e0-130">Définition d’une stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="210e0-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="210e0-131">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="210e0-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="210e0-132">Vous devez utiliser le même ID de stratégie si vous utilisez toujours les mêmes jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs destinées à demeurer en place pendant une longue période (stratégies sans chargement).</span><span class="sxs-lookup"><span data-stu-id="210e0-132">You should use the same policy ID if you are always using the same days / access permissions, for example, policies for locators that are intended to remain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="210e0-133">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="210e0-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="210e0-134">Demande :</span><span class="sxs-lookup"><span data-stu-id="210e0-134">Request:</span></span>

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    Host: media.windows.net
    Content-Length: 68

    {"Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

<span data-ttu-id="210e0-135">Réponse :</span><span class="sxs-lookup"><span data-stu-id="210e0-135">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 311
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https:/media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3A69c80d98-7830-407f-a9af-e25f4b0d3e5f')
    Server: Microsoft-IIS/8.5
    request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-request-id: a877528a-bdb4-4414-9862-273f8e64f882
    x-ms-client-request-id: 6bcfd511-a561-448d-a022-a319a89ecffa
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:52:09 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AccessPolicies/@Element","Id":"nb:pid:UUID:69c80d98-7830-407f-a9af-e25f4b0d3e5f","Created":"2015-02-18T06:52:09.8862191Z","LastModified":"2015-02-18T06:52:09.8862191Z","Name":"access policy","DurationInMinutes":43200.0,"Permissions":1}

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="210e0-136">Création d’un localisateur de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="210e0-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="210e0-137">Créez le localisateur pour la ressource et la stratégie de ressource spécifiées.</span><span class="sxs-lookup"><span data-stu-id="210e0-137">Create the locator for the specified asset and asset policy.</span></span>

<span data-ttu-id="210e0-138">Demande :</span><span class="sxs-lookup"><span data-stu-id="210e0-138">Request:</span></span>

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstest1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1424263184&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=NWE%2f986Hr5lZTzVGKtC%2ftzHm9n6U%2fxpTFULItxKUGC4%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    Host: media.windows.net
    Content-Length: 181

    {"AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872Z","Type":2}

<span data-ttu-id="210e0-139">Réponse :</span><span class="sxs-lookup"><span data-stu-id="210e0-139">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 637
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Abe245661-2bbd-4fc6-b14f-9cf9a1492e5e')
    Server: Microsoft-IIS/8.5
    request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-request-id: 5bd5864a-0afd-44c0-a67a-4044a2c9043b
    x-ms-client-request-id: ac159492-9a0c-40c3-aacc-551b1b4c5f62
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 18 Feb 2015 06:58:37 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#Locators/@Element","Id":"nb:lid:UUID:be245661-2bbd-4fc6-b14f-9cf9a1492e5e","ExpirationDateTime":"2015-03-20T06:34:47.267872+00:00","Type":2,"Path":"http://amstest1.streaming.mediaservices.windows.net/be245661-2bbd-4fc6-b14f-9cf9a1492e5e/","BaseUri":"http://amstest1.streaming.mediaservices.windows.net","ContentAccessComponent":"be245661-2bbd-4fc6-b14f-9cf9a1492e5e","AccessPolicyId":"nb:pid:UUID:1480030d-c481-430a-9687-535c6a5cb272","AssetId":"nb:cid:UUID:cc1e445d-1500-80bd-538e-f1e4b71b465e","StartTime":"2015-02-18T06:34:47.267872+00:00","Name":null}

### <a name="build-streaming-urls"></a><span data-ttu-id="210e0-140">Création d’URL de diffusion</span><span class="sxs-lookup"><span data-stu-id="210e0-140">Build streaming URLs</span></span>
<span data-ttu-id="210e0-141">Utilisez la valeur **Chemin d’accès** renvoyée après la création du localisateur pour générer les URL Smooth, HLS et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="210e0-141">Use the **Path** value returned after the creation of the locator to build the Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="210e0-142">Smooth Streaming : **Chemin d’accès** + nom du fichier manifeste + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="210e0-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="210e0-143">exemple :</span><span class="sxs-lookup"><span data-stu-id="210e0-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="210e0-144">HLS : **Chemin d’accès** + nom du fichier manifeste "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="210e0-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="210e0-145">exemple :</span><span class="sxs-lookup"><span data-stu-id="210e0-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="210e0-146">DASH : **Chemin d’accès** + nom du fichier manifeste + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="210e0-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="210e0-147">exemple :</span><span class="sxs-lookup"><span data-stu-id="210e0-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="210e0-148">Génération d’URL de téléchargement progressif</span><span class="sxs-lookup"><span data-stu-id="210e0-148">Build progressive download URLs</span></span>
<span data-ttu-id="210e0-149">Utilisez la valeur **Chemin d’accès** renvoyée après la création du localisateur pour générer l’URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="210e0-149">Use the **Path** value returned after the creation of the locator to build the progressive download URL.</span></span>   

<span data-ttu-id="210e0-150">URL : **Chemin d’accès** + nom du fichier de ressource mp4</span><span class="sxs-lookup"><span data-stu-id="210e0-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="210e0-151">exemple :</span><span class="sxs-lookup"><span data-stu-id="210e0-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="210e0-152"><a id="types"></a>Types Enum</span><span class="sxs-lookup"><span data-stu-id="210e0-152"><a id="types"></a>Enum types</span></span>
    [Flags]
    public enum AccessPermissions
    {
        None = 0,
        Read = 1,
        Write = 2,
        Delete = 4,
        List = 8,
    }

    public enum LocatorType
    {
        None = 0,
        Sas = 1,
        OnDemandOrigin = 2,
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="210e0-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="210e0-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="210e0-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="210e0-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="210e0-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="210e0-155">See also</span></span>
[<span data-ttu-id="210e0-156">Vue d’ensemble de l’API REST Media Services Operations</span><span class="sxs-lookup"><span data-stu-id="210e0-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="210e0-157">Configurer une stratégie de distribution d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="210e0-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

