---
title: "stratégies de remise aaaConfiguring actif à l’aide des API REST Media Services | Documents Microsoft"
description: "Cette rubrique montre comment tooconfigure des stratégies de remise différents actif à l’aide des API REST Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5cb9d32a-e68b-4585-aa82-58dded0691d0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 8203230d570935e17382c598820dbfe42f83f8d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="73723-103">Configuration des stratégies de remise de ressources</span><span class="sxs-lookup"><span data-stu-id="73723-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="73723-104">Si vous envisagez toodeliver dynamiquement chiffré actifs, une des hello étapes Bonjour Media Services de contenu de flux de travail de remise consiste à configurer des stratégies de remise pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="73723-104">If you plan toodeliver dynamically encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="73723-105">stratégie de livraison des actifs Hello indique comment vous souhaitez pour votre toobe asset remis à Media Services : dans le protocole de diffusion en continu doit votre élément multimédia dynamiquement packagé (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), vous souhaitez toodynamically ou non chiffrer votre élément multimédia et comment (enveloppe ou chiffrement commun).</span><span class="sxs-lookup"><span data-stu-id="73723-105">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="73723-106">Cette rubrique explique pourquoi et comment toocreate et configurer des stratégies de remise d’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="73723-106">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="73723-107">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="73723-107">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="73723-108">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="73723-108">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="73723-109">En outre, toobe toouse en mesure de mise en package dynamique et le chiffrement dynamique votre élément multimédia doit contenir un ensemble de fichiers à débit adaptatif MP4s ou des fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="73723-109">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="73723-110">Vous pouvez appliquer différentes stratégies toohello même actif.</span><span class="sxs-lookup"><span data-stu-id="73723-110">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="73723-111">Par exemple, vous pouvez appliquer PlayReady chiffrement tooSmooth diffusion en continu et l’enveloppe AES chiffrement tooMPEG DASH et HLS.</span><span class="sxs-lookup"><span data-stu-id="73723-111">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="73723-112">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="73723-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="73723-113">Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini.</span><span class="sxs-lookup"><span data-stu-id="73723-113">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="73723-114">Ensuite, tous les protocoles seront autorisés en hello clair.</span><span class="sxs-lookup"><span data-stu-id="73723-114">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="73723-115">Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="73723-115">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="73723-116">Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise.</span><span class="sxs-lookup"><span data-stu-id="73723-116">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="73723-117">Par exemple, toodeliver votre élément multimédia chiffré avec la clé de chiffrement d’enveloppe Standard (AES), définissez le type de stratégie hello trop**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="73723-117">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="73723-118">tooremove le chiffrement de stockage et les actifs de hello flux Bonjour claires, le type de stratégie hello défini trop**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="73723-118">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="73723-119">Exemples qui montrent comment tooconfigure suivent ces types de stratégie.</span><span class="sxs-lookup"><span data-stu-id="73723-119">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="73723-120">Selon la façon dont vous configurez la stratégie de livraison des actifs hello vous serait sera en mesure de toodynamically package, dynamiquement chiffrer et diffuser en continu hello suite de protocoles de diffusion en continu : Smooth Streaming, HLS, les flux MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="73723-120">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="73723-121">Hello suivant liste affiche hello met en forme que vous utilisez toostream Smooth, HLS, tiret.</span><span class="sxs-lookup"><span data-stu-id="73723-121">hello following list shows hello formats that you use toostream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="73723-122">Smooth Streaming :</span><span class="sxs-lookup"><span data-stu-id="73723-122">Smooth Streaming:</span></span>

<span data-ttu-id="73723-123">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest</span><span class="sxs-lookup"><span data-stu-id="73723-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="73723-124">HLS :</span><span class="sxs-lookup"><span data-stu-id="73723-124">HLS:</span></span>

<span data-ttu-id="73723-125">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="73723-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="73723-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="73723-126">MPEG DASH</span></span>

