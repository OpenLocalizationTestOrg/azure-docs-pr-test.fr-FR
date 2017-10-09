---
title: "stratégies de remise aaaConfigure actif avec le Kit de développement .NET | Documents Microsoft"
description: "Cette rubrique montre comment les stratégies tooconfigure asset différents remise avec Azure Media Services .NET SDK."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 3ec46f58-6cbb-4d49-bac6-1fd01a5a456b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/13/2017
ms.author: juliako;mingfeiy
ms.openlocfilehash: a6f2644d639cd36d4cdc269b6f01fd4acdf7160b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-asset-delivery-policies-with-net-sdk"></a><span data-ttu-id="ba3c3-103">Configuration de stratégies de remise de ressources à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="ba3c3-103">Configure asset delivery policies with .NET SDK</span></span>
[!INCLUDE [media-services-selector-asset-delivery-policy](../../includes/media-services-selector-asset-delivery-policy.md)]

## <a name="overview"></a><span data-ttu-id="ba3c3-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ba3c3-104">Overview</span></span>
<span data-ttu-id="ba3c3-105">Si vous envisagez toodelivery chiffré actifs, une des hello étapes Bonjour Media Services de contenu de flux de travail de remise consiste à configurer des stratégies de remise pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-105">If you plan toodelivery encrypted assets, one of hello steps in hello Media Services content delivery workflow is configuring delivery policies for assets.</span></span> <span data-ttu-id="ba3c3-106">stratégie de livraison des actifs Hello indique comment vous souhaitez pour votre toobe asset remis à Media Services : dans le protocole de diffusion en continu doit votre élément multimédia dynamiquement packagé (par exemple, MPEG DASH, HLS, Smooth Streaming ou tous), vous souhaitez toodynamically ou non chiffrer votre élément multimédia et comment (enveloppe ou chiffrement commun).</span><span class="sxs-lookup"><span data-stu-id="ba3c3-106">hello asset delivery policy tells Media Services how you want for your asset toobe delivered: into which streaming protocol should your asset be dynamically packaged (for example, MPEG DASH, HLS, Smooth Streaming, or all), whether or not you want toodynamically encrypt your asset and how (envelope or common encryption).</span></span>

<span data-ttu-id="ba3c3-107">Cette rubrique explique pourquoi et comment toocreate et configurer des stratégies de remise d’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-107">This topic discusses why and how toocreate and configure asset delivery policies.</span></span>

>[!NOTE]
><span data-ttu-id="ba3c3-108">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-108">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="ba3c3-109">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-109">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 
>
><span data-ttu-id="ba3c3-110">En outre, toobe toouse en mesure de mise en package dynamique et le chiffrement dynamique votre élément multimédia doit contenir un ensemble de fichiers à débit adaptatif MP4s ou des fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-110">Also, toobe able toouse dynamic packaging and dynamic encryption your asset must contain a set of adaptive bitrate MP4s or adaptive bitrate Smooth Streaming files.</span></span>


<span data-ttu-id="ba3c3-111">Vous pouvez appliquer différentes stratégies toohello même actif.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-111">You could apply different policies toohello same asset.</span></span> <span data-ttu-id="ba3c3-112">Par exemple, vous pouvez appliquer PlayReady chiffrement tooSmooth diffusion en continu et l’enveloppe AES chiffrement tooMPEG DASH et HLS.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-112">For example, you could apply PlayReady encryption tooSmooth Streaming and AES Envelope encryption tooMPEG DASH and HLS.</span></span> <span data-ttu-id="ba3c3-113">Tous les protocoles qui ne sont pas définis dans une stratégie de remise (par exemple, vous ajoutez une stratégie unique qui spécifie seulement le HLS en tant que protocole de hello) sera bloquée à partir de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-113">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="ba3c3-114">Hello exception toothis est si vous ne disposez d’aucune stratégie de remise actif du tout défini.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-114">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="ba3c3-115">Ensuite, tous les protocoles seront autorisés en hello clair.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-115">Then, all protocols will be allowed in hello clear.</span></span>

