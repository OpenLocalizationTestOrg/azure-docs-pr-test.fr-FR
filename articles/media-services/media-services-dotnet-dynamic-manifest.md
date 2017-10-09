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
# <a name="creating-filters-with-azure-media-services-net-sdk"></a>Création de filtres avec le Kit de développement logiciel (SDK) .NET Azure Media Services
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-dynamic-manifest.md)
> * [REST](media-services-rest-dynamic-manifest.md)
> 
> 

À compter de version 2.11, Media Services vous permet toodefine des filtres pour vos ressources. Ces filtres sont des règles côté serveur qui permettent à vos clients toochoose toodo opérations : lecture uniquement une section d’une vidéo (au lieu de hello vidéo complètes), ou spécifiez uniquement un sous-ensemble de formats audio et vidéo que les appareils de votre client peuvent traiter () au lieu de tous les formats de hello qui sont associés les actifs hello). Ce filtrage de vos éléments multimédias est possible grâce à **manifeste dynamique**s qui sont créées lors de toostream de demande de votre client une vidéo en fonction de filtres spécifiées.

Pour plus d’informations connexes toofilters et dynamique de manifeste, consultez [dynamique manifestes de vue d’ensemble](media-services-dynamic-manifest-overview.md).

Cette rubrique montre comment toouse toocreate de Media Services .NET SDK, mettre à jour et supprimer des filtres. 

Notez que si vous mettez à jour un filtre, il peut prendre jusqu'à minutes too2 de règles de hello toorefresh de point de terminaison de diffusion en continu. Si le contenu hello a été traitée à l’aide de ce filtre (et mises en cache proxys et CDN caches), mise à jour de ce filtre peut entraîner des échecs de lecteur. Il est recommandé de cache de hello tooclear après la mise à jour de filtre de hello. Si cette option n'est pas possible, envisagez d'utiliser un filtre différent. 

## <a name="types-used-toocreate-filters"></a>Les types utilisés toocreate filtres
les types suivants Hello sont utilisées lors de la création de filtres : 

* **IStreamingFilter**.  Ce type est basé sur hello suivant l’API REST [filtre](https://docs.microsoft.com/rest/api/media/operations/filter)
* **IStreamingAssetFilter**. Ce type est basé sur hello suivant l’API REST [AssetFilter](https://docs.microsoft.com/rest/api/media/operations/assetfilter)
* **PresentationTimeRange**. Ce type est basé sur hello suivant l’API REST [PresentationTimeRange](https://docs.microsoft.com/rest/api/media/operations/presentationtimerange)
* **FilterTrackSelectStatement** et **IFilterTrackPropertyCondition**. Ces types sont basés sur hello suivant l’API REST [FilterTrackSelect et FilterTrackPropertyCondition](https://docs.microsoft.com/rest/api/media/operations/filtertrackselect)

## <a name="createupdatereaddelete-global-filters"></a>Création/Mise à jour/Lecture/Suppression de filtres globaux
Hello de code suivant montre comment toouse .NET toocreate, mettre à jour, lire et supprimer des filtres actifs.

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


## <a name="createupdatereaddelete-asset-filters"></a>Création/Mise à jour/Lecture/Suppression de filtres d’éléments multimédia
Hello de code suivant montre comment toouse .NET toocreate, mettre à jour, lire et supprimer des filtres actifs.

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




## <a name="build-streaming-urls-that-use-filters"></a>Création d'URL de diffusion qui utilisent des filtres
Pour plus d’informations sur comment toopublish et proposer vos éléments multimédias, consultez [tooCustomers de fourniture de contenu vue d’ensemble](media-services-deliver-content-overview.md).

Hello exemples suivants montrent comment tooadd filtre tooyour URL de diffusion en continu.

**MPEG DASH** 

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V4**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl, filter=MyFilter)

**Apple HTTP Live Streaming (HLS) V3**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3, filter=MyFilter)

**Smooth Streaming**

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyFilter)


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Vue d'ensemble des manifestes dynamiques](media-services-dynamic-manifest-overview.md)

