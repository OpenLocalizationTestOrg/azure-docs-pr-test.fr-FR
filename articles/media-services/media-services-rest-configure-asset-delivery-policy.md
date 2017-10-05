---
title: "Configuration des stratégies de remise de ressources à l’aide de l’API REST Media Services | Microsoft Docs"
description: "Cette rubrique montre comment configurer différentes stratégies de remise de ressources à l’aide de l’API REST Media Services."
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
ms.openlocfilehash: 7ffbde11b943961dd3a3b5edebd0cfd52429e845
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-asset-delivery-policies"></a><span data-ttu-id="c4c93-103">Configuration des stratégies de remise de ressources</span><span class="sxs-lookup"><span data-stu-id="c4c93-103">Configuring asset delivery policies</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

<span data-ttu-id="c4c93-104">Si vous envisagez la remise de ressources chiffrées dynamiquement, l'une des étapes du workflow de remise de contenu Media Services consiste à configurer les stratégies de remise pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-104">If you plan to deliver dynamically encrypted assets, one of the steps in the Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="c4c93-105">La stratégie de remise de ressources indique à Media Services comment vous souhaitez distribuer vos ressources : dans quel protocole de diffusion en continu votre ressource doit être empaquetée dynamiquement (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), si vous souhaitez chiffrer dynamiquement votre ressource ou non et comment (chiffrement commun ou d’enveloppe).</span><span class="sxs-lookup"><span data-stu-id="c4c93-105">The asset delivery policy tells Media Services how you want for your asset to be delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want to dynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="c4c93-106">Cette rubrique explique pourquoi et comment créer et configurer des stratégies de livraison d’éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="c4c93-106">This topic discusses why and how to create and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="c4c93-107">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="c4c93-107">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="c4c93-108">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="c4c93-108">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> 
>
><span data-ttu-id="c4c93-109">De plus, pour pouvoir utiliser l’empaquetage et le chiffrement dynamiques, votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="c4c93-109">Also, to be able to use dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>

<span data-ttu-id="c4c93-110">Vous pouvez appliquer des stratégies différentes à la même ressource.</span><span class="sxs-lookup"><span data-stu-id="c4c93-110">You could apply different policies to the same asset.</span></span> <span data-ttu-id="c4c93-111">Par exemple, vous pouvez appliquer le chiffrement PlayReady pour la diffusion en continu lisse et AES en enveloppe pour MPEG DASH et TLS.</span><span class="sxs-lookup"><span data-stu-id="c4c93-111">For example, you could apply PlayReady encryption to Smooth Streaming and AES Envelope encryption to MPEG DASH and HLS.</span></span> <span data-ttu-id="c4c93-112">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, en cas d’ajout d’une stratégie unique qui spécifie uniquement TLS comme protocole) seront bloqués de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="c4c93-112">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as the protocol) will be blocked from streaming.</span></span> <span data-ttu-id="c4c93-113">Cela ne s’applique toutefois pas si vous n’avez défini aucune stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-113">The exception to this is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="c4c93-114">Tous les protocoles seront alors autorisés.</span><span class="sxs-lookup"><span data-stu-id="c4c93-114">Then, all protocols will be allowed in the clear.</span></span>

<span data-ttu-id="c4c93-115">Si vous souhaitez remettre une ressource à chiffrement de stockage, vous devez configurer la stratégie de remise de la ressource.</span><span class="sxs-lookup"><span data-stu-id="c4c93-115">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="c4c93-116">Avant de pouvoir diffuser votre ressource en continu, le serveur de diffusion supprime le chiffrement de stockage et transmet en continu votre contenu à l’aide de la stratégie de remise spécifiée.</span><span class="sxs-lookup"><span data-stu-id="c4c93-116">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="c4c93-117">Par exemple, pour remettre votre ressource chiffrée avec la clé de chiffrement d'enveloppe AES (Advanced Encryption Standard), définissez le type de stratégie sur **DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="c4c93-117">For example, to deliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set the policy type to **DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="c4c93-118">Pour supprimer le chiffrement de stockage et diffuser la ressource en clair, définissez le type de stratégie sur **NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="c4c93-118">To remove storage encryption and stream the asset in the clear, set the policy type to **NoDynamicEncryption**.</span></span> <span data-ttu-id="c4c93-119">Vous trouverez des exemples qui montrent comment configurer ces types de stratégie ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c4c93-119">Examples that show how to configure these policy types follow.</span></span>

