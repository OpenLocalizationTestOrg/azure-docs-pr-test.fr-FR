---
title: "schéma de métadonnées d’entrée de Media Services aaaAzure | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble du schéma de métadonnées d’entrée Azure Media Services."
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
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="2a0bd-103">Métadonnées d'entrée</span><span class="sxs-lookup"><span data-stu-id="2a0bd-103">Input Metadata</span></span>
<span data-ttu-id="2a0bd-104">Un travail d’encodage est associé à un élément multimédia d’entrée (ou actifs) sur lequel vous souhaitez tooperform certaines tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="2a0bd-105">À l’achèvement d’une tâche, une ressource de sortie est générée.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="2a0bd-106">la ressource en sortie Hello contient vidéo, audio, des miniatures, manifestes, etc. hello ressource en sortie contient également un fichier contenant des métadonnées sur l’élément multimédia d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="2a0bd-107">nom du fichier XML de métadonnées hello Hello a hello suivant le format : &lt;id_élément_multimédia&gt;_metadata.xml (par exemple, 41114ad3-eb5e - 4c 57-8d92-5354e2b7d4a4_metadata), où &lt;id_ressource&gt; est hello AssetId valeur de l’élément multimédia d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="2a0bd-108">Si vous souhaitez que le fichier de métadonnées tooexamine hello, vous pouvez créer un **SAS** recherche et le téléchargement hello ordinateur local tooyour de fichier.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="2a0bd-109">Vous trouverez un exemple sur la façon de toocreate un localisateur SAS et télécharger un fichier [à l’aide des Extensions de hello Media Services .NET SDK](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="2a0bd-110">Cette rubrique décrit les éléments de hello et types de schéma XML de hello de quels des métadonnées d’entrée de hello (&lt;id_élément_multimédia&gt;_metadata.xml) est basé.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="2a0bd-111">Pour plus d’informations sur le fichier hello qui contient des métadonnées sur l’élément multimédia de sortie hello, consultez [sortie métadonnées](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="2a0bd-112">Vous pouvez trouver hello [Code schéma](media-services-input-metadata-schema.md#code) un [exemple XML](media-services-input-metadata-schema.md#xml) à fin hello de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="2a0bd-113"><a name="AssetFiles"></a> Élément AssetFiles (élément racine)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="2a0bd-114">Contient une collection de [élément AssetFile](media-services-input-metadata-schema.md#AssetFile)s pour le travail d’encodage hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="2a0bd-115">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="2a0bd-116">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-116">Name</span></span> | <span data-ttu-id="2a0bd-117">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a0bd-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="2a0bd-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="2a0bd-120">Un élément enfant unique.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-120">A single child element.</span></span> <span data-ttu-id="2a0bd-121">Pour plus d'informations, consultez la page [Élément AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="2a0bd-122"><a name="AssetFile"></a> Élément AssetFile</span><span class="sxs-lookup"><span data-stu-id="2a0bd-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="2a0bd-123">Contient des attributs et des éléments qui décrivent une ressource.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="2a0bd-124">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-125">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-125">Attributes</span></span>
| <span data-ttu-id="2a0bd-126">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-126">Name</span></span> | <span data-ttu-id="2a0bd-127">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-127">Type</span></span> | <span data-ttu-id="2a0bd-128">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-129">**Name**</span></span><br /><br /> <span data-ttu-id="2a0bd-130">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-130">Required</span></span> |<span data-ttu-id="2a0bd-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-131">**xs:string**</span></span> |<span data-ttu-id="2a0bd-132">Nom du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-132">Asset file name.</span></span> |
| <span data-ttu-id="2a0bd-133">**Taille**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-133">**Size**</span></span><br /><br /> <span data-ttu-id="2a0bd-134">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-134">Required</span></span> |<span data-ttu-id="2a0bd-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-135">**xs:long**</span></span> |<span data-ttu-id="2a0bd-136">Taille de fichier d’élément multimédia hello en octets.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="2a0bd-137">**Durée**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-137">**Duration**</span></span><br /><br /> <span data-ttu-id="2a0bd-138">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-138">Required</span></span> |<span data-ttu-id="2a0bd-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-139">**xs:duration**</span></span> |<span data-ttu-id="2a0bd-140">Durée de lecture du contenu.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-140">Content play back duration.</span></span> <span data-ttu-id="2a0bd-141">Exemple : Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="2a0bd-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="2a0bd-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="2a0bd-143">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-143">Required</span></span> |<span data-ttu-id="2a0bd-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-144">**xs:int**</span></span> |<span data-ttu-id="2a0bd-145">Nombre de flux dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="2a0bd-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="2a0bd-147">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-147">Required</span></span> |<span data-ttu-id="2a0bd-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-148">**xs:string**</span></span> |<span data-ttu-id="2a0bd-149">Noms de format.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-149">Format names.</span></span> |
| <span data-ttu-id="2a0bd-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="2a0bd-151">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-151">Required</span></span> |<span data-ttu-id="2a0bd-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-152">**xs:string**</span></span> |<span data-ttu-id="2a0bd-153">Noms détaillés des formats.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-153">Format verbose names.</span></span> |
| <span data-ttu-id="2a0bd-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-154">**StartTime**</span></span> |<span data-ttu-id="2a0bd-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-155">**xs:duration**</span></span> |<span data-ttu-id="2a0bd-156">Heure de début du contenu.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-156">Content start time.</span></span> <span data-ttu-id="2a0bd-157">Exemple : StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="2a0bd-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="2a0bd-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-158">**OverallBitRate**</span></span> |<span data-ttu-id="2a0bd-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-159">**xs:int**</span></span> |<span data-ttu-id="2a0bd-160">Débit binaire moyen du fichier d’actif hello en Kbits/s.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="2a0bd-161">Hello les 4 éléments enfants doit apparaître dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="2a0bd-162">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="2a0bd-162">Child elements</span></span>
| <span data-ttu-id="2a0bd-163">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-163">Name</span></span> | <span data-ttu-id="2a0bd-164">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-164">Type</span></span> | <span data-ttu-id="2a0bd-165">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-166">**Programmes**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-166">**Programs**</span></span><br /><br /> <span data-ttu-id="2a0bd-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-167">minOccurs="0"</span></span> | |<span data-ttu-id="2a0bd-168">Collection de tous les [élément Programs](media-services-input-metadata-schema.md#Programs) lorsque le fichier d’élément multimédia hello est dans un format MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="2a0bd-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="2a0bd-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-170">minOccurs="0"</span></span> | |<span data-ttu-id="2a0bd-171">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="2a0bd-172">Cet élément constituée une collection de tous les [élément VideoTracks](media-services-input-metadata-schema.md#VideoTracks) qui font partie d’un fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="2a0bd-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="2a0bd-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-174">minOccurs="0"</span></span> | |<span data-ttu-id="2a0bd-175">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="2a0bd-176">Cet élément constituée une collection de tous les [élément AudioTracks](media-services-input-metadata-schema.md#AudioTracks) qui font partie d’un fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="2a0bd-177">**Métadonnées**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="2a0bd-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2a0bd-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="2a0bd-180">Les métadonnées du fichier de ressource représentées sous la forme de chaînes clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="2a0bd-181">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2a0bd-181">For example:</span></span><br /><br /> <span data-ttu-id="2a0bd-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="2a0bd-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="2a0bd-184">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-185">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-185">Attributes</span></span>
| <span data-ttu-id="2a0bd-186">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-186">Name</span></span> | <span data-ttu-id="2a0bd-187">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-187">Type</span></span> | <span data-ttu-id="2a0bd-188">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-189">**Id**</span></span><br /><br /> <span data-ttu-id="2a0bd-190">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-190">Required</span></span> |<span data-ttu-id="2a0bd-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-191">**xs:int**</span></span> |<span data-ttu-id="2a0bd-192">Index de base zéro de cette piste audio ou vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="2a0bd-193">Cela n’est pas nécessairement que hello trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="2a0bd-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-194">**Codec**</span></span> |<span data-ttu-id="2a0bd-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-195">**xs:string**</span></span> |<span data-ttu-id="2a0bd-196">Chaîne de codec de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-196">Video track codec string.</span></span> |
| <span data-ttu-id="2a0bd-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-197">**CodecLongName**</span></span> |<span data-ttu-id="2a0bd-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-198">**xs:string**</span></span> |<span data-ttu-id="2a0bd-199">Nom long du codec de piste audio ou vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="2a0bd-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="2a0bd-201">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-201">Required</span></span> |<span data-ttu-id="2a0bd-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-202">**xs:string**</span></span> |<span data-ttu-id="2a0bd-203">Période.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-203">Time base.</span></span> <span data-ttu-id="2a0bd-204">Exemple : TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="2a0bd-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-205">**NumberOfFrames**</span></span> |<span data-ttu-id="2a0bd-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-206">**xs:int**</span></span> |<span data-ttu-id="2a0bd-207">Nombre de trames (présent pour les pistes vidéo).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="2a0bd-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-208">**StartTime**</span></span> |<span data-ttu-id="2a0bd-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-209">**xs:duration**</span></span> |<span data-ttu-id="2a0bd-210">Suivre l’heure de début.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-210">Track start time.</span></span> <span data-ttu-id="2a0bd-211">Exemple : StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="2a0bd-212">**Durée**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-212">**Duration**</span></span> |<span data-ttu-id="2a0bd-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-213">**xs:duration**</span></span> |<span data-ttu-id="2a0bd-214">Durée de la piste.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-214">Track duration.</span></span> <span data-ttu-id="2a0bd-215">Exemple : Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="2a0bd-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="2a0bd-216">Hello les 2 éléments enfants doit apparaître dans une séquence.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="2a0bd-217">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="2a0bd-217">Child elements</span></span>
| <span data-ttu-id="2a0bd-218">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-218">Name</span></span> | <span data-ttu-id="2a0bd-219">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-219">Type</span></span> | <span data-ttu-id="2a0bd-220">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="2a0bd-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="2a0bd-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="2a0bd-224">Contient des informations de présentation (par exemple, si une piste audio particulière est destinée aux utilisateurs malvoyants).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="2a0bd-225">**Métadonnées**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="2a0bd-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2a0bd-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="2a0bd-228">Chaînes clé/valeur générique qui peuvent être utilisé toohold diverses informations.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="2a0bd-229">Par exemple, key=”language”, et value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="2a0bd-230"><a name="AudioTrackType"></a> AudioTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="2a0bd-231">**AudioTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="2a0bd-232">type de Hello représente une piste audio spécifique dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="2a0bd-233">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-234">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-234">Attributes</span></span>
| <span data-ttu-id="2a0bd-235">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-235">Name</span></span> | <span data-ttu-id="2a0bd-236">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-236">Type</span></span> | <span data-ttu-id="2a0bd-237">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-238">**SampleFormat**</span></span> |<span data-ttu-id="2a0bd-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-239">**xs:string**</span></span> |<span data-ttu-id="2a0bd-240">Exemple de format.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-240">Sample format.</span></span> |
| <span data-ttu-id="2a0bd-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-241">**ChannelLayout**</span></span> |<span data-ttu-id="2a0bd-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-242">**xs:string**</span></span> |<span data-ttu-id="2a0bd-243">Disposition de canal.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-243">Channel layout.</span></span> |
| <span data-ttu-id="2a0bd-244">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-244">**Channels**</span></span><br /><br /> <span data-ttu-id="2a0bd-245">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-245">Required</span></span> |<span data-ttu-id="2a0bd-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-246">**xs:int**</span></span> |<span data-ttu-id="2a0bd-247">Nombre (0 ou plus) de canaux audio.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="2a0bd-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="2a0bd-249">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-249">Required</span></span> |<span data-ttu-id="2a0bd-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-250">**xs:int**</span></span> |<span data-ttu-id="2a0bd-251">Taux d’échantillonnage audio en échantillons/sec ou Hz.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="2a0bd-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-252">**Bitrate**</span></span> |<span data-ttu-id="2a0bd-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-253">**xs:int**</span></span> |<span data-ttu-id="2a0bd-254">Débit binaire audio moyen en bits par seconde, tel que calculé à partir du fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="2a0bd-255">Seulement charge utile hello flux élémentaire est comptée et surcharge de packaging hello n’est pas inclus dans ce nombre.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="2a0bd-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-256">**BitsPerSample**</span></span> |<span data-ttu-id="2a0bd-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-257">**xs:int**</span></span> |<span data-ttu-id="2a0bd-258">Type de bits par échantillon pour le format wFormatTag hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="2a0bd-259"><a name="VideoTrackType"></a> VideoTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="2a0bd-260">**VideoTrackType** est un type complexe global qui hérite de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="2a0bd-261">type de Hello représente une piste vidéo spécifique dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="2a0bd-262">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-263">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-263">Attributes</span></span>
| <span data-ttu-id="2a0bd-264">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-264">Name</span></span> | <span data-ttu-id="2a0bd-265">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-265">Type</span></span> | <span data-ttu-id="2a0bd-266">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="2a0bd-268">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-268">Required</span></span> |<span data-ttu-id="2a0bd-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-269">**xs:string**</span></span> |<span data-ttu-id="2a0bd-270">Code FourCC du codec vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="2a0bd-271">**Profil**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-271">**Profile**</span></span> |<span data-ttu-id="2a0bd-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-272">**xs:string**</span></span> |<span data-ttu-id="2a0bd-273">Profil de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-273">Video track's profile.</span></span> |
| <span data-ttu-id="2a0bd-274">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-274">**Level**</span></span> |<span data-ttu-id="2a0bd-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-275">**xs:string**</span></span> |<span data-ttu-id="2a0bd-276">Niveau de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-276">Video track's level.</span></span> |
| <span data-ttu-id="2a0bd-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-277">**PixelFormat**</span></span> |<span data-ttu-id="2a0bd-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-278">**xs:string**</span></span> |<span data-ttu-id="2a0bd-279">Format de pixel de la piste vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="2a0bd-280">**Largeur**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-280">**Width**</span></span><br /><br /> <span data-ttu-id="2a0bd-281">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-281">Required</span></span> |<span data-ttu-id="2a0bd-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-282">**xs:int**</span></span> |<span data-ttu-id="2a0bd-283">Largeur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="2a0bd-284">**Hauteur**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-284">**Height**</span></span><br /><br /> <span data-ttu-id="2a0bd-285">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-285">Required</span></span> |<span data-ttu-id="2a0bd-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-286">**xs:int**</span></span> |<span data-ttu-id="2a0bd-287">Hauteur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="2a0bd-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="2a0bd-289">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-289">Required</span></span> |<span data-ttu-id="2a0bd-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-290">**xs:double**</span></span> |<span data-ttu-id="2a0bd-291">Numérateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="2a0bd-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="2a0bd-293">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-293">Required</span></span> |<span data-ttu-id="2a0bd-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-294">**xs:double**</span></span> |<span data-ttu-id="2a0bd-295">Dénominateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="2a0bd-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="2a0bd-297">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-297">Required</span></span> |<span data-ttu-id="2a0bd-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-298">**xs:double**</span></span> |<span data-ttu-id="2a0bd-299">Numérateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="2a0bd-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="2a0bd-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-301">**xs:double**</span></span> |<span data-ttu-id="2a0bd-302">Numérateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="2a0bd-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="2a0bd-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-304">**xs:double**</span></span> |<span data-ttu-id="2a0bd-305">Dénominateur des proportions d’échantillon vidéo.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="2a0bd-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="2a0bd-307">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-307">Required</span></span> |<span data-ttu-id="2a0bd-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-308">**xs:decimal**</span></span> |<span data-ttu-id="2a0bd-309">Fréquence d’images vidéo mesurée au format .3f.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="2a0bd-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-310">**Bitrate**</span></span> |<span data-ttu-id="2a0bd-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-311">**xs:int**</span></span> |<span data-ttu-id="2a0bd-312">Débit binaire vidéo moyen en kilobits par seconde, tel que calculé à partir du fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="2a0bd-313">Seulement charge utile hello flux élémentaire est comptée et surcharge de packaging hello n’est pas inclus.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="2a0bd-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="2a0bd-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-315">**xs:int**</span></span> |<span data-ttu-id="2a0bd-316">Vitesse de transmission moyenne GOP maximum pour cette piste vidéo, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="2a0bd-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-317">**HasBFrames**</span></span> |<span data-ttu-id="2a0bd-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-318">**xs:int**</span></span> |<span data-ttu-id="2a0bd-319">Numéro de piste vidéo des trames B.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="2a0bd-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="2a0bd-321">**MetadataType** est un type complexe global qui décrit les métadonnées d’un fichier de ressource en tant que chaînes clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="2a0bd-322">Par exemple, key=”language”, et value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="2a0bd-323">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-324">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-324">Attributes</span></span>
| <span data-ttu-id="2a0bd-325">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-325">Name</span></span> | <span data-ttu-id="2a0bd-326">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-326">Type</span></span> | <span data-ttu-id="2a0bd-327">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-328">**key**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-328">**key**</span></span><br /><br /> <span data-ttu-id="2a0bd-329">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-329">Required</span></span> |<span data-ttu-id="2a0bd-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-330">**xs:string**</span></span> |<span data-ttu-id="2a0bd-331">clé Hello dans la paire clé/valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="2a0bd-332">**value**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-332">**value**</span></span><br /><br /> <span data-ttu-id="2a0bd-333">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-333">Required</span></span> |<span data-ttu-id="2a0bd-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-334">**xs:string**</span></span> |<span data-ttu-id="2a0bd-335">valeur de Hello dans la paire clé/valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="2a0bd-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="2a0bd-337">**ProgramType** est un type complexe global qui décrit un programme.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-338">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-338">Attributes</span></span>
| <span data-ttu-id="2a0bd-339">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-339">Name</span></span> | <span data-ttu-id="2a0bd-340">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-340">Type</span></span> | <span data-ttu-id="2a0bd-341">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="2a0bd-343">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-343">Required</span></span> |<span data-ttu-id="2a0bd-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-344">**xs:int**</span></span> |<span data-ttu-id="2a0bd-345">ID de programme</span><span class="sxs-lookup"><span data-stu-id="2a0bd-345">Program Id</span></span> |
| <span data-ttu-id="2a0bd-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="2a0bd-347">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-347">Required</span></span> |<span data-ttu-id="2a0bd-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-348">**xs:int**</span></span> |<span data-ttu-id="2a0bd-349">Nombre de programmes.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-349">Number of programs.</span></span> |
| <span data-ttu-id="2a0bd-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="2a0bd-351">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-351">Required</span></span> |<span data-ttu-id="2a0bd-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-352">**xs:int**</span></span> |<span data-ttu-id="2a0bd-353">Les tables de correspondance de programme (PMT) contiennent des informations sur les programmes.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="2a0bd-354">Pour plus d'informations, consultez [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="2a0bd-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="2a0bd-356">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-356">Required</span></span> |<span data-ttu-id="2a0bd-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-357">**xs:int**</span></span> |<span data-ttu-id="2a0bd-358">Utilisé par le décodeur.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-358">Used by decoder.</span></span> <span data-ttu-id="2a0bd-359">Pour plus d'informations, consultez [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="2a0bd-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-360">**StartPTS**</span></span> |<span data-ttu-id="2a0bd-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-361">**xs: long**</span></span> |<span data-ttu-id="2a0bd-362">Horodatage de début de présentation.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="2a0bd-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-363">**EndPTS**</span></span> |<span data-ttu-id="2a0bd-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-364">**xs: long**</span></span> |<span data-ttu-id="2a0bd-365">Horodatage de fin de présentation.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="2a0bd-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="2a0bd-367">**StreamDispositionType** est un type complexe global qui décrit le flux de données hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="2a0bd-368">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="2a0bd-369">Attributs</span><span class="sxs-lookup"><span data-stu-id="2a0bd-369">Attributes</span></span>
| <span data-ttu-id="2a0bd-370">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-370">Name</span></span> | <span data-ttu-id="2a0bd-371">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-371">Type</span></span> | <span data-ttu-id="2a0bd-372">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-373">**Par défaut**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-373">**Default**</span></span><br /><br /> <span data-ttu-id="2a0bd-374">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-374">Required</span></span> |<span data-ttu-id="2a0bd-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-375">**xs:int**</span></span> |<span data-ttu-id="2a0bd-376">Définissez cette tooindicate de too1 attribut de qu'il s’agit présentation par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="2a0bd-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-377">**Dub**</span></span><br /><br /> <span data-ttu-id="2a0bd-378">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-378">Required</span></span> |<span data-ttu-id="2a0bd-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-379">**xs:int**</span></span> |<span data-ttu-id="2a0bd-380">Définissez cette propriété cette tooindicate de too1 d’attribut est hello doublage de présentation.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="2a0bd-381">**Ressource d’origine**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-381">**Original**</span></span><br /><br /> <span data-ttu-id="2a0bd-382">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-382">Required</span></span> |<span data-ttu-id="2a0bd-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-383">**xs:int**</span></span> |<span data-ttu-id="2a0bd-384">Définition de cette tooindicate de too1 attribut de qu'il s’agit la présentation d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="2a0bd-385">**Commentaire**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-385">**Comment**</span></span><br /><br /> <span data-ttu-id="2a0bd-386">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-386">Required</span></span> |<span data-ttu-id="2a0bd-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-387">**xs:int**</span></span> |<span data-ttu-id="2a0bd-388">Définissez cette tooindicate de too1 attribut cette piste contient des commentaires.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="2a0bd-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="2a0bd-390">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-390">Required</span></span> |<span data-ttu-id="2a0bd-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-391">**xs:int**</span></span> |<span data-ttu-id="2a0bd-392">Définissez cette tooindicate de too1 attribut cette piste contient des paroles.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="2a0bd-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="2a0bd-394">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-394">Required</span></span> |<span data-ttu-id="2a0bd-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-395">**xs:int**</span></span> |<span data-ttu-id="2a0bd-396">Affectez cette tooindicate de too1 attribut représente hello piste karaoké (musique de fond, aucune voix).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="2a0bd-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-397">**Forced**</span></span><br /><br /> <span data-ttu-id="2a0bd-398">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-398">Required</span></span> |<span data-ttu-id="2a0bd-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-399">**xs:int**</span></span> |<span data-ttu-id="2a0bd-400">Définition de cette tooindicate de too1 attribut de qu'il s’agit la présentation de hello forcé.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="2a0bd-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="2a0bd-402">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-402">Required</span></span> |<span data-ttu-id="2a0bd-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-403">**xs:int**</span></span> |<span data-ttu-id="2a0bd-404">Définissez cette tooindicate de too1 attribut que cette piste est destinée aux personnes malentendantes de hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="2a0bd-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="2a0bd-406">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-406">Required</span></span> |<span data-ttu-id="2a0bd-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-407">**xs:int**</span></span> |<span data-ttu-id="2a0bd-408">Définissez cette tooindicate de too1 attribut que cette piste est destinée hello malvoyants.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="2a0bd-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="2a0bd-410">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-410">Required</span></span> |<span data-ttu-id="2a0bd-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-411">**xs:int**</span></span> |<span data-ttu-id="2a0bd-412">Définissez cette tooindicate de too1 attribut que cette piste contient effets propres.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="2a0bd-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="2a0bd-414">Requis</span><span class="sxs-lookup"><span data-stu-id="2a0bd-414">Required</span></span> |<span data-ttu-id="2a0bd-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-415">**xs:int**</span></span> |<span data-ttu-id="2a0bd-416">Définir ce tooindicate de too1 attribut que cette piste contient des images.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="2a0bd-417"><a name="Programs"></a> Programmes (élément)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="2a0bd-418">Élément wrapper contenant plusieurs éléments **Program**.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="2a0bd-419">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="2a0bd-419">Child elements</span></span>
| <span data-ttu-id="2a0bd-420">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-420">Name</span></span> | <span data-ttu-id="2a0bd-421">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-421">Type</span></span> | <span data-ttu-id="2a0bd-422">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-423">**Programme**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-423">**Program**</span></span><br /><br /> <span data-ttu-id="2a0bd-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2a0bd-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="2a0bd-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="2a0bd-426">Pour les fichiers de ressources qui sont dans un format MPEG-TS, contient des informations sur les programmes dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="2a0bd-427"><a name="VideoTracks"></a> Élément VideoTracks</span><span class="sxs-lookup"><span data-stu-id="2a0bd-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="2a0bd-428">Élément wrapper contenant plusieurs éléments **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="2a0bd-429">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="2a0bd-430">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="2a0bd-430">Child elements</span></span>
| <span data-ttu-id="2a0bd-431">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-431">Name</span></span> | <span data-ttu-id="2a0bd-432">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-432">Type</span></span> | <span data-ttu-id="2a0bd-433">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="2a0bd-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2a0bd-436">VideoTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="2a0bd-437">Contient des informations sur les pistes vidéo dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="2a0bd-438"><a name="AudioTracks"></a> Élément AudioTracks</span><span class="sxs-lookup"><span data-stu-id="2a0bd-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="2a0bd-439">Élément wrapper contenant plusieurs éléments **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="2a0bd-440">Voir un exemple XML à la fin de hello de cette rubrique : [exemple XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="2a0bd-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="2a0bd-441">elements</span><span class="sxs-lookup"><span data-stu-id="2a0bd-441">elements</span></span>
| <span data-ttu-id="2a0bd-442">Nom</span><span class="sxs-lookup"><span data-stu-id="2a0bd-442">Name</span></span> | <span data-ttu-id="2a0bd-443">Type</span><span class="sxs-lookup"><span data-stu-id="2a0bd-443">Type</span></span> | <span data-ttu-id="2a0bd-444">Description</span><span class="sxs-lookup"><span data-stu-id="2a0bd-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2a0bd-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="2a0bd-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="2a0bd-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="2a0bd-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="2a0bd-447">AudioTrackType (hérite de TrackType)</span><span class="sxs-lookup"><span data-stu-id="2a0bd-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="2a0bd-448">Contient des informations sur les pistes audio dans le fichier d’élément multimédia hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="2a0bd-449"><a name="code"></a> Code du schéma</span><span class="sxs-lookup"><span data-stu-id="2a0bd-449"><a name="code"></a> Schema Code</span></span>
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
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
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
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
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
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
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
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
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
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
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
                    <xs:documentation>hello media asset file name</xs:documentation>  
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
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
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


## <span data-ttu-id="2a0bd-450"><a name="xml"></a> Exemple XML</span><span class="sxs-lookup"><span data-stu-id="2a0bd-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="2a0bd-451">Hello Voici un exemple de fichier de métadonnées d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="2a0bd-451">hello following is an example of hello Input metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="2a0bd-452">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a0bd-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2a0bd-453">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2a0bd-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