<span data-ttu-id="ba3c3-116">Si vous voulez toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de l’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-116">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="ba3c3-117">Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-117">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="ba3c3-118">Par exemple, toodeliver votre élément multimédia chiffré avec la clé de chiffrement d’enveloppe Standard (AES), définissez le type de stratégie hello trop**DynamicEnvelopeEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-118">For example, toodeliver your asset encrypted with Advanced Encryption Standard (AES) envelope encryption key, set hello policy type too**DynamicEnvelopeEncryption**.</span></span> <span data-ttu-id="ba3c3-119">tooremove le chiffrement de stockage et les actifs de hello flux Bonjour claires, le type de stratégie hello défini trop**NoDynamicEncryption**.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-119">tooremove storage encryption and stream hello asset in hello clear, set hello policy type too**NoDynamicEncryption**.</span></span> <span data-ttu-id="ba3c3-120">Exemples qui montrent comment tooconfigure suivent ces types de stratégie.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-120">Examples that show how tooconfigure these policy types follow.</span></span>

<span data-ttu-id="ba3c3-121">Selon la façon dont vous configurez la stratégie de livraison des actifs hello vous serait sera en mesure de toodynamically package, dynamiquement chiffrer et diffuser en continu hello suite de protocoles de diffusion en continu : flux de diffusion en continu lisse, HLS et MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-121">Depending on how you configure hello asset delivery policy you would be able toodynamically package, dynamically encrypt, and stream hello following streaming protocols: Smooth Streaming, HLS, and MPEG DASH streams.</span></span>

<span data-ttu-id="ba3c3-122">Hello liste suivante présente les formats hello que vous utilisez toostream Smooth, HLS et DASH.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-122">hello following list shows hello formats that you use toostream Smooth, HLS, and DASH.</span></span>

<span data-ttu-id="ba3c3-123">Smooth Streaming :</span><span class="sxs-lookup"><span data-stu-id="ba3c3-123">Smooth Streaming:</span></span>

<span data-ttu-id="ba3c3-124">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest</span><span class="sxs-lookup"><span data-stu-id="ba3c3-124">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest</span></span>

<span data-ttu-id="ba3c3-125">HLS :</span><span class="sxs-lookup"><span data-stu-id="ba3c3-125">HLS:</span></span>

<span data-ttu-id="ba3c3-126">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=m3u8-aapl)</span><span class="sxs-lookup"><span data-stu-id="ba3c3-126">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)</span></span>

<span data-ttu-id="ba3c3-127">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="ba3c3-127">MPEG DASH</span></span>

<span data-ttu-id="ba3c3-128">{nom du point de terminaison de diffusion en continu-nom du compte media services}.streaming.mediaservices.windows.net/{ID_de_localisateur}/{nom_de_fichier}.ISM/Manifest(format=mpd-time-csf)</span><span class="sxs-lookup"><span data-stu-id="ba3c3-128">{streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)</span></span>