<span data-ttu-id="c4c93-120">Selon la configuration de la stratégie de remise de ressources, vous pourrez empaqueter dynamiquement, chiffrer dynamiquement et diffuser les protocoles de diffusion en continu suivants : Smooth Streaming, HLS et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="c4c93-120">Depending on how you configure the asset delivery policy you would be able to dynamically package, dynamically encrypt, and stream the following streaming protocols: Smooth Streaming, HLS, MPEG DASH streams.</span></span>

<span data-ttu-id="c4c93-121">La liste suivante présente les formats utilisés pour diffuser en continu Smooth, HLS et DASH.</span><span class="sxs-lookup"><span data-stu-id="c4c93-121">The following list shows the formats that you use to stream Smooth, HLS, DASH.</span></span>

<span data-ttu-id="c4c93-122">Smooth Streaming :</span><span class="sxs-lookup"><span data-stu-id="c4c93-122">Smooth Streaming:</span></span>

<span data-ttu-id="c4c93-123">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest</span><span class="sxs-lookup"><span data-stu-id="c4c93-123">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="c4c93-124">HLS :</span><span class="sxs-lookup"><span data-stu-id="c4c93-124">HLS:</span></span>

<span data-ttu-id="c4c93-125">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="c4c93-125">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="c4c93-126">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="c4c93-126">MPEG DASH</span></span>

<span data-ttu-id="c4c93-127">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="c4c93-127">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


