---
title: "vue d’ensemble de mise en package dynamique de Media Services aaaAzure | Documents Microsoft"
description: "fournit les rubrique Hello et vue d’ensemble de l’empaquetage dynamique."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="3f8ad-103">l’empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="3f8ad-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="3f8ad-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3f8ad-104">Overview</span></span>
<span data-ttu-id="3f8ad-105">Microsoft Azure Media Services peut être utilisé toodeliver source du média nombreux formats de fichiers et formats de diffusion en continu de contenus multimédias protection du contenu formats tooa diverses technologies clientes (par exemple, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="3f8ad-106">Ces clients comprennent différents protocoles. Par exemple, iOS nécessite un format HTTP Live Streaming (HLS) V4, tandis que Silverlight et Xbox nécessitent le format Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="3f8ad-107">Si vous disposez d’un ensemble de fichiers à débit adaptatif (plusieurs débits binaires) MP4 les fichiers (ISO Base Media 14496-12) ou un ensemble de fichiers de diffusion en continu lisse à débit adaptatif que vous souhaitez tooclients tooserve qui comprennent MPEG DASH, HLS ou Smooth Streaming, vous devez tirer profit de média Services d’empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="3f8ad-108">Avec l’empaquetage dynamique, vous devez est toocreate une ressource qui contient un ensemble de fichiers MP4 ou de fichiers de diffusion en continu lisse à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="3f8ad-109">Ensuite, en fonction hello le format spécifié dans le manifeste de hello ou demande de fragment, hello à la demande de diffusion en continu serveur garantit que vous recevez des flux de hello protocole hello que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="3f8ad-110">Par conséquent, vous devez uniquement toostore et payer pour les fichiers hello dans un seul format de stockage et le service Media Services pour la génération et fournit hello de réponse appropriée en fonction des demandes d’un client.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="3f8ad-111">Hello diagramme suivant illustre encodage traditionnel hello et flux de travail empaquetage statique.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Encodage statique](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="3f8ad-113">Hello diagramme suivant montre du flux de travail hello empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Encodage dynamique](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="3f8ad-115">Scénario courant</span><span class="sxs-lookup"><span data-stu-id="3f8ad-115">Common scenario</span></span>
1. <span data-ttu-id="3f8ad-116">Téléchargez un fichier d'entrée (appelé fichier mezzanine).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="3f8ad-117">Par exemple, H.264, MP4 ou WMV (pour la liste des formats pris en charge hello consultez [Formats pris en charge par hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="3f8ad-118">Encoder vos jeux de mezzanine fichier tooH.264 MP4 à débit adaptatif.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="3f8ad-119">Publier asset hello contenant hello ensemble à débit adaptatif MP4 en créant hello recherche de la demande.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="3f8ad-120">Générez des hello tooaccess des URL de diffusion en continu et diffuser votre contenu.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="3f8ad-121">Préparation des éléments multimédias pour un streaming dynamique</span><span class="sxs-lookup"><span data-stu-id="3f8ad-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="3f8ad-122">tooprepare votre élément multimédia pour dynamique de diffusion en continu vous avez deux options :</span><span class="sxs-lookup"><span data-stu-id="3f8ad-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="3f8ad-123">[Chargez un fichier maître](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="3f8ad-124">[Utiliser des jeux de hello Media Encoder Standard encodeur tooproduce H.264 MP4 à débit adaptatif](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="3f8ad-125">[Diffusez votre contenu](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f8ad-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="3f8ad-126"><a id="unsupported_formats"></a>Formats non pris en charge pour l'empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="3f8ad-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="3f8ad-127">Hello des formats de fichier source suivants ne sont pas pris en charge par l’empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="3f8ad-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="3f8ad-128">Fichiers MP4 Dolby Digital</span><span class="sxs-lookup"><span data-stu-id="3f8ad-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="3f8ad-129">Fichiers Smooth Streaming Dolby Digital</span><span class="sxs-lookup"><span data-stu-id="3f8ad-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3f8ad-130">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="3f8ad-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3f8ad-131">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3f8ad-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

