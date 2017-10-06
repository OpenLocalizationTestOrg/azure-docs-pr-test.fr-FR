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
# <a name="publish-azure-media-services-content-using-net"></a>Publier du contenu Azure Media Services à l’aide de .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-deliver-streaming-content.md)
> * [.NET](media-services-deliver-streaming-content.md)
> * [Portail](media-services-portal-publish.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Vous pouvez diffuser un MP4 à débit adaptatif défini par la création d’un localisateur de diffusion en continu à la demande et la création d’une URL de diffusion en continu. Hello [encodage d’un élément multimédia](media-services-encode-asset.md) rubrique montre comment définie les tooencode dans un MP4 à débit adaptatif. 

> [!NOTE]
> Si votre contenu est chiffré, configurez la stratégie de livraison d’éléments multimédias (comme décrit dans [cette](media-services-dotnet-configure-asset-delivery-policy.md) rubrique) avant de créer un localisateur. 
> 
> 

Vous pouvez également utiliser une URL de toobuild que les fichiers de point de tooMP4 qui peuvent être téléchargé progressivement de diffusion en continu à la demande.  

Cette rubrique montre comment toocreate une toopublish de localisateur de diffusion en continu votre actif et la build un Smooth Streaming, MPEG DASH et HLS URL de diffusion en continu à la demande. Il montre également à chaud toobuild URL de téléchargement progressif. 

## <a name="create-an-ondemand-streaming-locator"></a>Création d’un localisateur de diffusion en continu à la demande
toocreate hello localisateur de diffusion en continu à la demande et obtenir l’URL, vous devez hello toodo suivant choses :

1. Si le contenu de hello est chiffré, définir une stratégie d’accès.
2. Création d’un localisateur de diffusion en continu à la demande.
3. Si vous envisagez toostream, obtenir hello de diffusion en continu le fichier manifeste (.ism) dans l’élément multimédia de hello. 
   
   Si vous envisagez de téléchargement de tooprogressively, obtenir les noms de hello de fichiers MP4 dans un élément multimédia de hello.  
4. Générer le fichier de manifeste toohello URL ou fichiers MP4. 


>[!NOTE]
>Un nombre limite de 1 000 000 a été défini pour les différentes stratégies AMS (par exemple, pour la stratégie de localisateur ou pour ContentKeyAuthorizationPolicy). Utilisez hello même ID de stratégie si vous utilisez toujours hello même jours / autorisations d’accès. Par exemple, des stratégies pour les localisateurs qui sont destinés à tooremain en place un certain temps (non-téléchargement stratégies). Pour plus d’informations, consultez [cette rubrique](media-services-dotnet-manage-entities.md#limit-access-policies) .

### <a name="use-media-services-net-sdk"></a>Utilisation du Kit de développement logiciel (SDK) .NET de Media Services
Création d’URL de diffusion 

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

Hello sorties :

    URL toomanifest for client streaming using Smooth Streaming protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest
    URL toomanifest for client streaming using HLS protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=m3u8-aapl)
    URL toomanifest for client streaming using MPEG DASH protocol:
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny.ism/manifest(format=mpd-time-csf)


> [!NOTE]
> Vous pouvez aussi diffuser votre contenu via une connexion SSL. toodo cette approche, assurez-vous que votre Démarrer URL de diffusion en continu avec HTTPS. Actuellement, AMS ne prend pas en charge SSL avec les domaines personnalisés.
> 
> 

Génération d’URL de téléchargement progressif 

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

Hello sorties :

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4
    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4

    . . . 

### <a name="use-media-services-net-sdk-extensions"></a>Utilisation des extensions du Kit de développement logiciel (SDK) Media Services pour .NET
Hello de code suivant appelle les méthodes extensions .NET SDK créer un localisateur et génèrent hello Smooth Streaming, HLS et MPEG-DASH URL de diffusion adaptative en continu.

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


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
* [Télécharger les éléments multimédias](media-services-deliver-asset-download.md)
* [Configurer une stratégie de distribution d’éléments multimédias](media-services-dotnet-configure-asset-delivery-policy.md)

