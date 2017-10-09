---
title: aaaMedia Analytique sur une plateforme de Media Services hello | Documents Microsoft
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
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="4fa2c-103">Analytique multimédia sur la plateforme de Media Services hello</span><span class="sxs-lookup"><span data-stu-id="4fa2c-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="4fa2c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4fa2c-104">Overview</span></span>
<span data-ttu-id="4fa2c-105">Plusieurs organisations utilisent vidéo comme hello tootrain moyenne par défaut leurs employés, retenir leurs clients et les fonctions commerciales de document.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="4fa2c-106">Le cloud computing offre un moyen toostore, flux et accéder à ces fichiers multimédias volumineux.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="4fa2c-107">Mais comme bibliothèque d’une société de contenu vidéo augmente, il doit aussi efficaces de l’extraction d’informations à partir du contenu de hello.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="4fa2c-108">tooaddress ce besoin croissant, Azure Media Services offre Azure Media Analytique.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="4fa2c-109">Support Analytique est une collection de composants de la reconnaissance vocale et de la vision qui rend plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="4fa2c-110">Générée à l’aide de composants de la plateforme hello core Media Services, support Analytique peut gérer media à grande échelle sur le premier jour de traitement.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="4fa2c-111">Avec Media Analytics, les développeurs peuvent rapidement ajouter des fonctionnalités avancées aux applications.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="4fa2c-112">Il fournit les environnements d’entreprise complet hello, conformité, la sécurité et portée requis par les organisations de grande taille.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="4fa2c-113">Hello diagramme suivant montre Analytique de support et d’autres parties principales de plateforme de Media Services hello.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Flux de travail VOD](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="4fa2c-115">Les processeurs multimédias Media Analytics créent des fichiers MP4 ou JSON.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="4fa2c-116">Si un processeur multimédia génère un fichier MP4, vous pouvez télécharger progressivement les fichier hello.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="4fa2c-117">Si un processeur multimédia génère un fichier JSON, vous pouvez télécharger le fichier de hello à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="4fa2c-118">Services Media Analytics</span><span class="sxs-lookup"><span data-stu-id="4fa2c-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="4fa2c-119">Indexeur</span><span class="sxs-lookup"><span data-stu-id="4fa2c-119">Indexer</span></span>
<span data-ttu-id="4fa2c-120">Avec Azure Media Indexer, vous pouvez activer la recherche pour du contenu et générer des pistes de sous-titrage.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="4fa2c-121">Version précédente toohello comparés, Azure Media Indexer en version préliminaire 2 prend en charge les langage plus rapide d’indexation et plus large.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="4fa2c-122">Les langues prises en charge sont l’anglais, l’espagnol, le français, l’allemand, l’italien, le chinois, le portugais et l’arabe.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="4fa2c-123">Pour obtenir des informations détaillées et des exemples, consultez [Traiter les vidéos avec l’Indexeur multimédia Azure 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="4fa2c-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="4fa2c-124">Hyperlapse</span></span>
<span data-ttu-id="4fa2c-125">Microsoft Hyperlapse combine stabilisation vidéo et capacité séquentiel toocreate rapide, utilisable à partir de votre contenu sous forme longue.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="4fa2c-126">Outre la création intermittente, vous pouvez utiliser les vidéos stables de Hyperlapse toocreate de vidéos tremblement capturées à l’aide de téléphones et de caméscopes.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="4fa2c-127">Pour obtenir des informations détaillées et des exemples, consultez [Fichiers multimédia hyperlapse avec Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="4fa2c-128">Motion Detector</span><span class="sxs-lookup"><span data-stu-id="4fa2c-128">Motion Detector</span></span>
<span data-ttu-id="4fa2c-129">Vous pouvez utiliser le mouvement de toodetect de détecteur de mouvement dans une vidéo avec des arrière-plans STATIONNAIRES.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="4fa2c-130">Cela rend possible toocheck de faux positifs sur les événements de mouvement détectées par des caméras de surveillance.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="4fa2c-131">Pour obtenir des informations détaillées et des exemples, consultez [Détection de mouvement pour Azure Media Analytics](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="4fa2c-132">Face Detector</span><span class="sxs-lookup"><span data-stu-id="4fa2c-132">Face Detector</span></span>
<span data-ttu-id="4fa2c-133">Avec Face Detector, vous pouvez détecter les visages et les émotions qui y sont exprimées, comme la joie, la tristesse et la surprise.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="4fa2c-134">Ce service est très utile dans plusieurs secteurs d’activité, comme expliqué plus tard, notamment pour l’agrégation et l’analyse des réactions des personnes participant à un événement.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="4fa2c-135">Pour obtenir des informations détaillées et des exemples, consultez [Détection des visages et des émotions pour Azure Media Analytics](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="4fa2c-136">Video Summarization (Création de résumés de vidéos)</span><span class="sxs-lookup"><span data-stu-id="4fa2c-136">Video summarization</span></span>
<span data-ttu-id="4fa2c-137">Synthèse vidéo peut vous aider à créer des résumés de vidéos long en sélectionnant automatiquement extraits intéressantes à partir de la vidéo source de hello.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="4fa2c-138">Cette capacité est utile lorsque vous souhaitez tooprovide un aperçu rapide de quel tooexpect dans une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="4fa2c-139">Pour plus d’informations et d’exemples, consultez [synthèse vidéo de miniatures de vidéo utiliser Azure Media toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="4fa2c-140">Reconnaissance optique de caractères</span><span class="sxs-lookup"><span data-stu-id="4fa2c-140">Optical character recognition</span></span>
<span data-ttu-id="4fa2c-141">Avec Azure Media OCR (reconnaissance optique de caractères), vous pouvez convertir le contenu texte de fichiers vidéo en un texte numérique modifiable et pouvant faire l’objet d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="4fa2c-142">Vous pouvez automatiser extraction hello de métadonnées significatives à partir de signal vidéo de hello de votre support.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="4fa2c-143">Rédaction de face évolutive</span><span class="sxs-lookup"><span data-stu-id="4fa2c-143">Scalable face redaction</span></span>
<span data-ttu-id="4fa2c-144">Azure Media Redactor est un processeur multimédia Media Analytique qui offre la rédaction de face évolutives dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="4fa2c-145">À l’aide de rédaction de face, vous pouvez modifier votre vidéo tooblur de face d’individus sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="4fa2c-146">Vous pouvez choisir le service de rédaction de face toouse hello dans les médias ou la sécurité publique est impliquée.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="4fa2c-147">Quelques minutes de film qui contient plusieurs polices peuvent prendre des heures tooredact manuellement, mais avec ce service, face rédaction prend seulement quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="4fa2c-148">Pour plus d’informations, consultez hello [procéder faces avec Azure Media Analytique](media-services-face-redaction.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="4fa2c-149">Scénarios courants</span><span class="sxs-lookup"><span data-stu-id="4fa2c-149">Common scenarios</span></span>
<span data-ttu-id="4fa2c-150">Media Analytics peut aider les organisations et entreprises à mieux exploiter et cibler leurs contenus vidéo et à améliorer la gestion des gros volumes de contenus vidéo.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="4fa2c-151">Voici quelques exemples de scénario :</span><span class="sxs-lookup"><span data-stu-id="4fa2c-151">Here are several scenarios:</span></span>

* <span data-ttu-id="4fa2c-152">**Centres d’appel**.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-152">**Call centers**.</span></span> <span data-ttu-id="4fa2c-153">Même avec l’apparition de hello de médias sociaux, centres d’appels client facilitent encore un grand pourcentage des transactions du service clientèle.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="4fa2c-154">Codé dans ces données audio sont une grande quantité d’informations sur le client qui peuvent être analysées tooachieve satisfaction des clients plus élevée.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="4fa2c-155">Avec Media Indexer, les organisations peuvent extraire du texte et créer des index de recherche et des tableaux de bord.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="4fa2c-156">Ils peuvent ensuite extraire des informations sur les réclamations, les causes des réclamations et autres données pertinentes.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="4fa2c-157">**Modération du contenu généré par les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-157">**User-generated content moderation**.</span></span> <span data-ttu-id="4fa2c-158">À partir des services de médias prises toopolice, de nombreuses organisations possèdent des portails publics qui acceptent généré par l’utilisateur les supports tels que des vidéos et des images.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="4fa2c-159">volume Hello de contenu peut grimper toounexpected événements d’échéance.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="4fa2c-160">Dans ces scénarios, il est difficile tooconduct révisions du manuel efficace du contenu de manière correcte.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="4fa2c-161">Les clients peuvent reposer sur toofocus du service de modération de contenu hello sur le contenu qui est approprié.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="4fa2c-162">**Surveillance**.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-162">**Surveillance**.</span></span> <span data-ttu-id="4fa2c-163">Hello s’accompagne de croissance en cours d’utilisation des caméras IP un inventaire croissant de vidéo de surveillance.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="4fa2c-164">Examen manuel de vidéo de surveillance est toohuman intensive et susceptible d’engendrer des erreurs au moment.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="4fa2c-165">Support Analytique fournit des services tels que la détection de mouvement, la détection de visage et Hyperlapse toomake hello processus de révision, la gestion et création dérivés plus facile.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="4fa2c-166">Processeurs multimédia Media Analytics</span><span class="sxs-lookup"><span data-stu-id="4fa2c-166">Media Analytics media processors</span></span>
<span data-ttu-id="4fa2c-167">Cette section processeurs multimédias de listes hello Media Analytique et montre comment tooget un objet de processeur (MP) multimédia toouse .NET ou REST.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="4fa2c-168">Noms MP</span><span class="sxs-lookup"><span data-stu-id="4fa2c-168">MP names</span></span>
* <span data-ttu-id="4fa2c-169">Azure Media Indexer 2 Preview</span><span class="sxs-lookup"><span data-stu-id="4fa2c-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="4fa2c-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="4fa2c-170">Azure Media Indexer</span></span>
* <span data-ttu-id="4fa2c-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="4fa2c-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="4fa2c-172">Détecteur de visage Azure Media</span><span class="sxs-lookup"><span data-stu-id="4fa2c-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="4fa2c-173">Détecteur de mouvement Azure Media</span><span class="sxs-lookup"><span data-stu-id="4fa2c-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="4fa2c-174">Miniatures vidéo Azure Media</span><span class="sxs-lookup"><span data-stu-id="4fa2c-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="4fa2c-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="4fa2c-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="4fa2c-176">.NET</span><span class="sxs-lookup"><span data-stu-id="4fa2c-176">.NET</span></span>
<span data-ttu-id="4fa2c-177">Hello après la fonction prend hello spécifié MP noms et retourne un objet de pack d’administration.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="4fa2c-178">REST</span><span class="sxs-lookup"><span data-stu-id="4fa2c-178">REST</span></span>
<span data-ttu-id="4fa2c-179">Demande :</span><span class="sxs-lookup"><span data-stu-id="4fa2c-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="4fa2c-180">Réponse :</span><span class="sxs-lookup"><span data-stu-id="4fa2c-180">Response:</span></span>

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

## <a name="demos"></a><span data-ttu-id="4fa2c-181">Démonstrations</span><span class="sxs-lookup"><span data-stu-id="4fa2c-181">Demos</span></span>
<span data-ttu-id="4fa2c-182">Consultez les [Démonstrations Azure Media Analytics](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fa2c-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fa2c-183">Next steps</span></span>
<span data-ttu-id="4fa2c-184">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4fa2c-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4fa2c-185">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4fa2c-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="4fa2c-186">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="4fa2c-186">Related articles</span></span>
<span data-ttu-id="4fa2c-187">Consultez [l’Annonce concernant Media Services Analytics](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="4fa2c-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