<span data-ttu-id="73723-127">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="73723-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="73723-128">Pour plus d’informations sur comment toopublish un élément multimédia et créer une URL de diffusion en continu, consultez [générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="73723-128">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="73723-129">Considérations</span><span class="sxs-lookup"><span data-stu-id="73723-129">Considerations</span></span>
* <span data-ttu-id="73723-130">Vous ne pouvez pas supprimer une stratégie AssetDeliveryPolicy associée à un élément multimédia alors qu’un localisateur (de diffusion en continuer) OnDemand existe pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="73723-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="73723-131">stratégie de hello tooremove à partir de l’élément multimédia de hello il est recommandé de Hello avant de supprimer la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="73723-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="73723-132">Il est impossible de créer un localisateur de diffusion en continu sur un élément multimédia chiffré de stockage quand aucune stratégie de distribution d’éléments multimédias n’est définie.</span><span class="sxs-lookup"><span data-stu-id="73723-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="73723-133">Si hello actif n’est pas chiffré de stockage, système de hello sera vous permettent de créer un élément multimédia hello de recherche et de flux Bonjour effacer sans une stratégie de livraison des actifs.</span><span class="sxs-lookup"><span data-stu-id="73723-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="73723-134">Vous pouvez avoir plusieurs stratégies de remise actif associés à un seul élément multimédia, mais vous ne pouvez spécifier qu’une façon toohandle un AssetDeliveryProtocol donné.</span><span class="sxs-lookup"><span data-stu-id="73723-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="73723-135">Ce qui signifie que si vous essayez de toolink deux stratégies de remise qui spécifient le protocole AssetDeliveryProtocol.SmoothStreaming hello qui entraîne une erreur car le système de hello ne sait pas celui que vous souhaitez tooapply lorsqu’un client effectue une demande de diffusion en continu lisse.</span><span class="sxs-lookup"><span data-stu-id="73723-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="73723-136">Si vous avez un élément multimédia avec un localisateur de diffusion en continu, Impossible de lier un élément multimédia de nouvelle stratégie toohello, dissocier une stratégie existante à partir de l’élément multimédia de hello ou mettre à jour une stratégie de remise associée hello actif.</span><span class="sxs-lookup"><span data-stu-id="73723-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset, unlink an existing policy from hello asset, or update a delivery policy associated with hello asset.</span></span>  <span data-ttu-id="73723-137">Vous tout d’abord avez localisateur de diffusion en continu tooremove hello, ajustez les stratégies de hello, puis recréez hello localisateur de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="73723-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="73723-138">Vous pouvez utiliser hello locatorId même lorsque vous recréez hello de diffusion en continu de la recherche, mais vous devez vous assurer que causer des problèmes pour les clients, car le contenu peut être mis en cache à l’origine de hello ou un CDN en aval.</span><span class="sxs-lookup"><span data-stu-id="73723-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="73723-139">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="73723-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="73723-140">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="73723-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="73723-141">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="73723-141">Connect tooMedia Services</span></span>

