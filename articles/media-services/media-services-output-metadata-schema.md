---
title: "schéma de métadonnées de sortie de Media Services aaaAzure | Documents Microsoft"
description: "rubrique de Hello donne une vue d’ensemble du schéma de métadonnées de sortie Azure Media Services."
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
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="28b8e-103">Métadonnées de sortie</span><span class="sxs-lookup"><span data-stu-id="28b8e-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="28b8e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="28b8e-104">Overview</span></span>
<span data-ttu-id="28b8e-105">Un travail d’encodage est associé à un élément multimédia d’entrée (ou actifs) sur lequel vous souhaitez tooperform certaines tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="28b8e-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="28b8e-106">Par exemple, pour encoder un fichier MP4 tooH.264 MP4 des fichiers à débit adaptatif définit ; créer une miniature ; créer des superpositions.</span><span class="sxs-lookup"><span data-stu-id="28b8e-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="28b8e-107">À l’achèvement d’une tâche, une ressource de sortie est générée.</span><span class="sxs-lookup"><span data-stu-id="28b8e-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="28b8e-108">la ressource en sortie Hello contient vidéo, audio, miniatures, etc. hello ressource en sortie contient également un fichier contenant des métadonnées sur l’élément multimédia de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="28b8e-109">nom du fichier XML de métadonnées hello Hello a hello suivant le format : &lt;nom_fichier_source&gt;_manifest.xml (par exemple, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="28b8e-110">Si vous souhaitez que le fichier de métadonnées tooexamine hello, vous pouvez créer un **SAS** recherche et le téléchargement hello ordinateur local tooyour de fichier.</span><span class="sxs-lookup"><span data-stu-id="28b8e-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="28b8e-111">Cette rubrique décrit les éléments de hello et types de schéma XML de hello sur la résultat de hello des métadonnées (&lt;nom_fichier_source&gt;_manifest.xml) est basé.</span><span class="sxs-lookup"><span data-stu-id="28b8e-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="28b8e-112">Pour plus d’informations sur le fichier hello qui contient des métadonnées sur l’élément multimédia d’entrée de hello, consultez [d’entrée de métadonnées](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="28b8e-113">Vous pouvez trouver le code du schéma complet hello et exemple de code XML à la fin de hello de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="28b8e-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="28b8e-114"><a name="AssetFiles "></a> Élément racine AssetFiles</span><span class="sxs-lookup"><span data-stu-id="28b8e-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="28b8e-115">Collection d’entrées AssetFile pour le travail d’encodage hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="28b8e-116">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-116">Child elements</span></span>
| <span data-ttu-id="28b8e-117">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-117">Name</span></span> | <span data-ttu-id="28b8e-118">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="28b8e-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="28b8e-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="28b8e-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="28b8e-121">Un [élément AssetFile](media-services-output-metadata-schema.md) qui fait partie de hello collection AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="28b8e-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="28b8e-122"><a name="AssetFile "></a> Élément AssetFile</span><span class="sxs-lookup"><span data-stu-id="28b8e-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="28b8e-123">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="28b8e-124">Attributs</span><span class="sxs-lookup"><span data-stu-id="28b8e-124">Attributes</span></span>
| <span data-ttu-id="28b8e-125">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-125">Name</span></span> | <span data-ttu-id="28b8e-126">Type</span><span class="sxs-lookup"><span data-stu-id="28b8e-126">Type</span></span> | <span data-ttu-id="28b8e-127">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28b8e-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="28b8e-128">**Name**</span></span><br/><br/> <span data-ttu-id="28b8e-129">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-129">Required</span></span> |<span data-ttu-id="28b8e-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-130">**xs:string**</span></span> |<span data-ttu-id="28b8e-131">Hello nom du fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="28b8e-131">hello media asset file name.</span></span> |
| <span data-ttu-id="28b8e-132">**Taille**</span><span class="sxs-lookup"><span data-stu-id="28b8e-132">**Size**</span></span><br/><br/> <span data-ttu-id="28b8e-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-134">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-134">Required</span></span> |<span data-ttu-id="28b8e-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="28b8e-135">**xs:long**</span></span> |<span data-ttu-id="28b8e-136">Taille de fichier d’élément multimédia hello en octets.</span><span class="sxs-lookup"><span data-stu-id="28b8e-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="28b8e-137">**Durée**</span><span class="sxs-lookup"><span data-stu-id="28b8e-137">**Duration**</span></span><br/><br/> <span data-ttu-id="28b8e-138">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-138">Required</span></span> |<span data-ttu-id="28b8e-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="28b8e-139">**xs:duration**</span></span> |<span data-ttu-id="28b8e-140">Durée de lecture du contenu.</span><span class="sxs-lookup"><span data-stu-id="28b8e-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="28b8e-141">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-141">Child elements</span></span>
| <span data-ttu-id="28b8e-142">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-142">Name</span></span> | <span data-ttu-id="28b8e-143">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="28b8e-144">**Sources**</span></span> |<span data-ttu-id="28b8e-145">Collection de fichiers de média d’entrée/source, qui a été traitée dans commande tooproduce cet AssetFile.</span><span class="sxs-lookup"><span data-stu-id="28b8e-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="28b8e-146">Pour plus d'informations, consultez la page [Élément source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="28b8e-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="28b8e-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="28b8e-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="28b8e-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="28b8e-149">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="28b8e-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="28b8e-150">Il s’agit de collection hello de toutes ces pistes vidéos.</span><span class="sxs-lookup"><span data-stu-id="28b8e-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="28b8e-151">Pour plus d’informations, consultez [élément VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="28b8e-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="28b8e-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="28b8e-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="28b8e-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="28b8e-154">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="28b8e-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="28b8e-155">Il s’agit de collection hello de toutes ces pistes audio.</span><span class="sxs-lookup"><span data-stu-id="28b8e-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="28b8e-156">Pour plus d’informations, consultez [élément AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="28b8e-157"><a name="Sources "></a> Sources (élément)</span><span class="sxs-lookup"><span data-stu-id="28b8e-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="28b8e-158">Collection de fichiers de média d’entrée/source, qui a été traitée dans commande tooproduce cet AssetFile.</span><span class="sxs-lookup"><span data-stu-id="28b8e-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="28b8e-159">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="28b8e-160">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-160">Child elements</span></span>
| <span data-ttu-id="28b8e-161">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-161">Name</span></span> | <span data-ttu-id="28b8e-162">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-163">**Source**</span><span class="sxs-lookup"><span data-stu-id="28b8e-163">**Source**</span></span><br/><br/> <span data-ttu-id="28b8e-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="28b8e-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="28b8e-165">Un fichier d’entrée/source utilisé lors de la génération de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="28b8e-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="28b8e-166">Pour plus d'informations, consultez la page [Contrôle du code source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="28b8e-167"><a name="Source "></a> Élément source</span><span class="sxs-lookup"><span data-stu-id="28b8e-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="28b8e-168">Un fichier d’entrée/source utilisé lors de la génération de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="28b8e-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="28b8e-169">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="28b8e-170">Attributs</span><span class="sxs-lookup"><span data-stu-id="28b8e-170">Attributes</span></span>
| <span data-ttu-id="28b8e-171">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-171">Name</span></span> | <span data-ttu-id="28b8e-172">Type</span><span class="sxs-lookup"><span data-stu-id="28b8e-172">Type</span></span> | <span data-ttu-id="28b8e-173">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28b8e-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="28b8e-174">**Name**</span></span><br/><br/> <span data-ttu-id="28b8e-175">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-175">Required</span></span> |<span data-ttu-id="28b8e-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-176">**xs:string**</span></span> |<span data-ttu-id="28b8e-177">Nom du fichier source d’entrée.</span><span class="sxs-lookup"><span data-stu-id="28b8e-177">Input source file name.</span></span> |