## <a name="considerations"></a><span data-ttu-id="ba3c3-129">Considérations</span><span class="sxs-lookup"><span data-stu-id="ba3c3-129">Considerations</span></span>
* <span data-ttu-id="ba3c3-130">Vous ne pouvez pas supprimer une stratégie AssetDeliveryPolicy associée à un élément multimédia alors qu’un localisateur (de diffusion en continuer) OnDemand existe pour cet élément.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-130">You cannot delete an AssetDeliveryPolicy associated with an asset while an OnDemand (streaming) locator exists for that asset.</span></span> <span data-ttu-id="ba3c3-131">stratégie de hello tooremove à partir de l’élément multimédia de hello il est recommandé de Hello avant de supprimer la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-131">hello recommendation is tooremove hello policy from hello asset before deleting hello policy.</span></span>
* <span data-ttu-id="ba3c3-132">Il est impossible de créer un localisateur de diffusion en continu sur un élément multimédia chiffré de stockage quand aucune stratégie de distribution d’éléments multimédias n’est définie.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-132">A streaming locator cannot be created on a storage encrypted asset when no asset delivery policy is set.</span></span>  <span data-ttu-id="ba3c3-133">Si hello actif n’est pas chiffré de stockage, système de hello sera vous permettent de créer un élément multimédia hello de recherche et de flux Bonjour effacer sans une stratégie de livraison des actifs.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-133">If hello Asset isn’t storage encrypted, hello system will let you create a locator and stream hello asset in hello clear without an asset delivery policy.</span></span>
* <span data-ttu-id="ba3c3-134">Vous pouvez avoir plusieurs stratégies de remise actif associés à un seul élément multimédia, mais vous ne pouvez spécifier qu’une façon toohandle un AssetDeliveryProtocol donné.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-134">You can have multiple asset delivery policies associated with a single asset but you can only specify one way toohandle a given AssetDeliveryProtocol.</span></span>  <span data-ttu-id="ba3c3-135">Ce qui signifie que si vous essayez de toolink deux stratégies de remise qui spécifient le protocole AssetDeliveryProtocol.SmoothStreaming hello qui entraîne une erreur car le système de hello ne sait pas celui que vous souhaitez tooapply lorsqu’un client effectue une demande de diffusion en continu lisse.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-135">Meaning if you try toolink two delivery policies that specify hello AssetDeliveryProtocol.SmoothStreaming protocol that will result in an error because hello system does not know which one you want it tooapply when a client makes a Smooth Streaming request.</span></span>
* <span data-ttu-id="ba3c3-136">Si vous avez un élément multimédia avec un localisateur de diffusion en continu, vous ne peut pas lier un nouveau composant toohello de stratégie (vous pouvez supprimer le lien d’une stratégie existante à partir de l’élément multimédia de hello, ou mettre à jour une stratégie de remise associée hello actif).</span><span class="sxs-lookup"><span data-stu-id="ba3c3-136">If you have an asset with an existing streaming locator, you cannot link a new policy toohello asset (you can either unlink an existing policy from hello asset, or update a delivery policy associated with hello asset).</span></span>  <span data-ttu-id="ba3c3-137">Vous tout d’abord avez localisateur de diffusion en continu tooremove hello, ajustez les stratégies de hello, puis recréez hello localisateur de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-137">You first have tooremove hello streaming locator, adjust hello policies, and then re-create hello streaming locator.</span></span>  <span data-ttu-id="ba3c3-138">Vous pouvez utiliser hello locatorId même lorsque vous recréez hello de diffusion en continu de la recherche, mais vous devez vous assurer que causer des problèmes pour les clients, car le contenu peut être mis en cache à l’origine de hello ou un CDN en aval.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-138">You can use hello same locatorId when you recreate hello streaming locator but you should ensure that won’t cause issues for clients since content can be cached by hello origin or a downstream CDN.</span></span>

## <a name="clear-asset-delivery-policy"></a><span data-ttu-id="ba3c3-139">Stratégie de remise de ressources</span><span class="sxs-lookup"><span data-stu-id="ba3c3-139">Clear asset delivery policy</span></span>

<span data-ttu-id="ba3c3-140">suivant de Hello **ConfigureClearAssetDeliveryPolicy** méthode spécifie toonot appliquer le chiffrement dynamique et de protocoles de flux de données toodeliver hello dans un des hello suivant : protocoles MPEG DASH, HLS et Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-140">hello following **ConfigureClearAssetDeliveryPolicy** method specifies toonot apply dynamic encryption and toodeliver hello stream in any of hello following protocols:  MPEG DASH, HLS, and Smooth Streaming protocols.</span></span> <span data-ttu-id="ba3c3-141">Vous pourriez tooapply des ressources de stockage chiffrée cette tooyour stratégie.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-141">You might want tooapply this policy tooyour storage encrypted assets.</span></span>

<span data-ttu-id="ba3c3-142">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-142">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void ConfigureClearAssetDeliveryPolicy(IAsset asset)
    {
        IAssetDeliveryPolicy policy =
        _context.AssetDeliveryPolicies.Create("Clear Policy",
        AssetDeliveryPolicyType.NoDynamicEncryption,
        AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.Dash, null);
        
        asset.DeliveryPolicies.Add(policy);
    }

## <a name="dynamiccommonencryption-asset-delivery-policy"></a><span data-ttu-id="ba3c3-143">Stratégie de remise de ressources DynamicCommonEncryption</span><span class="sxs-lookup"><span data-stu-id="ba3c3-143">DynamicCommonEncryption asset delivery policy</span></span>

<span data-ttu-id="ba3c3-144">suivant de Hello **CreateAssetDeliveryPolicy** méthode crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement commun dynamique (**DynamicCommonEncryption**) tooa (les autres protocoles seront bloqués à partir de la diffusion en continu) de protocole de diffusion en continu lisse.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-144">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic common encryption (**DynamicCommonEncryption**) tooa smooth streaming protocol (other protocols will be blocked from streaming).</span></span> <span data-ttu-id="ba3c3-145">méthode Hello accepte deux paramètres : **Asset** (hello toowhich asset tooapply hello remise stratégie) et **IContentKey** (clé de contenu hello Hello **CommonEncryption**de type, pour plus d’informations, consultez : [création d’une clé de contenu](media-services-dotnet-create-contentkey.md#common_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ba3c3-145">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **CommonEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#common_contentkey)).</span></span>

