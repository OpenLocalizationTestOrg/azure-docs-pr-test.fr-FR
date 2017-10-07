---
title: "contenu d’Azure Media Services aaaPublish à l’aide de REST"
description: "Découvrez comment toocreate un localisateur de toobuild utilisé une URL de diffusion en continu. code de Hello utilise l’API REST."
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
ms.openlocfilehash: f849e21b3103b9b33bc652e886b2016ea495b19a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-rest"></a><span data-ttu-id="ec1d7-104">Publier du contenu Azure Media Services à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="ec1d7-104">Publish Azure Media Services content using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec1d7-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ec1d7-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="ec1d7-106">REST</span><span class="sxs-lookup"><span data-stu-id="ec1d7-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="ec1d7-107">Portail</span><span class="sxs-lookup"><span data-stu-id="ec1d7-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ec1d7-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ec1d7-108">Overview</span></span>
<span data-ttu-id="ec1d7-109">Vous pouvez diffuser un MP4 à débit adaptatif défini par la création d’un localisateur de diffusion en continu à la demande et la création d’une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="ec1d7-110">Hello [encodage d’un élément multimédia](media-services-rest-encode-asset.md) rubrique montre comment définie les tooencode dans un MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-110">hello [encoding an asset](media-services-rest-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> <span data-ttu-id="ec1d7-111">Si votre contenu est chiffré, configurez la stratégie de livraison d’éléments multimédias (comme décrit dans [cette](media-services-rest-configure-asset-delivery-policy.md) rubrique) avant de créer un localisateur.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-rest-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 

<span data-ttu-id="ec1d7-112">Vous pouvez également utiliser une URL de toobuild que les fichiers de point de tooMP4 qui peuvent être téléchargé progressivement de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="ec1d7-113">Cette rubrique montre comment toocreate un localisateur de diffusion en continu à la demande de commande toopublish votre élément multimédia et le générer un Smooth Streaming, MPEG DASH et HLS URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-113">This topic shows how toocreate an OnDemand streaming locator in order toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="ec1d7-114">Il montre également à chaud toobuild URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-114">It also shows hot toobuild progressive download URLs.</span></span>

