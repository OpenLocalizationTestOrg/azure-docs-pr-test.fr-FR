---
title: aaaAzure Forum aux questions de Media Services | Documents Microsoft
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
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="2f390-103">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="2f390-103">Frequently asked questions</span></span>

<span data-ttu-id="2f390-104">Cet article répond aux questions fréquemment posées déclenchées par la Communauté d’utilisateurs hello Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="2f390-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="2f390-105">Forum Aux Questions - Généralités AMS</span><span class="sxs-lookup"><span data-stu-id="2f390-105">General AMS FAQs</span></span>
<span data-ttu-id="2f390-106">Q : comment mettre à l’échelle l’indexation ?</span><span class="sxs-lookup"><span data-stu-id="2f390-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="2f390-107">A: unités de hello réservé sont hello même pour l’encodage et l’indexation des tâches.</span><span class="sxs-lookup"><span data-stu-id="2f390-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="2f390-108">Suivez les instructions de [comment unités réservées d’encodage tooScale](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f390-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="2f390-109">**Remarque** : le fonctionnement de l’indexeur n’est pas affecté par le type d’unité réservée.</span><span class="sxs-lookup"><span data-stu-id="2f390-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="2f390-110">Q : j’ai chargé, encodé et publié une vidéo.</span><span class="sxs-lookup"><span data-stu-id="2f390-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="2f390-111">Quel serait vidéo de hello raison hello n’est pas lu lors de le toostream il ?</span><span class="sxs-lookup"><span data-stu-id="2f390-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="2f390-112">R : un des hello des raisons de la plus courante est inutile de hello de diffusion en continu de point de terminaison à partir de laquelle vous essayez de tooplayback Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="2f390-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="2f390-113">Q : la composition d’un flux dynamique est-elle possible ?</span><span class="sxs-lookup"><span data-stu-id="2f390-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="2f390-114">R : la composition de flux live est actuellement pas disponible dans Azure Media Services, et vous devez donc toopre-composer sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f390-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="2f390-115">Q : puis-je utiliser le CDN Azure avec la vidéo en flux continu ?</span><span class="sxs-lookup"><span data-stu-id="2f390-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="2f390-116">R : Media Services prend en charge l’intégration à Azure CDN (pour plus d’informations, consultez [comment tooManage points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="2f390-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="2f390-117">Vous pouvez utiliser la vidéo en flux continu avec le CDN.</span><span class="sxs-lookup"><span data-stu-id="2f390-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="2f390-118">Azure Media Services fournit des sorties aux formats Smooth Streaming, HLS et MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="2f390-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="2f390-119">Tous ces formats utilisent le protocole HTTP pour transférer les données et bénéficient des avantages de la mise en cache HTTP.</span><span class="sxs-lookup"><span data-stu-id="2f390-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="2f390-120">Dynamique de diffusion en continu des données audio/vidéo réelles est divisé toofragments et des fragments mis en cache dans le CDN.</span><span class="sxs-lookup"><span data-stu-id="2f390-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="2f390-121">Uniquement les toobe besoins données actualisées donnée hello manifeste.</span><span class="sxs-lookup"><span data-stu-id="2f390-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="2f390-122">CDN actualise régulièrement les données de manifeste.</span><span class="sxs-lookup"><span data-stu-id="2f390-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="2f390-123">Q : le stockage des images est-il pris en charge par Azure Media Services ?</span><span class="sxs-lookup"><span data-stu-id="2f390-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="2f390-124">R : Si vous souhaitez simplement toostore JPEG ou des images PNG, vous devez conserver celles figurant dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2f390-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="2f390-125">Il n’existe aucun tooputting avantage dans vos Services de support compte sauf si vous souhaitez tookeep que les associé à vos vidéo ou Audio.</span><span class="sxs-lookup"><span data-stu-id="2f390-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="2f390-126">Ou si vous pouvez avoir un toouse besoin hello images comme superpositions dans un encodeur vidéo de hello. Media Encoder Standard prend en charge les images de superposition par-dessus les vidéos, et c’est qu’il répertorie JPEG et PNG pris en charge d’entrée de formats.</span><span class="sxs-lookup"><span data-stu-id="2f390-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="2f390-127">Pour plus d’informations, consultez la page [Création de superpositions](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="2f390-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="2f390-128">Q : Comment puis-je copier des ressources à partir d’un tooanother de compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="2f390-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="2f390-129">R : toocopy des ressources à partir d’un tooanother de compte Media Services à l’aide de .NET, utilisez [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) méthode d’extension disponible dans hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) référentiel.</span><span class="sxs-lookup"><span data-stu-id="2f390-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="2f390-130">Pour plus d’informations, consultez [cette publication de forum](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) .</span><span class="sxs-lookup"><span data-stu-id="2f390-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="2f390-131">Q : quelles sont les hello caractères pris en charge pour nommer les fichiers lorsque vous travaillez avec AMS ?</span><span class="sxs-lookup"><span data-stu-id="2f390-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="2f390-132">R : Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="2f390-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="2f390-133">Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ».</span><span class="sxs-lookup"><span data-stu-id="2f390-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="2f390-134">En outre, il ne peut exister qu’un seul « . »</span><span class="sxs-lookup"><span data-stu-id="2f390-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="2f390-135">pour l’extension de nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="2f390-135">for hello file name extension.</span></span>

<span data-ttu-id="2f390-136">Q : comment tooconnect à l’aide de REST ?</span><span class="sxs-lookup"><span data-stu-id="2f390-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="2f390-137">R : pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="2f390-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="2f390-138">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="2f390-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="2f390-139">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="2f390-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="2f390-140">Q : Comment puis-je pivoter une vidéo pendant hello processus de codage.</span><span class="sxs-lookup"><span data-stu-id="2f390-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="2f390-141">R : hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge de la rotation par les angles de 90/180/270.</span><span class="sxs-lookup"><span data-stu-id="2f390-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="2f390-142">comportement par défaut de Hello est « Auto », où il tente de métadonnées de rotation toodetect hello dans le fichier MP4/MOV entrant hello et compensation.</span><span class="sxs-lookup"><span data-stu-id="2f390-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="2f390-143">Suivants de hello **Sources** tooone élément des présélections de json hello défini [ici](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="2f390-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="2f390-144">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="2f390-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2f390-145">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2f390-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