<span data-ttu-id="ba3c3-146">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-146">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);
        
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
                new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            };
    
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                    "AssetDeliveryPolicy",
                AssetDeliveryPolicyType.DynamicCommonEncryption,
                AssetDeliveryProtocol.SmoothStreaming,
                assetDeliveryPolicyConfiguration);
    
            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);
    
            Console.WriteLine();
            Console.WriteLine("Adding Asset Delivery Policy: " +
                assetDeliveryPolicy.AssetDeliveryPolicyType);
     }

<span data-ttu-id="ba3c3-147">Azure Media Services vous permet également le chiffrement Widevine tooadd.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-147">Azure Media Services also enables you tooadd Widevine encryption.</span></span> <span data-ttu-id="ba3c3-148">Hello exemple suivant illustre PlayReady et Widevine ajouté toohello stratégie de livraison des actifs.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-148">hello following example demonstrates both PlayReady and Widevine being added toohello asset delivery policy.</span></span>

    static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {
        // Get hello PlayReady license service URL.
        Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);


        // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
        // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
        // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption 
        // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
        // As a result Widevine license acquisition URL will have KID appended twice, 
        // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

        Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
        UriBuilder uriBuilder = new UriBuilder(widevineUrl);
        uriBuilder.Query = String.Empty;
        widevineUrl = uriBuilder.Uri;

        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
        {
            {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
            {AssetDeliveryPolicyConfigurationKey.WidevineLicenseAcquisitionUrl, widevineUrl.ToString()}

        };

        var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

    }

> [!NOTE]
> <span data-ttu-id="ba3c3-149">Lors du chiffrement avec Widevine, vous serez uniquement en mesure de toodeliver à l’aide de tiret.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-149">When encrypting with Widevine, you would only be able toodeliver using DASH.</span></span> <span data-ttu-id="ba3c3-150">Assurez-vous que toospecify tiret dans le protocole de livraison hello actif.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-150">Make sure toospecify DASH in hello asset delivery protocol.</span></span>
> 
> 

