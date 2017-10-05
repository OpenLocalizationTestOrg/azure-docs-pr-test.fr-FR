---
title: "Schéma de métadonnées d’entrée Azure Media Services | Microsoft Docs"
description: "Cette rubrique fournit une vue d’ensemble du schéma de métadonnées d’entrée d’Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 4787e4033e1afda6339b0b917263ecc165e400ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="input-metadata"></a><span data-ttu-id="dd997-103">Métadonnées d'entrée</span><span class="sxs-lookup"><span data-stu-id="dd997-103">Input Metadata</span></span>
<span data-ttu-id="dd997-104">Un travail d’encodage est associé à un élément multimédia d’entrée (ou plusieurs) sur lequel vous souhaitez effectuer des tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="dd997-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span>  <span data-ttu-id="dd997-105">À l’achèvement d’une tâche, une ressource de sortie est générée.</span><span class="sxs-lookup"><span data-stu-id="dd997-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="dd997-106">L’élément multimédia de sortie contient la vidéo, l’audio, les miniatures, le manifeste, et ainsi de suite. Il contient également un fichier avec des métadonnées relatives à l’élément multimédia d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dd997-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="dd997-107">Le nom du fichier XML de métadonnées a le format suivant : &lt;asset_id&gt;_metadata.xml (par exemple, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), où &lt;asset_id&gt; est la valeur AssetId de l’élément multimédia d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dd997-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span></span>  