<span data-ttu-id="73723-142">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="73723-142">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="73723-143">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="73723-143">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="73723-144">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="73723-144">You must make subsequent calls toohello new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="73723-145">Stratégie de remise de ressources</span><span class="sxs-lookup"><span data-stu-id="73723-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="73723-146"><a id="create_asset_delivery_policy"></a>Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="73723-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="73723-147">Hello requête HTTP suivante crée une stratégie de remise actif qui spécifie toonot appliquer le chiffrement dynamique et de protocoles de flux de données toodeliver hello dans un des hello suivant : protocoles MPEG DASH, HLS et Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="73723-147">hello following HTTP request creates an asset delivery policy that specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="73723-148">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="73723-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="73723-149">Demande :</span><span class="sxs-lookup"><span data-stu-id="73723-149">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    Host: media.windows.net

    {"Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null}

<span data-ttu-id="73723-150">Réponse :</span><span class="sxs-lookup"><span data-stu-id="73723-150">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 363
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 4651882c-d7ad-4d5e-86ab-f07f47dcb41e
    request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    x-ms-request-id: 6aedbf93-4bc2-4586-8845-fd45590136af
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 06:21:27 GMT

    {"odata.metadata":"https://media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element",
    "Id":"nb:adpid:UUID:92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd",
    "Name":"Clear Policy",
    "AssetDeliveryProtocol":7,
    "AssetDeliveryPolicyType":2,
    "AssetDeliveryConfiguration":null,
    "Created":"2015-02-08T06:21:27.6908329Z",
    "LastModified":"2015-02-08T06:21:27.6908329Z"}

### <span data-ttu-id="73723-151"><a id="link_asset_with_asset_delivery_policy"></a>Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="73723-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="73723-152">Hello suivant hello de liens de demande HTTP spécifié asset toohello asset remise stratégie.</span><span class="sxs-lookup"><span data-stu-id="73723-152">hello following HTTP request links hello specified asset toohello asset delivery policy to.</span></span>

<span data-ttu-id="73723-153">Demande :</span><span class="sxs-lookup"><span data-stu-id="73723-153">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A86933344-9539-4d0c-be7d-f842458693e0')/$links/DeliveryPolicies HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-e769-3344-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423397827&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Szo6lbJAvL3dyecAeVmyAnzv3mGzfUNClR5shk9Ivbk%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 56d2763f-6e72-419d-ba3c-685f6db97e81
    Host: media.windows.net

    {"uri":"https://media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3A92b0f6ba-3c9f-49b6-a5fa-2a8703b04ecd')"}

<span data-ttu-id="73723-154">Réponse :</span><span class="sxs-lookup"><span data-stu-id="73723-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="73723-155">Stratégie de remise de ressources DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="73723-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-envelopeencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="73723-156">Créer la clé de contenu de type de EnvelopeEncryption hello et le lier toohello actif</span><span class="sxs-lookup"><span data-stu-id="73723-156">Create content key of hello EnvelopeEncryption type and link it toohello asset</span></span>
<span data-ttu-id="73723-157">Lorsque vous spécifiez la stratégie de livraison DynamicEnvelopeEncryption, vous devez toomake des toolink que votre clé de contenu tooa asset Hello EnvelopeEncryption type.</span><span class="sxs-lookup"><span data-stu-id="73723-157">When specifying DynamicEnvelopeEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello EnvelopeEncryption type.</span></span> <span data-ttu-id="73723-158">Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="73723-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="73723-159"><a id="get_delivery_url"></a>Obtention de l’URL de remise</span><span class="sxs-lookup"><span data-stu-id="73723-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="73723-160">URL de remise Get hello pour hello spécifié méthode de remise de clé de contenu hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="73723-160">Get hello delivery URL for hello specified delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="73723-161">Un client utilise hello retourné URL toorequest une clé AES ou une licence PlayReady Bonjour tooplayback de commande du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="73723-161">A client uses hello returned URL toorequest an AES key or a PlayReady license in order tooplayback hello protected content.</span></span>

<span data-ttu-id="73723-162">Spécifiez type hello de hello URL tooget dans le corps hello de requête HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="73723-162">Specify hello type of hello URL tooget in hello body of hello HTTP request.</span></span> <span data-ttu-id="73723-163">Si vous protégez votre contenu avec PlayReady, demandez une URL d’acquisition de licence PlayReady de Media Services, à l’aide de 1 pour hello keyDeliveryType : {« keyDeliveryType » : 1}.</span><span class="sxs-lookup"><span data-stu-id="73723-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for hello keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="73723-164">Si vous protégez votre contenu avec chiffrement d’enveloppe hello, demandez une URL d’acquisition de clé en spécifiant 2 pour keyDeliveryType : {« keyDeliveryType » : 2}.</span><span class="sxs-lookup"><span data-stu-id="73723-164">If you are protecting your content with hello envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="73723-165">Demande :</span><span class="sxs-lookup"><span data-stu-id="73723-165">Request:</span></span>

    POST https://media.windows.net/api/ContentKeys('nb:kid:UUID:dc88f996-2859-4cf7-a279-c52a9d6b2f04')/GetKeyDeliveryUrl HTTP/1.1
    Content-Type: application/json
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423452029&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=IEXV06e3drSIN5naFRBdhJZCbfEqQbFZsGSIGmawhEo%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    Host: media.windows.net
    Content-Length: 21

    {"keyDeliveryType":2}

<span data-ttu-id="73723-166">Réponse :</span><span class="sxs-lookup"><span data-stu-id="73723-166">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 198
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 569d4b7c-a446-4edc-b77c-9fb686083dd8
    request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    x-ms-request-id: d26f65d2-fe65-4136-8fcf-31545be68377
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 08 Feb 2015 21:42:30 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#Edm.String","value":"https://amsaccount1.keydelivery.mediaservices.windows.net/?KID=dc88f996-2859-4cf7-a279-c52a9d6b2f04"}


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="73723-167">Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="73723-167">Create asset delivery policy</span></span>
<span data-ttu-id="73723-168">requête HTTP suivante Hello crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement dynamique enveloppe (**DynamicEnvelopeEncryption**) toohello **HLS**protocole (dans cet exemple, d’autres protocoles seront bloqués de diffusion en continu).</span><span class="sxs-lookup"><span data-stu-id="73723-168">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) toohello **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="73723-169">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="73723-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="73723-170">Demande :</span><span class="sxs-lookup"><span data-stu-id="73723-170">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]"}