## <span data-ttu-id="28b8e-178"><a name="VideoTracks "></a> Élément VideoTracks</span><span class="sxs-lookup"><span data-stu-id="28b8e-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="28b8e-179">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes vidéo entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="28b8e-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="28b8e-180">Il s’agit de collection hello de toutes ces pistes vidéos.</span><span class="sxs-lookup"><span data-stu-id="28b8e-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="28b8e-181">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="28b8e-182">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-182">Child elements</span></span>
| <span data-ttu-id="28b8e-183">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-183">Name</span></span> | <span data-ttu-id="28b8e-184">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="28b8e-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="28b8e-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="28b8e-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="28b8e-187">Une piste vidéo spécifique dans l’élément AssetFile parent de hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="28b8e-188">Pour plus d’informations, consultez [élément VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="28b8e-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="28b8e-189"><a name="VideoTrack"></a> Élément VideoTrack</span><span class="sxs-lookup"><span data-stu-id="28b8e-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="28b8e-190">Une piste vidéo spécifique dans l’élément AssetFile parent de hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="28b8e-191">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="28b8e-192">Attributs</span><span class="sxs-lookup"><span data-stu-id="28b8e-192">Attributes</span></span>
| <span data-ttu-id="28b8e-193">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-193">Name</span></span> | <span data-ttu-id="28b8e-194">Type</span><span class="sxs-lookup"><span data-stu-id="28b8e-194">Type</span></span> | <span data-ttu-id="28b8e-195">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28b8e-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="28b8e-196">**Id**</span></span><br/><br/> <span data-ttu-id="28b8e-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-198">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-198">Required</span></span> |<span data-ttu-id="28b8e-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-199">**xs:int**</span></span> |<span data-ttu-id="28b8e-200">Index de base zéro de cette piste vidéo. **Remarque :** cela n’est pas nécessairement hello trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="28b8e-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="28b8e-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="28b8e-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="28b8e-202">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-202">Required</span></span> |<span data-ttu-id="28b8e-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-203">**xs:string**</span></span> |<span data-ttu-id="28b8e-204">Code FourCC du codec vidéo.</span><span class="sxs-lookup"><span data-stu-id="28b8e-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="28b8e-205">**Profil**</span><span class="sxs-lookup"><span data-stu-id="28b8e-205">**Profile**</span></span> |<span data-ttu-id="28b8e-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-206">**xs:string**</span></span> |<span data-ttu-id="28b8e-207">Profil h264 (uniquement applicable tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="28b8e-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="28b8e-208">**Niveau**</span><span class="sxs-lookup"><span data-stu-id="28b8e-208">**Level**</span></span> |<span data-ttu-id="28b8e-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-209">**xs:string**</span></span> |<span data-ttu-id="28b8e-210">Niveau h264 (uniquement applicable tooH264 codec).</span><span class="sxs-lookup"><span data-stu-id="28b8e-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="28b8e-211">**Largeur**</span><span class="sxs-lookup"><span data-stu-id="28b8e-211">**Width**</span></span><br/><br/> <span data-ttu-id="28b8e-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-213">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-213">Required</span></span> |<span data-ttu-id="28b8e-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-214">**xs:int**</span></span> |<span data-ttu-id="28b8e-215">Largeur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="28b8e-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="28b8e-216">**Hauteur**</span><span class="sxs-lookup"><span data-stu-id="28b8e-216">**Height**</span></span><br/><br/> <span data-ttu-id="28b8e-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-218">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-218">Required</span></span> |<span data-ttu-id="28b8e-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-219">**xs:int**</span></span> |<span data-ttu-id="28b8e-220">Hauteur vidéo encodée en pixels.</span><span class="sxs-lookup"><span data-stu-id="28b8e-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="28b8e-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="28b8e-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="28b8e-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-223">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-223">Required</span></span> |<span data-ttu-id="28b8e-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="28b8e-224">**xs:double**</span></span> |<span data-ttu-id="28b8e-225">Numérateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="28b8e-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="28b8e-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="28b8e-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="28b8e-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-228">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-228">Required</span></span> |<span data-ttu-id="28b8e-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="28b8e-229">**xs:double**</span></span> |<span data-ttu-id="28b8e-230">Dénominateur des proportions d’affichage vidéo.</span><span class="sxs-lookup"><span data-stu-id="28b8e-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="28b8e-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="28b8e-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-233">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-233">Required</span></span> |<span data-ttu-id="28b8e-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="28b8e-234">**xs:decimal**</span></span> |<span data-ttu-id="28b8e-235">Fréquence d’images vidéo mesurée au format .3f.</span><span class="sxs-lookup"><span data-stu-id="28b8e-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="28b8e-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="28b8e-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-238">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-238">Required</span></span> |<span data-ttu-id="28b8e-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="28b8e-239">**xs:decimal**</span></span> |<span data-ttu-id="28b8e-240">Fréquence d’images vidéo cible prédéfinie au format .3f.</span><span class="sxs-lookup"><span data-stu-id="28b8e-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="28b8e-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="28b8e-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-243">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-243">Required</span></span> |<span data-ttu-id="28b8e-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-244">**xs:int**</span></span> |<span data-ttu-id="28b8e-245">Débit binaire vidéo moyen en kilobits par seconde, tel que calculé à partir de hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="28b8e-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="28b8e-246">Compte seule charge utile de flux élémentaire hello et n’inclut pas de surcharge de packaging hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="28b8e-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="28b8e-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-249">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-249">Required</span></span> |<span data-ttu-id="28b8e-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-250">**xs:int**</span></span> |<span data-ttu-id="28b8e-251">Cibler le débit binaire moyen pour cette piste vidéo, tel que demandé via hello valeur prédéfinie d’encodage, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="28b8e-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="28b8e-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="28b8e-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-253">minInclusive ="0"</span></span> |<span data-ttu-id="28b8e-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-254">**xs:int**</span></span> |<span data-ttu-id="28b8e-255">Vitesse de transmission moyenne GOP maximum pour cette piste vidéo, en kilobits par seconde.</span><span class="sxs-lookup"><span data-stu-id="28b8e-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="28b8e-256"><a name="AudioTracks "></a> Élément AudioTracks</span><span class="sxs-lookup"><span data-stu-id="28b8e-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="28b8e-257">Chaque élément AssetFile physique peut contenir zéro ou plusieurs pistes audio entrelacées dans un format de conteneur approprié.</span><span class="sxs-lookup"><span data-stu-id="28b8e-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="28b8e-258">Il s’agit de collection hello de toutes ces pistes audio.</span><span class="sxs-lookup"><span data-stu-id="28b8e-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="28b8e-259">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="28b8e-260">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-260">Child elements</span></span>
| <span data-ttu-id="28b8e-261">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-261">Name</span></span> | <span data-ttu-id="28b8e-262">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="28b8e-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="28b8e-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="28b8e-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="28b8e-265">Une piste audio spécifique dans l’élément AssetFile parent de hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="28b8e-266">Pour plus d’informations, consultez [élément AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="28b8e-267"><a name="AudioTrack "></a> Élément AudioTrack</span><span class="sxs-lookup"><span data-stu-id="28b8e-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="28b8e-268">Une piste audio spécifique dans l’élément AssetFile parent de hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="28b8e-269">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="28b8e-270">Attributs</span><span class="sxs-lookup"><span data-stu-id="28b8e-270">Attributes</span></span>
| <span data-ttu-id="28b8e-271">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-271">Name</span></span> | <span data-ttu-id="28b8e-272">Type</span><span class="sxs-lookup"><span data-stu-id="28b8e-272">Type</span></span> | <span data-ttu-id="28b8e-273">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28b8e-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="28b8e-274">**Id**</span></span><br/><br/> <span data-ttu-id="28b8e-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-276">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-276">Required</span></span> |<span data-ttu-id="28b8e-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-277">**xs:int**</span></span> |<span data-ttu-id="28b8e-278">Index de base zéro de cette piste audio. **Remarque :** cela n’est pas nécessairement hello trackid tel qu’utilisé dans un fichier MP4.</span><span class="sxs-lookup"><span data-stu-id="28b8e-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="28b8e-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="28b8e-279">**Codec**</span></span> |<span data-ttu-id="28b8e-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-280">**xs:string**</span></span> |<span data-ttu-id="28b8e-281">Chaîne du codec de piste audio.</span><span class="sxs-lookup"><span data-stu-id="28b8e-281">Audio track codec string.</span></span> |
| <span data-ttu-id="28b8e-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="28b8e-282">**EncoderVersion**</span></span> |<span data-ttu-id="28b8e-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-283">**xs:string**</span></span> |<span data-ttu-id="28b8e-284">Chaîne de version d’encodeur facultative, requise pour EAC3.</span><span class="sxs-lookup"><span data-stu-id="28b8e-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="28b8e-285">**Canaux**</span><span class="sxs-lookup"><span data-stu-id="28b8e-285">**Channels**</span></span><br/><br/> <span data-ttu-id="28b8e-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-287">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-287">Required</span></span> |<span data-ttu-id="28b8e-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-288">**xs:int**</span></span> |<span data-ttu-id="28b8e-289">Nombre de canaux audio.</span><span class="sxs-lookup"><span data-stu-id="28b8e-289">Number of audio channels.</span></span> |
| <span data-ttu-id="28b8e-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="28b8e-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-292">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-292">Required</span></span> |<span data-ttu-id="28b8e-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-293">**xs:int**</span></span> |<span data-ttu-id="28b8e-294">Taux d’échantillonnage audio en échantillons/sec ou Hz.</span><span class="sxs-lookup"><span data-stu-id="28b8e-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="28b8e-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="28b8e-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="28b8e-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-297">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-297">Required</span></span> |<span data-ttu-id="28b8e-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-298">**xs:int**</span></span> |<span data-ttu-id="28b8e-299">Débit binaire audio moyen en bits par seconde, tel que calculé à partir de hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="28b8e-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="28b8e-300">Compte seule charge utile de flux élémentaire hello et n’inclut pas de surcharge de packaging hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="28b8e-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="28b8e-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="28b8e-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="28b8e-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="28b8e-303">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-303">Required</span></span> |<span data-ttu-id="28b8e-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-304">**xs:int**</span></span> |<span data-ttu-id="28b8e-305">Type de bits par échantillon pour le format wFormatTag hello.</span><span class="sxs-lookup"><span data-stu-id="28b8e-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="28b8e-306">Éléments enfants</span><span class="sxs-lookup"><span data-stu-id="28b8e-306">Child elements</span></span>
| <span data-ttu-id="28b8e-307">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-307">Name</span></span> | <span data-ttu-id="28b8e-308">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28b8e-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="28b8e-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="28b8e-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="28b8e-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="28b8e-311">Paramètres de résultat de mesure du niveau sonore.</span><span class="sxs-lookup"><span data-stu-id="28b8e-311">Loudness metering result parameters.</span></span> <span data-ttu-id="28b8e-312">Pour plus d’informations, consultez [élément LoudnessMeteringResultParameters](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28b8e-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="28b8e-313"><a name="LoudnessMeteringResultParameters "></a> Élément LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="28b8e-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="28b8e-314">Paramètres de résultat de mesure du niveau sonore.</span><span class="sxs-lookup"><span data-stu-id="28b8e-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="28b8e-315">Vous trouverez un exemple de XML [Exemple de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="28b8e-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="28b8e-316">Attributs</span><span class="sxs-lookup"><span data-stu-id="28b8e-316">Attributes</span></span>
| <span data-ttu-id="28b8e-317">Nom</span><span class="sxs-lookup"><span data-stu-id="28b8e-317">Name</span></span> | <span data-ttu-id="28b8e-318">Type</span><span class="sxs-lookup"><span data-stu-id="28b8e-318">Type</span></span> | <span data-ttu-id="28b8e-319">Description</span><span class="sxs-lookup"><span data-stu-id="28b8e-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28b8e-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="28b8e-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="28b8e-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-321">**xs:string**</span></span> |<span data-ttu-id="28b8e-322">Version du kit de développement **Dolby** Professional Loudness Metering.</span><span class="sxs-lookup"><span data-stu-id="28b8e-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="28b8e-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="28b8e-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="28b8e-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="28b8e-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="28b8e-325">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-325">Required</span></span> |<span data-ttu-id="28b8e-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="28b8e-326">**xs:int**</span></span> |<span data-ttu-id="28b8e-327">DialogNormalization généré par DPLM, requis lorsque LoudnessMetering est défini</span><span class="sxs-lookup"><span data-stu-id="28b8e-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="28b8e-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="28b8e-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="28b8e-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="28b8e-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="28b8e-330">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-330">Required</span></span> |<span data-ttu-id="28b8e-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="28b8e-331">**xs:float**</span></span> |<span data-ttu-id="28b8e-332">Niveau sonore intégré</span><span class="sxs-lookup"><span data-stu-id="28b8e-332">Integrated loudness</span></span> |
| <span data-ttu-id="28b8e-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="28b8e-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="28b8e-334">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-334">Required</span></span> |<span data-ttu-id="28b8e-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-335">**xs:string**</span></span> |<span data-ttu-id="28b8e-336">Unité de niveau sonore intégrée.</span><span class="sxs-lookup"><span data-stu-id="28b8e-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="28b8e-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="28b8e-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="28b8e-338">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-338">Required</span></span> |<span data-ttu-id="28b8e-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="28b8e-339">**xs:string**</span></span> |<span data-ttu-id="28b8e-340">Identificateur de régulation</span><span class="sxs-lookup"><span data-stu-id="28b8e-340">Gating identifier</span></span> |
| <span data-ttu-id="28b8e-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="28b8e-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="28b8e-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="28b8e-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="28b8e-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="28b8e-343">**xs:float**</span></span> |<span data-ttu-id="28b8e-344">Contenu vocal via le programme hello, sous forme de pourcentage.</span><span class="sxs-lookup"><span data-stu-id="28b8e-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="28b8e-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="28b8e-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="28b8e-346">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-346">Required</span></span> |<span data-ttu-id="28b8e-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="28b8e-347">**xs:float**</span></span> |<span data-ttu-id="28b8e-348">Valeur d’échantillonnage absolue de crête, depuis la réinitialisation ou depuis la dernière suppression, par canal.</span><span class="sxs-lookup"><span data-stu-id="28b8e-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="28b8e-349">Les unités sont dBFS.</span><span class="sxs-lookup"><span data-stu-id="28b8e-349">Units are dBFS.</span></span> |
| <span data-ttu-id="28b8e-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="28b8e-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="28b8e-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="28b8e-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="28b8e-352">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-352">Required</span></span> |<span data-ttu-id="28b8e-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="28b8e-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="28b8e-354">Exemple d’unité de crête.</span><span class="sxs-lookup"><span data-stu-id="28b8e-354">Sample peak unit.</span></span> |
| <span data-ttu-id="28b8e-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="28b8e-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="28b8e-356">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-356">Required</span></span> |<span data-ttu-id="28b8e-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="28b8e-357">**xs:float**</span></span> |<span data-ttu-id="28b8e-358">Valeur true peak maximale, selon ITU-R BS.1770-2, depuis la réinitialisation ou depuis la dernière suppression, par canal.</span><span class="sxs-lookup"><span data-stu-id="28b8e-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="28b8e-359">Les unités sont dBTP.</span><span class="sxs-lookup"><span data-stu-id="28b8e-359">Units are dBTP.</span></span> |
| <span data-ttu-id="28b8e-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="28b8e-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="28b8e-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="28b8e-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="28b8e-362">Requis</span><span class="sxs-lookup"><span data-stu-id="28b8e-362">Required</span></span> |<span data-ttu-id="28b8e-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="28b8e-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="28b8e-364">Unité de true peak.</span><span class="sxs-lookup"><span data-stu-id="28b8e-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="28b8e-365">Code du schéma</span><span class="sxs-lookup"><span data-stu-id="28b8e-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
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
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
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
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
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
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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



## <span data-ttu-id="28b8e-366"><a name="xml"></a> Exemple XML</span><span class="sxs-lookup"><span data-stu-id="28b8e-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="28b8e-367">Hello Voici un exemple hello métadonnées du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="28b8e-367">hello following is an example of hello Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="28b8e-368">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28b8e-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="28b8e-369">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="28b8e-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
