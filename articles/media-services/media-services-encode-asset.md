---
title: "aaaOverview et comparaison d’Azure sur demande les encodeurs media | Documents Microsoft"
description: "Cette rubrique donne une vue d’ensemble des encodeurs multimédia à la demande Azure et les compare."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="de476-103">Vue d’ensemble et comparaison d’encodeurs multimédia à la demande Azure</span><span class="sxs-lookup"><span data-stu-id="de476-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="de476-104">Vue d’ensemble de l’encodage</span><span class="sxs-lookup"><span data-stu-id="de476-104">Encoding overview</span></span>
<span data-ttu-id="de476-105">Azure Media Services propose plusieurs options pour l’encodage de hello de support dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="de476-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="de476-106">Lorsque vous démarrez avec Media Services, il est différence de hello toounderstand important entre les codecs et formats de fichier.</span><span class="sxs-lookup"><span data-stu-id="de476-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="de476-107">Les codecs sont des logiciels de hello qui implémente les algorithmes de compression/décompression hello tandis que les formats de fichier sont des conteneurs qui contiennent la vidéo de hello compressé.</span><span class="sxs-lookup"><span data-stu-id="de476-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="de476-108">Media Services fournit l’empaquetage dynamique qui vous permet de toodeliver votre vitesse de transmission adaptative MP4 ou Smooth Streaming encodé contenu de diffusion en continu des formats pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) sans que vous ayez toore-package dans ces formats de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="de476-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="de476-109">Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état.</span><span class="sxs-lookup"><span data-stu-id="de476-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="de476-110">toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état.</span><span class="sxs-lookup"><span data-stu-id="de476-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="de476-111">avantage tootake de [empaquetage dynamique](media-services-dynamic-packaging-overview.md), toodo, hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="de476-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="de476-112">En outre, encoder votre fichier source dans un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif (les étapes de codage hello sont décrites plus loin dans ce didacticiel).</span><span class="sxs-lookup"><span data-stu-id="de476-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="de476-113">Media Services prend en charge suivantes d’hello sur les encodeurs à la demande qui sont décrites dans cet article :</span><span class="sxs-lookup"><span data-stu-id="de476-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="de476-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="de476-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="de476-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="de476-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="de476-116">Cet article donne une vue d’ensemble de la demande des encodeurs de support et fournit des liens tooarticles qui fournissent des informations plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="de476-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="de476-117">rubrique de Hello compare également les encodeurs hello.</span><span class="sxs-lookup"><span data-stu-id="de476-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="de476-118">Par défaut, chaque compte Media Services peut avoir une tâche d’encodage active à la fois.</span><span class="sxs-lookup"><span data-stu-id="de476-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="de476-119">Vous pouvez réserver les unités d’encodage qui vous permettent de toohave s’exécutant simultanément, un pour chaque unité d’encodage réservée que vous achetez plusieurs tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="de476-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="de476-120">Pour plus d’informations, consultez [Mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de476-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="de476-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="de476-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="de476-122">Comment toouse</span><span class="sxs-lookup"><span data-stu-id="de476-122">How toouse</span></span>
[<span data-ttu-id="de476-123">Comment tooencode avec Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="de476-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="de476-124">Formats</span><span class="sxs-lookup"><span data-stu-id="de476-124">Formats</span></span>
[<span data-ttu-id="de476-125">Formats et codecs</span><span class="sxs-lookup"><span data-stu-id="de476-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="de476-126">Présélections</span><span class="sxs-lookup"><span data-stu-id="de476-126">Presets</span></span>
<span data-ttu-id="de476-127">Encodeur de support Standard est configuré d’à l’aide d’une des présélections d’encodeur hello décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="de476-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="de476-128">Métadonnées d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="de476-128">Input and output metadata</span></span>
<span data-ttu-id="de476-129">Hello encodeurs des métadonnées d’entrée sont décrit [ici](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="de476-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="de476-130">Hello encodeurs sortie métadonnées décrit [ici](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="de476-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="de476-131">Génération de miniatures</span><span class="sxs-lookup"><span data-stu-id="de476-131">Generate thumbnails</span></span>
<span data-ttu-id="de476-132">Pour plus d’informations, consultez [comment miniatures toogenerate à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="de476-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="de476-133">Découpage de vidéos (extrait)</span><span class="sxs-lookup"><span data-stu-id="de476-133">Trim videos (clipping)</span></span>
<span data-ttu-id="de476-134">Pour plus d’informations, consultez [comment vidéos tootrim à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="de476-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="de476-135">Création de superpositions</span><span class="sxs-lookup"><span data-stu-id="de476-135">Create overlays</span></span>
<span data-ttu-id="de476-136">Pour plus d’informations, consultez [comment superpositions toocreate à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="de476-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="de476-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="de476-137">See also</span></span>
[<span data-ttu-id="de476-138">blog de Media Services Hello</span><span class="sxs-lookup"><span data-stu-id="de476-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="de476-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="de476-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="de476-140">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="de476-140">Overview</span></span>
[<span data-ttu-id="de476-141">Présentation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="de476-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="de476-142">Comment toouse</span><span class="sxs-lookup"><span data-stu-id="de476-142">How toouse</span></span>
<span data-ttu-id="de476-143">Media Encoder Premium Workflow se configure à l’aide de flux de travail complexes.</span><span class="sxs-lookup"><span data-stu-id="de476-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="de476-144">Fichiers de flux de travail peut être créés et mis à jour avec hello [le Concepteur de flux de travail](media-services-workflow-designer.md) outil.</span><span class="sxs-lookup"><span data-stu-id="de476-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="de476-145">Comment tooUse Premium encodage dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="de476-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="de476-146">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="de476-146">Known issues</span></span>
<span data-ttu-id="de476-147">Si votre vidéo d’entrée ne contient pas de sous-titrage, hello de sortie Qu'actif contient toujours un fichier TTML vide.</span><span class="sxs-lookup"><span data-stu-id="de476-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="de476-148">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="de476-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="de476-149">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="de476-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="de476-150">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="de476-150">Related articles</span></span>
* [<span data-ttu-id="de476-151">Exécution de tâches d’encodage avancées via la personnalisation des présélections Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="de476-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="de476-152">Quotas et limitations</span><span class="sxs-lookup"><span data-stu-id="de476-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
