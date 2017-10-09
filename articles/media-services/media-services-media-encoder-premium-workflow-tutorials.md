---
title: "didacticiels de Workflow d’encodeur multimédia Premium aaaAvanced"
description: "Ce document contient des procédures pas à pas qui montrent comment tooperform avancé des tâches de Workflow d’encodeur multimédia Premium et également comment toocreate de workflows complexes avec le Concepteur de flux de travail."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="9f3b4-103">Didacticiels de workflows avancés Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="9f3b4-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="9f3b4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9f3b4-104">Overview</span></span>
<span data-ttu-id="9f3b4-105">Ce document contient des procédures pas à pas qui montrent comment les flux de travail toocustomize avec **le Concepteur de flux de travail**.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="9f3b4-106">Vous pouvez trouver hello les fichiers de flux de travail réelle [ici](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="9f3b4-107">Table des matières</span><span class="sxs-lookup"><span data-stu-id="9f3b4-107">TOC</span></span>
<span data-ttu-id="9f3b4-108">Hello rubriques suivantes est traitée :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="9f3b4-109">Encodage du fichier MXF au format MP4 à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="9f3b4-110">Démarrage d’un nouveau workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="9f3b4-111">À l’aide de hello entrée de fichier de média</span><span class="sxs-lookup"><span data-stu-id="9f3b4-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="9f3b4-112">Inspection des flux multimédias</span><span class="sxs-lookup"><span data-stu-id="9f3b4-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="9f3b4-113">Ajout d’un encodeur vidéo pour la génération de fichiers MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="9f3b4-114">Les flux de données audio encodage hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="9f3b4-115">Multiplexage des flux audio et vidéo dans un conteneur de fichiers MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="9f3b4-116">L’écriture du fichier MP4 hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="9f3b4-117">Création d’un élément multimédia Media Services à partir du fichier de sortie hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="9f3b4-118">Hello du test terminé localement les flux de travail</span><span class="sxs-lookup"><span data-stu-id="9f3b4-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="9f3b4-119">Encodage du fichier MXF en fichiers MP4 multidébit avec l’empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="9f3b4-120">Ajout d’une ou plusieurs sorties MP4 supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9f3b4-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="9f3b4-121">Noms de sortie de fichier hello configuration</span><span class="sxs-lookup"><span data-stu-id="9f3b4-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="9f3b4-122">Ajout d’une piste audio distincte</span><span class="sxs-lookup"><span data-stu-id="9f3b4-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="9f3b4-123">Ajout de hello. Fichier SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="9f3b4-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="9f3b4-124">Encodage du fichier MXF en fichiers MP4 multidébit : plan optimisé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="9f3b4-125">Tooenhance de vue d’ensemble du flux de travail</span><span class="sxs-lookup"><span data-stu-id="9f3b4-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="9f3b4-126">Conventions d’appellation de fichiers</span><span class="sxs-lookup"><span data-stu-id="9f3b4-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="9f3b4-127">Propriétés du composant de publication sur la racine du flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="9f3b4-128">Utilisation des valeurs de propriété publiées pour les noms de fichiers de sortie générés</span><span class="sxs-lookup"><span data-stu-id="9f3b4-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="9f3b4-129">Ajout d’une sortie de miniatures toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="9f3b4-130">Flux de travail vue d’ensemble tooadd miniatures</span><span class="sxs-lookup"><span data-stu-id="9f3b4-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="9f3b4-131">Ajout d’un encodage JPG</span><span class="sxs-lookup"><span data-stu-id="9f3b4-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="9f3b4-132">Conversion de l’espace colorimétrique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="9f3b4-133">Miniatures de hello en écriture</span><span class="sxs-lookup"><span data-stu-id="9f3b4-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="9f3b4-134">Détection des erreurs dans un workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="9f3b4-135">Worflow terminé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="9f3b4-136">Découpage temporel du fichier de sortie MP4 multidébit</span><span class="sxs-lookup"><span data-stu-id="9f3b4-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="9f3b4-137">Toostart de vue d’ensemble du flux de travail ajout d’ajustement</span><span class="sxs-lookup"><span data-stu-id="9f3b4-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="9f3b4-138">À l’aide de hello découpage de flux de données</span><span class="sxs-lookup"><span data-stu-id="9f3b4-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="9f3b4-139">Worflow terminé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="9f3b4-140">Présentation de hello composant de script</span><span class="sxs-lookup"><span data-stu-id="9f3b4-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="9f3b4-141">Écriture de scripts dans un workflow : Hello World</span><span class="sxs-lookup"><span data-stu-id="9f3b4-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="9f3b4-142">Découpage par images du fichier de sortie MP4 multidébit</span><span class="sxs-lookup"><span data-stu-id="9f3b4-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="9f3b4-143">Géomètre toostart vue d’ensemble Ajout d’ajustement</span><span class="sxs-lookup"><span data-stu-id="9f3b4-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="9f3b4-144">À l’aide de hello XML de liste de découpage</span><span class="sxs-lookup"><span data-stu-id="9f3b4-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="9f3b4-145">Modification de la liste de découpage hello à partir d’un composant de script</span><span class="sxs-lookup"><span data-stu-id="9f3b4-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="9f3b4-146">Ajout d’une propriété de commodité ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="9f3b4-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="9f3b4-147"><a id="MXF_to_MP4"></a>Encodage du fichier MXF au format MP4 à débit binaire unique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="9f3b4-148">Dans cette procédure pas à pas, nous allons créer un fichier .MP4 à débit binaire unique avec des données audio encodées en AAC-HE à partir d’un fichier d’entrée .MXF.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="9f3b4-149"><a id="MXF_to_MP4_start_new"></a>Démarrage d’un nouveau workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="9f3b4-150">Ouvrez Workflow Designer et sélectionnez « Fichier » > « Nouvel espace de travail » > « Plan de transcodage ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="9f3b4-151">nouveau flux de travail Hello affiche les 3 éléments :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="9f3b4-152">Fichier source principal</span><span class="sxs-lookup"><span data-stu-id="9f3b4-152">Primary Source File</span></span>
* <span data-ttu-id="9f3b4-153">Fichier XML de liste de séquences</span><span class="sxs-lookup"><span data-stu-id="9f3b4-153">Clip List XML</span></span>
* <span data-ttu-id="9f3b4-154">Fichier/élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="9f3b4-154">Output File/Asset</span></span>  

![Nouveau workflow d’encodage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="9f3b4-156">*Nouveau workflow d’encodage*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="9f3b4-157"><a id="MXF_to_MP4_with_file_input"></a>À l’aide de hello entrée de fichier de média</span><span class="sxs-lookup"><span data-stu-id="9f3b4-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="9f3b4-158">Dans l’ordre tooaccept notre fichier multimédia d’entrée, une commence par ajout d’un composant Media fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="9f3b4-159">tooadd un flux de travail toohello du composant, regardez dans la zone de recherche du référentiel hello et faites glisser d’entrée de hello souhaité sur le volet de concepteur hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="9f3b4-160">Cela pour hello Media fichier d’entrée et se connecter hello fichier Source principal composant toohello nom de fichier d’entrée code confidentiel de hello Media fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![Composant Media File Input connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="9f3b4-162">*Composant Media File Input connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-162">*Connected Media File Input*</span></span>

<span data-ttu-id="9f3b4-163">Avant que nous pouvons faire beaucoup d’autres, nous aurons besoin tout d’abord le fichier d’exemple aux tooindicate le Concepteur de flux de travail toohello nous aimerions toouse toodesign avec notre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="9f3b4-164">toodo par conséquent, cliquez sur arrière-plan du volet de concepteur hello et rechercher pour la propriété du fichier Source principal hello sur le volet de droite propriété hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="9f3b4-165">Cliquez sur icône du dossier hello et flux de travail hello hello sélectionnez souhaité pour fichier tootest avec.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="9f3b4-166">Dès que cette opération est effectuée, composant de support, fichier d’entrée hello inspecter le fichier de hello et renseigner ses broches de sortie tooreflect fichier hello qu'il inspecté.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![Composant Media File Input renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="9f3b4-168">*Composant Media File Input renseigné*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-168">*Populated Media File Input*</span></span>

<span data-ttu-id="9f3b4-169">Alors que cela spécifie avec le type de données, nous souhaiterions toowork avec, il n’indique pas encore où doit atteindre la sortie de hello encodé.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="9f3b4-170">Similaire hello toohow principal fichier Source a été configuré, à présent configurer hello propriété de la Variable de dossier de sortie, juste en dessous.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![Propriétés d’entrée et de sortie configurées](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="9f3b4-172">*Propriétés d’entrée et de sortie configurées*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="9f3b4-173"><a id="MXF_to_MP4_streams"></a>Inspection des flux multimédias</span><span class="sxs-lookup"><span data-stu-id="9f3b4-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="9f3b4-174">Souvent, il est souhaité tooknow aspect que des flux de données hello transite par le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="9f3b4-175">tooinspect un flux de données à tout moment dans le flux de travail hello, cliquez simplement sur une sortie ou une broche d’entrée sur un des composants de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="9f3b4-176">Dans ce cas, essayez de cliquer sur une broche de sortie hello vidéo non compressé à partir de notre fichier multimédia d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="9f3b4-177">Une boîte de dialogue s’ouvre et permet la vidéo de tooinspect hello sortant.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![Broche de sortie de l’inspection hello vidéo non compressé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="9f3b4-179">*Broche de sortie de l’inspection hello vidéo non compressé*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="9f3b4-180">Dans notre cas, nous savons par exemple que nous avons affaire à une entrée 1920 x 1080 à 24 images par seconde en échantillonnage 4:2:2 pour une vidéo d’un peu moins de 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="9f3b4-181"><a id="MXF_to_MP4_file_generation"></a>Ajout d’un encodeur vidéo pour la génération de fichiers MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="9f3b4-182">Notez que notre composant Media File Input comporte maintenant une broche de sortie Uncompressed Video et plusieurs broches de sortie Uncompressed Audio.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="9f3b4-183">Dans l’ordre tooencode hello vidéo entrant, nous avons besoin d’un composant de codage - dans ce cas pour la génération. Fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="9f3b4-184">tooencode hello tooH.264 de flux vidéo, ajouter l’aire du Concepteur de composant toohello encodeur de vidéo AVC hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="9f3b4-185">Ce composant utilise un flux vidéo non compressé comme entrée et génère un flux vidéo AVC compressé sur sa broche de sortie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![Encodeur AVC non connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="9f3b4-187">*Encodeur AVC non connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="9f3b4-188">Ses propriétés déterminent comment l’encodage hello exactement.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="9f3b4-189">Nous allons avoir un aperçu des hello plus importants :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="9f3b4-190">Largeur de sortie et la hauteur de la sortie : ils déterminent la résolution de la vidéo de hello encodé hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="9f3b4-191">Dans le cas présent, partons sur une résolution de 640 x 360.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="9f3b4-192">Fréquence d’images : lorsque toopassthrough ensemble il sera juste adoptent la fréquence d’images source hello, il est possible toooverride comme vous le voyez.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="9f3b4-193">Notez que cette conversion de fréquence d’images n’est pas compensée en mouvement.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="9f3b4-194">Niveau et un profil : ils déterminent le profil de hello AVC et le niveau.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="9f3b4-195">tooconveniently obtenir plus d’informations sur les différents niveaux de hello et les profils, cliquez sur icône du point d’interrogation hello sur le composant d’encodeur de vidéo AVC hello et la page d’aide hello affiche plus de détails sur chacun des niveaux de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="9f3b4-196">Pour notre exemple, passons avec profil principal au niveau 3.2 (valeur par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="9f3b4-197">Mode de contrôle du débit et débit binaire (kbit/s) : dans notre scénario, nous allons opter pour un débit binaire constant (CBR) à 1 200 kbit/s.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="9f3b4-198">Format vidéo : il s’agit sur hello VUI (informations sur la facilité d’utilisation vidéo) qui est écrites dans le flux de données hello H.264 (informations côté qui peuvent être utilisées par un affichage de décodeur tooenhance hello, mais non essentiel toocorrectly décoder) :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="9f3b4-199">NTSC (standard aux États-Unis ou au Japon, avec un débit de 30 images par seconde)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="9f3b4-200">PAL (standard en Europe, avec un débit de 25 images par seconde)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="9f3b4-201">Mode de taille de groupe d’images : nous allons ici configurer une taille de groupe d’images fixe avec un intervalle de clé de 2 secondes et des groupes d’images fermés.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="9f3b4-202">Cela garantit la compatibilité avec hello qu'empaquetage dynamique Azure Media Services fournit.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="9f3b4-203">toofeed notre encodeur AVC, source broche de sortie vidéo non compressé hello hello Media fichier d’entrée composant toohello vidéo non compressé broche d’entrée à partir de l’encodeur de hello AVC.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![Encodeur AVC connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="9f3b4-205">*Encodeur AVC principal connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="9f3b4-206"><a id="MXF_to_MP4_audio"></a>Les flux de données audio encodage hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="9f3b4-207">À ce stade, nous avons codées vidéo mais hello le flux audio non compressé d’origine doit toujours toobe compressé.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="9f3b4-208">Pour cela, nous allons passer avec AAC codage par hello composant AAC encodeur (Dolby).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="9f3b4-209">Ajouter toohello le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-209">Add it toohello workflow.</span></span>

![Encodeur AVC non connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="9f3b4-211">*Encodeur AAC non connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="9f3b4-212">Maintenant il existe une incompatibilité : il est uniquement une seule non compressée audio broche d’entrée à partir de hello AAC encodeur lors de la plus probable hello fichier d’entrée de support dispose de deux différents décompressé flux audio disponible : un pour hello gauche du canal et l’autre pour hello Oui.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="9f3b4-213">(soit 6 canaux dans le cas d’un son surround). Il est donc pas possible toodirectly Branchez audio de hello à partir de la source d’entrée de fichier de média hello encodeur audio AAC de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="9f3b4-214">composant AAC Hello attend un flux audio « entrelacé » soi-disant : un flux unique qui possède ces deux hello canaux gauche et hello droite entrelacés avec eux.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="9f3b4-215">Une fois que nous savons à partir de notre fichier du média source les pistes audio sur quelle position dans la source de hello, nous pouvons générer correctement ce flux audio entrelacé avec hello assignés positions haut-parleur de gauche et droite.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="9f3b4-216">Tout d’abord un pouvez toogenerated un flux entrelacé de canaux audio de sources hello requis.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="9f3b4-217">composant d’ENTRELACEUR de flux Audio Hello gère cela pour nous.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="9f3b4-218">Ajouter des flux de travail toohello et connecter les sorties audio hello de hello entrée de fichier de média dans ce.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![Composant Audio Stream Interleaver connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="9f3b4-220">*Composant Audio Stream Interleaver connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="9f3b4-221">Maintenant que nous avons un flux audio entrelacé, nous n’a pas spécifier où les haut-parleurs tooassign hello gauche ou droite de positions.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="9f3b4-222">Dans commande toospecify cela, nous pouvons exploiter hello haut-parleur de la Position assigne.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![Ajout d’un composant Speaker Position Assigner](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="9f3b4-224">*Ajout d’un composant Speaker Position Assigner*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="9f3b4-225">Configurer hello haut-parleur de la Position assigne pour une utilisation avec un flux d’entrée stéréo via un filtre de présélection d’encodeur de « Custom » et hello canal prédéfini appelé « 2.0 (L, R) ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="9f3b4-226">(Cela permet d’affecter hello haut-parleur gauche position toochannel 1 et hello haut-parleur droit position toochannel 2.)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="9f3b4-227">Connectez sortie hello d’entrée de toohello hello haut-parleur de la Position assigne de hello AAC encodeur.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="9f3b4-228">Ensuite, indiquez toowork de AAC encodeur hello avec un « 2.0 (L, R) » prédéfini de canal, afin qu’il sache toodeal avec audio stéréo en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="9f3b4-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexage des flux audio et vidéo dans un conteneur de fichiers MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="9f3b4-230">Nous pouvons maintenant capturer notre flux vidéo encodé en AVC et notre flux audio encodé en AAC dans un conteneur de fichiers .MP4.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="9f3b4-231">processus de Hello de mélange de différents flux en un seul est appelé « multiplexage » (ou « muxing »).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="9f3b4-232">Dans ce cas, nous allons entrelacement hello flux audio et hello vidéo dans une seule cohérente. Package de fichiers MP4.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="9f3b4-233">composant Hello qui coordonne d’un. MP4 conteneur est appelé hello multiplexeur ISO MPEG-4.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="9f3b4-234">Ajouter une aire du concepteur toohello et connecter hello AVC vidéo encodeur et entrées de tooits AAC encodeur hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![Multiplexeur MPEG4 connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="9f3b4-236">*Multiplexeur MPEG4 connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="9f3b4-237"><a id="MXF_to_MP4_writing_mp4"></a>L’écriture du fichier MP4 hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="9f3b4-238">Lorsque vous écrivez un fichier de sortie, le composant de sortie du fichier hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="9f3b4-239">Nous pouvons nous connecter cette sortie toohello Hello multiplexeur ISO MPEG-4, afin que sa sortie obtient écrit toodisk.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="9f3b4-240">toodo, connecter hello conteneur (MPEG-4) sortie pin toohello écriture broche d’entrée de fichier de sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![Composant File Output connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="9f3b4-242">*Composant File Output connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-242">*Connected File Output*</span></span>

<span data-ttu-id="9f3b4-243">Hello de nom de fichier qui sera utilisé est déterminé par hello propriété de fichier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="9f3b4-244">Si cette propriété peut être codé en dur les tooa valeur donnée, probablement un souhaiteront tooset par le biais d’une expression à la place.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="9f3b4-245">flux de travail toohave hello déterminer automatiquement la sortie de hello propriété à partir d’une expression de nom de fichier, cliquez sur le nom de fichier hello bouton suivant toohello (icône de dossier suivant toohello).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="9f3b4-246">À partir de hello menu déroulant, puis sélectionnez « Expression ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="9f3b4-247">Éditeur d’expression hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="9f3b4-248">Effacer tout d’abord le contenu de hello de l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-248">Clear hello contents of hello editor first.</span></span>

![Éditeur d’expressions vide](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="9f3b4-250">*Éditeur d’expressions vide*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="9f3b4-251">Éditeur d’expression Hello permet tooenter toute valeur littérale, combiné avec une ou plusieurs variables.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="9f3b4-252">Les variables commencent par le symbole de dollar.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="9f3b4-253">Lorsque vous atteignez la clé de $ hello, éditeur de hello affiche une zone de liste déroulante avec un choix de variables disponibles.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="9f3b4-254">Dans le cas présent, nous allons utiliser une combinaison de variable de répertoire de sortie hello et variable de nom de fichier d’entrée de base hello :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Éditeur d’expressions renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="9f3b4-256">*Éditeur d’expressions renseigné*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="9f3b4-257">Dans l’ordre toosee voir un fichier de sortie de votre travail d’encodage dans Azure, vous devez fournir une valeur dans l’éditeur d’expression hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="9f3b4-258">Lorsque vous confirmez l’expression de hello en appuyant sur OK, fenêtre des propriétés hello aperçu toowhat valeur hello fichier propriété résout à ce stade.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![L’expression du fichier résout le répertoire de sortie](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="9f3b4-260">*L’expression du fichier résout le répertoire de sortie*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="9f3b4-261"><a id="MXF_to_MP4_asset_from_output"></a>Création d’un élément multimédia Media Services à partir du fichier de sortie hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="9f3b4-262">Pendant que nous avons écrit un fichier de sortie MP4, nous devons encore tooindicate que ce fichier appartienne toohello de sortie actif, les services de support générera suite à l’exécution de ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="9f3b4-263">fin de toothis, nœud d’élément multimédia sortie fichier hello sur le canevas de flux de travail hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="9f3b4-264">Tous les fichiers entrants dans ce nœud fera partie d’actifs d’Azure Media Services qui en résulte hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="9f3b4-265">Se connecter hello sortie du fichier composant toohello fichier/élément multimédia de sortie composant toofinish hello du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![Worflow terminé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="9f3b4-267">*Worflow terminé*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-267">*Finished Workflow*</span></span>

### <span data-ttu-id="9f3b4-268"><a id="MXF_to_MP4_test"></a>Hello du test terminé localement les flux de travail</span><span class="sxs-lookup"><span data-stu-id="9f3b4-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="9f3b4-269">tootest hello flux de travail local, d’accès au bouton de lecture hello dans la barre d’outils hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="9f3b4-270">Lorsque le flux de travail hello terminé son exécution, inspecter la sortie hello généré dans le dossier de sortie hello configuré.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="9f3b4-271">Vous verrez hello fin de fichier de sortie MP4 qui a été encodée à partir des fichiers de source d’entrée MXF hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="9f3b4-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encodage du fichier MXF en fichiers MP4 multidébit avec l’empaquetage dynamique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="9f3b4-273">Dans cette procédure pas à pas, nous allons créer un ensemble de fichiers .MP4 multidébit avec un flux audio encodé en AAC à partir d’un seul fichier d’entrée .MXF.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="9f3b4-274">Quand une sortie d’élément multimédia débits est souhaitée pour une utilisation en association avec les fonctionnalités d’empaquetage dynamique hello offertes par Azure Media Services, plusieurs fichiers MP4 alignés GOP de chacun une autre vitesse de transmission et la résolution devez toobe généré.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="9f3b4-275">toodo hello donc [MXF de codage dans une vitesse de transmission unique MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) procédure pas à pas fournit un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![Démarrage du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="9f3b4-277">*Démarrage du workflow*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-277">*Starting Workflow*</span></span>

### <span data-ttu-id="9f3b4-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Ajout d’une ou plusieurs sorties MP4 supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9f3b4-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="9f3b4-279">Chaque fichier MP4 contenu dans l’élément multimédia Azure Media Services que nous avons généré prendra en charge des valeurs de débit binaire et de résolution différentes.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="9f3b4-280">Vous allez ajouter un ou plusieurs fichiers MP4 sortie fichiers toohello du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="9f3b4-281">toomake que nous avons tous nos encodeurs vidéos créés avec hello les mêmes paramètres, ses tooduplicate mieux hello d’encodeur vidéo AVC déjà existants et configurer une autre combinaison de résolution et de la vitesse de transmission (nous allons ajouter l’un de 960 x 540 à 25 images par seconde à 2,5 Mbits/s).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="9f3b4-282">tooduplicate d’encodeur existants hello, copier et coller il sur l’aire du concepteur hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="9f3b4-283">Connexion de la broche de sortie vidéo non compressé hello Hello entrée de fichier de média dans notre nouveau composant AVC.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![Deuxième encodeur AVC connecté](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="9f3b4-285">*Deuxième encodeur AVC connecté*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="9f3b4-286">Maintenant adapter configuration hello pour notre toooutput encodeur de nouveau AVC 960 x 540 à Mbits/s 2,5.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="9f3b4-287">(Pour cela, utilisez les propriétés « largeur de sortie », « hauteur de sortie » et « débit binaire (Kbit/s) »).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="9f3b4-288">Fonction nous souhaitons asset résultant de hello toouse avec mise en package dynamique Azure Media Services, hello point de terminaison de diffusion en continu doit toobe capable de générer à partir de ces fichiers MP4 des fragments de TLS/fragmenté MP4/DASH qui sont exactement aligné tooeach autre de façon que les clients qui sont de commutation entre différents débits binaires obtiennent une seule expérience sans heurts continue audio et vidéo.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="9f3b4-289">toomake qui se produisent, nous devons tooensure que, dans les propriétés des deux encodeurs AVC hello hello taille GOP (« groupe d’images ») pour les deux fichiers MP4 a la valeur too2 secondes, ce qui peuvent être effectuées par :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="9f3b4-290">définir la taille de GOP hello Mode de dimensionnement GOP tooFixed et</span><span class="sxs-lookup"><span data-stu-id="9f3b4-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="9f3b4-291">Hello Key Frame intervalle tootwo en secondes.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="9f3b4-292">également définir hello GOP IDR contrôle tooClosed GOP tooensure tous les GOP est permanent sur leurs propres sans dépendances</span><span class="sxs-lookup"><span data-stu-id="9f3b4-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="9f3b4-293">toomake notre toounderstand pratique de flux de travail, renommer les encodeur AVC première hello trop « encodeur de vidéo AVC 640 x 360 Kbits/s 1200 » et hello deuxième encodeur de AVC » l’encodeur vidéo AVC 960 x 540 Kbits/s 2500 ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="9f3b4-294">Ajoutez maintenant un deuxième multiplexeur ISO MPEG-4 et un deuxième composant File Output.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="9f3b4-295">Se connecter hello multiplexeur toohello nouvel AVC encodeur et assurez-vous que sa sortie est dirigée dans hello fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="9f3b4-296">Puis également vous connecter de nouveau de toohello de sortie du codeur audio AAC hello entrée de multiplexeur.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="9f3b4-297">Hello, fichier de sortie à son tour peut ensuite être tooadd de nœud de fichier/élément multimédia de sortie toohello connecté il toohello Services multimédia qui sera créé.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![Deuxièmes composants Muxer et File Output connectés](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="9f3b4-299">*Deuxièmes composants Muxer et File Output connectés*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="9f3b4-300">Pour la compatibilité avec l’empaquetage dynamique d’Azure Media Services, configurer la durée ou au nombre de tooGOP hello du multiplexeur Mode de segment et définir GOP hello par segment too1.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="9f3b4-301">(Il doit s’agir par défaut de hello).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-301">(This should be hello default.)</span></span>

![Modes bloc du multiplexeur](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="9f3b4-303">*Modes bloc du multiplexeur*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="9f3b4-304">Remarque : vous souhaiterez toorepeat ce processus pour toute vitesse de transmission et de la résolution combinaisons de toohave ajouté une sortie d’élément multimédia toohello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="9f3b4-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Noms de sortie de fichier hello configuration</span><span class="sxs-lookup"><span data-stu-id="9f3b4-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="9f3b4-306">Nous avons plus d’une ressource en sortie toohello Ajout de fichier unique.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="9f3b4-307">Cela fournit un hello vraiment besoin toomake pour chacun des hello les noms de fichiers de sortie fichiers diffèrent les uns des autres et peut-être même appliquent une convention d’affectation de noms de fichier afin qu’il devienne clair hello nom de fichier que vous avez affaire à.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="9f3b4-308">Nom de sortie de fichier peut être contrôlée par des expressions dans le Concepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="9f3b4-309">Ouvrez le volet des propriétés pour un des composants de la sortie de fichier hello hello et ouvrir l’éditeur d’expression hello pour hello propriété de fichier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="9f3b4-310">Notre premier fichier de sortie a été configuré via l’expression suivante de hello (consultez Didacticiel hello pour allant [à débit binaire unique MXF tooa MP4 sortie](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)) :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="9f3b4-311">Cela signifie que votre nom de fichier est déterminée par deux variables : hello sortie Active toowrite hello et en nom base du fichier source.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="9f3b4-312">ancienne de Hello est exposé en tant que propriété sur la racine du flux de travail hello et hello ce dernier est déterminée par les fichiers entrants hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="9f3b4-313">Notez ce répertoire de sortie hello est ce que vous utilisez pour le test local ; Cette propriété sera remplacée par le moteur de flux de travail hello lorsque le flux de travail hello est exécutée par le processeur d’un média basé sur le cloud hello dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="9f3b4-314">toogive à la fois une sortie cohérente d’affectation de noms de fichiers de notre sortie, de modification hello fichiers tout d’abord une expression d’affectation de noms à :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="9f3b4-315">et hello ensuite à :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="9f3b4-316">Exécutez un test intermédiaire exécuter toomake que les deux fichiers de sortie MP4 sont correctement générés.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="9f3b4-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Ajout d’une piste audio distincte</span><span class="sxs-lookup"><span data-stu-id="9f3b4-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="9f3b4-318">Comme nous verrons plus tard lorsque nous générons une toogo de fichier .ism avec ses fichiers de sortie MP4, nous doit disposer d’un fichier MP4 audio uniquement en tant que piste audio de hello notre diffusion adaptative en continu.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="9f3b4-319">toocreate ce fichier, ajouter un flux de travail supplémentaires muxer toohello (multiplexeur ISO-MPEG-4) et se connecter broche de sortie de l’encodeur hello AAC avec son code confidentiel d’entrée pour la piste 1.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![Ajout du multiplexeur audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="9f3b4-321">*Ajout du multiplexeur audio*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="9f3b4-322">Créer un troisième fichier composant toooutput hello sortant le flux de sortie à partir de hello muxer et configurer l’expression d’affectation de noms de fichier hello en tant que :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Création du composant File Output par le multiplexeur audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="9f3b4-324">*Création du composant File Output par le multiplexeur audio*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="9f3b4-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Ajout de hello. Fichier SMIL ISM</span><span class="sxs-lookup"><span data-stu-id="9f3b4-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="9f3b4-326">Pour toowork d’empaquetage dynamique hello en combinaison avec les deux fichiers MP4 les fichiers (et hello MP4 audio uniquement) dans notre élément multimédia Media Services, nous devons également un fichier manifeste (également appelé fichier de « SMIL » : synchronisé Multimedia Integration Language).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="9f3b4-327">Ce fichier indique tooAzure Media Services quels fichiers MP4 sont disponibles pour l’empaquetage dynamique et de ces tooconsider pour la diffusion audio hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="9f3b4-328">Le fichier manifeste associé à un ensemble de fichiers MP4 à un seul flux audio se présente généralement comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="9f3b4-329">fichier .ism de Hello contient au sein d’une instruction switch, un tooeach de référence de hello MP4 vidéo des fichiers individuels, et en outre les fichiers audio toothose également un (ou plus) fait référence à tooan MP4 contenant uniquement des données audio de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="9f3b4-330">Génération du fichier manifeste hello pour notre ensemble de MP4 est possible via un composant appelé hello « AMS manifeste Writer ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="9f3b4-331">toouse, faites glisser sur l’aire de hello et connecter hello broches de sortie « Écriture terminée » à partir de toohello de composants de la sortie de fichier trois hello Writer de manifeste AMS d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="9f3b4-332">Vérifiez que sortie de hello tooconnect de hello Writer de manifeste AMS toohello fichier/élément multimédia de sortie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="9f3b4-333">Comme avec nos autres composants de sortie de fichier, configurez hello nom de sortie du fichier .ism avec une expression :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="9f3b4-334">Notre flux de travail terminé ressemble à hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-334">Our finished workflow looks like hello below:</span></span>

![Flux de travail MP4 terminé MXF toomultibitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="9f3b4-336">*Flux de travail MP4 terminé MXF toomultibitrate*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="9f3b4-337"><a id="MXF_to__multibitrate_MP4"></a>Encodage du fichier MXF en fichiers MP4 multidébit : plan optimisé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="9f3b4-338">Bonjour [procédure pas à pas de flux de travail précédent](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) nous l’avons vu comment un élément multimédia d’entrée unique MXF peut être converti en un élément multimédia de sortie avec des fichiers MP4 à plusieurs débits, un fichier MP4 audio uniquement et un fichier manifest à utiliser conjointement avec Azure Media Services d’empaquetage dynamique.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="9f3b4-339">Cette procédure pas à pas affiche comment certaines des aspects de hello peuvent être améliorés et rendue plus pratique.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="9f3b4-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de vue d’ensemble du flux de travail</span><span class="sxs-lookup"><span data-stu-id="9f3b4-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![Tooenhance du flux de travail Multibitrate MP4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="9f3b4-342">*Tooenhance du flux de travail Multibitrate MP4*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="9f3b4-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>Conventions d’appellation de fichiers</span><span class="sxs-lookup"><span data-stu-id="9f3b4-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="9f3b4-344">Dans le flux de travail précédent hello que nous avons spécifié une expression simple en tant que base de hello pour générer les noms de fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="9f3b4-345">Nous avons des valeurs en double si : tous les composants de fichier de sortie individuelle de hello hello telle expression spécifiée.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="9f3b4-346">Par exemple, notre composant de sortie de fichier pour le premier fichier de vidéo hello est configuré avec cette expression :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="9f3b4-347">Pour la sortie de la deuxième de hello vidéo, nous disposons d’une expression telle que :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="9f3b4-348">Pourquoi ne pas rendre tout cela plus clair, juste et pratique en évitant ces doublons et en renforçant les possibilités de configuration ?</span><span class="sxs-lookup"><span data-stu-id="9f3b4-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="9f3b4-349">Heureusement, nous pouvons : les fonctionnalités d’expression du concepteur hello en association avec les propriétés personnalisées de toocreate possibilité hello sur notre racine du flux de travail donne une couche supplémentaire de commodité.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="9f3b4-350">Supposons que nous allons lecteur configuration du nom de fichier à partir de débits binaires de hello de fichiers MP4 hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="9f3b4-351">Ces débits binaires que nous allons visent tooconfigure dans un centre placer (sur hello racine notre graphique), à partir d’où ils seront d’accès tooconfigure et lecteur nom génération du fichier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="9f3b4-352">toodo, nous allons commencer par la propriété de vitesse de transmission hello à partir de deux racine AVC encodeurs toohello notre flux de travail, de publication pour qu’elle devienne accessible depuis les deux racine hello ainsi que les encodeurs hello AVC.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="9f3b4-353">(même si cette propriété s’affiche à deux endroits différents, il n’y a qu’une seule valeur sous-jacente).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="9f3b4-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Propriétés du composant de publication sur la racine du flux de travail hello</span><span class="sxs-lookup"><span data-stu-id="9f3b4-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="9f3b4-355">Ouvrir les encodeur AVC première hello, atteindre la propriété de débit binaire (Kbits/s) toohello et à partir de la liste déroulante de hello choisissez Publier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![Propriété de vitesse de transmission hello publication](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="9f3b4-357">*Propriété de vitesse de transmission hello publication*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="9f3b4-358">Configurer hello publier la boîte de dialogue toopublish toohello racine de notre graphique de flux de travail, avec un nom publié de « video1bitrate » et un nom complet explicite de « Vitesse de transmission vidéo 1 ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="9f3b4-359">Configurez un nom de groupe personnalisé appelé « Streaming Bitrates » et appuyez sur Publier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![Propriété de vitesse de transmission hello publication](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="9f3b4-361">*Boîte de dialogue de publication pour la propriété de débit binaire*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="9f3b4-362">Répétez ces étapes hello identiques pour la propriété de vitesse de transmission hello Hello deuxième encodeur de AVC et nommez-la « video2bitrate » avec un nom d’affichage de « Vitesse de transmission vidéo 2 », Bonjour personnalisé de groupe « Débits binaires de diffusion en continu ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="9f3b4-363">Si nous avons maintenant examiner les propriétés racine du flux de travail hello, nous allons voir notre groupe personnalisé avec hello deux propriétés publiées s’affichent.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="9f3b4-364">Les deux sont reflétant la valeur hello de leur transmission d’encodeur AVC respectif.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![Propriétés de débit binaire publiées sur la racine du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="9f3b4-366">Chaque fois que nous souhaitons tooaccess ces propriétés à partir du code ou à partir d’une expression, nous pouvons le faire comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="9f3b4-367">à partir de code inline à partir d’un composant juste sous la racine de hello : node.getPropertyAsString('.. / video1bitrate', la valeur null)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="9f3b4-368">dans une expression : ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="9f3b4-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="9f3b4-369">Nous allons terminer le groupe de « Débits binaires de diffusion en continu » hello en publiant notre bitrate piste audio sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="9f3b4-370">Dans Propriétés de hello de hello AAC encodeur, recherchez le paramètre de vitesse de transmission hello et sélectionnez Publier dans tooit suivant de liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="9f3b4-371">Publier racine toohello du graphique hello avec le nom « audio1bitrate » et afficher le nom « Vitesse de transmission Audio 1 » au sein de notre groupe personnalisé « Débits binaires de diffusion en continu ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![Boîte de dialogue de publication pour le débit audio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="9f3b4-373">*Boîte de dialogue de publication pour le débit audio*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-373">*Publishing dialog for audio bitrate*</span></span>

![Propriétés vidéo et audio générées à la racine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="9f3b4-375">*Propriétés vidéo et audio générées à la racine*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="9f3b4-376">Notez que la modification de ces trois valeurs également reconfigure et modifications hello valeurs sur les composants respectifs hello qu’ils sont liés par (et où publiées à partir de).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="9f3b4-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Utilisation des valeurs de propriété publiées pour les noms de fichiers de sortie générés</span><span class="sxs-lookup"><span data-stu-id="9f3b4-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="9f3b4-378">Au lieu de coder en dur nos noms de fichier généré, nous pouvons de maintenant modifier votre expression de nom de fichier sur chacun des toorely de composants de la sortie de fichier hello sur les propriétés de vitesse de transmission hello que nous venez de publier sur la racine du graphique hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="9f3b4-379">À partir de notre première sortie de fichier, de trouver la propriété de fichier hello et modifier l’expression hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="9f3b4-380">différents paramètres de cette expression Hello sont accessibles et entrés en appuyant sur le signe dollar de hello clavier hello tandis que dans la fenêtre d’expression hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="9f3b4-381">Un des paramètres disponibles de hello est notre propriété video1bitrate que nous avons publié précédemment.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![Accès aux paramètres dans une expression](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="9f3b4-383">*Accès aux paramètres dans une expression*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="9f3b4-384">Hello même pour la sortie de fichier hello pour notre vidéo deuxième :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="9f3b4-385">et pour la sortie du fichier audio uniquement hello :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="9f3b4-386">Si nous modifions maintenant le débit hello des hello fichiers vidéo ou audio, encodeur respectifs de hello est reconfiguré et convention de nom de fichier basé sur la vitesse de transmission hello sera honorée automatique toutes les.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="9f3b4-387"><a id="thumbnails_to__multibitrate_MP4"></a>Ajout d’une sortie de miniatures toomultibitrate MP4</span><span class="sxs-lookup"><span data-stu-id="9f3b4-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="9f3b4-388">À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner dans Ajout d’une sortie toohello de miniatures.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="9f3b4-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Flux de travail vue d’ensemble tooadd miniatures</span><span class="sxs-lookup"><span data-stu-id="9f3b4-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![Toostart de flux de travail Multibitrate MP4 à partir de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="9f3b4-391">*Toostart de flux de travail Multibitrate MP4 à partir de*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="9f3b4-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Ajout d’un encodage JPG</span><span class="sxs-lookup"><span data-stu-id="9f3b4-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="9f3b4-393">cœur de Hello de notre la génération de miniatures sera composant JPG encodeur hello toooutput en mesure des fichiers JPG.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![Encodeur JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="9f3b4-395">*Encodeur JPG*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-395">*JPG Encoder*</span></span>

<span data-ttu-id="9f3b4-396">Nous ne pouvons pas toutefois vous connecter directement notre flux vidéo non compressé à partir de hello entrée de fichier de média dans un encodeur JPG hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="9f3b4-397">Au lieu de cela, il attend toobe transmettre des frames individuels.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="9f3b4-398">Cette opération, nous pouvons faire via un composant de vidéo Frame porte hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-398">This, we can do through hello Video Frame Gate component.</span></span>

![Connexion d’un encodeur de frame porte toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="9f3b4-400">*Connexion d’un encodeur de frame porte toohello JPG*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="9f3b4-401">porte de frame Hello une seule fois chaque secondes ou les cadres autant autorise un toopass images vidéo.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="9f3b4-402">Hello hello et intervalle de décalage horaire avec lequel cela se produit est configurable dans les propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![Propriétés du composant Video Frame Gate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="9f3b4-404">*Propriétés du composant Video Frame Gate*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="9f3b4-405">Créez une miniature de chaque minute en définissant le mode de hello tooTime (secondes) et hello too60 d’intervalle.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="9f3b4-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Conversion de l’espace colorimétrique</span><span class="sxs-lookup"><span data-stu-id="9f3b4-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="9f3b4-407">Pendant qu’il peut sembler logique à la fois des codes confidentiels vidéo non compressée de la porte de frame hello et hello entrée de fichier de média peuvent maintenant être connectés, vous obtenez un avertissement si nous pour cela.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![Erreur de l’espace colorimétrique d’entrée](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="9f3b4-409">*Erreur de l’espace colorimétrique d’entrée*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-409">*Input color space error*</span></span>

<span data-ttu-id="9f3b4-410">Il s’agit, car hello dans quelle couleur informations sont représentées dans notre flux d’origine brute non compressée vidéo, en provenance de notre MXF, est différent de quel hello JPG encodeur attend.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="9f3b4-411">Plus spécifiquement, un dite « espace de couleurs » de « RVB » ou « Gris » est attendu tooflow dans.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="9f3b4-412">Cela signifie que flux vidéo entrant de ce hello vidéo Frame de porte devez toohave une conversion appliquée concernant son espace de couleurs en premier.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="9f3b4-413">Faites glisser sur hello de flux de travail hello convertisseur d’espace de couleurs - Intel et connectez-la porte de frame tooour.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![Connexion d’un convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="9f3b4-415">*Connexion d’un convertisseur d’espace colorimétrique*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="9f3b4-416">Dans la fenêtre de propriétés hello, choisissez entrée hello RVB 24 à partir de la liste de présélection hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="9f3b4-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniatures de hello en écriture</span><span class="sxs-lookup"><span data-stu-id="9f3b4-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="9f3b4-418">Différents à partir de notre vidéo MP4, hello encodeur JPG composant produira et plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="9f3b4-419">Dans toodeal d’ordre avec cette, un composant de Writer de fichier JPG scène recherche peut être utilisé : elle prend les miniatures JPG entrants hello et les écrire, chaque nom de fichier qui est suivie d’un nombre différent.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="9f3b4-420">(nombre de hello généralement indiquant hello différents/unités de secondes dans le flux hello hello miniature a été dessiné à partir de).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![Présentation de hello Writer de fichier JPG scène recherche](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="9f3b4-422">*Présentation de hello Writer de fichier JPG scène recherche*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="9f3b4-423">Configurer la propriété de chemin d’accès du dossier de sortie hello avec expression de hello : ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="9f3b4-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="9f3b4-424">et hello propriété préfixe de nom de fichier :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="9f3b4-425">préfixe de Hello déterminent comment les fichiers de miniatures hello sont nommés.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="9f3b4-426">Est le suffixe à la position d’un nombre indiquant hello du curseur dans le flux de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![Propriétés du composant Scene Search JPG File Writer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="9f3b4-428">*Propriétés du composant Scene Search JPG File Writer*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="9f3b4-429">Connectez le nœud d’élément multimédia sortie fichier hello Writer de fichier JPG scène recherche toohello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="9f3b4-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Détection des erreurs dans un workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="9f3b4-431">Se connecter entrée hello hello couleur espace convertisseur toohello brute non compressée sortie vidéo.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="9f3b4-432">Maintenant effectuer une série de flux de travail hello de tests locale.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="9f3b4-433">Il y a un flux de travail de fortes chances hello est soudainement arrêter l’exécution et indiquer avec un contour rouge sur le composant hello a rencontré une erreur :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![Erreur du convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="9f3b4-435">*Erreur du convertisseur d’espace colorimétrique*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-435">*Color Space Converter error*</span></span>

<span data-ttu-id="9f3b4-436">Cliquez sur l’icône « E » hello peu rouge dans hello coin supérieur droit de hello convertisseur d’espace de couleurs composant toosee quelle est la raison hello Échec de la tentative de codage hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![Boîte de dialogue d’erreur du convertisseur d’espace colorimétrique](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="9f3b4-438">*Boîte de dialogue d’erreur du convertisseur d’espace colorimétrique*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="9f3b4-439">Il s’avère, comme vous pouvez le voir, que rec601 toobe pour notre conversion demandée de YUV tooRGB hello entrants espace de couleurs standard pour le convertisseur d’espace de couleurs hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="9f3b4-440">Apparemment, notre flux n’indique pas qu’il s’agit de la norme rec601</span><span class="sxs-lookup"><span data-stu-id="9f3b4-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="9f3b4-441">(Rec 601 est une norme d’encodage de signaux vidéo analogiques entrelacés sous forme de vidéo numérique.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="9f3b4-442">Elle spécifie une région active couvrant 720 échantillons de luminance et 360 échantillons de chrominance par ligne.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="9f3b4-443">système de codage de couleur de Hello est appelé parade 4:2:2.)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="9f3b4-444">toofix, nous allons indiquer des métadonnées de hello de notre flux que nous manipulons rec601 contenu.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="9f3b4-445">toodo, nous allons utiliser un composant de mise à jour de Type de données vidéo, nous mettrons entre nos brut source et hello couleur espace composant de conversion.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="9f3b4-446">Cette mise à jour du type de données permet de propriétés de type pour la mise à jour manuelle de hello de certaines données vidéos.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="9f3b4-447">Configurer tooindicate un espace couleur Standard de « Rec 601 ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="9f3b4-448">Cela entraîne un flux de hello tootag hello mise à jour de Type de données vidéo avec l’espace de couleurs « Rec 601 » hello s’il y a aucun espace colorimétrique encore définie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="9f3b4-449">(Il ne remplace pas toutes les métadonnées existantes, sauf si la case à cocher du remplacement de hello a été activée.)</span><span class="sxs-lookup"><span data-stu-id="9f3b4-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![Mise à jour de couleur espace Standard sur hello mise à jour du Type de données](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="9f3b4-451">*Mise à jour de couleur espace Standard sur hello mise à jour du Type de données*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="9f3b4-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Worflow terminé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="9f3b4-453">Maintenant que notre notre flux de travail est terminé, effectuez une autre série de tests toosee s’il satisfait.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![Flux de travail terminé pour la sortie MP4 multidébit avec miniatures](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="9f3b4-455">*Flux de travail terminé pour la sortie MP4 multidébit avec miniatures*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="9f3b4-456"><a id="time_based_trim"></a>Découpage temporel du fichier de sortie MP4 multidébit</span><span class="sxs-lookup"><span data-stu-id="9f3b4-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="9f3b4-457">À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner en réduisant hello source vidéo basé sur un horodatage.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="9f3b4-458"><a id="time_based_trim_start"></a>Toostart de vue d’ensemble du flux de travail ajout d’ajustement</span><span class="sxs-lookup"><span data-stu-id="9f3b4-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![Ajustement de flux de travail tooadd de démarrage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="9f3b4-460">*Ajustement de flux de travail tooadd de démarrage*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="9f3b4-461"><a id="time_based_trim_use_stream_trimmer"></a>À l’aide de hello découpage de flux de données</span><span class="sxs-lookup"><span data-stu-id="9f3b4-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="9f3b4-462">composant de flux de données découpage Hello permet tootrim hello début et à la fin d’un flux d’entrée de base sur les informations de minutage (secondes, minutes,...). découpage de Hello ne prend pas en charge basée sur le frame de suppression.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![Composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="9f3b4-464">*Composant Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-464">*Stream Trimmer*</span></span>

<span data-ttu-id="9f3b4-465">Au lieu de lier directement les encodeurs hello AVC et haut-parleur de la position assigne toohello entrée de fichier de média, nous mettrons entre ces découpage de flux hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="9f3b4-466">(Un pour les signaux vidéo hello et pour le signal audio entrelacée de hello).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![Insertion du composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="9f3b4-468">*Insertion du composant Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="9f3b4-469">Permet de configurer le découpage de hello afin que nous traiterons uniquement vidéo et audio entre 15 et 60 secondes dans une vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="9f3b4-470">Accédez de propriétés toohello Hello découpage du flux vidéo et configurer l’heure de début (15 s) et les propriétés de l’heure de fin (60 s).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="9f3b4-471">Nous publierons toomake qu’à la fois notre découpage audio et vidéo est toujours configurée toohello même début et de fin des valeurs, ces racine toohello hello de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![Publication de la propriété d’heure de début à partir du composant Stream Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="9f3b4-473">*Publication de la propriété d’heure de début à partir du composant Stream Trimmer*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-473">*Publish start time property from Stream Trimmer*</span></span>

![Boîte de dialogue des propriétés de publication pour l’heure de début](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="9f3b4-475">*Boîte de dialogue des propriétés de publication pour l’heure de début*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-475">*Publish property dialog for start time*</span></span>

![Boîte de dialogue des propriétés de publication pour l’heure de fin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="9f3b4-477">*Boîte de dialogue des propriétés de publication pour l’heure de fin*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="9f3b4-478">Si nous avons maintenant inspecter racine hello notre flux de travail, les deux propriétés seront soigneusement affichée et peut être configuré à partir de là.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![Propriétés publiées disponibles sur la racine](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="9f3b4-480">*Propriétés publiées disponibles sur la racine*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-480">*Published properties available on root*</span></span>

<span data-ttu-id="9f3b4-481">Ouvrez les propriétés de rognage hello de découpage d’audio hello et configurer des heures de début et de fin d’une expression qui fait référence toohello publié les propriétés de la racine hello notre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="9f3b4-482">Pour l’heure de début d’ajustement audio hello :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="9f3b4-483">et pour son heure de fin :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="9f3b4-484"><a id="time_based_trim_finish"></a>Worflow terminé</span><span class="sxs-lookup"><span data-stu-id="9f3b4-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![Worflow terminé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="9f3b4-486">*Worflow terminé*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-486">*Finished Workflow*</span></span>

## <span data-ttu-id="9f3b4-487"><a id="scripting"></a>Présentation de hello composant de script</span><span class="sxs-lookup"><span data-stu-id="9f3b4-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="9f3b4-488">Les composants sous forme de script peuvent exécuter des scripts arbitraires au cours des phases d’exécution de hello de notre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="9f3b4-489">Il existe quatre différents scripts qui peuvent être exécutés, chacun avec des caractéristiques spécifiques et leur propres sur place dans le cycle de vie de workflow hello :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="9f3b4-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="9f3b4-490">**commandScript**</span></span>
* <span data-ttu-id="9f3b4-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="9f3b4-491">**realizeScript**</span></span>
* <span data-ttu-id="9f3b4-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="9f3b4-492">**processInputScript**</span></span>
* <span data-ttu-id="9f3b4-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="9f3b4-493">**lifeCycleScript**</span></span>

<span data-ttu-id="9f3b4-494">documentation Hello Hello composant de script va plus en détail pour chacun des hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="9f3b4-495">Dans [hello suivants section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** composant de script est tooconstruct utilisé un fichier xml de liste de séquences volée hello lorsque hello workflow démarre.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="9f3b4-496">Ce script est appelé lors de l’installation de composant hello, ce qui se produit une seule fois dans son cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="9f3b4-497"><a id="scripting_hello_world"></a>Écriture de scripts dans un workflow : Hello World</span><span class="sxs-lookup"><span data-stu-id="9f3b4-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="9f3b4-498">Faites glisser un composant de l’objet d’un script sur l’aire du concepteur hello et renommez-le (par exemple, « SetClipListXML »).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![Ajout d’un composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="9f3b4-500">*Ajout d’un composant de script*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="9f3b4-501">Lorsque vous examinez les propriétés hello de hello composant de script, hello quatre types différents de script seront affiche, chaque script différents tooa configurable.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriétés du composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="9f3b4-503">*Propriétés du composant de script*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-503">*Scripted Component properties*</span></span>

<span data-ttu-id="9f3b4-504">Désactivez hello processInputScript et ouvrir l’éditeur de hello pour hello realizeScript.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="9f3b4-505">Maintenant nous est configurés et prêt toostart de script.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="9f3b4-506">Les scripts sont écrits en Groovy, un langage de script compilé de manière dynamique pour la plate-forme Java hello qui conserve la compatibilité avec Java.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="9f3b4-507">En fait, la plupart des codes Java sont considérés comme du code Groovy valide.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="9f3b4-508">Nous allons écrire un script de sensationnelle simple hello world dans un contexte hello de notre realizeScript.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="9f3b4-509">Entrez les informations suivantes de hello dans l’éditeur de hello :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="9f3b4-510">Exécutez maintenant une série de tests en local.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-510">Now execute a local test run.</span></span> <span data-ttu-id="9f3b4-511">Après cette exécution, inspecter (via l’onglet système hello hello composant de script) hello propriété de journaux.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Sortie du journal Hello World](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="9f3b4-513">*Sortie du journal Hello World*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-513">*Hello world log output*</span></span>

<span data-ttu-id="9f3b4-514">objet de nœud Hello nous appeler la méthode hello du journal, fait référence tooour actuel « nœud » ou un composant hello nous mettons scripts dans.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="9f3b4-515">Ainsi, chaque composant a les données de journalisation toooutput de capacité salutation, disponibles via l’onglet système de hello. Dans ce cas, nous sortie hello littéral de chaîne « hello world ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="9f3b4-516">Toounderstand important ici est que cela peut s’avérer toobe un outil de débogage précieux, en vous fournissant des informations sur le script hello est en fait.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="9f3b4-517">À partir de dans notre environnement de script, nous avons accès tooproperties avec d’autres composants.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="9f3b4-518">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="9f3b4-519">Notre fenêtre journal permet de visualiser hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-519">Our log window will show us hello following:</span></span>

![Sortie de journal pour l’accès aux chemins du nœud](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="9f3b4-521">*Sortie de journal pour l’accès aux chemins du nœud*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="9f3b4-522"><a id="frame_based_trim"></a>Découpage par images du fichier de sortie MP4 multidébit</span><span class="sxs-lookup"><span data-stu-id="9f3b4-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="9f3b4-523">À partir d’un flux de travail qui génère [une sortie à plusieurs débits MP4 à partir d’une entrée de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), nous allons maintenant l’examiner en réduisant hello source vidéo en fonction du frame.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="9f3b4-524"><a id="frame_based_trim_start"></a>Géomètre toostart vue d’ensemble Ajout d’ajustement</span><span class="sxs-lookup"><span data-stu-id="9f3b4-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![Toostart de flux de travail ajout d’ajustement](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="9f3b4-526">*Toostart de flux de travail ajout d’ajustement*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="9f3b4-527"><a id="frame_based_trim_clip_list"></a>À l’aide de hello XML de liste de découpage</span><span class="sxs-lookup"><span data-stu-id="9f3b4-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="9f3b4-528">Dans tous les didacticiels précédents de flux de travail, nous avons utilisé le composant de fichier d’entrée de média hello en tant que source d’entrée vidéo.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="9f3b4-529">Pour ce scénario, nous utiliserons composant de Source de la liste hello à la place.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="9f3b4-530">Notez que cela ne doit pas être la méthode hello préféré de travail ; Utilisez uniquement hello Source de la liste lorsqu’il existe donc un toodo véritable raison (comme dans hello ci-dessous cas, où nous procédons à utiliser les fonctionnalités de suppression de liste de découpage hello).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="9f3b4-531">tooswitch à partir de notre toohello d’entrée de fichier de média Clip liste Source, faites glisser de composant de Source de la liste de hello sur l’aire de conception hello et se connecter hello Clip liste pin toohello Clip liste XML nœud XML du Concepteur de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="9f3b4-532">Cela doit remplir hello Source de la liste des codes confidentiels de sortie, selon la vidéo d’entrée de tooour.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="9f3b4-533">Maintenant vous connecter les broches non compressée vidéo et Audio non compressé hello de hello hello Clip liste Source toohello respectifs AVC encodeurs et ENTRELACEUR de flux Audio.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="9f3b4-534">Supprimer hello entrée de fichier de média.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-534">Now remove hello Media File Input.</span></span>

![Remplacé hello entrée de fichier de média avec hello Clip liste Source](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="9f3b4-536">*Remplacé hello entrée de fichier de média avec hello Clip liste Source*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="9f3b4-537">composant de Source de la liste Hello prend comme entrée un « XML de liste de découpage ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="9f3b4-538">Lorsque vous sélectionnez hello tootest de fichier source avec localement, ce xml de liste de découpage est rempli automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![Propriété du fichier XML de liste de séquences automatiquement renseigné](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="9f3b4-540">*Propriété du fichier XML de liste de séquences automatiquement renseigné*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="9f3b4-541">Recherchez un peu plus toohello xml, voici comment il ressemble à :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![Boîte de dialogue de modification de la liste de séquences](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="9f3b4-543">*Boîte de dialogue de modification de la liste de séquences*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="9f3b4-544">Toutefois, cela ne reflète pas les fonctions hello hello clip liste XML.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="9f3b4-545">Une option que nous avons est tooadd un élément « Trim » sous la vidéo de hello et la source de l’audio, comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![Ajout d’une liste de découpage toohello élément trim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="9f3b4-547">*Ajout d’une liste de découpage toohello élément trim*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="9f3b4-548">Si vous modifiez du code xml de liste de découpage hello comme ci-dessus et effectuez une série de tests locale, vous verrez la vidéo de hello été correctement supprimés entre 10 et 20 secondes dans une vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="9f3b4-549">Toowhat contraire se produit lorsque vous effectuez une exécution locale, bien que ce code xml de liste de séquences très même n’aurait pas hello même effet en cas d’application dans un flux de travail qui s’exécute dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="9f3b4-550">Lorsque Azure Premium encodeur démarre, xml de liste de séquences hello est généré chaque fois, en fonction de l’encodage du hello hello fichier d’entrée le travail a été spécifié.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="9f3b4-551">Cela signifie que toutes les modifications sur hello xml sont malheureusement substituées.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="9f3b4-552">xml de liste de séquences hello toocounter leur réinitialisation au démarrage d’une tâche de codage, nous pouvons générer de nouveau il hello volée juste après le début de hello de notre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="9f3b4-553">Ces actions personnalisées peuvent être exécutées via ce que l’on appelle un « composant de script ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="9f3b4-554">Pour plus d’informations, consultez [présentation hello composant de script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span><span class="sxs-lookup"><span data-stu-id="9f3b4-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="9f3b4-555">Faites glisser un composant de l’objet d’un script sur l’aire du concepteur hello et renommez-le trop « SetClipListXML ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![Ajout d’un composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="9f3b4-557">*Ajout d’un composant de script*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="9f3b4-558">Lorsque vous examinez les propriétés hello de hello composant de script, hello quatre types différents de script seront affiche, chaque script différents tooa configurable.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![Propriétés du composant de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="9f3b4-560">*Propriétés du composant de script*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="9f3b4-561"><a id="frame_based_trim_modify_clip_list"></a>Modification de la liste de découpage hello à partir d’un composant de script</span><span class="sxs-lookup"><span data-stu-id="9f3b4-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="9f3b4-562">Avant que nous pouvons réécrire xml de liste de séquences de hello est généré lors du démarrage du flux de travail, nous avons besoin de contenu et la propriété xml de toohave accès toohello liste de séquences.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="9f3b4-563">Pour cela, nous pouvons procéder de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Liste de séquences entrantes consignée dans le journal](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="9f3b4-565">*Liste de séquences entrantes consignée dans le journal*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="9f3b4-566">Tout d’abord, nous devons un toodetermine moyen point à partir duquel jusqu'à quel point nous souhaitons tootrim hello vidéo.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="9f3b4-567">publication de cet utilisateur de moins technique toohello pratique de flux de travail hello, toomake racine toohello de deux propriétés de graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="9f3b4-568">toodo, cliquez avec le bouton droit sur aire du concepteur hello et sélectionnez « Ajouter une propriété » :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="9f3b4-569">Première propriété : « ClippingTimeStart » de type : « TIMECODE »</span><span class="sxs-lookup"><span data-stu-id="9f3b4-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="9f3b4-570">Deuxième propriété : « ClippingTimeEND » de type : « TIMECODE »</span><span class="sxs-lookup"><span data-stu-id="9f3b4-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![Boîte de dialogue Ajouter une propriété pour l’heure de début du découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="9f3b4-572">*Boîte de dialogue Ajouter une propriété pour l’heure de début du découpage*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-572">*Add Property dialog for clipping start time*</span></span>

![Propriétés de temps de découpage publiées sur la racine du workflow](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="9f3b4-574">*Propriétés de temps de découpage publiées sur la racine du workflow*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="9f3b4-575">Configurez les deux valeur appropriée de tooa de propriétés :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-575">Configure both properties tooa suitable value:</span></span>

![Configurer hello extrait les propriétés de début et de fin](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="9f3b4-577">*Configurer hello extrait les propriétés de début et de fin*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="9f3b4-578">À partir de dans notre script, nous pouvons désormais accéder aux deux propriétés, comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Fenêtre de journal indiquant le début et la fin du découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="9f3b4-580">*Fenêtre de journal indiquant le début et la fin du découpage*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="9f3b4-581">Nous allons analyser des chaînes de code temporel hello dans un formulaire toouse plus pratique, à l’aide d’une expression régulière simple :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Fenêtre de journal avec la sortie du code temporel analysé](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="9f3b4-583">*Fenêtre de journal avec la sortie du code temporel analysé*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="9f3b4-584">Avec ces informations à portée de main, nous pouvons maintenant modifier hello liste de séquences xml tooreflect hello et heures de fin des hello souhaité précis extrait de film de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![Éléments trim tooadd de code de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="9f3b4-586">*Éléments trim tooadd de code de script*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="9f3b4-587">Nous avons utilisé pour cela des opérations normales de manipulation de chaîne.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="9f3b4-588">xml de liste Hello obtenu image modifiée est réécrites toohello clipListXML propriété sur la racine du flux de travail hello via la méthode de « setProperty » hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="9f3b4-589">fenêtre de journal Hello après l’exécution d’un autre test nous indiquerait hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-589">hello log window after another test run would show us hello following:</span></span>

![Liste des images qui en résulte hello de journalisation](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="9f3b4-591">*Liste des images qui en résulte hello de journalisation*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="9f3b4-592">Effectuer un toosee de série de tests comment les flux vidéo et audio hello ont été réduits.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="9f3b4-593">Comme vous allez effectuer plus d’une série de tests avec des valeurs différentes pour les points de rognage hello, vous remarquerez que celles ne seront pas pris en compte toutefois !</span><span class="sxs-lookup"><span data-stu-id="9f3b4-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="9f3b4-594">raison Hello est ce concepteur hello, contrairement aux hello runtime Azure, ne pas remplacer xml de liste de séquences d’hello chaque exécution.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="9f3b4-595">Cela signifie qu’uniquement hello première fois que vous avez défini hello et l’extraction des points, cause hello xml tootransform, de tous les autres hello fois, notre clause guard (si (clipListXML.indexOf («<trim>») == -1)) empêche les flux de travail hello d’ajouter un autre découpage élément s’il existe déjà présent.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="9f3b4-596">toomake notre flux de travail pratique tootest localement, nous meilleures ajouter du code de conservation de maison qui vérifie si un élément de découpage était déjà présent.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="9f3b4-597">Dans ce cas, vous pouvez le supprimer avant de continuer en modifiant le xml hello avec de nouvelles valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="9f3b4-598">Au lieu d’utiliser des manipulations de chaîne simple, il est probablement plus sûre toodo grâce à l’objet réel xml de modèle d’analyse.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="9f3b4-599">Avant que nous pouvons ajouter ce code Cependant, nous devrons tooadd qu'un nombre d’instructions d’importation à hello démarrer d’abord de notre script :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="9f3b4-600">Après cela, nous pouvons ajouter hello requis du code de nettoyage :</span><span class="sxs-lookup"><span data-stu-id="9f3b4-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="9f3b4-601">Ce code va juste au-dessus de point hello auquel nous ajoutons hello éléments toohello liste des séquences xml.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="9f3b4-602">À ce stade, nous pouvons exécuter et modifier notre flux de travail que nous voulons que bien que les modifications de hello appliquées jamais de temps.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="9f3b4-603"><a id="frame_based_trim_clippingenabled_prop"></a>Ajout d’une propriété de commodité ClippingEnabled</span><span class="sxs-lookup"><span data-stu-id="9f3b4-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="9f3b4-604">Comme vous toujours pouvez ajustement toohappen, nous allons terminer notre flux de travail en ajoutant un pratique indicateur booléen qui indique si nous voulons tooenable trimming / extrait.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="9f3b4-605">Comme avant, publiez une nouvelle racine toohello de propriété de notre flux de travail appelé « ClippingEnabled » de type « BOOLEAN ».</span><span class="sxs-lookup"><span data-stu-id="9f3b4-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![Publication d’une propriété activant le découpage](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="9f3b4-607">*Publication d’une propriété activant le découpage*</span><span class="sxs-lookup"><span data-stu-id="9f3b4-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="9f3b4-608">Avec hello ci-dessous clause de garde simple, nous pouvons vérifier si la suppression est requise et décidez si la liste des images en tant que tel toobe modifié ou non.</span><span class="sxs-lookup"><span data-stu-id="9f3b4-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="9f3b4-609"><a id="code"></a>Code complet</span><span class="sxs-lookup"><span data-stu-id="9f3b4-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="9f3b4-610">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9f3b4-610">Also see</span></span>
[<span data-ttu-id="9f3b4-611">Présentation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9f3b4-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="9f3b4-612">Comment tooUse Premium encodage dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9f3b4-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="9f3b4-613">Encodage de contenu à la demande avec Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9f3b4-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="9f3b4-614">Codecs et formats de Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="9f3b4-615">Exemples de fichiers de workflow</span><span class="sxs-lookup"><span data-stu-id="9f3b4-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="9f3b4-616">Outil Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="9f3b4-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="9f3b4-617">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9f3b4-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9f3b4-618">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9f3b4-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
