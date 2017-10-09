---
title: Filtres aaaCreating avec Azure Media Services .NET SDK
description: "Cette rubrique décrit comment toocreate filtre votre client peut utiliser les toostream des sections spécifiques d’un flux. Media Services crée les manifestes dynamique tooachieve cette diffusion sélective."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2f6894ca-fb43-43c0-9151-ddbb2833cafd
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako;cenkdin
ms.openlocfilehash: 16d9497d48ab1d3f841dd97efb0f66016a2435c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="f4e51-104">Création de filtres avec le Kit de développement logiciel (SDK) .NET Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f4e51-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4e51-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f4e51-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="f4e51-106">REST</span><span class="sxs-lookup"><span data-stu-id="f4e51-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="f4e51-107">À compter de version 2.11, Media Services vous permet toodefine des filtres pour vos ressources.</span><span class="sxs-lookup"><span data-stu-id="f4e51-107">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="f4e51-108">Ces filtres sont des règles côté serveur qui permettent à vos clients toochoose toodo opérations : lecture uniquement une section d’une vidéo (au lieu de hello vidéo complètes), ou spécifiez uniquement un sous-ensemble de formats audio et vidéo que les appareils de votre client peuvent traiter () au lieu de tous les formats de hello qui sont associés les actifs hello).</span><span class="sxs-lookup"><span data-stu-id="f4e51-108">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="f4e51-109">Ce filtrage de vos éléments multimédias est possible grâce à **manifeste dynamique**s qui sont créées lors de toostream de demande de votre client une vidéo en fonction de filtres spécifiées.</span><span class="sxs-lookup"><span data-stu-id="f4e51-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="f4e51-110">Pour plus d’informations connexes toofilters et dynamique de manifeste, consultez [dynamique manifestes de vue d’ensemble](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4e51-110">For more detailed information related toofilters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="f4e51-111">Cette rubrique montre comment toouse toocreate de Media Services .NET SDK, mettre à jour et supprimer des filtres.</span><span class="sxs-lookup"><span data-stu-id="f4e51-111">This topic shows how toouse Media Services .NET SDK toocreate, update, and delete filters.</span></span> 

<span data-ttu-id="f4e51-112">Notez que si vous mettez à jour un filtre, il peut prendre jusqu'à minutes too2 de règles de hello toorefresh de point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f4e51-112">Note if you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="f4e51-113">Si le contenu hello a été traitée à l’aide de ce filtre (et mises en cache proxys et CDN caches), mise à jour de ce filtre peut entraîner des échecs de lecteur.</span><span class="sxs-lookup"><span data-stu-id="f4e51-113">If hello content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="f4e51-114">Il est recommandé de cache de hello tooclear après la mise à jour de filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="f4e51-114">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="f4e51-115">Si cette option n'est pas possible, envisagez d'utiliser un filtre différent.</span><span class="sxs-lookup"><span data-stu-id="f4e51-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-toocreate-filters"></a><span data-ttu-id="f4e51-116">Les types utilisés toocreate filtres</span><span class="sxs-lookup"><span data-stu-id="f4e51-116">Types used toocreate filters</span></span>
<span data-ttu-id="f4e51-117">les types suivants Hello sont utilisées lors de la création de filtres :</span><span class="sxs-lookup"><span data-stu-id="f4e51-117">hello following types are used when creating filters:</span></span> 

* <span data-ttu-id="f4e51-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="f4e51-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="f4e51-119">Ce type est basé sur hello suivant l’API REST [filtre](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="f4e51-119">This type is based on hello following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="f4e51-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="f4e51-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="f4e51-121">Ce type est basé sur hello suivant l’API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="f4e51-121">This type is based on hello following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="f4e51-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="f4e51-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="f4e51-123">Ce type est basé sur hello suivant l’API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="f4e51-123">This type is based on hello following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="f4e51-124">**FilterTrackSelectStatement** et **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="f4e51-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="f4e51-125">Ces types sont basés sur hello suivant l’API REST [FilterTrackSelect et FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="f4e51-125">These types are based on hello following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="f4e51-126">Création/Mise à jour/Lecture/Suppression de filtres globaux</span><span class="sxs-lookup"><span data-stu-id="f4e51-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="f4e51-127">Hello de code suivant montre comment toouse .NET toocreate, mettre à jour, lire et supprimer des filtres actifs.</span><span class="sxs-lookup"><span data-stu-id="f4e51-127">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string filterName = "GlobalFilter_" + Guid.NewGuid().ToString();

    List<FilterTrackSelectStatement> filterTrackSelectStatements = new List<FilterTrackSelectStatement>();

    FilterTrackSelectStatement filterTrackSelectStatement = new FilterTrackSelectStatement();
    filterTrackSelectStatement.PropertyConditions = new List<IFilterTrackPropertyCondition>();
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackNameCondition("Track Name", FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackBitrateRangeCondition(new FilterTrackBitrateRange(0, 1), FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatement.PropertyConditions.Add(new FilterTrackTypeCondition(FilterTrackType.Audio, FilterTrackCompareOperator.NotEqual));
    filterTrackSelectStatements.Add(filterTrackSelectStatement);

    // Create
    IStreamingFilter filter = _context.Filters.Create(filterName, new PresentationTimeRange(), filterTrackSelectStatements);

    // Update
    filter.PresentationTimeRange = new PresentationTimeRange(timescale: 500);
    filter.Update();

    // Read
    var filterUpdated = _context.Filters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filter.Delete();


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="f4e51-128">Création/Mise à jour/Lecture/Suppression de filtres d’éléments multimédia</span><span class="sxs-lookup"><span data-stu-id="f4e51-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="f4e51-129">Hello de code suivant montre comment toouse .NET toocreate, mettre à jour, lire et supprimer des filtres actifs.</span><span class="sxs-lookup"><span data-stu-id="f4e51-129">hello following code shows how toouse .NET toocreate, update,read, and delete asset filters.</span></span>

    string assetName = "AssetFilter_" + Guid.NewGuid().ToString();
    var asset = _context.Assets.Create(assetName, AssetCreationOptions.None);

    string filterName = "AssetFilter_" + Guid.NewGuid().ToString();


    // Create
    IStreamingAssetFilter filter = asset.AssetFilters.Create(filterName,
                                        new PresentationTimeRange(), 
                                        new List<FilterTrackSelectStatement>());

    // Update
    filter.PresentationTimeRange = 
            new PresentationTimeRange(start: 6000000000, end: 72000000000);

    filter.Update();

    // Read
    asset = _context.Assets.Where(c => c.Id == asset.Id).FirstOrDefault();
    var filterUpdated = asset.AssetFilters.FirstOrDefault();
    Console.WriteLine(filterUpdated.Name);

    // Delete
    filterUpdated.Delete();




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="f4e51-130">Création d'URL de diffusion qui utilisent des filtres</span><span class="sxs-lookup"><span data-stu-id="f4e51-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="f4e51-131">Pour plus d’informations sur comment toopublish et proposer vos éléments multimédias, consultez [tooCustomers de fourniture de contenu vue d’ensemble](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4e51-131">For information on how toopublish and deliver your assets, see [Delivering Content tooCustomers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="f4e51-132">Hello exemples suivants montrent comment tooadd filtre tooyour URL de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f4e51-132">hello following examples show how tooadd filters tooyour streaming URLs.</span></span>

<span data-ttu-id="f4e51-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="f4e51-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="f4e51-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="f4e51-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="f4e51-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="f4e51-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="f4e51-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="f4e51-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="f4e51-137">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f4e51-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4e51-138">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f4e51-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f4e51-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f4e51-139">See Also</span></span>
[<span data-ttu-id="f4e51-140">Vue d'ensemble des manifestes dynamiques</span><span class="sxs-lookup"><span data-stu-id="f4e51-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