<span data-ttu-id="73723-171">Réponse :</span><span class="sxs-lookup"><span data-stu-id="73723-171">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 460
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: media.windows.net/api/AssetDeliveryPolicies('nb%3Aadpid%3AUUID%3Aec9b994e-672c-4a5b-8490-a464eeb7964b')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    x-ms-request-id: c2a1ac0e-9644-474f-b38f-b9541c3a7c5f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 09 Feb 2015 05:24:38 GMT

    {"odata.metadata":"media.windows.net/api/$metadata#AssetDeliveryPolicies/@Element","Id":"nb:adpid:UUID:ec9b994e-672c-4a5b-8490-a464eeb7964b","Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":4,"AssetDeliveryPolicyType":3,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\\/\"}]","Created":"2015-02-09T05:24:38.9167436Z","LastModified":"2015-02-09T05:24:38.9167436Z"}


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="73723-172">Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="73723-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="73723-173">Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="73723-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="73723-174">Stratégie de remise de ressources DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="73723-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-hello-commonencryption-type-and-link-it-toohello-asset"></a><span data-ttu-id="73723-175">Créer la clé de contenu de type de CommonEncryption hello et le lier toohello actif</span><span class="sxs-lookup"><span data-stu-id="73723-175">Create content key of hello CommonEncryption type and link it toohello asset</span></span>
<span data-ttu-id="73723-176">Lorsque vous spécifiez la stratégie de livraison DynamicCommonEncryption, vous devez toomake des toolink que votre clé de contenu tooa asset Hello CommonEncryption type.</span><span class="sxs-lookup"><span data-stu-id="73723-176">When specifying DynamicCommonEncryption delivery policy, you need toomake sure toolink your asset tooa content key of hello CommonEncryption type.</span></span> <span data-ttu-id="73723-177">Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="73723-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="73723-178">Obtention de l’URL de remise</span><span class="sxs-lookup"><span data-stu-id="73723-178">Get Delivery URL</span></span>
<span data-ttu-id="73723-179">Obtenir l’URL de remise hello hello PlayReady mode de livraison de la clé de contenu hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="73723-179">Get hello delivery URL for hello PlayReady delivery method of hello content key created in hello previous step.</span></span> <span data-ttu-id="73723-180">Un client utilise hello retourné toorequest URL protégée par une licence PlayReady Bonjour tooplayback de commande contenu.</span><span class="sxs-lookup"><span data-stu-id="73723-180">A client uses hello returned URL toorequest a PlayReady license in order tooplayback hello protected content.</span></span> <span data-ttu-id="73723-181">Pour plus d’informations, consultez la rubrique [Obtention de l’URL de remise](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="73723-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="73723-182">Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="73723-182">Create asset delivery policy</span></span>
<span data-ttu-id="73723-183">requête HTTP suivante Hello crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement commun dynamique (**DynamicCommonEncryption**) toohello **Smooth Streaming**  protocole (dans cet exemple, d’autres protocoles seront bloqués de diffusion en continu).</span><span class="sxs-lookup"><span data-stu-id="73723-183">hello following HTTP request creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) toohello **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="73723-184">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="73723-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="73723-185">Demande :</span><span class="sxs-lookup"><span data-stu-id="73723-185">Request:</span></span>

    POST https://media.windows.net/api/AssetDeliveryPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amsaccount1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423480651&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=T2FG3tIV0e2ETzxQ6RDWxWAsAzuy3ez2ruXPhrBe62Y%3d
    x-ms-version: 2.11
    x-ms-client-request-id: fff319f6-71dd-4f6c-af27-b675c0066fa7
    Host: media.windows.net

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":1,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":2,\"Value\":\"https:\\/\\/amsaccount1.keydelivery.mediaservices.windows.net\/PlayReady\/"}]"}