## <a name="dynamicenvelopeencryption-asset-delivery-policy"></a><span data-ttu-id="ba3c3-151">Stratégie de remise de ressources DynamicEnvelopeEncryption</span><span class="sxs-lookup"><span data-stu-id="ba3c3-151">DynamicEnvelopeEncryption asset delivery policy</span></span>
<span data-ttu-id="ba3c3-152">suivant de Hello **CreateAssetDeliveryPolicy** méthode crée hello **AssetDeliveryPolicy** tooapply configuré qui est le chiffrement dynamique enveloppe (**DynamicEnvelopeEncryption** ) protocoles de diffusion en continu, HLS et DASH tooSmooth (si vous décidez de toonot spécifier certains protocoles, ils seront bloqués à partir de la diffusion en continu).</span><span class="sxs-lookup"><span data-stu-id="ba3c3-152">hello following **CreateAssetDeliveryPolicy** method creates hello **AssetDeliveryPolicy** that is configured tooapply dynamic envelope encryption (**DynamicEnvelopeEncryption**) tooSmooth Streaming, HLS, and DASH protocols (if you decide toonot specify some protocols, they will be blocked from streaming).</span></span> <span data-ttu-id="ba3c3-153">méthode Hello accepte deux paramètres : **Asset** (hello toowhich asset tooapply hello remise stratégie) et **IContentKey** (clé de contenu hello Hello **EnvelopeEncryption**de type, pour plus d’informations, consultez : [création d’une clé de contenu](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span><span class="sxs-lookup"><span data-stu-id="ba3c3-153">hello method takes two parameters : **Asset** (hello asset toowhich you want tooapply hello delivery policy) and **IContentKey** (hello content key of hello **EnvelopeEncryption** type, for more information, see: [Creating a content key](media-services-dotnet-create-contentkey.md#envelope_contentkey)).</span></span>

<span data-ttu-id="ba3c3-154">Pour plus d’informations sur les valeurs que vous pouvez spécifier lors de la création d’un AssetDeliveryPolicy, consultez hello [Types utilisés lors de la définition AssetDeliveryPolicy](#types) section.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-154">For information on what values you can specify when creating an AssetDeliveryPolicy, see hello [Types used when defining AssetDeliveryPolicy](#types) section.</span></span>   

    private static void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
    {

        //  Get hello Key Delivery Base Url by removing hello Query parameter.  hello Dynamic Encryption service will
        //  automatically add hello correct key identifier toohello url when it generates hello Envelope encrypted content
        //  manifest.  Omitting hello IV will also cause hello Dynamice Encryption service toogenerate a deterministic
        //  IV for hello content automatically.  By using hello EnvelopeBaseKeyAcquisitionUrl and omitting hello IV, this
        //  allows hello AssetDelivery policy toobe reused by more than one asset.
        //
        Uri keyAcquisitionUri = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.BaselineHttp);
        UriBuilder uriBuilder = new UriBuilder(keyAcquisitionUri);
        uriBuilder.Query = String.Empty;
        keyAcquisitionUri = uriBuilder.Uri;

        // hello following policy configuration specifies: 
        //   key url that will have KID=<Guid> appended toohello envelope and
        //   hello Initialization Vector (IV) toouse for hello envelope encryption.
        Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string> 
        {
            {AssetDeliveryPolicyConfigurationKey.EnvelopeBaseKeyAcquisitionUrl, keyAcquisitionUri.ToString()},
        };

        IAssetDeliveryPolicy assetDeliveryPolicy =
            _context.AssetDeliveryPolicies.Create(
                        "AssetDeliveryPolicy",
                        AssetDeliveryPolicyType.DynamicEnvelopeEncryption,
                        AssetDeliveryProtocol.SmoothStreaming | AssetDeliveryProtocol.HLS | AssetDeliveryProtocol.Dash,
                        assetDeliveryPolicyConfiguration);

        // Add AssetDelivery Policy toohello asset
        asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        Console.WriteLine();
        Console.WriteLine("Adding Asset Delivery Policy: " + assetDeliveryPolicy.AssetDeliveryPolicyType);
    }


## <span data-ttu-id="ba3c3-155"><a id="types"></a>Types utilisés durant la définition de AssetDeliveryPolicy</span><span class="sxs-lookup"><span data-stu-id="ba3c3-155"><a id="types"></a>Types used when defining AssetDeliveryPolicy</span></span>

### <span data-ttu-id="ba3c3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span><span class="sxs-lookup"><span data-stu-id="ba3c3-156"><a id="AssetDeliveryProtocol"></a>AssetDeliveryProtocol</span></span>

<span data-ttu-id="ba3c3-157">Hello enum suivant décrit les valeurs que vous pouvez définir pour le protocole de remise hello actif.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-157">hello following enum describes values you can set for hello asset delivery protocol.</span></span>

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

### <span data-ttu-id="ba3c3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span><span class="sxs-lookup"><span data-stu-id="ba3c3-158"><a id="AssetDeliveryPolicyType"></a>AssetDeliveryPolicyType</span></span>

<span data-ttu-id="ba3c3-159">Hello enum suivant décrit les valeurs que vous pouvez définir pour le type de stratégie de remise hello asset.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-159">hello following enum describes values you can set for hello asset delivery policy type.</span></span>  

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

### <span data-ttu-id="ba3c3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="ba3c3-160"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>

<span data-ttu-id="ba3c3-161">Hello enum suivant décrit les valeurs que vous pouvez utiliser la méthode de remise tooconfigure hello du client de contenu toohello clé hello.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-161">hello following enum describes values you can use tooconfigure hello delivery method of hello content key toohello client.</span></span>
    
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

### <span data-ttu-id="ba3c3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span><span class="sxs-lookup"><span data-stu-id="ba3c3-162"><a id="AssetDeliveryPolicyConfigurationKey"></a>AssetDeliveryPolicyConfigurationKey</span></span>

<span data-ttu-id="ba3c3-163">Hello suivant enum décrit les valeurs que vous pouvez définir la configuration spécifique du tooget tooconfigure clés utilisées pour une stratégie de livraison des actifs.</span><span class="sxs-lookup"><span data-stu-id="ba3c3-163">hello following enum describes values you can set tooconfigure keys used tooget specific configuration for an asset delivery policy.</span></span>

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="ba3c3-164">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ba3c3-164">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ba3c3-165">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ba3c3-165">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

