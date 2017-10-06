---
title: "contenu d’Azure Media Services aaaPublish à l’aide de .NET | Documents Microsoft"
description: "Découvrez comment toocreate un localisateur de toobuild utilisé une URL de diffusion en continu. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: c53b1f83-4cb1-4b09-840f-9c145b7d6f8d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: c941cd93c252a96e66546cce2793bb426afac059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-azure-media-services-content-using-net"></a><span data-ttu-id="ee550-104">Publier du contenu Azure Media Services à l’aide de .NET</span><span class="sxs-lookup"><span data-stu-id="ee550-104">Publish Azure Media Services content using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee550-105">REST</span><span class="sxs-lookup"><span data-stu-id="ee550-105">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> * [<span data-ttu-id="ee550-106">.NET</span><span class="sxs-lookup"><span data-stu-id="ee550-106">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="ee550-107">Portail</span><span class="sxs-lookup"><span data-stu-id="ee550-107">Portal</span></span>](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ee550-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ee550-108">Overview</span></span>
<span data-ttu-id="ee550-109">Vous pouvez diffuser un MP4 à débit adaptatif défini par la création d’un localisateur de diffusion en continu à la demande et la création d’une URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="ee550-109">You can stream an adaptive bitrate MP4 set by creating an OnDemand streaming locator and building a streaming URL.</span></span> <span data-ttu-id="ee550-110">Hello [encodage d’un élément multimédia](media-services-encode-asset.md) rubrique montre comment définie les tooencode dans un MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="ee550-110">hello [encoding an asset](media-services-encode-asset.md) topic shows how tooencode into an adaptive bitrate MP4 set.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee550-111">Si votre contenu est chiffré, configurez la stratégie de livraison d’éléments multimédias (comme décrit dans [cette](media-services-dotnet-configure-asset-delivery-policy.md) rubrique) avant de créer un localisateur.</span><span class="sxs-lookup"><span data-stu-id="ee550-111">If your content is encrypted, configure asset delivery policy (as described in [this](media-services-dotnet-configure-asset-delivery-policy.md) topic) before creating a locator.</span></span> 
> 
> 

<span data-ttu-id="ee550-112">Vous pouvez également utiliser une URL de toobuild que les fichiers de point de tooMP4 qui peuvent être téléchargé progressivement de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="ee550-112">You can also use an OnDemand streaming locator toobuild URLs that point tooMP4 files that can be progressively downloaded.</span></span>  

<span data-ttu-id="ee550-113">Cette rubrique montre comment toocreate une toopublish de localisateur de diffusion en continu votre actif et la build un Smooth Streaming, MPEG DASH et HLS URL de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="ee550-113">This topic shows how toocreate an OnDemand streaming locator toopublish your asset and build a Smooth, MPEG DASH, and HLS streaming URLs.</span></span> <span data-ttu-id="ee550-114">Il montre également à chaud toobuild URL de téléchargement progressif.</span><span class="sxs-lookup"><span data-stu-id="ee550-114">It also shows hot toobuild progressive download URLs.</span></span> 

## <a name="create-an-ondemand-streaming-locator"></a><span data-ttu-id="ee550-115">Création d’un localisateur de diffusion en continu à la demande</span><span class="sxs-lookup"><span data-stu-id="ee550-115">Create an OnDemand streaming locator</span></span>
<span data-ttu-id="ee550-116">toocreate hello localisateur de diffusion en continu à la demande et obtenir l’URL, vous devez hello toodo suivant choses :</span><span class="sxs-lookup"><span data-stu-id="ee550-116">toocreate hello OnDemand streaming locator and get URLs, you need toodo hello following things:</span></span>

1. <span data-ttu-id="ee550-117">Si le contenu de hello est chiffré, définir une stratégie d’accès.</span><span class="sxs-lookup"><span data-stu-id="ee550-117">If hello content is encrypted, define an access policy.</span></span>
2. <span data-ttu-id="ee550-118">Création d’un localisateur de diffusion en continu à la demande.</span><span class="sxs-lookup"><span data-stu-id="ee550-118">Create an OnDemand streaming locator.</span></span>
3. <span data-ttu-id="ee550-119">Si vous envisagez toostream, obtenir hello de diffusion en continu le fichier manifeste (.ism) dans l’élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="ee550-119">If you plan toostream, get hello streaming manifest file (.ism) in hello asset.</span></span> 
   
   <span data-ttu-id="ee550-120">Si vous envisagez de téléchargement de tooprogressively, obtenir les noms de hello de fichiers MP4 dans un élément multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="ee550-120">If you plan tooprogressively download, get hello names of MP4 files in hello asset.</span></span>  
4. <span data-ttu-id="ee550-121">Générer le fichier de manifeste toohello URL ou fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="ee550-121">Build URLs toohello manifest file or MP4 files.</span></span> 


>[!NOTE]
><span data-ttu-id="ee550-122">Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="ee550-122">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="ee550-123">Utilisez hello même ID de stratégie si vous utilisez toujours hello même jours / autorisations d’accès.</span><span class="sxs-lookup"><span data-stu-id="ee550-123">Use hello same policy ID if you are always using hello same days / access permissions.</span></span> <span data-ttu-id="ee550-124">Par exemple, des stratégies pour les localisateurs qui sont destinés à tooremain en place un certain temps (non-téléchargement stratégies).</span><span class="sxs-lookup"><span data-stu-id="ee550-124">For example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="ee550-125">Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .</span><span class="sxs-lookup"><span data-stu-id="ee550-125">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

