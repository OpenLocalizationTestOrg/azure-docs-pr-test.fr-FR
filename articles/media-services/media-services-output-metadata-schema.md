---
title: "Schéma de métadonnées de sortie Azure Media Services | Microsoft Docs"
description: "Cette rubrique fournit une vue d’ensemble du schéma de métadonnées de sortie d’Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: c175d359f93e7cd8cd73aa498ad8b71c4ec497f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="output-metadata"></a><span data-ttu-id="efa14-103">Métadonnées de sortie</span><span class="sxs-lookup"><span data-stu-id="efa14-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="efa14-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="efa14-104">Overview</span></span>
<span data-ttu-id="efa14-105">Un travail d’encodage est associé à un élément multimédia d’entrée (ou plusieurs) sur lequel vous souhaitez effectuer des tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="efa14-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="efa14-106">Par exemple, encoder un fichier MP4 en ensembles de fichiers MP4 à vitesse de transmission adaptative H.264, créer une miniature, créer des superpositions.</span><span class="sxs-lookup"><span data-stu-id="efa14-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="efa14-107">À l’achèvement d’une tâche, une ressource de sortie est générée.</span><span class="sxs-lookup"><span data-stu-id="efa14-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="efa14-108">L’élément multimédia de sortie contient la vidéo, l’audio, les miniatures, et ainsi de suite. L’élément multimédia de sortie contient également un fichier avec des métadonnées relatives à l’élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="efa14-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="efa14-109">Le nom du fichier XML de métadonnées a le format suivant : &lt;nom_fichier_source&gt;_manifest.xml (par exemple, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="efa14-110">Si vous souhaitez examiner le fichier de métadonnées, vous pouvez créer un localisateur **SAS** et télécharger le fichier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="efa14-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="efa14-111">Cette rubrique décrit les éléments et types du schéma XML sur lesquels les métadonnées de sortie (&lt;source_file_name&gt;_manifest.xml) sont basées.</span><span class="sxs-lookup"><span data-stu-id="efa14-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="efa14-112">Pour plus d’informations sur le fichier qui contient des métadonnées sur la ressource d’entrée, consultez [Métadonnées d’entrée](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="efa14-113">Vous pouvez trouver le Code du schéma complet et un exemple de XML à la fin de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="efa14-113">You can find the complete schema code and XML example at the end of this topic.</span></span>  
>
>

## <span data-ttu-id="efa14-114"><a name="AssetFiles "></a> Élément racine AssetFiles</span><span class="sxs-lookup"><span data-stu-id="efa14-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="efa14-115">Collection d’entrées AssetFile pour le travail d’encodage.</span><span class="sxs-lookup"><span data-stu-id="efa14-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="efa14-116">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-116">Child elements</span></span>
| <span data-ttu-id="efa14-117">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-117">Name</span></span> | <span data-ttu-id="efa14-118">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="efa14-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="efa14-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="efa14-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="efa14-121">Un [élément AssetFile](media-services-output-metadata-schema.md) qui fait partie de la collection AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="efa14-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <span data-ttu-id="efa14-122"><a name="AssetFile "></a> Élément AssetFile</span><span class="sxs-lookup"><span data-stu-id="efa14-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="efa14-123">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="efa14-124">Attributs</span><span class="sxs-lookup"><span data-stu-id="efa14-124">Attributes</span></span>
| <span data-ttu-id="efa14-125">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-125">Name</span></span> | <span data-ttu-id="efa14-126">Type</span><span class="sxs-lookup"><span data-stu-id="efa14-126">Type</span></span> | <span data-ttu-id="efa14-127">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa14-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="efa14-128">**Name**</span></span><br/><br/> <span data-ttu-id="efa14-129">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-129">Required</span></span> |<span data-ttu-id="efa14-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-130">**xs:string**</span></span> |<span data-ttu-id="efa14-131">Le nom du fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="efa14-131">The media asset file name.</span></span> |
| <span data-ttu-id="efa14-132">**Taille**</span><span class="sxs-lookup"><span data-stu-id="efa14-132">**Size**</span></span><br/><br/> <span data-ttu-id="efa14-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-134">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-134">Required</span></span> |<span data-ttu-id="efa14-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="efa14-135">**xs:long**</span></span> |<span data-ttu-id="efa14-136">Taille du fichier de ressource en octets.</span><span class="sxs-lookup"><span data-stu-id="efa14-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="efa14-137">**Durée**</span><span class="sxs-lookup"><span data-stu-id="efa14-137">**Duration**</span></span><br/><br/> <span data-ttu-id="efa14-138">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-138">Required</span></span> |<span data-ttu-id="efa14-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="efa14-139">**xs:duration**</span></span> |<span data-ttu-id="efa14-140">Durée de lecture du contenu.</span><span class="sxs-lookup"><span data-stu-id="efa14-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="efa14-141">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-141">Child elements</span></span>
| <span data-ttu-id="efa14-142">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-142">Name</span></span> | <span data-ttu-id="efa14-143">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="efa14-144">**Sources**</span></span> |<span data-ttu-id="efa14-145">Collection de fichiers multimédias d’entrée/source qui a été traitée afin de produire cet AssetFile.</span><span class="sxs-lookup"><span data-stu-id="efa14-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="efa14-146">Pour plus d'informations, consultez la page [Élément source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="efa14-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="efa14-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="efa14-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="efa14-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="efa14-149">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="efa14-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="efa14-150">Il s’agit de la collection de toutes les pistes vidéo.</span><span class="sxs-lookup"><span data-stu-id="efa14-150">This is the collection of all those video tracks.</span></span> <span data-ttu-id="efa14-151">Pour plus d’informations, consultez [élément VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="efa14-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="efa14-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="efa14-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="efa14-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="efa14-154">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="efa14-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="efa14-155">Il s’agit de la collection de toutes les pistes audio.</span><span class="sxs-lookup"><span data-stu-id="efa14-155">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="efa14-156">Pour plus d’informations, consultez [élément AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="efa14-157"><a name="Sources "></a> Sources (élément)</span><span class="sxs-lookup"><span data-stu-id="efa14-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="efa14-158">Collection de fichiers multimédias d’entrée/source qui a été traitée afin de produire cet AssetFile.</span><span class="sxs-lookup"><span data-stu-id="efa14-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="efa14-159">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="efa14-160">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-160">Child elements</span></span>
| <span data-ttu-id="efa14-161">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-161">Name</span></span> | <span data-ttu-id="efa14-162">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-163">**Source**</span><span class="sxs-lookup"><span data-stu-id="efa14-163">**Source**</span></span><br/><br/> <span data-ttu-id="efa14-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="efa14-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="efa14-165">Un fichier d’entrée/source utilisé lors de la génération de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="efa14-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="efa14-166">Pour plus d'informations, consultez la page [Contrôle du code source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="efa14-167"><a name="Source "></a> Élément source</span><span class="sxs-lookup"><span data-stu-id="efa14-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="efa14-168">Un fichier d’entrée/source utilisé lors de la génération de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="efa14-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="efa14-169">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="efa14-170">Attributs</span><span class="sxs-lookup"><span data-stu-id="efa14-170">Attributes</span></span>
| <span data-ttu-id="efa14-171">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-171">Name</span></span> | <span data-ttu-id="efa14-172">Type</span><span class="sxs-lookup"><span data-stu-id="efa14-172">Type</span></span> | <span data-ttu-id="efa14-173">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa14-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="efa14-174">**Name**</span></span><br/><br/> <span data-ttu-id="efa14-175">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-175">Required</span></span> |<span data-ttu-id="efa14-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-176">**xs:string**</span></span> |<span data-ttu-id="efa14-177">Nom du fichier source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="efa14-177">Input source file name.</span></span> |

## <span data-ttu-id="efa14-178"><a name="VideoTracks "></a> Élément VideoTracks</span><span class="sxs-lookup"><span data-stu-id="efa14-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="efa14-179">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="efa14-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="efa14-180">Il s’agit de la collection de toutes les pistes vidéo.</span><span class="sxs-lookup"><span data-stu-id="efa14-180">This is the collection of all those video tracks.</span></span>  

<span data-ttu-id="efa14-181">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="efa14-182">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-182">Child elements</span></span>
| <span data-ttu-id="efa14-183">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-183">Name</span></span> | <span data-ttu-id="efa14-184">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="efa14-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="efa14-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="efa14-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="efa14-187">Une piste vidéo spécifique dans l’élément AssetFile parent.</span><span class="sxs-lookup"><span data-stu-id="efa14-187">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="efa14-188">Pour plus d’informations, consultez [élément VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="efa14-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="efa14-189"><a name="VideoTrack"></a> Élément VideoTrack</span><span class="sxs-lookup"><span data-stu-id="efa14-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="efa14-190">Une piste vidéo spécifique dans l’élément AssetFile parent.</span><span class="sxs-lookup"><span data-stu-id="efa14-190">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="efa14-191">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="efa14-192">Attributs</span><span class="sxs-lookup"><span data-stu-id="efa14-192">Attributes</span></span>
| <span data-ttu-id="efa14-193">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-193">Name</span></span> | <span data-ttu-id="efa14-194">Type</span><span class="sxs-lookup"><span data-stu-id="efa14-194">Type</span></span> | <span data-ttu-id="efa14-195">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa14-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="efa14-196">**Id**</span></span><br/><br/> <span data-ttu-id="efa14-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-198">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-198">Required</span></span> |<span data-ttu-id="efa14-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-199">**xs:int**</span></span> |<span data-ttu-id="efa14-200">Index de base zéro de cette piste vidéo. **Remarque :**  Il ne s’agit pas nécessairement du trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="efa14-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="efa14-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="efa14-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="efa14-202">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-202">Required</span></span> |<span data-ttu-id="efa14-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-203">**xs:string**</span></span> |<span data-ttu-id="efa14-204">Code FourCC du codec vidéo.</span><span class="sxs-lookup"><span data-stu-id="efa14-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="efa14-205">**Profil**</span><span class="sxs-lookup"><span data-stu-id="efa14-205">**Profile**</span></span> |<span data-ttu-id="efa14-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-206">**xs:string**</span></span> |<span data-ttu-id="efa14-207">Profil H264 (uniquement applicable au codec H264).</span><span class="sxs-lookup"><span data-stu-id="efa14-207">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="efa14-208">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="efa14-208">**Level**</span></span> |<span data-ttu-id="efa14-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-209">**xs:string**</span></span> |<span data-ttu-id="efa14-210">Niveau H264 (uniquement applicable au codec H264).</span><span class="sxs-lookup"><span data-stu-id="efa14-210">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="efa14-211">**Largeur**</span><span class="sxs-lookup"><span data-stu-id="efa14-211">**Width**</span></span><br/><br/> <span data-ttu-id="efa14-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-213">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-213">Required</span></span> |<span data-ttu-id="efa14-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-214">**xs:int**</span></span> |<span data-ttu-id="efa14-215">Largeur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="efa14-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="efa14-216">**Hauteur**</span><span class="sxs-lookup"><span data-stu-id="efa14-216">**Height**</span></span><br/><br/> <span data-ttu-id="efa14-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-218">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-218">Required</span></span> |<span data-ttu-id="efa14-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-219">**xs:int**</span></span> |<span data-ttu-id="efa14-220">Hauteur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="efa14-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="efa14-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="efa14-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="efa14-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-223">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-223">Required</span></span> |<span data-ttu-id="efa14-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="efa14-224">**xs:double**</span></span> |<span data-ttu-id="efa14-225">Numérateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="efa14-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="efa14-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="efa14-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="efa14-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-228">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-228">Required</span></span> |<span data-ttu-id="efa14-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="efa14-229">**xs:double**</span></span> |<span data-ttu-id="efa14-230">Dénominateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="efa14-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="efa14-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="efa14-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="efa14-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-233">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-233">Required</span></span> |<span data-ttu-id="efa14-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="efa14-234">**xs:decimal**</span></span> |<span data-ttu-id="efa14-235">Fréquence d’images vidéo mesurée au format .3f.</span><span class="sxs-lookup"><span data-stu-id="efa14-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="efa14-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="efa14-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="efa14-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-238">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-238">Required</span></span> |<span data-ttu-id="efa14-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="efa14-239">**xs:decimal**</span></span> |<span data-ttu-id="efa14-240">Fréquence d’images vidéo cible prédéfinie au format .3f.</span><span class="sxs-lookup"><span data-stu-id="efa14-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="efa14-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="efa14-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="efa14-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-243">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-243">Required</span></span> |<span data-ttu-id="efa14-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-244">**xs:int**</span></span> |<span data-ttu-id="efa14-245">Vitesse de transmission vidéo moyenne en kilobits par seconde, telle que calculée à partir du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="efa14-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="efa14-246">Compte uniquement la charge utile de flux élémentaire et n’inclut pas la surcharge de packaging.</span><span class="sxs-lookup"><span data-stu-id="efa14-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="efa14-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="efa14-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="efa14-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-249">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-249">Required</span></span> |<span data-ttu-id="efa14-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-250">**xs:int**</span></span> |<span data-ttu-id="efa14-251">Vitesse de transmission cible moyenne pour cette piste vidéo, comme demandé via paramètres prédéfinis d’encodage, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="efa14-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="efa14-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="efa14-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="efa14-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-253">minInclusive ="0"</span></span> |<span data-ttu-id="efa14-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-254">**xs:int**</span></span> |<span data-ttu-id="efa14-255">Vitesse de transmission moyenne GOP maximum pour cette piste vidéo, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="efa14-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="efa14-256"><a name="AudioTracks "></a> Élément AudioTracks</span><span class="sxs-lookup"><span data-stu-id="efa14-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="efa14-257">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="efa14-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="efa14-258">Il s’agit de la collection de toutes les pistes audio.</span><span class="sxs-lookup"><span data-stu-id="efa14-258">This is the collection of all those audio tracks.</span></span>  

<span data-ttu-id="efa14-259">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="efa14-260">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-260">Child elements</span></span>
| <span data-ttu-id="efa14-261">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-261">Name</span></span> | <span data-ttu-id="efa14-262">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="efa14-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="efa14-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="efa14-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="efa14-265">Une piste audio spécifique dans l’élément AssetFile parent.</span><span class="sxs-lookup"><span data-stu-id="efa14-265">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="efa14-266">Pour plus d’informations, consultez [élément AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="efa14-267"><a name="AudioTrack "></a> Élément AudioTrack</span><span class="sxs-lookup"><span data-stu-id="efa14-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="efa14-268">Une piste audio spécifique dans l’élément AssetFile parent.</span><span class="sxs-lookup"><span data-stu-id="efa14-268">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="efa14-269">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="efa14-270">Attributs</span><span class="sxs-lookup"><span data-stu-id="efa14-270">Attributes</span></span>
| <span data-ttu-id="efa14-271">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-271">Name</span></span> | <span data-ttu-id="efa14-272">Type</span><span class="sxs-lookup"><span data-stu-id="efa14-272">Type</span></span> | <span data-ttu-id="efa14-273">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa14-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="efa14-274">**Id**</span></span><br/><br/> <span data-ttu-id="efa14-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-276">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-276">Required</span></span> |<span data-ttu-id="efa14-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-277">**xs:int**</span></span> |<span data-ttu-id="efa14-278">Index de base zéro de cette piste audio. **Remarque :**  Il ne s’agit pas nécessairement du trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="efa14-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="efa14-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="efa14-279">**Codec**</span></span> |<span data-ttu-id="efa14-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-280">**xs:string**</span></span> |<span data-ttu-id="efa14-281">Chaîne du codec de piste audio.</span><span class="sxs-lookup"><span data-stu-id="efa14-281">Audio track codec string.</span></span> |
| <span data-ttu-id="efa14-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="efa14-282">**EncoderVersion**</span></span> |<span data-ttu-id="efa14-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-283">**xs:string**</span></span> |<span data-ttu-id="efa14-284">Chaîne de version d’encodeur facultative, requise pour EAC3.</span><span class="sxs-lookup"><span data-stu-id="efa14-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="efa14-285">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="efa14-285">**Channels**</span></span><br/><br/> <span data-ttu-id="efa14-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-287">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-287">Required</span></span> |<span data-ttu-id="efa14-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-288">**xs:int**</span></span> |<span data-ttu-id="efa14-289">Nombre de canaux audio.</span><span class="sxs-lookup"><span data-stu-id="efa14-289">Number of audio channels.</span></span> |
| <span data-ttu-id="efa14-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="efa14-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="efa14-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-292">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-292">Required</span></span> |<span data-ttu-id="efa14-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-293">**xs:int**</span></span> |<span data-ttu-id="efa14-294">Taux d’échantillonnage audio en échantillons/sec ou Hz.</span><span class="sxs-lookup"><span data-stu-id="efa14-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="efa14-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="efa14-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="efa14-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-297">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-297">Required</span></span> |<span data-ttu-id="efa14-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-298">**xs:int**</span></span> |<span data-ttu-id="efa14-299">Débit binaire audio moyen en bits par seconde, tel que calculé à partir du fichier de ressource.</span><span class="sxs-lookup"><span data-stu-id="efa14-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="efa14-300">Compte uniquement la charge utile de flux élémentaire et n’inclut pas la surcharge de packaging.</span><span class="sxs-lookup"><span data-stu-id="efa14-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="efa14-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="efa14-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="efa14-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="efa14-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="efa14-303">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-303">Required</span></span> |<span data-ttu-id="efa14-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-304">**xs:int**</span></span> |<span data-ttu-id="efa14-305">Bits par échantillon pour le type de format wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="efa14-305">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="efa14-306">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="efa14-306">Child elements</span></span>
| <span data-ttu-id="efa14-307">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-307">Name</span></span> | <span data-ttu-id="efa14-308">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="efa14-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="efa14-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="efa14-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="efa14-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="efa14-311">Paramètres de résultat de mesure du niveau sonore.</span><span class="sxs-lookup"><span data-stu-id="efa14-311">Loudness metering result parameters.</span></span> <span data-ttu-id="efa14-312">Pour plus d’informations, consultez [élément LoudnessMeteringResultParameters](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="efa14-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="efa14-313"><a name="LoudnessMeteringResultParameters "></a> Élément LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="efa14-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="efa14-314">Paramètres de résultat de mesure du niveau sonore.</span><span class="sxs-lookup"><span data-stu-id="efa14-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="efa14-315">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="efa14-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="efa14-316">Attributs</span><span class="sxs-lookup"><span data-stu-id="efa14-316">Attributes</span></span>
| <span data-ttu-id="efa14-317">Nom</span><span class="sxs-lookup"><span data-stu-id="efa14-317">Name</span></span> | <span data-ttu-id="efa14-318">Type</span><span class="sxs-lookup"><span data-stu-id="efa14-318">Type</span></span> | <span data-ttu-id="efa14-319">Description</span><span class="sxs-lookup"><span data-stu-id="efa14-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efa14-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="efa14-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="efa14-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-321">**xs:string**</span></span> |<span data-ttu-id="efa14-322">Version du kit de développement **Dolby** Professional Loudness Metering.</span><span class="sxs-lookup"><span data-stu-id="efa14-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="efa14-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="efa14-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="efa14-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="efa14-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="efa14-325">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-325">Required</span></span> |<span data-ttu-id="efa14-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="efa14-326">**xs:int**</span></span> |<span data-ttu-id="efa14-327">DialogNormalization généré par DPLM, requis lorsque LoudnessMetering est défini</span><span class="sxs-lookup"><span data-stu-id="efa14-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="efa14-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="efa14-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="efa14-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="efa14-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="efa14-330">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-330">Required</span></span> |<span data-ttu-id="efa14-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="efa14-331">**xs:float**</span></span> |<span data-ttu-id="efa14-332">Niveau sonore intégré</span><span class="sxs-lookup"><span data-stu-id="efa14-332">Integrated loudness</span></span> |
| <span data-ttu-id="efa14-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="efa14-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="efa14-334">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-334">Required</span></span> |<span data-ttu-id="efa14-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-335">**xs:string**</span></span> |<span data-ttu-id="efa14-336">Unité de niveau sonore intégrée.</span><span class="sxs-lookup"><span data-stu-id="efa14-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="efa14-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="efa14-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="efa14-338">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-338">Required</span></span> |<span data-ttu-id="efa14-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="efa14-339">**xs:string**</span></span> |<span data-ttu-id="efa14-340">Identificateur de régulation</span><span class="sxs-lookup"><span data-stu-id="efa14-340">Gating identifier</span></span> |
| <span data-ttu-id="efa14-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="efa14-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="efa14-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="efa14-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="efa14-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="efa14-343">**xs:float**</span></span> |<span data-ttu-id="efa14-344">Contenu vocal sur le programme, sous forme de pourcentage.</span><span class="sxs-lookup"><span data-stu-id="efa14-344">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="efa14-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="efa14-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="efa14-346">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-346">Required</span></span> |<span data-ttu-id="efa14-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="efa14-347">**xs:float**</span></span> |<span data-ttu-id="efa14-348">Valeur d’échantillonnage absolue de crête, depuis la réinitialisation ou depuis la dernière suppression, par canal.</span><span class="sxs-lookup"><span data-stu-id="efa14-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="efa14-349">Les unités sont dBFS.</span><span class="sxs-lookup"><span data-stu-id="efa14-349">Units are dBFS.</span></span> |
| <span data-ttu-id="efa14-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="efa14-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="efa14-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="efa14-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="efa14-352">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-352">Required</span></span> |<span data-ttu-id="efa14-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="efa14-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="efa14-354">Exemple d’unité de crête.</span><span class="sxs-lookup"><span data-stu-id="efa14-354">Sample peak unit.</span></span> |
| <span data-ttu-id="efa14-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="efa14-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="efa14-356">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-356">Required</span></span> |<span data-ttu-id="efa14-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="efa14-357">**xs:float**</span></span> |<span data-ttu-id="efa14-358">Valeur true peak maximale, selon ITU-R BS.1770-2, depuis la réinitialisation ou depuis la dernière suppression, par canal.</span><span class="sxs-lookup"><span data-stu-id="efa14-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="efa14-359">Les unités sont dBTP.</span><span class="sxs-lookup"><span data-stu-id="efa14-359">Units are dBTP.</span></span> |
| <span data-ttu-id="efa14-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="efa14-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="efa14-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="efa14-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="efa14-362">Requis</span><span class="sxs-lookup"><span data-stu-id="efa14-362">Required</span></span> |<span data-ttu-id="efa14-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="efa14-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="efa14-364">Unité de true peak.</span><span class="sxs-lookup"><span data-stu-id="efa14-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="efa14-365">Code du schéma</span><span class="sxs-lookup"><span data-stu-id="efa14-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="efa14-366"><a name="xml"></a> Exemple XML</span><span class="sxs-lookup"><span data-stu-id="efa14-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="efa14-367">Voici un exemple de fichier de métadonnées de sortie.</span><span class="sxs-lookup"><span data-stu-id="efa14-367">The following is an example of the Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="efa14-368">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="efa14-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="efa14-369">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="efa14-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
