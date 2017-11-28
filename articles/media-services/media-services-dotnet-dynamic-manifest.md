---
title: "Création de filtres avec le Kit de développement logiciel (SDK) .NET Azure Media Services"
description: "Cette rubrique décrit comment créer des filtres pour que votre client puisse les utiliser pour diffuser des sections spécifiques d'un flux. Media Services crée des manifestes dynamiques pour obtenir cette diffusion sélective."
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
ms.openlocfilehash: 6c43473b86c14679ace558de478bd95f41d476da
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-filters-with-azure-media-services-net-sdk"></a><span data-ttu-id="9544a-104">Création de filtres avec le Kit de développement logiciel (SDK) .NET Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9544a-104">Creating Filters with Azure Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9544a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9544a-105">.NET</span></span>](media-services-dotnet-dynamic-manifest.md)
> * [<span data-ttu-id="9544a-106">REST</span><span class="sxs-lookup"><span data-stu-id="9544a-106">REST</span></span>](media-services-rest-dynamic-manifest.md)
> 
> 

<span data-ttu-id="9544a-107">À partir de la version 2.11, Media Services vous permet de définir des filtres pour vos éléments multimédias.</span><span class="sxs-lookup"><span data-stu-id="9544a-107">Starting with 2.11 release, Media Services enables you to define filters for your assets.</span></span> <span data-ttu-id="9544a-108">Ces filtres sont des règles côté serveur qui permettent à vos clients de choisir d'effectuer des opérations comme les suivantes : lecture d'une section d'une vidéo uniquement (au lieu de la vidéo entière), spécification d'un seul sous-ensemble de rendus audio et vidéo pouvant être gérés par l'appareil de votre client (au lieu de tous les rendus associés à l'élément multimédia).</span><span class="sxs-lookup"><span data-stu-id="9544a-108">These filters are server side rules that will allow your customers to choose to do things like: playback only a section of a video (instead of playing the whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all the renditions that are associated with the asset).</span></span> <span data-ttu-id="9544a-109">Ce filtrage de vos éléments multimédias est obtenu via des **manifestes dynamiques**créés à la demande de votre client pour diffuser une vidéo selon des filtres spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9544a-109">This filtering of your assets is achieved through **Dynamic Manifest**s that are created upon your customer's request to stream a video based on specified filter(s).</span></span>