### <a name="use-media-services-net-sdk"></a><span data-ttu-id="ee550-126">Utilisation du Kit de développement logiciel (SDK) .NET de Media Services</span><span class="sxs-lookup"><span data-stu-id="ee550-126">Use Media Services .NET SDK</span></span>
<span data-ttu-id="ee550-127">Création d’URL de diffusion</span><span class="sxs-lookup"><span data-stu-id="ee550-127">Build Streaming URLs</span></span> 

    private static void BuildStreamingURLs(IAsset asset)
    {

        // Create a 30-day readonly access policy. 
          // You cannot create a streaming locator using an AccessPolicy that includes write or delete permissions.
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create a locator toohello streaming content on an origin. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get a reference toohello streaming manifest file from hello  
        // collection of files in hello asset. 
        var manifestFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                                    EndsWith(".ism")).
                                    FirstOrDefault();

        // Create a full URL toohello manifest file. Use this for playback
        // in streaming media clients. 
        string urlForClientStreaming = originLocator.Path + manifestFile.Name + "/manifest";
        Console.WriteLine("URL toomanifest for client streaming using Smooth Streaming protocol: ");
        Console.WriteLine(urlForClientStreaming);
        Console.WriteLine("URL toomanifest for client streaming using HLS protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=m3u8-aapl)");
        Console.WriteLine("URL toomanifest for client streaming using MPEG DASH protocol: ");
        Console.WriteLine(urlForClientStreaming + "(format=mpd-time-csf)"); 
        Console.WriteLine();
    }

<span data-ttu-id="ee550-128">Hello sorties :</span><span class="sxs-lookup"><span data-stu-id="ee550-128">hello outputs:</span></span>

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> <span data-ttu-id="ee550-129">Vous pouvez aussi diffuser votre contenu via une connexion SSL.</span><span class="sxs-lookup"><span data-stu-id="ee550-129">You can also stream your content over an SSL connection.</span></span> <span data-ttu-id="ee550-130">toodo cette approche, assurez-vous que votre Démarrer URL de diffusion en continu avec HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ee550-130">toodo this approach, make sure your streaming URLs start with HTTPS.</span></span> <span data-ttu-id="ee550-131">Actuellement, AMS ne prend pas en charge SSL avec les domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ee550-131">Currently, AMS doesn’t support SSL with custom domains.</span></span>
> 
> 

<span data-ttu-id="ee550-132">Génération d’URL de téléchargement progressif</span><span class="sxs-lookup"><span data-stu-id="ee550-132">Build progressive download URLs</span></span> 

    private static void BuildProgressiveDownloadURLs(IAsset asset)
    {
        // Create a 30-day readonly access policy. 
        IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

        // Create an OnDemandOrigin locator toohello asset. 
        ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

        // Display some useful values based on hello locator.
        Console.WriteLine("Streaming asset base path on origin: ");
        Console.WriteLine(originLocator.Path);
        Console.WriteLine();

        // Get MP4 files.
        IEnumerable<IAssetFile> mp4AssetFiles = asset
            .AssetFiles
            .ToList()
            .Where(af => af.Name.EndsWith(".mp4", StringComparison.OrdinalIgnoreCase));

        // Create a full URL toohello MP4 files. Use this tooprogressively download files.
        foreach (var pd in mp4AssetFiles)
            Console.WriteLine(originLocator.Path + pd.Name);
    }

<span data-ttu-id="ee550-133">Hello sorties :</span><span class="sxs-lookup"><span data-stu-id="ee550-133">hello outputs:</span></span>

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a><span data-ttu-id="ee550-134">Utilisation des extensions du Kit de développement logiciel (SDK) Media Services pour .NET</span><span class="sxs-lookup"><span data-stu-id="ee550-134">Use Media Services .NET SDK Extensions</span></span>
<span data-ttu-id="ee550-135">Hello de code suivant appelle les méthodes extensions .NET SDK créer un localisateur et génèrent hello Smooth Streaming, HLS et MPEG-DASH URL de diffusion adaptative en continu.</span><span class="sxs-lookup"><span data-stu-id="ee550-135">hello following code calls .NET SDK extensions methods that create a locator and generate hello Smooth Streaming, HLS, and MPEG-DASH URLs for adaptive streaming.</span></span>

    // Create a loctor.
    _context.Locators.Create(
        LocatorType.OnDemandOrigin,
        inputAsset,
        AccessPermissions.Read,
        TimeSpan.FromDays(30));

    // Get hello streaming URLs.
    Uri smoothStreamingUri = inputAsset.GetSmoothStreamingUri();
    Uri hlsUri = inputAsset.GetHlsUri();
    Uri mpegDashUri = inputAsset.GetMpegDashUri();

    Console.WriteLine(smoothStreamingUri);
    Console.WriteLine(hlsUri);
    Console.WriteLine(mpegDashUri);


## <a name="media-services-learning-paths"></a><span data-ttu-id="ee550-136">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="ee550-136">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ee550-137">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="ee550-137">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ee550-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee550-138">Next steps</span></span>
* [<span data-ttu-id="ee550-139">Télécharger les éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="ee550-139">Download assets</span></span>](media-services-deliver-asset-download.md)
* [<span data-ttu-id="ee550-140">Configurer une stratégie de distribution d’éléments multimédias</span><span class="sxs-lookup"><span data-stu-id="ee550-140">Configure asset delivery policy</span></span>](media-services-dotnet-configure-asset-delivery-policy.md)

