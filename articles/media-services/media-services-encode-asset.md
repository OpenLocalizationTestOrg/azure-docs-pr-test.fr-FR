---
title: "Vue d’ensemble et comparaison d’encodeurs multimédia à la demande Azure | Microsoft Docs"
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
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="8d7c8-103">Vue d’ensemble et comparaison d’encodeurs multimédia à la demande Azure</span><span class="sxs-lookup"><span data-stu-id="8d7c8-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="8d7c8-104">Vue d’ensemble de l’encodage</span><span class="sxs-lookup"><span data-stu-id="8d7c8-104">Encoding overview</span></span>
<span data-ttu-id="8d7c8-105">Azure Media Services fournit plusieurs options pour l’encodage de fichiers multimédias dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="8d7c8-106">Quand vous commencez à utiliser Media Services, il est important de bien comprendre la différence entre les codecs et les formats de fichiers.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="8d7c8-107">Les codecs sont les logiciels qui implémentent les algorithmes de compression/décompression, tandis que les formats de fichiers sont des conteneurs qui contiennent la vidéo compressée.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="8d7c8-108">Media Services fournit l’empaquetage dynamique qui permet de distribuer un contenu en diffusion continue en MP4 ou Smooth Streaming dans un format pris en charge par Media Services (MPEG DASH, HLS, Smooth Streaming) sans avoir à recréer de nouveaux packages dans ces formats.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="8d7c8-109">Une fois votre compte AMS créé, un point de terminaison de streaming **par défaut** est ajouté à votre compte à l’état **Arrêté**.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="8d7c8-110">Pour démarrer la diffusion en continu de votre contenu et tirer parti de l’empaquetage et du chiffrement dynamiques, le point de terminaison de streaming à partir duquel vous souhaitez diffuser du contenu doit se trouver à l’état **En cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="8d7c8-111">Pour tirer parti de l’ [empaquetage dynamique](media-services-dynamic-packaging-overview.md), vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d7c8-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="8d7c8-112">De même, encoder votre fichier source dans un ensemble de fichiers mp4 à débit adaptatif ou de fichiers Smooth Streaming à débit adaptatif (les étapes de codage sont décrites plus loin dans ce didacticiel).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="8d7c8-113">Media Services prend en charge les éléments suivants sur les encodeurs à la demande décrits dans cet article :</span><span class="sxs-lookup"><span data-stu-id="8d7c8-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="8d7c8-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="8d7c8-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="8d7c8-115">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="8d7c8-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="8d7c8-116">Cet article donne un bref aperçu des encodeurs multimédia à la demande et fournit des liens vers des articles fournissant des informations plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="8d7c8-117">Cette rubrique compare également les encodeurs.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="8d7c8-118">Par défaut, chaque compte Media Services peut avoir une tâche d’encodage active à la fois.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="8d7c8-119">Vous pouvez réserver des unités d’encodage qui vous permettent d’exécuter plusieurs tâches d’encodage simultanément, une pour chaque unité réservée d’encodage que vous achetez.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="8d7c8-120">Pour plus d’informations, consultez [Mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="8d7c8-121">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="8d7c8-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="8d7c8-122">Utilisation</span><span class="sxs-lookup"><span data-stu-id="8d7c8-122">How to use</span></span>
[<span data-ttu-id="8d7c8-123">Encodage avec Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="8d7c8-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="8d7c8-124">Formats</span><span class="sxs-lookup"><span data-stu-id="8d7c8-124">Formats</span></span>
[<span data-ttu-id="8d7c8-125">Formats et codecs</span><span class="sxs-lookup"><span data-stu-id="8d7c8-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="8d7c8-126">Présélections</span><span class="sxs-lookup"><span data-stu-id="8d7c8-126">Presets</span></span>
<span data-ttu-id="8d7c8-127">Media Encoder Standard est configuré à l’aide d’une des présélections d’encodeur décrites [ici](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="8d7c8-128">Métadonnées d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="8d7c8-128">Input and output metadata</span></span>
<span data-ttu-id="8d7c8-129">Les métadonnées d’entrée des encodeurs sont décrites [ici](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="8d7c8-130">Les métadonnées de sortie des encodeurs sont décrites [ici](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="8d7c8-131">Génération de miniatures</span><span class="sxs-lookup"><span data-stu-id="8d7c8-131">Generate thumbnails</span></span>
<span data-ttu-id="8d7c8-132">Pour plus d’informations, consultez [Génération de miniatures à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="8d7c8-133">Découpage de vidéos (extrait)</span><span class="sxs-lookup"><span data-stu-id="8d7c8-133">Trim videos (clipping)</span></span>
<span data-ttu-id="8d7c8-134">Pour plus d’informations, consultez [Découpage de vidéos à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="8d7c8-135">Création de superpositions</span><span class="sxs-lookup"><span data-stu-id="8d7c8-135">Create overlays</span></span>
<span data-ttu-id="8d7c8-136">Pour plus d’informations, consultez [Création de superpositions à l’aide de Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="8d7c8-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="8d7c8-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8d7c8-137">See also</span></span>
[<span data-ttu-id="8d7c8-138">Blog sur Media Services</span><span class="sxs-lookup"><span data-stu-id="8d7c8-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="8d7c8-139">Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="8d7c8-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="8d7c8-140">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8d7c8-140">Overview</span></span>
[<span data-ttu-id="8d7c8-141">Présentation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8d7c8-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="8d7c8-142">Utilisation</span><span class="sxs-lookup"><span data-stu-id="8d7c8-142">How to use</span></span>
<span data-ttu-id="8d7c8-143">Media Encoder Premium Workflow se configure à l’aide de flux de travail complexes.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="8d7c8-144">Les fichiers de flux de travail peuvent être créés et mis à jour à l’aide de l’outil [Concepteur de flux de travail](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="8d7c8-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="8d7c8-145">Utilisation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8d7c8-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="8d7c8-146">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="8d7c8-146">Known issues</span></span>
<span data-ttu-id="8d7c8-147">Si votre vidéo d’entrée ne contient pas de sous-titres, l’élément multimédia de sortie actif comportera toujours un fichier TTML vide.</span><span class="sxs-lookup"><span data-stu-id="8d7c8-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="8d7c8-148">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="8d7c8-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8d7c8-149">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="8d7c8-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="8d7c8-150">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="8d7c8-150">Related articles</span></span>
* [<span data-ttu-id="8d7c8-151">Exécution de tâches d’encodage avancées via la personnalisation des présélections Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="8d7c8-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="8d7c8-152">Quotas et limitations</span><span class="sxs-lookup"><span data-stu-id="8d7c8-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