<span data-ttu-id="c4c93-128">Pour savoir comment publier une ressource et générer une URL de diffusion en continu, consultez [Générer une URL de diffusion en continu](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="c4c93-128">For instructions on how to publish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="considerations"></a><span data-ttu-id="c4c93-129">Considérations</span><span class="sxs-lookup"><span data-stu-id="c4c93-129">Considerations</span></span>
* <span data-ttu-id="c4c93-130">Vous ne pouvez pas supprimer une stratégie AssetDeliveryPolicy associée à un élément multimédia alors qu’un localisateur (de diffusion en continuer) OnDemand existe pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="c4c93-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="c4c93-131">Il est recommandé de retirer la stratégie de l’élément multimédia avant de la supprimer.</span><span class="sxs-lookup"><span data-stu-id="c4c93-131">The recommendation is to remove the policy from the asset before deleting the policy.</span></span>
* <span data-ttu-id="c4c93-132">Il est impossible de créer un localisateur de diffusion en continu sur un élément multimédia chiffré de stockage quand aucune stratégie de distribution d’éléments multimédias n’est définie.</span><span class="sxs-lookup"><span data-stu-id="c4c93-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="c4c93-133">Si l’élément multimédia n’est pas chiffré dans le stockage, le système vous permet de créer un localisateur et de diffuser en continu l’élément multimédia en clair sans stratégie de distribution d’éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="c4c93-133">If the Asset isn’t storage encrypted, the system will let you create a locator and stream the asset in the clear without an asset delivery policy.</span></span>
* <span data-ttu-id="c4c93-134">Vous pouvez avoir plusieurs stratégies de distribution d’éléments multimédias associées à un même élément multimédia, mais vous ne pouvez spécifier qu’une seule façon de traiter un AssetDeliveryProtocol donné.</span><span class="sxs-lookup"><span data-stu-id="c4c93-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way to handle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="c4c93-135">Cela signifie que si vous essayez de lier deux stratégies de distribution qui spécifient le protocole AssetDeliveryProtocol.SmoothStreaming, cela va générer une erreur, car le système ne sait pas laquelle appliquer quand un client émet une demande Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c4c93-135">Meaning if you try to link two delivery policies that specify the AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because the system does not know which one you want it to apply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="c4c93-136">Si vous avez un élément multimédia avec un localisateur de diffusion en continu existant, vous ne pouvez pas lier une nouvelle stratégie à l’élément multimédia. supprimer le lien d’une stratégie existante de l’élément multimédia ou mettre à jour une stratégie de distribution associée à l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="c4c93-136">If you have an asset with an existing streaming locator, you cannot link a new policy to the asset, unlink an existing policy from the asset, or update a delivery policy associated with the asset.</span></span>  <span data-ttu-id="c4c93-137">Vous devez d’abord supprimer le localisateur de diffusion en continu, ajuster les stratégies, puis recréer le localisateur de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="c4c93-137">You first have to remove the streaming locator, adjust the policies, and then re-create the streaming locator.</span></span>  <span data-ttu-id="c4c93-138">Vous pouvez utiliser le même ID de localisateur (locatorId) quand vous recréez le localisateur de diffusion en continu. Vous devez cependant vérifier que cela ne crée pas de problèmes pour les clients, car le contenu peut être mis en cache par l’origine ou un CDN en aval.</span><span class="sxs-lookup"><span data-stu-id="c4c93-138">You can use the same locatorId when you recreate the streaming locator but you should ensure that won’t cause issues for clients since content can be cached by the origin or a downstream CDN.</span></span>

>[!NOTE]

><span data-ttu-id="c4c93-139">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="c4c93-139">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="c4c93-140">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c4c93-140">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="c4c93-141">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="c4c93-141">Connect to Media Services</span></span>

<span data-ttu-id="c4c93-142">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="c4c93-142">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="c4c93-143">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="c4c93-143">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="c4c93-144">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="c4c93-144">You must make subsequent calls to the new URI.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="c4c93-145">Stratégie de remise de ressources</span><span class="sxs-lookup"><span data-stu-id="c4c93-145">Clear asset delivery policy</span></span>
### <span data-ttu-id="c4c93-146"><a id="create_asset_delivery_policy"></a>Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="c4c93-146"><a id="create_asset_delivery_policy"></a>Create asset delivery policy</span></span>
<span data-ttu-id="c4c93-147">La requête HTTP suivante permet de créer une stratégie de remise d’éléments multimédias qui précise de ne pas appliquer de chiffrement dynamique et de fournir le flux avec l’un des protocoles suivants : MPEG DASH, HLS et Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="c4c93-147">The following HTTP request creates an asset delivery policy that specifies to not apply dynamic encryption and to deliver the stream in any of the following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> 

<span data-ttu-id="c4c93-148">Pour plus d'informations sur les valeurs que vous pouvez spécifier au moment de la création d'une AssetDeliveryPolicy, consultez la section [Types utilisés au moment de la définition d'AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="c4c93-148">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="c4c93-149">Demande :</span><span class="sxs-lookup"><span data-stu-id="c4c93-149">Request:</span></span>

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

<span data-ttu-id="c4c93-150">Réponse :</span><span class="sxs-lookup"><span data-stu-id="c4c93-150">Response:</span></span>

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

### <span data-ttu-id="c4c93-151"><a id="link_asset_with_asset_delivery_policy"></a>Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="c4c93-151"><a id="link_asset_with_asset_delivery_policy"></a>Link asset with asset delivery policy</span></span>
<span data-ttu-id="c4c93-152">La demande HTTP suivante lie la ressource spécifiée à la stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-152">The following HTTP request links the specified asset to the asset delivery policy to.</span></span>

<span data-ttu-id="c4c93-153">Demande :</span><span class="sxs-lookup"><span data-stu-id="c4c93-153">Request:</span></span>

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

<span data-ttu-id="c4c93-154">Réponse :</span><span class="sxs-lookup"><span data-stu-id="c4c93-154">Response:</span></span>

    HTTP/1.1 204 No Content


## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="c4c93-155">Stratégie de remise de ressources DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="c4c93-155">DynamicEnvelopeEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-envelopeencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="c4c93-156">Création de la clé de contenu de type EnvelopeEncryption et liaison à la ressource</span><span class="sxs-lookup"><span data-stu-id="c4c93-156">Create content key of the EnvelopeEncryption type and link it to the asset</span></span>
<span data-ttu-id="c4c93-157">Lorsque vous spécifiez la stratégie de remise DynamicEnvelopeEncryption, vous devez veiller à lier votre ressource à une clé de contenu de type EnvelopeEncryption.</span><span class="sxs-lookup"><span data-stu-id="c4c93-157">When specifying DynamicEnvelopeEncryption delivery policy, you need to make sure to link your asset to a content key of the EnvelopeEncryption type.</span></span> <span data-ttu-id="c4c93-158">Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="c4c93-158">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <span data-ttu-id="c4c93-159"><a id="get_delivery_url"></a>Obtention de l’URL de remise</span><span class="sxs-lookup"><span data-stu-id="c4c93-159"><a id="get_delivery_url"></a>Get delivery URL</span></span>
<span data-ttu-id="c4c93-160">Obtenez l’URL de remise pour la méthode de remise spécifiée de la clé de contenu créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c4c93-160">Get the delivery URL for the specified delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="c4c93-161">Un client utilise l’URL retournée pour demander une clé AES ou une licence PlayReady afin de lire le contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="c4c93-161">A client uses the returned URL to request an AES key or a PlayReady license in order to playback the protected content.</span></span>

<span data-ttu-id="c4c93-162">Spécifiez le type d’URL à obtenir dans le corps de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="c4c93-162">Specify the type of the URL to get in the body of the HTTP request.</span></span> <span data-ttu-id="c4c93-163">Si vous protégez votre contenu avec PlayReady, demandez une URL d’acquisition de licence PlayReady Media Services, en utilisant 1 pour keyDeliveryType : {"keyDeliveryType":1}.</span><span class="sxs-lookup"><span data-stu-id="c4c93-163">If you are protecting your content with PlayReady, request a Media Services PlayReady license acquisition URL, using 1 for the keyDeliveryType: {"keyDeliveryType":1}.</span></span> <span data-ttu-id="c4c93-164">Si vous protégez votre contenu avec le chiffrement d’enveloppe, demandez une URL d’acquisition de clé en spécifiant 2 pour keyDeliveryType :{"keyDeliveryType":2}.</span><span class="sxs-lookup"><span data-stu-id="c4c93-164">If you are protecting your content with the envelope encryption, request a key acquisition URL by specifying 2 for keyDeliveryType: {"keyDeliveryType":2}.</span></span>

<span data-ttu-id="c4c93-165">Demande :</span><span class="sxs-lookup"><span data-stu-id="c4c93-165">Request:</span></span>

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

<span data-ttu-id="c4c93-166">Réponse :</span><span class="sxs-lookup"><span data-stu-id="c4c93-166">Response:</span></span>

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


### <a name="create-asset-delivery-policy"></a><span data-ttu-id="c4c93-167">Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="c4c93-167">Create asset delivery policy</span></span>
<span data-ttu-id="c4c93-168">La demande HTTP suivante crée la stratégie **AssetDeliveryPolicy** configurée pour appliquer le chiffrement dynamique en enveloppe (**DynamicEnvelopeEncryption**) au protocole **HLS** (dans cet exemple, les autres protocoles ne pourront pas être diffusés en continu).</span><span class="sxs-lookup"><span data-stu-id="c4c93-168">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic envelope encryption (**DynamicEnvelopeEncryption**) to the **HLS** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="c4c93-169">Pour plus d'informations sur les valeurs que vous pouvez spécifier au moment de la création d'une AssetDeliveryPolicy, consultez la section [Types utilisés au moment de la définition d'AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="c4c93-169">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="c4c93-170">Demande :</span><span class="sxs-lookup"><span data-stu-id="c4c93-170">Request:</span></span>

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


<span data-ttu-id="c4c93-171">Réponse :</span><span class="sxs-lookup"><span data-stu-id="c4c93-171">Response:</span></span>

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


### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="c4c93-172">Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="c4c93-172">Link asset with asset delivery policy</span></span>
<span data-ttu-id="c4c93-173">Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="c4c93-173">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="c4c93-174">Stratégie de remise de ressources DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="c4c93-174">DynamicCommonEncryption asset delivery policy</span></span>
### <a name="create-content-key-of-the-commonencryption-type-and-link-it-to-the-asset"></a><span data-ttu-id="c4c93-175">Création de la clé de contenu de type CommonEncryption et liaison à la ressource</span><span class="sxs-lookup"><span data-stu-id="c4c93-175">Create content key of the CommonEncryption type and link it to the asset</span></span>
<span data-ttu-id="c4c93-176">Lorsque vous spécifiez la stratégie de remise DynamicCommonEncryption, vous devez veiller à lier votre ressource à une clé de contenu de type CommonEncryption.</span><span class="sxs-lookup"><span data-stu-id="c4c93-176">When specifying DynamicCommonEncryption delivery policy, you need to make sure to link your asset to a content key of the CommonEncryption type.</span></span> <span data-ttu-id="c4c93-177">Pour plus d’informations, consultez la page [Création d’une clé de contenu](media-services-rest-create-contentkey.md)).</span><span class="sxs-lookup"><span data-stu-id="c4c93-177">For more information, see: [Creating a content key](media-services-rest-create-contentkey.md)).</span></span>

### <a name="get-delivery-url"></a><span data-ttu-id="c4c93-178">Obtention de l’URL de remise</span><span class="sxs-lookup"><span data-stu-id="c4c93-178">Get Delivery URL</span></span>
<span data-ttu-id="c4c93-179">Obtenez l’URL de remise pour la méthode de remise PlayReady de la clé de contenu créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c4c93-179">Get the delivery URL for the PlayReady delivery method of the content key created in the previous step.</span></span> <span data-ttu-id="c4c93-180">Un client utilise l’URL retournée pour demander une licence PlayReady afin de lire le contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="c4c93-180">A client uses the returned URL to request a PlayReady license in order to playback the protected content.</span></span> <span data-ttu-id="c4c93-181">Pour plus d’informations, consultez la rubrique [Obtention de l’URL de remise](#get_delivery_url).</span><span class="sxs-lookup"><span data-stu-id="c4c93-181">For more information, see [Get Delivery URL](#get_delivery_url).</span></span>

### <a name="create-asset-delivery-policy"></a><span data-ttu-id="c4c93-182">Création d’une stratégie de remise d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="c4c93-182">Create asset delivery policy</span></span>
<span data-ttu-id="c4c93-183">La demande HTTP suivante crée la stratégie **AssetDeliveryPolicy** configurée pour appliquer le chiffrement dynamique commun (**DynamicCommonEncryption**) au protocole **Smooth Streaming** (dans cet exemple, les autres protocoles ne pourront pas être diffusés en continu).</span><span class="sxs-lookup"><span data-stu-id="c4c93-183">The following HTTP request creates the **AssetDeliveryPolicy** that is configured to apply dynamic common encryption (**DynamicCommonEncryption**) to the **Smooth Streaming** protocol (in this example, other protocols will be blocked from streaming).</span></span> 

<span data-ttu-id="c4c93-184">Pour plus d'informations sur les valeurs que vous pouvez spécifier au moment de la création d'une AssetDeliveryPolicy, consultez la section [Types utilisés au moment de la définition d'AssetDeliveryPolicy](#types) .</span><span class="sxs-lookup"><span data-stu-id="c4c93-184">For information on what values you can specify when creating an AssetDeliveryPolicy, see the [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

<span data-ttu-id="c4c93-185">Demande :</span><span class="sxs-lookup"><span data-stu-id="c4c93-185">Request:</span></span>

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


<span data-ttu-id="c4c93-186">Si vous souhaitez protéger votre contenu à l’aide de Widevine DRM, mettez à jour les valeurs AssetDeliveryConfiguration pour utiliser WidevineLicenseAcquisitionUrl (dont la valeur est 7) et indiquez l’URL d’un service de remise de licence.</span><span class="sxs-lookup"><span data-stu-id="c4c93-186">If you want to protect your content using Widevine DRM, update the AssetDeliveryConfiguration values to use WidevineLicenseAcquisitionUrl (which has the value of 7) and specify the URL of a license delivery service.</span></span> <span data-ttu-id="c4c93-187">Vous pouvez utiliser les partenaires AMS suivants pour vous aider à fournir des licences Widevine : [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="c4c93-187">You can use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="c4c93-188">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c4c93-188">For example:</span></span> 

    {"Name":"AssetDeliveryPolicy","AssetDeliveryProtocol":2,"AssetDeliveryPolicyType":4,"AssetDeliveryConfiguration":"[{\"Key\":7,\"Value\":\"https:\\/\\/example.net\/WidevineLicenseAcquisition\/"}]"}

> [!NOTE]
> <span data-ttu-id="c4c93-189">Lors du chiffrement avec Widevine, vous ne pourriez effectuer une remise qu’avec DASH.</span><span class="sxs-lookup"><span data-stu-id="c4c93-189">When encrypting with Widevine, you would only be able to deliver using DASH.</span></span> <span data-ttu-id="c4c93-190">Veillez à spécifier DASH (2) dans le protocole de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-190">Make sure to specify DASH (2) in the asset delivery protocol.</span></span>
> 
> 

### <a name="link-asset-with-asset-delivery-policy"></a><span data-ttu-id="c4c93-191">Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia</span><span class="sxs-lookup"><span data-stu-id="c4c93-191">Link asset with asset delivery policy</span></span>
<span data-ttu-id="c4c93-192">Consultez la rubrique [Liaison d’un élément multimédia à la stratégie de remise d’élément multimédia](#link_asset_with_asset_delivery_policy)</span><span class="sxs-lookup"><span data-stu-id="c4c93-192">See [Link asset with asset delivery policy](#link_asset_with_asset_delivery_policy)</span></span>

## <span data-ttu-id="c4c93-193"><a id="types"></a>Types utilisés durant la définition de AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="c4c93-193"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <a name="assetdeliveryprotocol"></a><span data-ttu-id="c4c93-194">AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="c4c93-194">AssetDeliveryProtocol</span></span>

<span data-ttu-id="c4c93-195">La valeur d’énumération suivante décrit les valeurs que vous pouvez définir pour le protocole de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-195">The following enum describes values you can set for the asset delivery protocol.</span></span>

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

### <a name="assetdeliverypolicytype"></a><span data-ttu-id="c4c93-196">AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="c4c93-196">AssetDeliveryPolicyType</span></span>

<span data-ttu-id="c4c93-197">La valeur d’énumération suivante décrit les valeurs que vous pouvez définir pour le type de protocole de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-197">The following enum describes values you can set for the asset delivery policy type.</span></span>  

    public enum AssetDeliveryPolicyType
    {
        /// <summary>
        /// Delivery Policy Type not set.  An invalid value.
        /// </summary>
        None,

        /// <summary>
        /// The Asset should not be delivered via this AssetDeliveryProtocol. 
        /// </summary>
        Blocked, 

        /// <summary>
        /// Do not apply dynamic encryption to the asset.
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

### <a name="contentkeydeliverytype"></a><span data-ttu-id="c4c93-198">ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="c4c93-198">ContentKeyDeliveryType</span></span>

<span data-ttu-id="c4c93-199">La valeur d’énumération suivante décrit les valeurs que vous pouvez utiliser pour configurer la méthode de remise de la clé de contenu au client.</span><span class="sxs-lookup"><span data-stu-id="c4c93-199">The following enum describes values you can use to configure the delivery method of the content key to the client.</span></span>
    
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


### <a name="assetdeliverypolicyconfigurationkey"></a><span data-ttu-id="c4c93-200">AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="c4c93-200">AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="c4c93-201">La valeur d’énumération suivante décrit les valeurs que vous pouvez définir pour configurer les clés utilisées pour obtenir une configuration spécifique pour une stratégie de remise de ressources.</span><span class="sxs-lookup"><span data-stu-id="c4c93-201">The following enum describes values you can set to configure keys used to get specific configuration for an asset delivery policy.</span></span>

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
        /// The initialization vector to use for envelope encryption in Base64 format.
        /// </summary>
        EnvelopeEncryptionIVAsBase64,

        /// <summary>
        /// The PlayReady License Acquisition Url to use for common encryption.
        /// </summary>
        PlayReadyLicenseAcquisitionUrl,

        /// <summary>
        /// The PlayReady Custom Attributes to add to the PlayReady Content Header
        /// </summary>
        PlayReadyCustomAttributes,

        /// <summary>
        /// The initialization vector to use for envelope encryption.
        /// </summary>
        EnvelopeEncryptionIV,

        /// <summary>
        /// Widevine DRM acquisition url
        /// </summary>
        WidevineLicenseAcquisitionUrl
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="c4c93-202">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c4c93-202">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4c93-203">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="c4c93-203">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

