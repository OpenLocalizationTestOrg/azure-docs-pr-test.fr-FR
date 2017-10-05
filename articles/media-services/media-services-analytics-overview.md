---
title: Media Analytics sur la plateforme Media Services | Microsoft Docs
description: "Présentation de la version préliminaire publique de Media Analytics, un ensemble de services de reconnaissance vocale et de vision par ordinateur destinés aux entreprises et répondant aux exigences de conformité, de sécurité et de présence mondiale"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: c0bbe6f80370515fa783b12757434897fe2221b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="2bb6d-103">Media Analytics sur la plateforme Media Services</span><span class="sxs-lookup"><span data-stu-id="2bb6d-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="2bb6d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2bb6d-104">Overview</span></span>
<span data-ttu-id="2bb6d-105">Les organisations sont de plus en plus nombreuses à privilégier les supports vidéo pour former leurs employés, susciter l’intérêt de leurs clients et présenter leurs activités commerciales.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="2bb6d-106">Le cloud computing offre un moyen de stocker, diffuser et accéder à ces fichiers multimédias volumineux.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="2bb6d-107">Mais lorsque la bibliothèque de contenu vidéo d’une société augmente, elle nécessite des moyens tout aussi efficaces d’extraire des analyses du contenu.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="2bb6d-108">Pour répondre à ce besoin croissant, Azure Media Services propose Azure Media Analytics.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="2bb6d-109">Media Analytics est une collection de composants visuels et vocaux qui aident les organisations et les entreprises à extraire des connaissances exploitables de leurs fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="2bb6d-110">Reposant sur les principaux composants de la plateforme Azure Media Services, Media Analytics est à même de traiter les données multimédias à l’échelle souhaitée.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="2bb6d-111">Avec Media Analytics, les développeurs peuvent rapidement ajouter des fonctionnalités avancées aux applications.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="2bb6d-112">Il répond aux attentes des grandes entreprises en matière d’échelle, de conformité, de sécurité et de présence mondiale.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="2bb6d-113">Le diagramme suivant montre Media Analytics et d’autres parties principales de la plateforme Media Services.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![Flux de travail VOD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="2bb6d-115">Les processeurs multimédias Media Analytics créent des fichiers MP4 ou JSON.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="2bb6d-116">Si un processeur multimédia produit un fichier MP4, vous pouvez télécharger ce dernier progressivement.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="2bb6d-117">Si un processeur multimédia a produit un fichier JSON, vous pouvez télécharger ce dernier à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="2bb6d-118">Services Media Analytics</span><span class="sxs-lookup"><span data-stu-id="2bb6d-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="2bb6d-119">Indexeur</span><span class="sxs-lookup"><span data-stu-id="2bb6d-119">Indexer</span></span>
<span data-ttu-id="2bb6d-120">Avec Azure Media Indexer, vous pouvez activer la recherche pour du contenu et générer des pistes de sous-titrage.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="2bb6d-121">Par rapport à la version précédente d’Azure Media Indexer 2 Preview a une indexation plus rapide et une prise en charge plus large des langues.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="2bb6d-122">Les langues prises en charge sont l’anglais, l’espagnol, le français, l’allemand, l’italien, le chinois, le portugais et l’arabe.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="2bb6d-123">Pour obtenir des informations détaillées et des exemples, consultez [Traiter les vidéos avec l’Indexeur multimédia Azure 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="2bb6d-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2bb6d-124">Hyperlapse</span></span>
<span data-ttu-id="2bb6d-125">Microsoft Hyperlapse associe des fonctionnalités de stabilisation vidéo et de création de séquences pour créer rapidement des vidéos immédiatement diffusables à partir de vos vidéos plus longues.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="2bb6d-126">En plus de la création de vidéos en accéléré, Hyperlapse vous permet de stabiliser des vidéos tremblantes qui ont été prises avec un téléphone portable ou un caméscope.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="2bb6d-127">Pour obtenir des informations détaillées et des exemples, consultez [Fichiers multimédia hyperlapse avec Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="2bb6d-128">Motion Detector</span><span class="sxs-lookup"><span data-stu-id="2bb6d-128">Motion Detector</span></span>
<span data-ttu-id="2bb6d-129">Vous pouvez utiliser Motion Detector pour détecter les mouvements dans les vidéos à arrière-plan fixe.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="2bb6d-130">Cela permet d’identifier les faux positifs sur les événements de mouvement détectés par les caméras de surveillance.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="2bb6d-131">Pour obtenir des informations détaillées et des exemples, consultez [Détection de mouvement pour Azure Media Analytics](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="2bb6d-132">Face Detector</span><span class="sxs-lookup"><span data-stu-id="2bb6d-132">Face Detector</span></span>
<span data-ttu-id="2bb6d-133">Avec Face Detector, vous pouvez détecter les visages et les émotions qui y sont exprimées, comme la joie, la tristesse et la surprise.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="2bb6d-134">Ce service est très utile dans plusieurs secteurs d’activité, comme expliqué plus tard, notamment pour l’agrégation et l’analyse des réactions des personnes participant à un événement.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="2bb6d-135">Pour obtenir des informations détaillées et des exemples, consultez [Détection des visages et des émotions pour Azure Media Analytics](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="2bb6d-136">Video Summarization (Création de résumés de vidéos)</span><span class="sxs-lookup"><span data-stu-id="2bb6d-136">Video summarization</span></span>
<span data-ttu-id="2bb6d-137">La synthèse d’une vidéo peut vous aider à créer des synthèses de longues vidéos en sélectionnant automatiquement des extraits intéressants à partir de la vidéo source.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="2bb6d-138">Cette fonctionnalité est utile quand vous voulez offrir une présentation rapide de ce qui se trouve dans une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="2bb6d-139">Pour obtenir des informations détaillées et des exemples, consultez [Utiliser Azure Media Video Thumbnails pour créer une synthèse d’une vidéo](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="2bb6d-140">Reconnaissance optique de caractères</span><span class="sxs-lookup"><span data-stu-id="2bb6d-140">Optical character recognition</span></span>
<span data-ttu-id="2bb6d-141">Avec Azure Media OCR (reconnaissance optique de caractères), vous pouvez convertir le contenu texte de fichiers vidéo en un texte numérique modifiable et pouvant faire l’objet d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="2bb6d-142">Vous pouvez ensuite automatiser l’extraction de métadonnées explicites à partir du signal vidéo de votre contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="2bb6d-143">Rédaction de face évolutive</span><span class="sxs-lookup"><span data-stu-id="2bb6d-143">Scalable face redaction</span></span>
<span data-ttu-id="2bb6d-144">Azure Media Redactor est un processeur multimédia Media Analytics qui offre la rédaction de face évolutive dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="2bb6d-145">La rédaction de face vous permet de modifier votre vidéo afin de flouter les visages des individus sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="2bb6d-146">Vous souhaitez peut-être utiliser le service de rédaction de face dans les médias d’actualité ou lorsque la sécurité publique est impliquée.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="2bb6d-147">Quelques minutes de séquences vidéo contenant plusieurs visages peuvent nécessiter des heures de traitement manuel, mais avec ce service, le processus de rédaction de face ne nécessite que quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="2bb6d-148">Pour plus d'informations, consultez l’article [Éditer les visages avec Azure Media Analytique](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="2bb6d-149">Scénarios courants</span><span class="sxs-lookup"><span data-stu-id="2bb6d-149">Common scenarios</span></span>
<span data-ttu-id="2bb6d-150">Media Analytics peut aider les organisations et entreprises à mieux exploiter et cibler leurs contenus vidéo et à améliorer la gestion des gros volumes de contenus vidéo.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="2bb6d-151">Voici quelques exemples de scénario :</span><span class="sxs-lookup"><span data-stu-id="2bb6d-151">Here are several scenarios:</span></span>

* <span data-ttu-id="2bb6d-152">**Centres d’appel**.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-152">**Call centers**.</span></span> <span data-ttu-id="2bb6d-153">Même avec le développement des médias sociaux, les centres d’appels client sont encore largement utilisés pour faciliter les opérations des services client.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-153">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="2bb6d-154">Ces données audio contiennent une mine d’informations sur les clients, qui peuvent être utilisées pour mieux répondre aux attentes des clients.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-154">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="2bb6d-155">Avec Media Indexer, les organisations peuvent extraire du texte et créer des index de recherche et des tableaux de bord.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="2bb6d-156">Ils peuvent ensuite extraire des informations sur les réclamations, les causes des réclamations et autres données pertinentes.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="2bb6d-157">**Modération du contenu généré par les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-157">**User-generated content moderation**.</span></span> <span data-ttu-id="2bb6d-158">Des médias d’information aux services de police, de nombreuses organisations ont des portails publics sur lesquels est publié du contenu multimédia généré par l’utilisateur, comme des vidéos et des images.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-158">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="2bb6d-159">Le volume de contenu peut fortement augmenter en raison d’événements inattendus.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-159">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="2bb6d-160">Dans ce type de scénario, il est difficile de vérifier manuellement et correctement la pertinence de tout le contenu.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-160">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="2bb6d-161">Les clients peuvent déléguer cette tâche au service de modération du contenu pour se concentrer sur le contenu approprié.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-161">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="2bb6d-162">**Surveillance**.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-162">**Surveillance**.</span></span> <span data-ttu-id="2bb6d-163">La généralisation de l’utilisation des caméras IP s’accompagne d’un inventaire croissant de vidéos de surveillance.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-163">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="2bb6d-164">L’examen manuel des vidéos de surveillance est long et sujet aux erreurs humaines.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-164">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="2bb6d-165">Media Analytics fournit plusieurs services, tels que la détection de mouvement, la détection des visages et Hyperlapse, pour faciliter l’examen, la gestion et la création d’éléments dérivés.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="2bb6d-166">Processeurs multimédia Media Analytics</span><span class="sxs-lookup"><span data-stu-id="2bb6d-166">Media Analytics media processors</span></span>
<span data-ttu-id="2bb6d-167">Cette section répertorie tous les processeurs multimédia Media Analytics et montre comment utiliser .NET ou REST pour obtenir un objet de processeur multimédia (MP).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-167">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="2bb6d-168">Noms MP</span><span class="sxs-lookup"><span data-stu-id="2bb6d-168">MP names</span></span>
* <span data-ttu-id="2bb6d-169">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="2bb6d-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="2bb6d-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="2bb6d-170">Azure Media Indexer</span></span>
* <span data-ttu-id="2bb6d-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="2bb6d-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="2bb6d-172">Détecteur de visage Azure Media</span><span class="sxs-lookup"><span data-stu-id="2bb6d-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="2bb6d-173">Détecteur de mouvement Azure Media</span><span class="sxs-lookup"><span data-stu-id="2bb6d-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="2bb6d-174">Miniatures vidéo Azure Media</span><span class="sxs-lookup"><span data-stu-id="2bb6d-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="2bb6d-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="2bb6d-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="2bb6d-176">.NET</span><span class="sxs-lookup"><span data-stu-id="2bb6d-176">.NET</span></span>
<span data-ttu-id="2bb6d-177">La fonction suivante sélectionne un des noms MP spécifiés et retourne un objet MP.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-177">The following function takes one of the specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="2bb6d-178">REST</span><span class="sxs-lookup"><span data-stu-id="2bb6d-178">REST</span></span>
<span data-ttu-id="2bb6d-179">Demande :</span><span class="sxs-lookup"><span data-stu-id="2bb6d-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="2bb6d-180">Réponse :</span><span class="sxs-lookup"><span data-stu-id="2bb6d-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="2bb6d-181">Démonstrations</span><span class="sxs-lookup"><span data-stu-id="2bb6d-181">Demos</span></span>
<span data-ttu-id="2bb6d-182">Consultez les [Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bb6d-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bb6d-183">Next steps</span></span>
<span data-ttu-id="2bb6d-184">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="2bb6d-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2bb6d-185">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2bb6d-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="2bb6d-186">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="2bb6d-186">Related articles</span></span>
<span data-ttu-id="2bb6d-187">Consultez [l’Annonce concernant Media Services Analytics](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="2bb6d-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