<span data-ttu-id="ec1d7-115">Hello [suivant](#types) section affiche hello types enum dont les valeurs sont utilisées dans les appels REST hello.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-115">hello [following](#types) section shows hello enum types whose values are used in hello REST calls.</span></span>   

> [!NOTE]
> <span data-ttu-id="ec1d7-116">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="ec1d7-117">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="ec1d7-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="ec1d7-118">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="ec1d7-118">Connect tooMedia Services</span></span>

<span data-ttu-id="ec1d7-119">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ec1d7-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="ec1d7-120">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="ec1d7-121">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="ec1d7-122">Création d’un localisateur de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="ec1d7-122">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="ec1d7-123">toocreate hello localisateur de diffusion en continu à la demande et obtenir l’URL que vous avez besoin de hello toodo suivant :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-123">toocreate hello OnDemand streaming locator and get URLs you need toodo hello following:</span></span>

1. <span data-ttu-id="ec1d7-124">Si le contenu de hello est chiffré, définir une stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-124">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="ec1d7-125">Création d’un localisateur de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-125">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="ec1d7-126">Si vous envisagez toostream, obtenir hello de diffusion en continu le fichier manifeste (.ism) dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-126">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="ec1d7-127">Si vous envisagez de téléchargement de tooprogressively, obtenir les noms de hello de fichiers MP4 dans un élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-127">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span> 
4. <span data-ttu-id="ec1d7-128">Générer le fichier de manifeste toohello URL ou fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-128">Build URLs toohello manifest file or MP4 files.</span></span> 
5. <span data-ttu-id="ec1d7-129">Notez que vous ne pouvez créer un localisateur de diffusion en continu en utilisant une stratégie d’accès qui inclut des autorisations d’écriture ou de suppression.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-129">Note that you cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.</span></span>

### <a name="create-an-access-policy"></a><span data-ttu-id="ec1d7-130">Définition d’une stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-130">Create an access policy</span></span>

>[!NOTE]
><span data-ttu-id="ec1d7-131">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="ec1d7-131">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ec1d7-132">Vous devez utiliser hello ID de stratégie même si vous utilisez toujours hello même jours / autorisations d’accès, par exemple, les stratégies pour les localisateurs sont tooremain prévue en place pendant une longue période (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="ec1d7-132">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ec1d7-133">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="ec1d7-133">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="ec1d7-134">Demande :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-134">Request:</span></span>

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

<span data-ttu-id="ec1d7-135">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-135">Response:</span></span>

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

### <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="ec1d7-136">Création d’un localisateur de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="ec1d7-136">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="ec1d7-137">Créer le repère hello pour élément multimédia spécifié de hello et stratégie d’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-137">Create hello locator for hello specified asset and asset policy.</span></span>

<span data-ttu-id="ec1d7-138">Demande :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-138">Request:</span></span>

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

<span data-ttu-id="ec1d7-139">Réponse :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-139">Response:</span></span>

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

### <a name="build-streaming-urls"></a><span data-ttu-id="ec1d7-140">Création d’URL de diffusion</span><span class="sxs-lookup"><span data-stu-id="ec1d7-140">Build streaming URLs</span></span>
<span data-ttu-id="ec1d7-141">Hello d’utilisation **chemin d’accès** valeur retournée après la création de hello Hello de hello localisateur toobuild Smooth, HLS et MPEG DASH URL.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-141">Use hello **Path** value returned after hello creation of hello locator toobuild hello Smooth, HLS, and MPEG DASH URLs.</span></span> 

<span data-ttu-id="ec1d7-142">Smooth Streaming : **Chemin d’accès** + nom du fichier manifeste + "/manifest"</span><span class="sxs-lookup"><span data-stu-id="ec1d7-142">Smooth Streaming: **Path** + manifest file name + "/manifest"</span></span>

<span data-ttu-id="ec1d7-143">exemple :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-143">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest

<span data-ttu-id="ec1d7-144">HLS : **Chemin d’accès** + nom du fichier manifeste "/manifest(format=m3u8-aapl)"</span><span class="sxs-lookup"><span data-stu-id="ec1d7-144">HLS: **Path** + manifest file name + "/manifest(format=m3u8-aapl)"</span></span>

<span data-ttu-id="ec1d7-145">exemple :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-145">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)


<span data-ttu-id="ec1d7-146">DASH : **Chemin d’accès** + nom du fichier manifeste + "/manifest(format=mpd-time-csf)"</span><span class="sxs-lookup"><span data-stu-id="ec1d7-146">DASH: **Path** + manifest file name + "/manifest(format=mpd-time-csf)"</span></span>

<span data-ttu-id="ec1d7-147">exemple :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-147">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


### <a name="build-progressive-download-urls"></a><span data-ttu-id="ec1d7-148">Génération d’URL de téléchargement progressif</span><span class="sxs-lookup"><span data-stu-id="ec1d7-148">Build progressive download URLs</span></span>
<span data-ttu-id="ec1d7-149">Hello d’utilisation **chemin d’accès** valeur retournée après la création de hello d’URL de téléchargement progressif hello locator toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="ec1d7-149">Use hello **Path** value returned after hello creation of hello locator toobuild hello progressive download URL.</span></span>   

<span data-ttu-id="ec1d7-150">URL : **Chemin d’accès** + nom du fichier de ressource mp4</span><span class="sxs-lookup"><span data-stu-id="ec1d7-150">URL: **Path** + asset file mp4 name</span></span>

<span data-ttu-id="ec1d7-151">exemple :</span><span class="sxs-lookup"><span data-stu-id="ec1d7-151">example:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

## <span data-ttu-id="ec1d7-152"><a id="types"></a>Types Enum</span><span class="sxs-lookup"><span data-stu-id="ec1d7-152"><a id="types"></a>Enum types</span></span>
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="ec1d7-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ec1d7-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ec1d7-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ec1d7-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="ec1d7-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ec1d7-155">See also</span></span>
[<span data-ttu-id="ec1d7-156">Vue d’ensemble de l’API REST Media Services Operations</span><span class="sxs-lookup"><span data-stu-id="ec1d7-156">Media Services operations REST API overview</span></span>](media-services-rest-how-to-use.md)

[<span data-ttu-id="ec1d7-157">Configurer une stratégie de distribution d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="ec1d7-157">Configure asset delivery policy</span></span>](media-services-rest-configure-asset-delivery-policy.md)