<span data-ttu-id="73723-186">Si vous souhaitez tooprotect votre contenu à l’aide de Widevine DRM, mettre à jour hello AssetDeliveryConfiguration valeurs toouse WidevineLicenseAcquisitionUrl (qui a la valeur hello 7) et spécifiez les URL de hello d’un service de remise de licences.</span><span class="sxs-lookup"><span data-stu-id="73723-186">If you want tooprotect your content using Widevine DRM, update hello AssetDeliveryConfiguration values toouse WidevineLicenseAcquisitionUrl (which has hello value of 7) and specify hello URL of a license delivery service.</span></span> <span data-ttu-id="73723-187">Vous pouvez utiliser hello suivant toohelp de partenaires AMS vous fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="73723-187">You can use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="73723-188">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="73723-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="73723-189">Lors du chiffrement avec Widevine, vous serez uniquement en mesure de toodeliver à l’aide de tiret.</span><span class="sxs-lookup"><span data-stu-id="73723-189">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="73723-190">Vérifiez le protocole de livraison actif que toospecify tiret hello en (2).</span><span class="sxs-lookup"><span data-stu-id="73723-190">Make sure toospecify DASH (2) in hello asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="73723-191">Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="73723-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="73723-192">Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="73723-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="73723-193"><a id="types"></a>Types utilisés durant la définition de AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="73723-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="73723-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="73723-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="73723-195">Hello enum suivant décrit les valeurs que vous pouvez définir pour le protocole de remise hello actif.</span><span class="sxs-lookup"><span data-stu-id="73723-195">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

    [Flags]
    public enum AssetDeliveryProtocol
    {
        /// <summary>
        /// No protocols.
        /// </summary>
        None = 0x0,

        /// <summary>
        /// Smooth streaming protocol.
        /// </summary>
        SmoothStreaming = 0x1,

        /// <summary>
        /// MPEG Dynamic Adaptive Streaming over HTTP (DASH)
        /// </summary>
        Dash = 0x2,

        /// <summary>
        /// Apple HTTP Live Streaming protocol.
        /// </summary>
        HLS = 0x4,

        ProgressiveDownload = 0x10, 
 
        /// <summary>
        /// Include all protocols.
        /// </summary>
        All = 0xFFFF
    }

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="73723-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="73723-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="73723-197">Hello enum suivant décrit les valeurs que vous pouvez définir pour le type de stratégie de remise hello asset.</span><span class="sxs-lookup"><span data-stu-id="73723-197">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// hello Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption toohello asset.
        /// </summary>
        /// 
        NoDynamicEncryption,  

        /// <summary>
        /// Apply Dynamic Envelope encryption.
        /// </summary>
        DynamicEnvelopeEncryption,

        /// <summary>
        /// Apply Dynamic Common encryption.
        /// </summary>
        DynamicCommonEncryption
        }

### <a name="contentkeydeliverytype"></a><span data-ttu-id="73723-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="73723-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="73723-199">Hello enum suivant décrit les valeurs que vous pouvez utiliser la méthode de remise tooconfigure hello du client de contenu toohello clé hello.</span><span class="sxs-lookup"><span data-stu-id="73723-199">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
    public enum ContentKeyDeliveryType
    {
        /// <summary>
        /// None.
        ///
        </summary>
        None = 0,

        /// <summary>
        /// Use PlayReady License acquistion protocol
        ///
        </summary>
        PlayReadyLicense = 1,

        /// <summary>
        /// Use MPEG Baseline HTTP key protocol.
        ///
        </summary>
        BaselineHttp = 2,

        /// <summary>
        /// Use Widevine License acquistion protocol
        ///
        </summary>
        Widevine = 3

    }


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="73723-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="73723-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="73723-201">Hello suivant enum décrit les valeurs que vous pouvez définir la configuration spécifique du tooget tooconfigure clés utilisées pour une stratégie de livraison des actifs.</span><span class="sxs-lookup"><span data-stu-id="73723-201">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

    public enum AssetDeliveryPolicyConfigurationKey
    {
        /// <summary>
        /// No policies.
        /// </summary>
        None,

        /// <summary>
        /// Exact Envelope key URL.
        /// </summary>
        EnvelopeKeyAcquisitionUrl,

        /// <summary>
        /// Base key url that will have KID=<Guid> appended for Envelope.
        /// </summary>
        EnvelopeBaseKeyAcquisitionUrl,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// hello PlayReady License Acquisition Url toouse for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// hello PlayReady Custom Attributes tooadd toohello PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// hello initialization vector toouse for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="73723-202">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="73723-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="73723-203">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="73723-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

