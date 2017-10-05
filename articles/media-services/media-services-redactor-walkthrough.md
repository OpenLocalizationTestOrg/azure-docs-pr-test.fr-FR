---
title: "Procédure d’édition des visages avec Azure Media Analytics | Microsoft Docs"
description: "Cette rubrique explique étape par étape comment exécuter un workflow de rédaction complet à l’aide d’Azure Media Services Explorer (AMSE) et d’Azure Media Redactor Visualizer (outil open source)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="d6a0d-103">Procédure d’édition des visages avec Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="d6a0d-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="d6a0d-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="d6a0d-104">Overview</span></span>

<span data-ttu-id="d6a0d-105">**Azure Media Redactor** est un processeur multimédia [Azure Media Analytics](media-services-analytics-overview.md) qui offre la rédaction de face évolutive dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="d6a0d-106">La rédaction de face vous permet de modifier votre vidéo afin de flouter les visages des individus sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="d6a0d-107">Vous souhaitez peut-être utiliser le service de rédaction de face dans des scénarios de média et de sécurité publics.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="d6a0d-108">Quelques minutes de séquences vidéo contenant plusieurs visages peuvent nécessiter des heures de traitement manuel, mais avec ce service, le processus de rédaction de face ne nécessitera que quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="d6a0d-109">Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="d6a0d-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="d6a0d-110">Pour plus d’informations sur **Azure Media Redactor**, consultez la rubrique [Vue d’ensemble de la rédaction de face](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="d6a0d-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="d6a0d-111">Cette rubrique explique étape par étape comment exécuter un workflow de rédaction complet à l’aide d’Azure Media Services Explorer (AMSE) et d’Azure Media Redactor Visualizer (outil open source).</span><span class="sxs-lookup"><span data-stu-id="d6a0d-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="d6a0d-112">Le processeur multimédia **Azure Media Redactor** est uniquement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="d6a0d-113">Il est disponible dans toutes les régions Azure publiques, ainsi que dans les centres de données de Chine et du Gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="d6a0d-114">Cette version préliminaire est actuellement disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-114">This preview is currently free of charge.</span></span> <span data-ttu-id="d6a0d-115">Dans la version actuelle, la longueur de vidéo traitée est limitée à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="d6a0d-116">Pour plus d’informations, consultez [ce](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="d6a0d-117">Worfkflow d’Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="d6a0d-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="d6a0d-118">La manière la plus simple de prendre en main Redactor consiste à utiliser l’outil AMSE open source sur github.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="d6a0d-119">Vous pouvez exécuter un workflow simplifié via le mode **combiné** si vous n’avez pas besoin d’accéder au json d’annotations ou aux images jpg de face.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="d6a0d-120">Téléchargement et configuration</span><span class="sxs-lookup"><span data-stu-id="d6a0d-120">Download and setup</span></span>

1. <span data-ttu-id="d6a0d-121">Téléchargez l’outil AMSE [ici](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="d6a0d-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="d6a0d-122">Connectez-vous à votre compte Media Services à l’aide de votre clé de service.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="d6a0d-123">Pour obtenir le nom du compte et les informations sur la clé, accédez au [portail Azure](https://portal.azure.com/) et sélectionnez votre compte AMS.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="d6a0d-124">Sélectionnez Paramètres > Clés.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="d6a0d-125">La fenêtre Gérer les clés affiche le nom du compte ainsi que les clés primaires et secondaires.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="d6a0d-126">Copiez les valeurs du nom du compte et de la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-126">Copy values of the account name and the primary key.</span></span>

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="d6a0d-128">Premier passage - Mode d’analyse</span><span class="sxs-lookup"><span data-stu-id="d6a0d-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="d6a0d-129">Chargez votre fichier multimédia via Ressource -> Charger, ou par un glisser -déplacer.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="d6a0d-130">Cliquez avec le bouton droit de la souris et traitez votre fichier multimédia en utilisant 	Analytique multimédia –> Azure Media Redactor –> Mode Analyze.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="d6a0d-133">La sortie inclut un fichier json d’annotations avec les données d’emplacement de face, ainsi qu’un fichier jpg de chaque face détectée.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="d6a0d-135">Second passage – Mode de rédaction</span><span class="sxs-lookup"><span data-stu-id="d6a0d-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="d6a0d-136">Chargez votre ressource vidéo d’origine sur la sortie dès le premier passage et définissez-la comme ressource principale.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="d6a0d-138">(Facultatif) Chargez un fichier « Dance_idlist.txt » qui comprend une liste (avec délimitation par un saut de ligne) des ID que vous souhaitez éditer.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="d6a0d-140">(Facultatif) Apportez des modifications au fichier .json d’annotations, telles qu’une augmentation des limites du cadre englobant.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="d6a0d-141">Cliquez avec le bouton droit sur la ressource de sortie à partir du premier passage, sélectionnez le Redactor et exécutez-le avec le mode **Rédaction**.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="d6a0d-143">Téléchargez ou partagez la ressource de sortie rédigée finale.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-143">Download or share the final redacted output asset.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="d6a0d-145">Outil open source Azure Media Redactor Visualizer</span><span class="sxs-lookup"><span data-stu-id="d6a0d-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="d6a0d-146">Un [outil de visualisation](https://github.com/Microsoft/azure-media-redactor-visualizer) open source est conçu pour aider les développeurs commençant à utiliser le format d’annotations avec l’analyse et à l’aide de la sortie.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="d6a0d-147">Une fois le référentiel cloné, vous devrez télécharger FFMPEG à partir du [site officiel](https://ffmpeg.org/download.html) pour exécuter le projet.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="d6a0d-148">Si vous êtes un développeur tentant d’analyser les données d’annotation JSON, recherchez des exemples de code dans Models.MetaData.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="d6a0d-149">Configuration de l’outil</span><span class="sxs-lookup"><span data-stu-id="d6a0d-149">Set up the tool</span></span>

1.  <span data-ttu-id="d6a0d-150">Téléchargez et générez la solution complète.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-150">Download and build the entire solution.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="d6a0d-152">Téléchargez FFMPEG [ici](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="d6a0d-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="d6a0d-153">Ce projet a été développé à l’origine avec la version be1d324 (04-10-2016) avec une liaison statique.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="d6a0d-154">Copiez ffmpeg.exe et ffprobe.exe dans le même dossier de sortie en tant que AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="d6a0d-156">Exécutez AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="d6a0d-157">Utiliser l’outil</span><span class="sxs-lookup"><span data-stu-id="d6a0d-157">Use the tool</span></span>

1. <span data-ttu-id="d6a0d-158">Traitez votre vidéo dans votre compte Azure Media Services avec le processeur multimédia Redactor sur le mode Analyse.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="d6a0d-159">Téléchargez le fichier vidéo d’origine et la sortie du travail Rédaction - Analyse.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="d6a0d-160">Exécutez l’application du visualiseur et choisissez les fichiers ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-160">Run the visualizer application and choose the files above.</span></span> 

    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="d6a0d-162">Affichez un aperçu de votre fichier.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-162">Preview your file.</span></span> <span data-ttu-id="d6a0d-163">Sélectionnez les faces à flouter via le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Rédaction de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="d6a0d-165">Le champ de texte en bas est mis à jour avec les ID de face.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="d6a0d-166">Créez un fichier appelé « idlist.txt » avec ces ID sous forme de liste délimitée par un saut de ligne.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="d6a0d-167">Le fichier idlist.txt doit être enregistré au format ANSI.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="d6a0d-168">Vous pouvez utiliser le Bloc-notes pour enregistrer au format ANSI.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="d6a0d-169">Chargez ce fichier dans la ressource de sortie de l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="d6a0d-170">Chargez la vidéo d’origine également dans cette ressource et définissez-la en tant que ressource principale.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="d6a0d-171">Lancez le travail de rédaction sur cette ressource avec le mode « Rédaction » pour obtenir la vidéo rédigée finale.</span><span class="sxs-lookup"><span data-stu-id="d6a0d-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d6a0d-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6a0d-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6a0d-173">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d6a0d-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d6a0d-174">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="d6a0d-174">Related links</span></span>
[<span data-ttu-id="d6a0d-175">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="d6a0d-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d6a0d-176">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="d6a0d-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="d6a0d-177">Annonce de Face Redaction pour Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="d6a0d-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
