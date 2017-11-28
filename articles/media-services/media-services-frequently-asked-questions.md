---
title: "Azure Media Services : FAQ | Microsoft Docs"
description: Forum Aux Questions (FAQ)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="3fbb1-103">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="3fbb1-103">Frequently asked questions</span></span>

<span data-ttu-id="3fbb1-104">Cet article répond aux questions fréquemment posées par communauté des utilisateurs d’Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="3fbb1-105">Forum Aux Questions - Généralités AMS</span><span class="sxs-lookup"><span data-stu-id="3fbb1-105">General AMS FAQs</span></span>
<span data-ttu-id="3fbb1-106">Q : comment mettre à l’échelle l’indexation ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="3fbb1-107">R : les unités réservées sont les mêmes pour les tâches d’encodage et d’indexation.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="3fbb1-108">Suivez les instructions de la page [Comment mettre à l’échelle des unités réservées mise à l’échelle des unités réservées d’encodage](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="3fbb1-109">**Remarque** : le fonctionnement de l’indexeur n’est pas affecté par le type d’unité réservée.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="3fbb1-110">Q : j’ai chargé, encodé et publié une vidéo.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="3fbb1-111">Pourquoi la vidéo n’est-elle pas lue lorsque j’essaie de la diffuser en continu ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="3fbb1-112">R : une des raisons les plus courantes est que le point de terminaison de streaming à partir duquel vous essayez de lire n’est pas dans l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="3fbb1-113">Q : la composition d’un flux dynamique est-elle possible ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="3fbb1-114">R : la composition de flux dynamiques n’est pas disponible pour le moment dans Azure Media Services. Vous devez donc effectuer la composition au préalable sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="3fbb1-115">Q : puis-je utiliser le CDN Azure avec la vidéo en flux continu ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="3fbb1-116">R : Media Services prend en charge l’intégration au CDN Azure (pour plus d’informations, consultez la rubrique [Gestion des points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="3fbb1-117">Vous pouvez utiliser la vidéo en flux continu avec le CDN.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="3fbb1-118">Azure Media Services fournit des sorties aux formats Smooth Streaming, HLS et MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="3fbb1-119">Tous ces formats utilisent le protocole HTTP pour transférer les données et bénéficient des avantages de la mise en cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="3fbb1-120">Lors d’une diffusion vidéo en flux continu, les données vidéo/audio sont divisées en fragments individuels qui sont mis en cache dans le CDN.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="3fbb1-121">Les seules données devant être actualisées sont les données de manifeste.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="3fbb1-122">CDN actualise régulièrement les données de manifeste.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="3fbb1-123">Q : le stockage des images est-il pris en charge par Azure Media Services ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="3fbb1-124">R : si vous cherchez uniquement à stocker des images JPEG ou PNG, nous vous recommandons de les conserver dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="3fbb1-125">Il n’y a aucun avantage à les placer dans votre compte Media Services, à moins que vous souhaitiez qu’elles restent associées à vos ressources vidéo ou audio</span><span class="sxs-lookup"><span data-stu-id="3fbb1-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="3fbb1-126">Ou, si vous avez besoin d'utiliser les images sous forme de superpositions dans l'encodeur vidéo, Media Encoder Standard prend en charge la superposition d’images sur les vidéos, ce qui explique pourquoi JPEG et PNG figurent parmi les formats d’entrée pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="3fbb1-127">Pour plus d’informations, consultez la page [Création de superpositions](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="3fbb1-128">Q : comment puis-je copier des éléments multimédias d’un compte Media Services vers un autre ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="3fbb1-129">R : pour copier des éléments multimédias d’un compte Media Services vers un autre à l’aide de .NET, utilisez la méthode d’extension [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) disponible dans le référentiel [Extensions du Kit de développement logiciel (SDK) Azure Media Services](https://github.com/Azure/azure-sdk-for-media-services-extensions/).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="3fbb1-130">Pour plus d’informations, consultez [cette publication de forum](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) .</span><span class="sxs-lookup"><span data-stu-id="3fbb1-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="3fbb1-131">Q: quels sont les caractères pris en charge pour les noms des fichiers en utilisant AMS ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="3fbb1-132">R : Media Services utilise la valeur de la propriété IAssetFile.Name lors de la génération d’URL pour le contenu de diffusion en continu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="3fbb1-133">La valeur de la propriété **Name** ne peut pas comporter les [caractères réservés à l’encodage en pourcentage suivants](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters) : !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="3fbb1-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="3fbb1-134">En outre, il ne peut exister qu’un seul « . »</span><span class="sxs-lookup"><span data-stu-id="3fbb1-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="3fbb1-135">pour l’extension de nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-135">for the file name extension.</span></span>

<span data-ttu-id="3fbb1-136">Q: comment se connecter avec REST ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="3fbb1-137">R : Pour savoir comment vous connecter à l’API Azure Media Services, voir [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="3fbb1-138">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="3fbb1-139">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="3fbb1-140">Q : comment faire pivoter une vidéo au cours du processus d’encodage ?</span><span class="sxs-lookup"><span data-stu-id="3fbb1-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="3fbb1-141">R : [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge trois angles de rotation (90, 180 et 270).</span><span class="sxs-lookup"><span data-stu-id="3fbb1-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="3fbb1-142">Le comportement par défaut est « Auto », ce qui signifie qu’il tente de détecter les métadonnées de rotation dans le fichier MP4/MOV entrant et de les compenser.</span><span class="sxs-lookup"><span data-stu-id="3fbb1-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="3fbb1-143">Incluez l’élément **Sources** suivant dans l’une des présélections json définies [ici](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="3fbb1-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="3fbb1-144">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="3fbb1-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3fbb1-145">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3fbb1-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
