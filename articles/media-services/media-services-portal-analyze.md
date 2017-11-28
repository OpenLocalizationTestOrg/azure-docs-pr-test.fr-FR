---
title: "Analyser vos éléments multimédias à l’aide du portail Azure | Microsoft Docs"
description: "Cette rubrique explique comment traiter vos éléments multimédia avec des processeurs multimédia Media Analytics à l’aide du portail Azure."
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
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a><span data-ttu-id="3bb1b-103">Analyser vos éléments multimédia à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3bb1b-103">Analyze your media using the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="3bb1b-104">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3bb1b-105">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bb1b-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="3bb1b-106">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="3bb1b-106">Overview</span></span>
<span data-ttu-id="3bb1b-107">Azure Media Services Analytics est un ensemble de composants de reconnaissance vocale et de vision qui répondent aux besoins des entreprises en termes de conformité, de sécurité et de portée mondiale, et qui aident les organisations et les entreprises à extraire des informations exploitables de leurs fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="3bb1b-108">Pour une présentation plus détaillée d’Azure Media Services Analytics, consultez [cette](media-services-analytics-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="3bb1b-109">Cette rubrique explique comment traiter vos éléments multimédia avec des processeurs multimédia Media Analytics à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-109">This topic discusses how to process your media with Media Analytics media processors (MPs) using the Azure portal.</span></span> <span data-ttu-id="3bb1b-110">Les processeurs multimédia Media Analytics créent des fichiers MP4 ou JSON.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="3bb1b-111">Si un processeur multimédia a produit un fichier MP4, vous pouvez télécharger ce dernier progressivement.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-111">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="3bb1b-112">Si un processeur multimédia a produit un fichier JSON, vous pouvez télécharger ce dernier à partir d’Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-112">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-to-analyze"></a><span data-ttu-id="3bb1b-113">Sélectionner une ressource que vous souhaitez analyser</span><span class="sxs-lookup"><span data-stu-id="3bb1b-113">Choose an asset that you want to analyze</span></span>
1. <span data-ttu-id="3bb1b-114">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="3bb1b-115">Dans la fenêtre **Paramètres**, sélectionnez **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-115">In the **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="3bb1b-116">.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-116">.</span></span>
    <span data-ttu-id="3bb1b-117">![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="3bb1b-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="3bb1b-118">Sélectionnez l’élément que vous souhaitez analyser, puis appuyez sur le bouton **Analyser**.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-118">Select the asset that you would like to analyze and press the **Analyze** button.</span></span>
   
    ![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="3bb1b-120">Dans la fenêtre **Traiter un fichier multimédia avec Analytique multimédia**, sélectionnez le processeur.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-120">In the **Process media asset with  Media Analytics** window, select the processor.</span></span> 
   
    <span data-ttu-id="3bb1b-121">Le reste de cet article explique pourquoi et comment utiliser chaque processeur.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-121">The rest of the article explains why and how to use each processor.</span></span> 
5. <span data-ttu-id="3bb1b-122">Appuyez sur **Créer** pour démarrer un travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-122">Press **Create** to the start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="3bb1b-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="3bb1b-123">Azure Media Indexer</span></span>
<span data-ttu-id="3bb1b-124">Le processeur multimédia **Azure Media Indexer** permet d’effectuer des recherches dans les fichiers multimédias et le contenu et de générer des pistes de sous-titrage.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-124">The **Azure Media Indexer** media processor enables you to make media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="3bb1b-125">Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="3bb1b-127">Langage</span><span class="sxs-lookup"><span data-stu-id="3bb1b-127">Language</span></span>
<span data-ttu-id="3bb1b-128">La langue naturelle à reconnaître dans le fichier multimédia.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-128">The natural language to be recognized in the multimedia file.</span></span> <span data-ttu-id="3bb1b-129">Par exemple, anglais ou espagnol.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="3bb1b-130">Sous-titres</span><span class="sxs-lookup"><span data-stu-id="3bb1b-130">Captions</span></span>
<span data-ttu-id="3bb1b-131">Vous pouvez choisir un format de sous-titre qui sera généré à partir de votre contenu.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="3bb1b-132">Un travail d’indexation peut générer des fichiers de sous-titres dans les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="3bb1b-132">An indexing job can generate closed caption files in the following formats:</span></span>  

* <span data-ttu-id="3bb1b-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-133">**SAMI**</span></span>
* <span data-ttu-id="3bb1b-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-134">**TTML**</span></span>
* <span data-ttu-id="3bb1b-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-135">**WebVTT**</span></span>

<span data-ttu-id="3bb1b-136">Les fichiers de sous-titre dans ces formats permettent de rendre un fichier audio et vidéo accessible aux malentendants.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-136">Closed Caption (CC) files in these formats can be used to make audio and video files accessible to people with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="3bb1b-137">Fichier AIB</span><span class="sxs-lookup"><span data-stu-id="3bb1b-137">AIB file</span></span>
<span data-ttu-id="3bb1b-138">Sélectionnez cette option si vous souhaitez générer le fichier Audio Index Blob pour une utilisation avec SQL Server IFilter personnalisé.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-138">Select this option if you would like to generate the Audio Index Blob file for use with the custom SQL Server IFilter.</span></span> <span data-ttu-id="3bb1b-139">Pour plus d’informations, consultez [ce](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="3bb1b-140">Mots clés</span><span class="sxs-lookup"><span data-stu-id="3bb1b-140">Keywords</span></span>
<span data-ttu-id="3bb1b-141">Sélectionnez cette option si vous souhaitez générer un fichier XML de mots clés.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-141">Select this option if you would like to generate a keywords XML file.</span></span> <span data-ttu-id="3bb1b-142">Ce fichier contient les mots clés extraits à partir du contenu de la reconnaissance vocale, avec les informations relatives à la fréquence et à la référence.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-142">This file contains keywords extracted from the speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="3bb1b-143">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="3bb1b-143">Job name</span></span>
<span data-ttu-id="3bb1b-144">Nom convivial qui vous permet d’identifier le travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-144">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="3bb1b-145">[Cet](media-services-portal-check-job-progress.md) article explique comment vous pouvez surveiller la progression d’un travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="3bb1b-146">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="3bb1b-146">Output file</span></span>
<span data-ttu-id="3bb1b-147">Nom convivial qui vous permet d’identifier le contenu en sortie.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-147">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="3bb1b-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="3bb1b-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="3bb1b-149">Azure Media Hyperlapse est un processeur multimédia qui crée des vidéos exceptionnelles image par image accélérées (time-lapse) à partir d’un contenu de caméra à la première personne (first-person camera) ou d’action.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="3bb1b-150">Pour plus d’informations, consultez [cette](media-services-hyperlapse-content.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="3bb1b-151">Cette section donne des informations sur les options que vous pouvez spécifier pour ce processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="3bb1b-153">Vitesse</span><span class="sxs-lookup"><span data-stu-id="3bb1b-153">Speed</span></span>
<span data-ttu-id="3bb1b-154">Indique la vitesse d’accélération de la vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-154">Specify the speed with which to speed up the input video.</span></span> <span data-ttu-id="3bb1b-155">La sortie est un rendu stabilisé et accéléré de l'entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-155">The output is a stabilized and time-lapsed rendition of the input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="3bb1b-156">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="3bb1b-156">Job name</span></span>
<span data-ttu-id="3bb1b-157">Nom convivial qui vous permet d’identifier le travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-157">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="3bb1b-158">[Cet](media-services-portal-check-job-progress.md) article explique comment vous pouvez surveiller la progression d’un travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="3bb1b-159">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="3bb1b-159">Output file</span></span>
<span data-ttu-id="3bb1b-160">Nom convivial qui vous permet d’identifier le contenu en sortie.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-160">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="3bb1b-161">Détecteur de visage Azure Media</span><span class="sxs-lookup"><span data-stu-id="3bb1b-161">Azure Media Face Detector</span></span>
<span data-ttu-id="3bb1b-162">Le processeur multimédia **Azure Media Face Detector** vous permet de compter, de suivre le mouvement, voire de mesurer la participation du public ainsi que ses réactions en analysant les expressions faciales.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-162">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="3bb1b-163">Ce service présente deux fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="3bb1b-163">This service contains two features:</span></span> 

* <span data-ttu-id="3bb1b-164">**Détection faciale**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-164">**Face detection**</span></span>
  
    <span data-ttu-id="3bb1b-165">La détection faciale détecte et suit les visages humains au sein d’une vidéo.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="3bb1b-166">Plusieurs visages peuvent être détectés et, par la suite, suivis dans leurs mouvements ; les métadonnées d’horodatage et de localisation seront retournées dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-166">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="3bb1b-167">Lors du suivi, la fonctionnalité tente d’attribuer un identificateur cohérent à un visage en mouvement, même si ce dernier quitte momentanément l’image ou s’il est caché.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-167">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3bb1b-168">Ce service n’effectue pas la reconnaissance faciale.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="3bb1b-169">Une personne qui quitte l’image ou dont le visage est caché pendant une période prolongée se voit attribuer un nouvel identifiant à son retour.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-169">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="3bb1b-170">**Détection d’émotions**</span><span class="sxs-lookup"><span data-stu-id="3bb1b-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="3bb1b-171">La détection d’émotions est un composant facultatif du processeur multimédia de détection faciale, qui analyse plusieurs caractéristiques émotionnelles sur les visages détectés, telles que le bonheur, la tristesse, la peur, la colère et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-171">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="3bb1b-173">Mode de détection</span><span class="sxs-lookup"><span data-stu-id="3bb1b-173">Detection mode</span></span>
<span data-ttu-id="3bb1b-174">Le processeur peut utiliser l’un des modes suivants :</span><span class="sxs-lookup"><span data-stu-id="3bb1b-174">One of the following modes can be used by the processor:</span></span>

* <span data-ttu-id="3bb1b-175">détection faciale</span><span class="sxs-lookup"><span data-stu-id="3bb1b-175">face detection</span></span>
* <span data-ttu-id="3bb1b-176">détection d’émotion par visage</span><span class="sxs-lookup"><span data-stu-id="3bb1b-176">per face emotion detection</span></span>
* <span data-ttu-id="3bb1b-177">détection d’émotion agrégée</span><span class="sxs-lookup"><span data-stu-id="3bb1b-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="3bb1b-178">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="3bb1b-178">Job name</span></span>
<span data-ttu-id="3bb1b-179">Nom convivial qui vous permet d’identifier le travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-179">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="3bb1b-180">[Cet](media-services-portal-check-job-progress.md) article explique comment vous pouvez surveiller la progression d’un travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="3bb1b-181">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="3bb1b-181">Output file</span></span>
<span data-ttu-id="3bb1b-182">Nom convivial qui vous permet d’identifier le contenu en sortie.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-182">A friendly name that lets you identify the output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="3bb1b-183">Détecteur de mouvement Azure Media</span><span class="sxs-lookup"><span data-stu-id="3bb1b-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="3bb1b-184">Le processeur multimédia **Azure Media Motion Detector** vous permet d’identifier efficacement les passages intéressants dans une vidéo qui, autrement, serait longue et monotone.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-184">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="3bb1b-185">La détection de mouvement peut être utilisée sur des séquences d’une caméra fixe pour identifier les passages de la vidéo où un mouvement se produit.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-185">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="3bb1b-186">Elle génère un fichier JSON contenant des métadonnées avec des horodateurs et le cadre de limitation de la vidéo où s’est produit l’événement.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-186">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="3bb1b-187">Ciblant les vidéos de surveillance, cette technologie est en mesure de classer les mouvements en événements pertinents et en faux positifs, tels que les ombres et les variations d’éclairage.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-187">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="3bb1b-188">Cela vous permet de générer des alertes de sécurité à partir de séquences vidéo sans perdre de temps avec d’innombrables faux positifs, et tout en accédant rapidement aux moments clés dans des vidéos de surveillance extrêmement longues.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-188">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="3bb1b-190">Miniatures vidéo Azure Media</span><span class="sxs-lookup"><span data-stu-id="3bb1b-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="3bb1b-191">Ce processeur peut vous aider à créer des synthèses de longues vidéos en sélectionnant automatiquement des extraits intéressants à partir de la vidéo source.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="3bb1b-192">Elle est utile quand vous voulez offrir une présentation rapide de ce qui se trouve dans une vidéo longue.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-192">This is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="3bb1b-193">Pour obtenir des informations détaillées et des exemples, consultez [Utiliser Azure Media Video Thumbnails pour créer une synthèse d’une vidéo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="3bb1b-193">For detailed information and examples, see [Use Azure Media Video Thumbnails to Create a Video Summarization](media-services-video-summarization.md)</span></span>

![Analyser des vidéos](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="3bb1b-195">Nom du travail</span><span class="sxs-lookup"><span data-stu-id="3bb1b-195">Job name</span></span>
<span data-ttu-id="3bb1b-196">Nom convivial qui vous permet d’identifier le travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-196">A friendly name that lets you identify the job.</span></span> <span data-ttu-id="3bb1b-197">[Cet](media-services-portal-check-job-progress.md) article explique comment vous pouvez surveiller la progression d’un travail.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor the progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="3bb1b-198">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="3bb1b-198">Output file</span></span>
<span data-ttu-id="3bb1b-199">Nom convivial qui vous permet d’identifier le contenu en sortie.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-199">A friendly name that lets you identify the output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3bb1b-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bb1b-200">Next steps</span></span>
<span data-ttu-id="3bb1b-201">Afficher les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="3bb1b-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3bb1b-202">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3bb1b-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

