---
title: "Vue d’ensemble de l’empaquetage dynamique Azure Media Services | Microsoft Docs"
description: Cette rubrique donne une vue d'ensemble de l'empaquetage dynamique.
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
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="22d85-103">Empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="22d85-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="22d85-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="22d85-104">Overview</span></span>
<span data-ttu-id="22d85-105">Vous pouvez utiliser Microsoft Azure Media Services pour distribuer de nombreux formats de fichiers sources multimédias, formats de streaming de contenu multimédia et formats de protection de contenu à diverses technologies clientes (par exemple, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="22d85-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="22d85-106">Ces clients comprennent différents protocoles. Par exemple, iOS nécessite un format HTTP Live Streaming (HLS) V4, tandis que Silverlight et Xbox nécessitent le format Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="22d85-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="22d85-107">Si vous voulez transmettre un ensemble de fichiers MP4 (ISO Base Media 14496-12) ou de fichiers Smooth Streaming à vitesse de transmission adaptative, à des clients qui utilisent le format MPEG DASH, HLS ou Smooth Streaming, nous vous recommandons de tirer profit de l'empaquetage dynamique Media Services.</span><span class="sxs-lookup"><span data-stu-id="22d85-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="22d85-108">Avec l'empaquetage dynamique, il vous suffit de créer un élément multimédia contenant un ensemble de fichiers MP4 ou de fichiers Smooth Streaming à vitesse de transmission adaptative.</span><span class="sxs-lookup"><span data-stu-id="22d85-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="22d85-109">Ensuite, en fonction du format spécifié dans le manifeste ou la demande de fragment, le serveur de streaming à la demande s'assure que vous recevez le flux conforme au protocole choisi.</span><span class="sxs-lookup"><span data-stu-id="22d85-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="22d85-110">Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Le service Media Services se charge de créer et de fournir la réponse appropriée en fonction des demandes des clients.</span><span class="sxs-lookup"><span data-stu-id="22d85-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="22d85-111">Le diagramme suivant illustre le flux traditionnel d'encodage et d'empaquetage statique.</span><span class="sxs-lookup"><span data-stu-id="22d85-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Encodage statique](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="22d85-113">Le diagramme suivant illustre le flux d'empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="22d85-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Encodage dynamique](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="22d85-115">Scénario courant</span><span class="sxs-lookup"><span data-stu-id="22d85-115">Common scenario</span></span>
1. <span data-ttu-id="22d85-116">Téléchargez un fichier d'entrée (appelé fichier mezzanine).</span><span class="sxs-lookup"><span data-stu-id="22d85-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="22d85-117">Par exemple, H.264, MP4 ou WMV (pour obtenir la liste des formats pris en charge, consultez [Formats pris en charge par Media Encoder Standard](media-services-media-encoder-standard-formats.md)).</span><span class="sxs-lookup"><span data-stu-id="22d85-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="22d85-118">Encodez votre fichier mezzanine en ensembles de fichiers MP4 à vitesse de transmission adaptative H.264.</span><span class="sxs-lookup"><span data-stu-id="22d85-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="22d85-119">Publiez l'élément multimédia qui contient l'ensemble de fichiers MP4 à vitesse de transmission adaptative en créant le localisateur à la demande.</span><span class="sxs-lookup"><span data-stu-id="22d85-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="22d85-120">Générez les URL de streaming pour accéder à votre contenu et le diffuser en continu.</span><span class="sxs-lookup"><span data-stu-id="22d85-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="22d85-121">Préparation des éléments multimédias pour un streaming dynamique</span><span class="sxs-lookup"><span data-stu-id="22d85-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="22d85-122">Pour préparer un élément multimédia à un streaming dynamique, vous disposez de deux options :</span><span class="sxs-lookup"><span data-stu-id="22d85-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="22d85-123">[Chargez un fichier maître](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="22d85-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="22d85-124">[Utilisez l’encodeur Media Encoder Standard pour produire des ensembles de fichiers MP4 à vitesse de transmission adaptative H.264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="22d85-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="22d85-125">[Diffusez votre contenu](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22d85-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="22d85-126"><a id="unsupported_formats"></a>Formats non pris en charge pour l'empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="22d85-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="22d85-127">Les formats de fichiers sources suivants ne sont pas pris en charge par l'empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="22d85-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="22d85-128">Fichiers MP4 Dolby Digital</span><span class="sxs-lookup"><span data-stu-id="22d85-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="22d85-129">Fichiers Smooth Streaming Dolby Digital</span><span class="sxs-lookup"><span data-stu-id="22d85-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="22d85-130">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="22d85-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22d85-131">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="22d85-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