<span data-ttu-id="9544a-110">Pour plus d'informations sur les filtres et le manifeste dynamique, consultez [Vue d'ensemble des manifestes dynamiques](media-services-dynamic-manifest-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9544a-110">For more detailed information related to filters and Dynamic Manifest, see [Dynamic manifests overview](media-services-dynamic-manifest-overview.md).</span></span>

<span data-ttu-id="9544a-111">Cette rubrique montre comment utiliser le SDK .NET de Media Services pour créer, mettre à jour et supprimer des filtres.</span><span class="sxs-lookup"><span data-stu-id="9544a-111">This topic shows how to use Media Services .NET SDK to create, update, and delete filters.</span></span> 

<span data-ttu-id="9544a-112">Remarque : si vous mettez à jour un filtre, il peut falloir jusqu’à 2 minutes pour que le point de terminaison de diffusion en continu actualise les règles.</span><span class="sxs-lookup"><span data-stu-id="9544a-112">Note if you update a filter, it can take up to 2 minutes for streaming endpoint to refresh the rules.</span></span> <span data-ttu-id="9544a-113">Si le contenu a été servi à l'aide de ce filtre (puis mis en cache dans des proxys et des caches CDN), la mise à jour de ce filtre peut entraîner des défaillances du lecteur.</span><span class="sxs-lookup"><span data-stu-id="9544a-113">If the content was served using this filter (and cached in proxies and CDN caches), updating this filter can result in player failures.</span></span> <span data-ttu-id="9544a-114">Il est recommandé d'effacer le cache après la mise à jour du filtre.</span><span class="sxs-lookup"><span data-stu-id="9544a-114">It is recommend to clear the cache after updating the filter.</span></span> <span data-ttu-id="9544a-115">Si cette option n'est pas possible, envisagez d'utiliser un filtre différent.</span><span class="sxs-lookup"><span data-stu-id="9544a-115">If this option is not possible, consider using a different filter.</span></span> 

## <a name="types-used-to-create-filters"></a><span data-ttu-id="9544a-116">Types utilisés pour créer des filtres</span><span class="sxs-lookup"><span data-stu-id="9544a-116">Types used to create filters</span></span>
<span data-ttu-id="9544a-117">Les types suivants sont utilisés lors de la création de filtres :</span><span class="sxs-lookup"><span data-stu-id="9544a-117">The following types are used when creating filters:</span></span> 

* <span data-ttu-id="9544a-118">**IStreamingFilter**.</span><span class="sxs-lookup"><span data-stu-id="9544a-118">**IStreamingFilter**.</span></span>  <span data-ttu-id="9544a-119">Ce type est basé sur l’API REST suivante : [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span><span class="sxs-lookup"><span data-stu-id="9544a-119">This type is based on the following REST API [Filter](https://docs.microsoft.com/rest/api/media/operations/filter)</span></span>
* <span data-ttu-id="9544a-120">**IStreamingAssetFilter**.</span><span class="sxs-lookup"><span data-stu-id="9544a-120">**IStreamingAssetFilter**.</span></span> <span data-ttu-id="9544a-121">Ce type est basé sur l’API REST suivante : [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span><span class="sxs-lookup"><span data-stu-id="9544a-121">This type is based on the following REST API [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)</span></span>
* <span data-ttu-id="9544a-122">**PresentationTimeRange**.</span><span class="sxs-lookup"><span data-stu-id="9544a-122">**PresentationTimeRange**.</span></span> <span data-ttu-id="9544a-123">Ce type est basé sur l’API REST suivante : [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span><span class="sxs-lookup"><span data-stu-id="9544a-123">This type is based on the following REST API [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)</span></span>
* <span data-ttu-id="9544a-124">**FilterTrackSelectStatement** et **IFilterTrackPropertyCondition**.</span><span class="sxs-lookup"><span data-stu-id="9544a-124">**FilterTrackSelectStatement** and **IFilterTrackPropertyCondition**.</span></span> <span data-ttu-id="9544a-125">Ces types sont basés sur les API REST suivantes [FilterTrackSelect et FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span><span class="sxs-lookup"><span data-stu-id="9544a-125">These types are based on the following REST APIs [FilterTrackSelect and FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)</span></span>

## <a name="createupdatereaddelete-global-filters"></a><span data-ttu-id="9544a-126">Création/Mise à jour/Lecture/Suppression de filtres globaux</span><span class="sxs-lookup"><span data-stu-id="9544a-126">Create/Update/Read/Delete global filters</span></span>
<span data-ttu-id="9544a-127">Le code suivant montre comment utiliser .NET pour créer, mettre à jour, lire et supprimer des filtres d’éléments multimédia.</span><span class="sxs-lookup"><span data-stu-id="9544a-127">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

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


## <a name="createupdatereaddelete-asset-filters"></a><span data-ttu-id="9544a-128">Création/Mise à jour/Lecture/Suppression de filtres d’éléments multimédia</span><span class="sxs-lookup"><span data-stu-id="9544a-128">Create/Update/Read/Delete asset filters</span></span>
<span data-ttu-id="9544a-129">Le code suivant montre comment utiliser .NET pour créer, mettre à jour, lire et supprimer des filtres d’éléments multimédia.</span><span class="sxs-lookup"><span data-stu-id="9544a-129">The following code shows how to use .NET to create, update,read, and delete asset filters.</span></span>

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




## <a name="build-streaming-urls-that-use-filters"></a><span data-ttu-id="9544a-130">Création d'URL de diffusion qui utilisent des filtres</span><span class="sxs-lookup"><span data-stu-id="9544a-130">Build streaming URLs that use filters</span></span>
<span data-ttu-id="9544a-131">Pour plus d'informations sur la publication et la distribution de vos éléments multimédias, consultez [Vue d'ensemble de la distribution de contenu aux clients](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9544a-131">For information on how to publish and deliver your assets, see [Delivering Content to Customers Overview](media-services-deliver-content-overview.md).</span></span>

<span data-ttu-id="9544a-132">Les exemples suivants montrent comment ajouter des filtres à vos URL de diffusion.</span><span class="sxs-lookup"><span data-stu-id="9544a-132">The following examples show how to add filters to your streaming URLs.</span></span>

<span data-ttu-id="9544a-133">**MPEG DASH**</span><span class="sxs-lookup"><span data-stu-id="9544a-133">**MPEG DASH**</span></span> 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

<span data-ttu-id="9544a-134">**Apple HTTP Live Streaming (HLS) V4**</span><span class="sxs-lookup"><span data-stu-id="9544a-134">**Apple HTTP Live Streaming (HLS) V4**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

<span data-ttu-id="9544a-135">**Apple HTTP Live Streaming (HLS) V3**</span><span class="sxs-lookup"><span data-stu-id="9544a-135">**Apple HTTP Live Streaming (HLS) V3**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

<span data-ttu-id="9544a-136">**Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="9544a-136">**Smooth Streaming**</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a><span data-ttu-id="9544a-137">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9544a-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9544a-138">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9544a-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9544a-139">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9544a-139">See Also</span></span>
[<span data-ttu-id="9544a-140">Vue d'ensemble des manifestes dynamiques</span><span class="sxs-lookup"><span data-stu-id="9544a-140">Dynamic manifests overview</span></span>](media-services-dynamic-manifest-overview.md)