<span data-ttu-id="dd997-108">Si vous souhaitez examiner le fichier de métadonnées, vous pouvez créer un localisateur **SAS** et télécharger le fichier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="dd997-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span> <span data-ttu-id="dd997-109">Vous trouverez un exemple illustrant comment créer un localisateur SAS et télécharger un fichier dans la rubrique [Utilisation des extensions du SDK Media Services .NET](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd997-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="dd997-110">Cette rubrique décrit les éléments et types du schéma XML sur lesquels les métadonnées d’entrée (&lt;asset_id&gt;_metadata.xml) sont basées.</span><span class="sxs-lookup"><span data-stu-id="dd997-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="dd997-111">Pour plus d’informations sur le fichier qui contient des métadonnées sur la ressource de sortie, consultez [Métadonnées de sortie](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="dd997-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="dd997-112">Vous pouvez trouver le [Code du schéma](media-services-input-metadata-schema.md#code) et un [exemple de XML](media-services-input-metadata-schema.md#xml) à la fin de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="dd997-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="dd997-113"><a name="AssetFiles"></a> Élément AssetFiles (élément racine)</span><span class="sxs-lookup"><span data-stu-id="dd997-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="dd997-114">Contient une collection [d’éléments AssetFile](media-services-input-metadata-schema.md#AssetFile) pour le travail d’encodage.</span><span class="sxs-lookup"><span data-stu-id="dd997-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span></span>  

<span data-ttu-id="dd997-115">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="dd997-116">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-116">Name</span></span> | <span data-ttu-id="dd997-117">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd997-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="dd997-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="dd997-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="dd997-120">Un élément enfant unique.</span><span class="sxs-lookup"><span data-stu-id="dd997-120">A single child element.</span></span> <span data-ttu-id="dd997-121">Pour plus d'informations, consultez la page [Élément AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="dd997-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="dd997-122"><a name="AssetFile"></a> Élément AssetFile</span><span class="sxs-lookup"><span data-stu-id="dd997-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="dd997-123">Contient des attributs et des éléments qui décrivent une ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="dd997-124">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-125">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-125">Attributes</span></span>
| <span data-ttu-id="dd997-126">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-126">Name</span></span> | <span data-ttu-id="dd997-127">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-127">Type</span></span> | <span data-ttu-id="dd997-128">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="dd997-129">**Name**</span></span><br /><br /> <span data-ttu-id="dd997-130">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-130">Required</span></span> |<span data-ttu-id="dd997-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-131">**xs:string**</span></span> |<span data-ttu-id="dd997-132">Nom du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-132">Asset file name.</span></span> |
| <span data-ttu-id="dd997-133">**Taille**</span><span class="sxs-lookup"><span data-stu-id="dd997-133">**Size**</span></span><br /><br /> <span data-ttu-id="dd997-134">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-134">Required</span></span> |<span data-ttu-id="dd997-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="dd997-135">**xs:long**</span></span> |<span data-ttu-id="dd997-136">Taille du fichier de ressource en octets.</span><span class="sxs-lookup"><span data-stu-id="dd997-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="dd997-137">**Durée**</span><span class="sxs-lookup"><span data-stu-id="dd997-137">**Duration**</span></span><br /><br /> <span data-ttu-id="dd997-138">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-138">Required</span></span> |<span data-ttu-id="dd997-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="dd997-139">**xs:duration**</span></span> |<span data-ttu-id="dd997-140">Durée de lecture du contenu.</span><span class="sxs-lookup"><span data-stu-id="dd997-140">Content play back duration.</span></span> <span data-ttu-id="dd997-141">Exemple : Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="dd997-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="dd997-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="dd997-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="dd997-143">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-143">Required</span></span> |<span data-ttu-id="dd997-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-144">**xs:int**</span></span> |<span data-ttu-id="dd997-145">Nombre de flux dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-145">Number of streams in the asset file.</span></span> |
| <span data-ttu-id="dd997-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="dd997-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="dd997-147">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-147">Required</span></span> |<span data-ttu-id="dd997-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-148">**xs:string**</span></span> |<span data-ttu-id="dd997-149">Noms de format.</span><span class="sxs-lookup"><span data-stu-id="dd997-149">Format names.</span></span> |
| <span data-ttu-id="dd997-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="dd997-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="dd997-151">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-151">Required</span></span> |<span data-ttu-id="dd997-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-152">**xs:string**</span></span> |<span data-ttu-id="dd997-153">Noms détaillés des formats.</span><span class="sxs-lookup"><span data-stu-id="dd997-153">Format verbose names.</span></span> |
| <span data-ttu-id="dd997-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="dd997-154">**StartTime**</span></span> |<span data-ttu-id="dd997-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="dd997-155">**xs:duration**</span></span> |<span data-ttu-id="dd997-156">Heure de début du contenu.</span><span class="sxs-lookup"><span data-stu-id="dd997-156">Content start time.</span></span> <span data-ttu-id="dd997-157">Exemple : StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="dd997-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="dd997-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="dd997-158">**OverallBitRate**</span></span> |<span data-ttu-id="dd997-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-159">**xs:int**</span></span> |<span data-ttu-id="dd997-160">Vitesse de transmission moyenne du fichier de ressource en kbit/s.</span><span class="sxs-lookup"><span data-stu-id="dd997-160">Average bitrate of the asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="dd997-161">Les 4 éléments enfants suivants doivent apparaître dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="dd997-161">The following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="dd997-162">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="dd997-162">Child elements</span></span>
| <span data-ttu-id="dd997-163">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-163">Name</span></span> | <span data-ttu-id="dd997-164">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-164">Type</span></span> | <span data-ttu-id="dd997-165">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-166">**Programmes**</span><span class="sxs-lookup"><span data-stu-id="dd997-166">**Programs**</span></span><br /><br /> <span data-ttu-id="dd997-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="dd997-167">minOccurs="0"</span></span> | |<span data-ttu-id="dd997-168">Collection de tous les [éléments Programs](media-services-input-metadata-schema.md#Programs) lorsque le fichier de ressource est au format MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="dd997-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="dd997-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="dd997-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="dd997-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="dd997-170">minOccurs="0"</span></span> | |<span data-ttu-id="dd997-171">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="dd997-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="dd997-172">Cet élément contient une collection de tous les [éléments VideoTracks](media-services-input-metadata-schema.md#VideoTracks) qui font partie du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="dd997-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="dd997-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="dd997-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="dd997-174">minOccurs="0"</span></span> | |<span data-ttu-id="dd997-175">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="dd997-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="dd997-176">Cet élément contient une collection de tous les [éléments AudioTracks](media-services-input-metadata-schema.md#AudioTracks) qui font partie du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="dd997-177">**Métadonnées**</span><span class="sxs-lookup"><span data-stu-id="dd997-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="dd997-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="dd997-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="dd997-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="dd997-180">Les métadonnées du fichier de ressource représentées sous la forme de chaînes clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="dd997-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="dd997-181">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd997-181">For example:</span></span><br /><br /> <span data-ttu-id="dd997-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="dd997-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="dd997-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="dd997-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="dd997-184">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-185">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-185">Attributes</span></span>
| <span data-ttu-id="dd997-186">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-186">Name</span></span> | <span data-ttu-id="dd997-187">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-187">Type</span></span> | <span data-ttu-id="dd997-188">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="dd997-189">**Id**</span></span><br /><br /> <span data-ttu-id="dd997-190">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-190">Required</span></span> |<span data-ttu-id="dd997-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-191">**xs:int**</span></span> |<span data-ttu-id="dd997-192">Index de base zéro de cette piste audio ou vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="dd997-193">Il ne s’agit pas nécessairement du trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="dd997-193">This is not necessarily that the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="dd997-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="dd997-194">**Codec**</span></span> |<span data-ttu-id="dd997-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-195">**xs:string**</span></span> |<span data-ttu-id="dd997-196">Chaîne de codec de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-196">Video track codec string.</span></span> |
| <span data-ttu-id="dd997-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="dd997-197">**CodecLongName**</span></span> |<span data-ttu-id="dd997-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-198">**xs:string**</span></span> |<span data-ttu-id="dd997-199">Nom long du codec de piste audio ou vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="dd997-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="dd997-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="dd997-201">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-201">Required</span></span> |<span data-ttu-id="dd997-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-202">**xs:string**</span></span> |<span data-ttu-id="dd997-203">Période.</span><span class="sxs-lookup"><span data-stu-id="dd997-203">Time base.</span></span> <span data-ttu-id="dd997-204">Exemple : TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="dd997-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="dd997-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="dd997-205">**NumberOfFrames**</span></span> |<span data-ttu-id="dd997-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-206">**xs:int**</span></span> |<span data-ttu-id="dd997-207">Nombre de trames (présent pour les pistes vidéo).</span><span class="sxs-lookup"><span data-stu-id="dd997-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="dd997-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="dd997-208">**StartTime**</span></span> |<span data-ttu-id="dd997-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="dd997-209">**xs:duration**</span></span> |<span data-ttu-id="dd997-210">Suivre l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="dd997-210">Track start time.</span></span> <span data-ttu-id="dd997-211">Exemple : StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="dd997-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="dd997-212">**Durée**</span><span class="sxs-lookup"><span data-stu-id="dd997-212">**Duration**</span></span> |<span data-ttu-id="dd997-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="dd997-213">**xs:duration**</span></span> |<span data-ttu-id="dd997-214">Durée de la piste.</span><span class="sxs-lookup"><span data-stu-id="dd997-214">Track duration.</span></span> <span data-ttu-id="dd997-215">Exemple : Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="dd997-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="dd997-216">Les 2 éléments enfants suivants doivent apparaître dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="dd997-216">The following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="dd997-217">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="dd997-217">Child elements</span></span>
| <span data-ttu-id="dd997-218">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-218">Name</span></span> | <span data-ttu-id="dd997-219">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-219">Type</span></span> | <span data-ttu-id="dd997-220">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="dd997-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="dd997-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="dd997-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="dd997-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="dd997-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="dd997-224">Contient des informations de présentation (par exemple, si une piste audio particulière est destinée aux utilisateurs malvoyants).</span><span class="sxs-lookup"><span data-stu-id="dd997-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="dd997-225">**Métadonnées**</span><span class="sxs-lookup"><span data-stu-id="dd997-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="dd997-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="dd997-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="dd997-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="dd997-228">Des chaînes clé/valeur génériques qui peuvent être utilisées pour contenir différents types d’informations.</span><span class="sxs-lookup"><span data-stu-id="dd997-228">Generic key/value strings that can be used to hold a variety of information.</span></span> <span data-ttu-id="dd997-229">Par exemple, key=”language”, et value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="dd997-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="dd997-230"><a name="AudioTrackType"></a> AudioTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="dd997-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="dd997-231">**AudioTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="dd997-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="dd997-232">Le type représente une piste audio spécifique dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-232">The type represents a specific audio track in the asset file.</span></span>  

 <span data-ttu-id="dd997-233">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-234">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-234">Attributes</span></span>
| <span data-ttu-id="dd997-235">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-235">Name</span></span> | <span data-ttu-id="dd997-236">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-236">Type</span></span> | <span data-ttu-id="dd997-237">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="dd997-238">**SampleFormat**</span></span> |<span data-ttu-id="dd997-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-239">**xs:string**</span></span> |<span data-ttu-id="dd997-240">Exemple de format.</span><span class="sxs-lookup"><span data-stu-id="dd997-240">Sample format.</span></span> |
| <span data-ttu-id="dd997-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="dd997-241">**ChannelLayout**</span></span> |<span data-ttu-id="dd997-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-242">**xs:string**</span></span> |<span data-ttu-id="dd997-243">Disposition de canal.</span><span class="sxs-lookup"><span data-stu-id="dd997-243">Channel layout.</span></span> |
| <span data-ttu-id="dd997-244">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="dd997-244">**Channels**</span></span><br /><br /> <span data-ttu-id="dd997-245">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-245">Required</span></span> |<span data-ttu-id="dd997-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-246">**xs:int**</span></span> |<span data-ttu-id="dd997-247">Nombre (0 ou plus) de canaux audio.</span><span class="sxs-lookup"><span data-stu-id="dd997-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="dd997-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="dd997-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="dd997-249">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-249">Required</span></span> |<span data-ttu-id="dd997-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-250">**xs:int**</span></span> |<span data-ttu-id="dd997-251">Taux d’échantillonnage audio en échantillons/sec ou Hz.</span><span class="sxs-lookup"><span data-stu-id="dd997-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="dd997-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="dd997-252">**Bitrate**</span></span> |<span data-ttu-id="dd997-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-253">**xs:int**</span></span> |<span data-ttu-id="dd997-254">Débit binaire audio moyen en bits par seconde, tel que calculé à partir du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-254">Average audio bit rate in bits per second, as calculated from the asset file.</span></span> <span data-ttu-id="dd997-255">Seule la charge utile de flux élémentaire est comptée et la surcharge de packaging n’est pas incluse dans ce nombre.</span><span class="sxs-lookup"><span data-stu-id="dd997-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="dd997-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="dd997-256">**BitsPerSample**</span></span> |<span data-ttu-id="dd997-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-257">**xs:int**</span></span> |<span data-ttu-id="dd997-258">Bits par échantillon pour le type de format wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="dd997-258">Bits per sample for the wFormatTag format type.</span></span> |

## <span data-ttu-id="dd997-259"><a name="VideoTrackType"></a> VideoTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="dd997-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="dd997-260">**VideoTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="dd997-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="dd997-261">Le type représente une piste vidéo spécifique dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-261">The type represents a specific video track in the asset file.</span></span>  

<span data-ttu-id="dd997-262">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-263">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-263">Attributes</span></span>
| <span data-ttu-id="dd997-264">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-264">Name</span></span> | <span data-ttu-id="dd997-265">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-265">Type</span></span> | <span data-ttu-id="dd997-266">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="dd997-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="dd997-268">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-268">Required</span></span> |<span data-ttu-id="dd997-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-269">**xs:string**</span></span> |<span data-ttu-id="dd997-270">Code FourCC du codec vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="dd997-271">**Profil**</span><span class="sxs-lookup"><span data-stu-id="dd997-271">**Profile**</span></span> |<span data-ttu-id="dd997-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-272">**xs:string**</span></span> |<span data-ttu-id="dd997-273">Profil de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-273">Video track's profile.</span></span> |
| <span data-ttu-id="dd997-274">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="dd997-274">**Level**</span></span> |<span data-ttu-id="dd997-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-275">**xs:string**</span></span> |<span data-ttu-id="dd997-276">Niveau de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-276">Video track's level.</span></span> |
| <span data-ttu-id="dd997-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="dd997-277">**PixelFormat**</span></span> |<span data-ttu-id="dd997-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-278">**xs:string**</span></span> |<span data-ttu-id="dd997-279">Format de pixel de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="dd997-280">**Largeur**</span><span class="sxs-lookup"><span data-stu-id="dd997-280">**Width**</span></span><br /><br /> <span data-ttu-id="dd997-281">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-281">Required</span></span> |<span data-ttu-id="dd997-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-282">**xs:int**</span></span> |<span data-ttu-id="dd997-283">Largeur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="dd997-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="dd997-284">**Hauteur**</span><span class="sxs-lookup"><span data-stu-id="dd997-284">**Height**</span></span><br /><br /> <span data-ttu-id="dd997-285">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-285">Required</span></span> |<span data-ttu-id="dd997-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-286">**xs:int**</span></span> |<span data-ttu-id="dd997-287">Hauteur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="dd997-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="dd997-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="dd997-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="dd997-289">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-289">Required</span></span> |<span data-ttu-id="dd997-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="dd997-290">**xs:double**</span></span> |<span data-ttu-id="dd997-291">Numérateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="dd997-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="dd997-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="dd997-293">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-293">Required</span></span> |<span data-ttu-id="dd997-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="dd997-294">**xs:double**</span></span> |<span data-ttu-id="dd997-295">Dénominateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="dd997-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="dd997-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="dd997-297">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-297">Required</span></span> |<span data-ttu-id="dd997-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="dd997-298">**xs:double**</span></span> |<span data-ttu-id="dd997-299">Numérateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="dd997-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="dd997-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="dd997-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="dd997-301">**xs:double**</span></span> |<span data-ttu-id="dd997-302">Numérateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="dd997-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="dd997-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="dd997-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="dd997-304">**xs:double**</span></span> |<span data-ttu-id="dd997-305">Dénominateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd997-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="dd997-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="dd997-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="dd997-307">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-307">Required</span></span> |<span data-ttu-id="dd997-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="dd997-308">**xs:decimal**</span></span> |<span data-ttu-id="dd997-309">Fréquence d’images vidéo mesurée au format .3f.</span><span class="sxs-lookup"><span data-stu-id="dd997-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="dd997-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="dd997-310">**Bitrate**</span></span> |<span data-ttu-id="dd997-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-311">**xs:int**</span></span> |<span data-ttu-id="dd997-312">Débit binaire vidéo moyen en kilobits par seconde, tel que calculé à partir du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span></span> <span data-ttu-id="dd997-313">Seule la charge utile de flux élémentaire est comptée et la surcharge de packaging n’est pas incluse.</span><span class="sxs-lookup"><span data-stu-id="dd997-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span></span> |
| <span data-ttu-id="dd997-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="dd997-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="dd997-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-315">**xs:int**</span></span> |<span data-ttu-id="dd997-316">Vitesse de transmission moyenne GOP maximum pour cette piste vidéo, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="dd997-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="dd997-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="dd997-317">**HasBFrames**</span></span> |<span data-ttu-id="dd997-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-318">**xs:int**</span></span> |<span data-ttu-id="dd997-319">Numéro de piste vidéo des trames B.</span><span class="sxs-lookup"><span data-stu-id="dd997-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="dd997-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="dd997-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="dd997-321">**MetadataType** est un type complexe global qui décrit les métadonnées d’un fichier de ressource en tant que chaînes clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="dd997-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="dd997-322">Par exemple, key=”language”, et value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="dd997-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="dd997-323">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-324">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-324">Attributes</span></span>
| <span data-ttu-id="dd997-325">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-325">Name</span></span> | <span data-ttu-id="dd997-326">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-326">Type</span></span> | <span data-ttu-id="dd997-327">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-328">**key**</span><span class="sxs-lookup"><span data-stu-id="dd997-328">**key**</span></span><br /><br /> <span data-ttu-id="dd997-329">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-329">Required</span></span> |<span data-ttu-id="dd997-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-330">**xs:string**</span></span> |<span data-ttu-id="dd997-331">La clé dans la paire clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="dd997-331">The key in the key/value pair.</span></span> |
| <span data-ttu-id="dd997-332">**value**</span><span class="sxs-lookup"><span data-stu-id="dd997-332">**value**</span></span><br /><br /> <span data-ttu-id="dd997-333">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-333">Required</span></span> |<span data-ttu-id="dd997-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="dd997-334">**xs:string**</span></span> |<span data-ttu-id="dd997-335">La valeur dans la paire clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="dd997-335">The value in the key/value pair.</span></span> |

## <span data-ttu-id="dd997-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="dd997-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="dd997-337">**ProgramType** est un type complexe global qui décrit un programme.</span><span class="sxs-lookup"><span data-stu-id="dd997-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-338">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-338">Attributes</span></span>
| <span data-ttu-id="dd997-339">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-339">Name</span></span> | <span data-ttu-id="dd997-340">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-340">Type</span></span> | <span data-ttu-id="dd997-341">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="dd997-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="dd997-343">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-343">Required</span></span> |<span data-ttu-id="dd997-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-344">**xs:int**</span></span> |<span data-ttu-id="dd997-345">ID de programme</span><span class="sxs-lookup"><span data-stu-id="dd997-345">Program Id</span></span> |
| <span data-ttu-id="dd997-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="dd997-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="dd997-347">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-347">Required</span></span> |<span data-ttu-id="dd997-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-348">**xs:int**</span></span> |<span data-ttu-id="dd997-349">Nombre de programmes.</span><span class="sxs-lookup"><span data-stu-id="dd997-349">Number of programs.</span></span> |
| <span data-ttu-id="dd997-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="dd997-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="dd997-351">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-351">Required</span></span> |<span data-ttu-id="dd997-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-352">**xs:int**</span></span> |<span data-ttu-id="dd997-353">Les tables de correspondance de programme (PMT) contiennent des informations sur les programmes.</span><span class="sxs-lookup"><span data-stu-id="dd997-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="dd997-354">Pour plus d'informations, consultez [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="dd997-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="dd997-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="dd997-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="dd997-356">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-356">Required</span></span> |<span data-ttu-id="dd997-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-357">**xs:int**</span></span> |<span data-ttu-id="dd997-358">Utilisé par le décodeur.</span><span class="sxs-lookup"><span data-stu-id="dd997-358">Used by decoder.</span></span> <span data-ttu-id="dd997-359">Pour plus d'informations, consultez [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="dd997-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="dd997-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="dd997-360">**StartPTS**</span></span> |<span data-ttu-id="dd997-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="dd997-361">**xs: long**</span></span> |<span data-ttu-id="dd997-362">Horodatage de début de présentation.</span><span class="sxs-lookup"><span data-stu-id="dd997-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="dd997-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="dd997-363">**EndPTS**</span></span> |<span data-ttu-id="dd997-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="dd997-364">**xs: long**</span></span> |<span data-ttu-id="dd997-365">Horodatage de fin de présentation.</span><span class="sxs-lookup"><span data-stu-id="dd997-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="dd997-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="dd997-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="dd997-367">**StreamDispositionType** est un type complexe global qui décrit le flux de données.</span><span class="sxs-lookup"><span data-stu-id="dd997-367">**StreamDispositionType** is a global complex type that describes the stream.</span></span>  

<span data-ttu-id="dd997-368">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="dd997-369">Attributs</span><span class="sxs-lookup"><span data-stu-id="dd997-369">Attributes</span></span>
| <span data-ttu-id="dd997-370">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-370">Name</span></span> | <span data-ttu-id="dd997-371">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-371">Type</span></span> | <span data-ttu-id="dd997-372">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-373">**Par défaut**</span><span class="sxs-lookup"><span data-stu-id="dd997-373">**Default**</span></span><br /><br /> <span data-ttu-id="dd997-374">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-374">Required</span></span> |<span data-ttu-id="dd997-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-375">**xs:int**</span></span> |<span data-ttu-id="dd997-376">Définissez cet attribut sur 1 pour indiquer qu’il s’agit de la présentation par défaut.</span><span class="sxs-lookup"><span data-stu-id="dd997-376">Set this attribute to 1 to indicate this is the default presentation.</span></span> |
| <span data-ttu-id="dd997-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="dd997-377">**Dub**</span></span><br /><br /> <span data-ttu-id="dd997-378">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-378">Required</span></span> |<span data-ttu-id="dd997-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-379">**xs:int**</span></span> |<span data-ttu-id="dd997-380">Définissez cet attribut sur 1 pour indiquer qu’il s’agit de la présentation doublée.</span><span class="sxs-lookup"><span data-stu-id="dd997-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span></span> |
| <span data-ttu-id="dd997-381">**Ressource d’origine**</span><span class="sxs-lookup"><span data-stu-id="dd997-381">**Original**</span></span><br /><br /> <span data-ttu-id="dd997-382">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-382">Required</span></span> |<span data-ttu-id="dd997-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-383">**xs:int**</span></span> |<span data-ttu-id="dd997-384">Définissez cet attribut sur 1 pour indiquer qu’il s’agit de la présentation d’origine.</span><span class="sxs-lookup"><span data-stu-id="dd997-384">Set this attribute to 1 to indicate this is the original presentation.</span></span> |
| <span data-ttu-id="dd997-385">**Commentaire**</span><span class="sxs-lookup"><span data-stu-id="dd997-385">**Comment**</span></span><br /><br /> <span data-ttu-id="dd997-386">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-386">Required</span></span> |<span data-ttu-id="dd997-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-387">**xs:int**</span></span> |<span data-ttu-id="dd997-388">Définissez cet attribut sur 1 pour indiquer que cette piste contient des commentaires.</span><span class="sxs-lookup"><span data-stu-id="dd997-388">Set this attribute to 1 to indicate this track contains commentary.</span></span> |
| <span data-ttu-id="dd997-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="dd997-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="dd997-390">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-390">Required</span></span> |<span data-ttu-id="dd997-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-391">**xs:int**</span></span> |<span data-ttu-id="dd997-392">Définissez cet attribut sur 1 pour indiquer que cette piste contient des paroles.</span><span class="sxs-lookup"><span data-stu-id="dd997-392">Set this attribute to 1 to indicate this track contains lyrics.</span></span> |
| <span data-ttu-id="dd997-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="dd997-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="dd997-394">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-394">Required</span></span> |<span data-ttu-id="dd997-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-395">**xs:int**</span></span> |<span data-ttu-id="dd997-396">Définissez cet attribut sur 1 pour indiquer qu’il s’agit d’une piste de karaoké (musique de fond, sans voix).</span><span class="sxs-lookup"><span data-stu-id="dd997-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="dd997-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="dd997-397">**Forced**</span></span><br /><br /> <span data-ttu-id="dd997-398">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-398">Required</span></span> |<span data-ttu-id="dd997-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-399">**xs:int**</span></span> |<span data-ttu-id="dd997-400">Définissez cet attribut sur 1 pour indiquer qu’il s’agit la présentation forcée.</span><span class="sxs-lookup"><span data-stu-id="dd997-400">Set this attribute to 1 to indicate this is the forced presentation.</span></span> |
| <span data-ttu-id="dd997-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="dd997-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="dd997-402">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-402">Required</span></span> |<span data-ttu-id="dd997-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-403">**xs:int**</span></span> |<span data-ttu-id="dd997-404">Définissez cet attribut sur 1 pour indiquer que cette piste est destinée aux personnes malentendantes.</span><span class="sxs-lookup"><span data-stu-id="dd997-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span></span> |
| <span data-ttu-id="dd997-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="dd997-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="dd997-406">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-406">Required</span></span> |<span data-ttu-id="dd997-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-407">**xs:int**</span></span> |<span data-ttu-id="dd997-408">Définissez cet attribut sur 1 pour indiquer que cette piste est destinée aux personnes malvoyantes.</span><span class="sxs-lookup"><span data-stu-id="dd997-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span></span> |
| <span data-ttu-id="dd997-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="dd997-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="dd997-410">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-410">Required</span></span> |<span data-ttu-id="dd997-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-411">**xs:int**</span></span> |<span data-ttu-id="dd997-412">Définissez cet attribut sur 1 pour indiquer que cette piste comporte des effets propres.</span><span class="sxs-lookup"><span data-stu-id="dd997-412">Set this attribute to 1 to indicate this track has clean effects.</span></span> |
| <span data-ttu-id="dd997-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="dd997-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="dd997-414">Requis</span><span class="sxs-lookup"><span data-stu-id="dd997-414">Required</span></span> |<span data-ttu-id="dd997-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="dd997-415">**xs:int**</span></span> |<span data-ttu-id="dd997-416">Définissez cet attribut sur 1 pour indiquer que cette piste contient des images.</span><span class="sxs-lookup"><span data-stu-id="dd997-416">Set this attribute to 1 to indicate this track has pictures.</span></span> |

## <span data-ttu-id="dd997-417"><a name="Programs"></a> Programmes (élément)</span><span class="sxs-lookup"><span data-stu-id="dd997-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="dd997-418">Élément wrapper contenant plusieurs éléments **Program**.</span><span class="sxs-lookup"><span data-stu-id="dd997-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="dd997-419">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="dd997-419">Child elements</span></span>
| <span data-ttu-id="dd997-420">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-420">Name</span></span> | <span data-ttu-id="dd997-421">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-421">Type</span></span> | <span data-ttu-id="dd997-422">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-423">**Programme**</span><span class="sxs-lookup"><span data-stu-id="dd997-423">**Program**</span></span><br /><br /> <span data-ttu-id="dd997-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="dd997-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="dd997-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="dd997-426">Pour les fichiers de ressource qui sont dans un format MPEG-TS, contient des informations sur les programmes dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span></span> |

## <span data-ttu-id="dd997-427"><a name="VideoTracks"></a> Élément VideoTracks</span><span class="sxs-lookup"><span data-stu-id="dd997-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="dd997-428">Élément wrapper contenant plusieurs éléments **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="dd997-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="dd997-429">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="dd997-430">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="dd997-430">Child elements</span></span>
| <span data-ttu-id="dd997-431">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-431">Name</span></span> | <span data-ttu-id="dd997-432">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-432">Type</span></span> | <span data-ttu-id="dd997-433">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="dd997-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="dd997-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="dd997-436">VideoTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="dd997-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="dd997-437">Contient des informations sur les pistes vidéo dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-437">Contains information about video tracks in the asset file.</span></span> |

## <span data-ttu-id="dd997-438"><a name="AudioTracks"></a> Élément AudioTracks</span><span class="sxs-lookup"><span data-stu-id="dd997-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="dd997-439">Élément wrapper contenant plusieurs éléments **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="dd997-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="dd997-440">Consultez l’exemple de XML à la fin de cette rubrique : [Exemple de XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="dd997-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="dd997-441">elements</span><span class="sxs-lookup"><span data-stu-id="dd997-441">elements</span></span>
| <span data-ttu-id="dd997-442">Nom</span><span class="sxs-lookup"><span data-stu-id="dd997-442">Name</span></span> | <span data-ttu-id="dd997-443">Type</span><span class="sxs-lookup"><span data-stu-id="dd997-443">Type</span></span> | <span data-ttu-id="dd997-444">Description</span><span class="sxs-lookup"><span data-stu-id="dd997-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd997-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="dd997-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="dd997-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="dd997-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="dd997-447">AudioTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="dd997-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="dd997-448">Contient des informations sur les pistes audio dans le fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="dd997-448">Contains information about audio tracks in the asset file.</span></span> |

## <span data-ttu-id="dd997-449"><a name="code"></a> Code du schéma</span><span class="sxs-lookup"><span data-stu-id="dd997-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="dd997-450"><a name="xml"></a> Exemple XML</span><span class="sxs-lookup"><span data-stu-id="dd997-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="dd997-451">Voici un exemple de fichier de métadonnées d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dd997-451">The following is an example of the Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="dd997-452">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd997-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd997-453">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="dd997-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

