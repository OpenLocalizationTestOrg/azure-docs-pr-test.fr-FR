---
title: "Éditer les visages avec Azure Media Analytics | Microsoft Docs"
description: "Cette rubrique illustre comment rédiger des faces avec Azure Media Analytics."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="3c08f-103">Éditer les visages avec Azure Media Analytique</span><span class="sxs-lookup"><span data-stu-id="3c08f-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="3c08f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3c08f-104">Overview</span></span>
<span data-ttu-id="3c08f-105">**Azure Media Redactor** est un processeur multimédia [Azure Media Analytics](media-services-analytics-overview.md) qui offre la rédaction de face évolutive dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="3c08f-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="3c08f-106">La rédaction de face vous permet de modifier votre vidéo afin de flouter les visages des individus sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="3c08f-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="3c08f-107">Vous souhaitez peut-être utiliser le service de rédaction de face dans des scénarios de média et de sécurité publics.</span><span class="sxs-lookup"><span data-stu-id="3c08f-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="3c08f-108">Quelques minutes de séquences vidéo contenant plusieurs visages peuvent nécessiter des heures de traitement manuel, mais avec ce service, le processus de rédaction de face ne nécessitera que quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="3c08f-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="3c08f-109">Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="3c08f-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="3c08f-110">Cette rubrique donne des informations détaillées sur **Azure Media Redactor** et illustre son utilisation avec le Kit de développement logiciel (SDK) Media Services pour .NET.</span><span class="sxs-lookup"><span data-stu-id="3c08f-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="3c08f-111">Le processeur multimédia **Azure Media Redactor** est uniquement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="3c08f-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="3c08f-112">Il est disponible dans toutes les régions Azure publiques, ainsi que dans les centres de données de Chine et du Gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="3c08f-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="3c08f-113">Cette version préliminaire est actuellement disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="3c08f-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="3c08f-114">Modes de rédaction de face</span><span class="sxs-lookup"><span data-stu-id="3c08f-114">Face redaction modes</span></span>
<span data-ttu-id="3c08f-115">La rédaction de face fonctionne en détectant les visages dans chaque image de la vidéo et en suivant l’objet de visage à la fois vers l’avant et l’arrière dans le temps, afin que la même personne puisse être floutée à partir d’autres angles également.</span><span class="sxs-lookup"><span data-stu-id="3c08f-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="3c08f-116">Le processus de rédaction automatisé est très complexe et ne produit pas toujours 100 % de la sortie souhaitée et c’est pourquoi Media Analytics vous fournit deux méthodes pour modifier la sortie finale.</span><span class="sxs-lookup"><span data-stu-id="3c08f-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="3c08f-117">Outre un mode entièrement automatique, il existe un flux de travail en deux passes qui permet la sélection/désélection des visages trouvés via une liste d’ID.</span><span class="sxs-lookup"><span data-stu-id="3c08f-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="3c08f-118">En outre, pour rendre arbitraires les réglages par image, le processeur multimédia utilise un fichier de métadonnées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="3c08f-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="3c08f-119">Ce flux de travail est divisé en modes **Analyser** et **Rédiger**.</span><span class="sxs-lookup"><span data-stu-id="3c08f-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="3c08f-120">Vous pouvez combiner les deux modes en une seule passe qui exécute les deux tâches dans un travail ; ce mode est appelé **Combiné**.</span><span class="sxs-lookup"><span data-stu-id="3c08f-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="3c08f-121">Mode Combiné</span><span class="sxs-lookup"><span data-stu-id="3c08f-121">Combined mode</span></span>
<span data-ttu-id="3c08f-122">Cela génère un mp4 rédigé automatiquement sans entrée manuelle.</span><span class="sxs-lookup"><span data-stu-id="3c08f-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="3c08f-123">Étape</span><span class="sxs-lookup"><span data-stu-id="3c08f-123">Stage</span></span> | <span data-ttu-id="3c08f-124">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="3c08f-124">File Name</span></span> | <span data-ttu-id="3c08f-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="3c08f-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c08f-126">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-126">Input asset</span></span> |<span data-ttu-id="3c08f-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="3c08f-127">foo.bar</span></span> |<span data-ttu-id="3c08f-128">Vidéo au format WMV, MOV ou MP4</span><span class="sxs-lookup"><span data-stu-id="3c08f-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="3c08f-129">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-129">Input config</span></span> |<span data-ttu-id="3c08f-130">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="3c08f-130">Job configuration preset</span></span> |<span data-ttu-id="3c08f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="3c08f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="3c08f-132">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="3c08f-132">Output asset</span></span> |<span data-ttu-id="3c08f-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="3c08f-133">foo_redacted.mp4</span></span> |<span data-ttu-id="3c08f-134">Vidéo avec flou appliqué</span><span class="sxs-lookup"><span data-stu-id="3c08f-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="3c08f-135">Exemple d’entrée :</span><span class="sxs-lookup"><span data-stu-id="3c08f-135">Input example:</span></span>
[<span data-ttu-id="3c08f-136">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="3c08f-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="3c08f-137">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="3c08f-137">Output example:</span></span>
[<span data-ttu-id="3c08f-138">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="3c08f-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="3c08f-139">Mode Analyser</span><span class="sxs-lookup"><span data-stu-id="3c08f-139">Analyze mode</span></span>
<span data-ttu-id="3c08f-140">La passe **Analyser** du flux de travail en deux passes accepte une entrée vidéo et produit un fichier JSON d’emplacements de visage et des images jpg de chaque visage détecté.</span><span class="sxs-lookup"><span data-stu-id="3c08f-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="3c08f-141">Étape</span><span class="sxs-lookup"><span data-stu-id="3c08f-141">Stage</span></span> | <span data-ttu-id="3c08f-142">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="3c08f-142">File Name</span></span> | <span data-ttu-id="3c08f-143">Remarques</span><span class="sxs-lookup"><span data-stu-id="3c08f-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c08f-144">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-144">Input asset</span></span> |<span data-ttu-id="3c08f-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="3c08f-145">foo.bar</span></span> |<span data-ttu-id="3c08f-146">Vidéo au format WMV, MPV ou MP4</span><span class="sxs-lookup"><span data-stu-id="3c08f-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="3c08f-147">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-147">Input config</span></span> |<span data-ttu-id="3c08f-148">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="3c08f-148">Job configuration preset</span></span> |<span data-ttu-id="3c08f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="3c08f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="3c08f-150">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="3c08f-150">Output asset</span></span> |<span data-ttu-id="3c08f-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="3c08f-151">foo_annotations.json</span></span> |<span data-ttu-id="3c08f-152">Données d’annotation des emplacements de visage au format JSON.</span><span class="sxs-lookup"><span data-stu-id="3c08f-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="3c08f-153">Cela peut être modifié par l’utilisateur pour changer les cadres de limitation du flou.</span><span class="sxs-lookup"><span data-stu-id="3c08f-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="3c08f-154">Voir l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3c08f-154">See sample below.</span></span> |
| <span data-ttu-id="3c08f-155">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="3c08f-155">Output asset</span></span> |<span data-ttu-id="3c08f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="3c08f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="3c08f-157">Une image jpg rognée de chaque visage détecté, où le nombre indique l’ID d’étiquette du visage</span><span class="sxs-lookup"><span data-stu-id="3c08f-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="3c08f-158">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="3c08f-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="3c08f-159">Mode Rédiger</span><span class="sxs-lookup"><span data-stu-id="3c08f-159">Redact mode</span></span>
<span data-ttu-id="3c08f-160">La deuxième passe du flux de travail prend un plus grand nombre d’entrées qui doivent être combinées en un seul élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="3c08f-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="3c08f-161">Cela inclut une liste des ID à flouter, la vidéo d’origine et les annotations JSON.</span><span class="sxs-lookup"><span data-stu-id="3c08f-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="3c08f-162">Ce mode utilise les annotations pour appliquer le flou sur la vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3c08f-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="3c08f-163">La sortie de la passe Analyser n’inclut pas la vidéo d’origine.</span><span class="sxs-lookup"><span data-stu-id="3c08f-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="3c08f-164">La vidéo doit être chargée dans l’élément multimédia d’entrée pour la tâche en mode Rédiger et sélectionnée comme fichier principal.</span><span class="sxs-lookup"><span data-stu-id="3c08f-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="3c08f-165">Étape</span><span class="sxs-lookup"><span data-stu-id="3c08f-165">Stage</span></span> | <span data-ttu-id="3c08f-166">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="3c08f-166">File Name</span></span> | <span data-ttu-id="3c08f-167">Remarques</span><span class="sxs-lookup"><span data-stu-id="3c08f-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3c08f-168">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-168">Input asset</span></span> |<span data-ttu-id="3c08f-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="3c08f-169">foo.bar</span></span> |<span data-ttu-id="3c08f-170">Vidéo au format WMV, MPV ou MP4.</span><span class="sxs-lookup"><span data-stu-id="3c08f-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="3c08f-171">Même vidéo que celle de l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="3c08f-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="3c08f-172">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-172">Input asset</span></span> |<span data-ttu-id="3c08f-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="3c08f-173">foo_annotations.json</span></span> |<span data-ttu-id="3c08f-174">Fichier de métadonnées d’annotations de la première phase, avec des modifications facultatives.</span><span class="sxs-lookup"><span data-stu-id="3c08f-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="3c08f-175">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-175">Input asset</span></span> |<span data-ttu-id="3c08f-176">foo_IDList.txt (facultatif)</span><span class="sxs-lookup"><span data-stu-id="3c08f-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="3c08f-177">Nouvelle liste facultative séparée par des lignes des ID de visage à traiter.</span><span class="sxs-lookup"><span data-stu-id="3c08f-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="3c08f-178">Si ce champ est laissé vide, tous les visages sont floutés.</span><span class="sxs-lookup"><span data-stu-id="3c08f-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="3c08f-179">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="3c08f-179">Input config</span></span> |<span data-ttu-id="3c08f-180">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="3c08f-180">Job configuration preset</span></span> |<span data-ttu-id="3c08f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="3c08f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="3c08f-182">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="3c08f-182">Output asset</span></span> |<span data-ttu-id="3c08f-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="3c08f-183">foo_redacted.mp4</span></span> |<span data-ttu-id="3c08f-184">Vidéo avec flou appliqué en fonction des annotations</span><span class="sxs-lookup"><span data-stu-id="3c08f-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="3c08f-185">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="3c08f-185">Example output</span></span>
<span data-ttu-id="3c08f-186">Il s’agit de la sortie à partir d’une liste d’ID avec un ID sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3c08f-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="3c08f-187">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="3c08f-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="3c08f-188">Exemple : foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="3c08f-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="3c08f-189">Types de flou</span><span class="sxs-lookup"><span data-stu-id="3c08f-189">Blur types</span></span>

<span data-ttu-id="3c08f-190">Dans le mode **Combiné** ou **Rédiger**, 5 modes de flou sont disponibles par le biais de la configuration d’entrée JSON : **Faible**, **Med** (Moyen), **Élevé**, **Débogage** et **Noir**.</span><span class="sxs-lookup"><span data-stu-id="3c08f-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="3c08f-191">Par défaut, **Med** (Moyen) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3c08f-191">By default **Med** is used.</span></span>

<span data-ttu-id="3c08f-192">Vous trouverez des exemples de types de flou ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3c08f-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="3c08f-193">Exemple JSON :</span><span class="sxs-lookup"><span data-stu-id="3c08f-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="3c08f-194">Faible</span><span class="sxs-lookup"><span data-stu-id="3c08f-194">Low</span></span>

![Faible](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="3c08f-196">Med (Moyen)</span><span class="sxs-lookup"><span data-stu-id="3c08f-196">Med</span></span>

![Med (Moyen)](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="3c08f-198">Élevé</span><span class="sxs-lookup"><span data-stu-id="3c08f-198">High</span></span>

![Élevé](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="3c08f-200">Déboguer</span><span class="sxs-lookup"><span data-stu-id="3c08f-200">Debug</span></span>

![Déboguer](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="3c08f-202">Noir</span><span class="sxs-lookup"><span data-stu-id="3c08f-202">Black</span></span>

![Noir](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="3c08f-204">Éléments du fichier de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="3c08f-204">Elements of the output JSON file</span></span>

<span data-ttu-id="3c08f-205">Le processeur multimédia de rédaction permet une détection d’emplacement et un suivi de visage très précis ; il peut détecter jusqu’à 64 visages humains dans une séquence vidéo.</span><span class="sxs-lookup"><span data-stu-id="3c08f-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="3c08f-206">Les visages filmés de face donnent les meilleurs résultats ; les visages filmés de côté ou les visages de taille réduite (24 x 24 pixels ou moins) posent plus de problèmes.</span><span class="sxs-lookup"><span data-stu-id="3c08f-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="3c08f-207">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="3c08f-207">.NET sample code</span></span>

<span data-ttu-id="3c08f-208">Le programme suivant montre comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="3c08f-208">The following program shows how to:</span></span>

1. <span data-ttu-id="3c08f-209">Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="3c08f-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="3c08f-210">Créer un travail avec une tâche de rédaction de face basée sur un fichier de configuration qui contient la présélection JSON suivante.</span><span class="sxs-lookup"><span data-stu-id="3c08f-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="3c08f-211">Télécharger les fichiers JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="3c08f-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3c08f-212">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c08f-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3c08f-213">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3c08f-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="3c08f-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="3c08f-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use the following event handler to check job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch the job.
            job.Submit();

            // Check job execution and wait for job to finish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, the event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

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

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="3c08f-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c08f-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3c08f-216">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3c08f-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="3c08f-217">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="3c08f-217">Related links</span></span>
[<span data-ttu-id="3c08f-218">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="3c08f-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="3c08f-219">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="3c08f-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

