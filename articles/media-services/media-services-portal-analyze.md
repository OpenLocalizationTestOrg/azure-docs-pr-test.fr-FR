---
title: "aaaAnalyze votre média à l’aide de hello le portail Azure | Documents Microsoft"
description: "Cette rubrique explique comment tooprocess votre média avec des processeurs multimédias de support Analytique (PA) à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="554c5-103">Analyser votre média à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="554c5-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="554c5-104">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="554c5-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="554c5-105">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="554c5-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="554c5-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="554c5-106">Overview</span></span>
<span data-ttu-id="554c5-107">Analytique de Services de support Azure est une collection de composants vocale et de la vision (à l’échelle de l’entreprise, la conformité, de sécurité et portée globale) qui le rendent plus facile pour les organisations et les entreprises tooderive d’informations exploitables à partir de leurs fichiers vidéos.</span><span class="sxs-lookup"><span data-stu-id="554c5-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="554c5-108">Pour une présentation plus détaillée d’Azure Media Services Analytics, consultez [cette](media-services-analytics-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="554c5-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="554c5-109">Cette rubrique explique comment tooprocess votre média avec des processeurs multimédias de support Analytique (PA) à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="554c5-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="554c5-110">Les processeurs multimédia Media Analytics créent des fichiers MP4 ou JSON.</span><span class="sxs-lookup"><span data-stu-id="554c5-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="554c5-111">Si un processeur multimédia produit un fichier MP4, vous pouvez télécharger progressivement les fichier hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="554c5-112">Si un processeur multimédia produit un fichier JSON, vous pouvez télécharger le fichier de hello de hello stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="554c5-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="554c5-113">Choisissez un élément multimédia que vous souhaitez tooanalyze</span><span class="sxs-lookup"><span data-stu-id="554c5-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="554c5-114">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="554c5-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="554c5-115">Bonjour **paramètres** fenêtre, sélectionnez **actifs**.</span><span class="sxs-lookup"><span data-stu-id="554c5-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="554c5-116">.</span><span class="sxs-lookup"><span data-stu-id="554c5-116">.</span></span>
    <span data-ttu-id="554c5-117">![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="554c5-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="554c5-118">Asset hello SELECT que vous aimeriez hello tooanalyze et appuyez sur **analyser** bouton.</span><span class="sxs-lookup"><span data-stu-id="554c5-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="554c5-120">Bonjour **processus multimédia ayant Media Analytique** fenêtre, le processeur de hello select.</span><span class="sxs-lookup"><span data-stu-id="554c5-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="554c5-121">rest Hello d’article de hello explique pourquoi et comment toouse chaque processeur.</span><span class="sxs-lookup"><span data-stu-id="554c5-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="554c5-122">Appuyez sur **créer** toohello démarrer une tâche.</span><span class="sxs-lookup"><span data-stu-id="554c5-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="554c5-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="554c5-123">Azure Media Indexer</span></span>
<span data-ttu-id="554c5-124">Hello **Azure Media Indexer** processeur multimédia vous permet de toomake des fichiers multimédias et contenu de recherche, ainsi que pour générer des pistes de sous-titres.</span><span class="sxs-lookup"><span data-stu-id="554c5-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="554c5-125">Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="554c5-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="554c5-127">language</span><span class="sxs-lookup"><span data-stu-id="554c5-127">Language</span></span>
<span data-ttu-id="554c5-128">toobe de langage naturel Hello reconnu dans le fichier multimédia de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="554c5-129">Par exemple, anglais ou espagnol.</span><span class="sxs-lookup"><span data-stu-id="554c5-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="554c5-130">Sous-titres</span><span class="sxs-lookup"><span data-stu-id="554c5-130">Captions</span></span>
<span data-ttu-id="554c5-131">Vous pouvez choisir un format de sous-titre qui sera généré à partir de votre contenu.</span><span class="sxs-lookup"><span data-stu-id="554c5-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="554c5-132">Un travail d’indexation peut générer des fichiers de sous-titres Bonjour suivant formats :</span><span class="sxs-lookup"><span data-stu-id="554c5-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="554c5-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="554c5-133">**SAMI**</span></span>
* <span data-ttu-id="554c5-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="554c5-134">**TTML**</span></span>
* <span data-ttu-id="554c5-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="554c5-135">**WebVTT**</span></span>

<span data-ttu-id="554c5-136">Les fichiers de sous-titres fermés dans ces formats peuvent être utilisés toomake audio et vidéo fichiers accessible toopeople malentendantes.</span><span class="sxs-lookup"><span data-stu-id="554c5-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="554c5-137">Fichier AIB</span><span class="sxs-lookup"><span data-stu-id="554c5-137">AIB file</span></span>
<span data-ttu-id="554c5-138">Sélectionnez cette option si vous serez comme fichier de son Index Blob toogenerate hello pour une utilisation avec hello IFilter de serveur SQL personnalisée.</span><span class="sxs-lookup"><span data-stu-id="554c5-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="554c5-139">Pour plus d’informations, consultez [ce](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="554c5-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="554c5-140">Mots clés</span><span class="sxs-lookup"><span data-stu-id="554c5-140">Keywords</span></span>
<span data-ttu-id="554c5-141">Sélectionnez cette option si vous souhaitez que toogenerate un fichier XML de mots clés.</span><span class="sxs-lookup"><span data-stu-id="554c5-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="554c5-142">Ce fichier contient des mots clés extraits à partir du contenu de reconnaissance vocale hello, avec la fréquence et les informations de décalage.</span><span class="sxs-lookup"><span data-stu-id="554c5-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="554c5-143">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="554c5-143">Job name</span></span>
<span data-ttu-id="554c5-144">Un nom convivial qui vous permet d’identifier la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="554c5-145">[Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="554c5-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="554c5-146">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="554c5-146">Output file</span></span>
<span data-ttu-id="554c5-147">Un nom convivial qui vous permet d’identifier le contenu de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="554c5-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="554c5-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="554c5-149">Azure Media Hyperlapse est un processeur multimédia qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d’un contenu de caméra à la première personne (first-person camera) ou d’action.</span><span class="sxs-lookup"><span data-stu-id="554c5-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="554c5-150">Pour plus d’informations, consultez [cette](media-services-hyperlapse-content.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="554c5-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="554c5-151">Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="554c5-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="554c5-153">Vitesse</span><span class="sxs-lookup"><span data-stu-id="554c5-153">Speed</span></span>
<span data-ttu-id="554c5-154">Spécifiez la vitesse hello avec le toospeed vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="554c5-155">sortie de Hello est un format de stabilisation et temps écoulé associé de la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="554c5-156">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="554c5-156">Job name</span></span>
<span data-ttu-id="554c5-157">Un nom convivial qui vous permet d’identifier la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="554c5-158">[Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="554c5-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="554c5-159">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="554c5-159">Output file</span></span>
<span data-ttu-id="554c5-160">Un nom convivial qui vous permet d’identifier le contenu de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="554c5-161">Détecteur de visage Azure Media</span><span class="sxs-lookup"><span data-stu-id="554c5-161">Azure Media Face Detector</span></span>
<span data-ttu-id="554c5-162">Hello **Azure Media Face détecteur** le processeur multimédia (MP) vous permet de toocount, les mouvements de suivi et même la participation jauge audience et réaction via des expressions visages.</span><span class="sxs-lookup"><span data-stu-id="554c5-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="554c5-163">Ce service présente deux fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="554c5-163">This service contains two features:</span></span> 

* <span data-ttu-id="554c5-164">**Détection faciale**</span><span class="sxs-lookup"><span data-stu-id="554c5-164">**Face detection**</span></span>
  
    <span data-ttu-id="554c5-165">La détection faciale détecte et suit les visages humains au sein d’une vidéo.</span><span class="sxs-lookup"><span data-stu-id="554c5-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="554c5-166">Plusieurs polices peuvent être détectées et par la suite être suivis comme ils sont en déplacement, avec hello heure et l’emplacement des métadonnées retournées dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="554c5-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="554c5-167">Lors du suivi, il va tenter de toogive un toohello ID cohérent même sont confrontés lors de la personne de hello tourne autour de l’écran, même s’ils sont coupés ou laisser brièvement les frames de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="554c5-168">Ce service n’effectue pas la reconnaissance faciale.</span><span class="sxs-lookup"><span data-stu-id="554c5-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="554c5-169">Une personne qui laisse le frame de hello ou devienne coupée pour trop longtemps recevra un nouvel ID lorsqu’elles retournent.</span><span class="sxs-lookup"><span data-stu-id="554c5-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="554c5-170">**Détection d’émotions**</span><span class="sxs-lookup"><span data-stu-id="554c5-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="554c5-171">Détection d’émotion est un composant facultatif de hello processeur multimédia de détection Face qui renvoie analysis sur plusieurs attributs émotionnels à partir de face hello détecté, y compris bonheur, leur, peur, colère et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="554c5-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="554c5-173">Mode de détection</span><span class="sxs-lookup"><span data-stu-id="554c5-173">Detection mode</span></span>
<span data-ttu-id="554c5-174">Une des hello suivant des modes peut être utilisée par le processeur hello :</span><span class="sxs-lookup"><span data-stu-id="554c5-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="554c5-175">détection faciale</span><span class="sxs-lookup"><span data-stu-id="554c5-175">face detection</span></span>
* <span data-ttu-id="554c5-176">détection d’émotion par visage</span><span class="sxs-lookup"><span data-stu-id="554c5-176">per face emotion detection</span></span>
* <span data-ttu-id="554c5-177">détection d’émotion agrégée</span><span class="sxs-lookup"><span data-stu-id="554c5-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="554c5-178">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="554c5-178">Job name</span></span>
<span data-ttu-id="554c5-179">Un nom convivial qui vous permet d’identifier la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="554c5-180">[Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="554c5-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="554c5-181">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="554c5-181">Output file</span></span>
<span data-ttu-id="554c5-182">Un nom convivial qui vous permet d’identifier le contenu de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="554c5-183">Détecteur de mouvement Azure Media</span><span class="sxs-lookup"><span data-stu-id="554c5-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="554c5-184">Hello **détecteur de mouvement Azure Media** permet de processeur (MP) support tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement.</span><span class="sxs-lookup"><span data-stu-id="554c5-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="554c5-185">Détection de mouvement peut être utilisée sur caméra statique enregistrements tooidentify sections de la vidéo de hello où se produit le mouvement.</span><span class="sxs-lookup"><span data-stu-id="554c5-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="554c5-186">Il génère un fichier JSON contenant des métadonnées avec les horodateurs et hello englobant la région où l’événement de hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="554c5-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="554c5-187">Cible des flux vidéo de sécurité, cette technologie est mouvement en mesure de toocategorize dans les événements pertinents et des faux positifs, tels que des changements d’éclairage et les ombres.</span><span class="sxs-lookup"><span data-stu-id="554c5-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="554c5-188">Ainsi, vous toogenerate les alertes de sécurité à partir de flux de l’appareil photo sans recevoir des messages indésirables avec les événements non pertinentes sans fin, tout en étant instants tooextract en mesure d’intérêt de vidéos de surveillance très longs.</span><span class="sxs-lookup"><span data-stu-id="554c5-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="554c5-190">Miniatures vidéo Azure Media</span><span class="sxs-lookup"><span data-stu-id="554c5-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="554c5-191">Ce processeur peut vous aider à créer des résumés de vidéos long en sélectionnant automatiquement extraits intéressantes à partir de la vidéo source de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="554c5-192">Cela est utile lorsque vous souhaitez tooprovide un aperçu rapide de quel tooexpect dans une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="554c5-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="554c5-193">Pour plus d’informations et d’exemples, consultez [utiliser Azure Media les miniatures vidéo tooCreate une synthèse de la vidéo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="554c5-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="554c5-195">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="554c5-195">Job name</span></span>
<span data-ttu-id="554c5-196">Un nom convivial qui vous permet d’identifier la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="554c5-197">[Cela](media-services-portal-check-job-progress.md) explique comment vous pouvez surveiller l’avancement hello d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="554c5-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="554c5-198">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="554c5-198">Output file</span></span>
<span data-ttu-id="554c5-199">Un nom convivial qui vous permet d’identifier le contenu de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="554c5-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="554c5-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="554c5-200">Next steps</span></span>
<span data-ttu-id="554c5-201">Afficher les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="554c5-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="554c5-202">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="554c5-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

