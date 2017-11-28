---
title: faces aaaRedact avec Azure Media Analytique | Documents Microsoft
description: "Cette rubrique montre comment tooredact fait face avec analytique d’Azure media."
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
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="61ab6-103">Éditer les visages avec Azure Media Analytique</span><span class="sxs-lookup"><span data-stu-id="61ab6-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="61ab6-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="61ab6-104">Overview</span></span>
<span data-ttu-id="61ab6-105">**Azure Media Redactor** est un [Azure Media Analytique](media-services-analytics-overview.md) processeur multimédia (MP) qui offre la rédaction de face évolutives dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="61ab6-106">Rédaction de face permet de vous toomodify votre vidéo dans faces de tooblur d’ordre d’individus sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="61ab6-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="61ab6-107">Vous pouvez choisir de service de rédaction face toouse hello dans les scénarios de sécurité et de médias public.</span><span class="sxs-lookup"><span data-stu-id="61ab6-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="61ab6-108">Quelques minutes de film qui contient plusieurs polices peuvent prendre des heures tooredact manuellement, mais avec cette face hello de service des processus de rédaction nécessite quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="61ab6-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="61ab6-109">Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="61ab6-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="61ab6-110">Cette rubrique fournit des détails sur **Azure Media Redactor** et montre comment toouse avec Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="61ab6-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="61ab6-111">Hello **Azure Media Redactor** Pack d’administration est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="61ab6-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="61ab6-112">Il est disponible dans toutes les régions Azure publiques, ainsi que dans les centres de données de Chine et du Gouvernement des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="61ab6-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="61ab6-113">Cette version préliminaire est actuellement disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="61ab6-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="61ab6-114">Modes de rédaction de face</span><span class="sxs-lookup"><span data-stu-id="61ab6-114">Face redaction modes</span></span>
<span data-ttu-id="61ab6-115">Rédaction visages utilise en détectant des faces dans chaque image de la vidéo et suivi du cadran de hello objet à la fois vers l’avant et vers l’arrière dans le temps, afin que hello même personne peut être rendue floue à partir des autres angles ainsi.</span><span class="sxs-lookup"><span data-stu-id="61ab6-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="61ab6-116">Bonjour les processus automatisés rédaction sont très complexe et ne produisent pas toujours 100 % de la sortie souhaitée, c’est pourquoi que Analytique de support vous offre deux manières la sortie finale toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="61ab6-117">Mode Ajout tooa entièrement automatique, il est un flux de travail deux passes qui permet de hello sélection/désérialiser-selection des faces trouvées via une liste d’ID.</span><span class="sxs-lookup"><span data-stu-id="61ab6-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="61ab6-118">En outre, toomake arbitraire par hello ajustements de frame du Pack d’administration utilise un fichier de métadonnées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="61ab6-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="61ab6-119">Ce flux de travail est divisé en modes **Analyser** et **Rédiger**.</span><span class="sxs-lookup"><span data-stu-id="61ab6-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="61ab6-120">Vous pouvez combiner les deux modes de hello en un seul passage qui exécute les deux tâches en tâches ; Ce mode est appelé **combinée**.</span><span class="sxs-lookup"><span data-stu-id="61ab6-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="61ab6-121">Mode Combiné</span><span class="sxs-lookup"><span data-stu-id="61ab6-121">Combined mode</span></span>
<span data-ttu-id="61ab6-122">Cela génère un mp4 rédigé automatiquement sans entrée manuelle.</span><span class="sxs-lookup"><span data-stu-id="61ab6-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="61ab6-123">Étape</span><span class="sxs-lookup"><span data-stu-id="61ab6-123">Stage</span></span> | <span data-ttu-id="61ab6-124">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="61ab6-124">File Name</span></span> | <span data-ttu-id="61ab6-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="61ab6-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ab6-126">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-126">Input asset</span></span> |<span data-ttu-id="61ab6-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="61ab6-127">foo.bar</span></span> |<span data-ttu-id="61ab6-128">Vidéo au format WMV, MOV ou MP4</span><span class="sxs-lookup"><span data-stu-id="61ab6-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="61ab6-129">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-129">Input config</span></span> |<span data-ttu-id="61ab6-130">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="61ab6-130">Job configuration preset</span></span> |<span data-ttu-id="61ab6-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="61ab6-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="61ab6-132">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-132">Output asset</span></span> |<span data-ttu-id="61ab6-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="61ab6-133">foo_redacted.mp4</span></span> |<span data-ttu-id="61ab6-134">Vidéo avec flou appliqué</span><span class="sxs-lookup"><span data-stu-id="61ab6-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="61ab6-135">Exemple d’entrée :</span><span class="sxs-lookup"><span data-stu-id="61ab6-135">Input example:</span></span>
[<span data-ttu-id="61ab6-136">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="61ab6-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="61ab6-137">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="61ab6-137">Output example:</span></span>
[<span data-ttu-id="61ab6-138">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="61ab6-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="61ab6-139">Mode Analyser</span><span class="sxs-lookup"><span data-stu-id="61ab6-139">Analyze mode</span></span>
<span data-ttu-id="61ab6-140">Hello **analyser** réussissent du flux de travail de deux passes hello accepte une entrée vidéo et génère un fichier JSON des emplacements de face et les images jpg de chaque détecté face.</span><span class="sxs-lookup"><span data-stu-id="61ab6-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="61ab6-141">Étape</span><span class="sxs-lookup"><span data-stu-id="61ab6-141">Stage</span></span> | <span data-ttu-id="61ab6-142">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="61ab6-142">File Name</span></span> | <span data-ttu-id="61ab6-143">Remarques</span><span class="sxs-lookup"><span data-stu-id="61ab6-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ab6-144">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-144">Input asset</span></span> |<span data-ttu-id="61ab6-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="61ab6-145">foo.bar</span></span> |<span data-ttu-id="61ab6-146">Vidéo au format WMV, MPV ou MP4</span><span class="sxs-lookup"><span data-stu-id="61ab6-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="61ab6-147">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-147">Input config</span></span> |<span data-ttu-id="61ab6-148">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="61ab6-148">Job configuration preset</span></span> |<span data-ttu-id="61ab6-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="61ab6-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="61ab6-150">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-150">Output asset</span></span> |<span data-ttu-id="61ab6-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="61ab6-151">foo_annotations.json</span></span> |<span data-ttu-id="61ab6-152">Données d’annotation des emplacements de visage au format JSON.</span><span class="sxs-lookup"><span data-stu-id="61ab6-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="61ab6-153">Cela peut être modifié par hello utilisateur toomodify hello flou des cadres.</span><span class="sxs-lookup"><span data-stu-id="61ab6-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="61ab6-154">Voir l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61ab6-154">See sample below.</span></span> |
| <span data-ttu-id="61ab6-155">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-155">Output asset</span></span> |<span data-ttu-id="61ab6-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="61ab6-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="61ab6-157">Jpg rognée de chaque détecté face, où le nombre de hello indique labelId hello du cadran de hello</span><span class="sxs-lookup"><span data-stu-id="61ab6-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="61ab6-158">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="61ab6-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="61ab6-159">Mode Rédiger</span><span class="sxs-lookup"><span data-stu-id="61ab6-159">Redact mode</span></span>
<span data-ttu-id="61ab6-160">deuxième passe de Hello du flux de travail hello prend un plus grand nombre d’entrées qui doivent être combinées en un seul élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="61ab6-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="61ab6-161">Cela inclut une liste des ID tooblur hello d’origine et la vidéo annotations de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="61ab6-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="61ab6-162">Ce mode utilise hello annotations tooapply flou sur la vidéo d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="61ab6-163">Hello sortie de test d’analyse hello n’inclut pas les vidéo d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="61ab6-164">Hello vidéo doit toobe chargé dans l’élément multimédia d’entrée de hello pour la tâche en mode de Redact hello et sélectionné comme fichier principal de hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="61ab6-165">Étape</span><span class="sxs-lookup"><span data-stu-id="61ab6-165">Stage</span></span> | <span data-ttu-id="61ab6-166">Nom de fichier</span><span class="sxs-lookup"><span data-stu-id="61ab6-166">File Name</span></span> | <span data-ttu-id="61ab6-167">Remarques</span><span class="sxs-lookup"><span data-stu-id="61ab6-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61ab6-168">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-168">Input asset</span></span> |<span data-ttu-id="61ab6-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="61ab6-169">foo.bar</span></span> |<span data-ttu-id="61ab6-170">Vidéo au format WMV, MPV ou MP4.</span><span class="sxs-lookup"><span data-stu-id="61ab6-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="61ab6-171">Même vidéo que celle de l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="61ab6-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="61ab6-172">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-172">Input asset</span></span> |<span data-ttu-id="61ab6-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="61ab6-173">foo_annotations.json</span></span> |<span data-ttu-id="61ab6-174">Fichier de métadonnées d’annotations de la première phase, avec des modifications facultatives.</span><span class="sxs-lookup"><span data-stu-id="61ab6-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="61ab6-175">Élément multimédia d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-175">Input asset</span></span> |<span data-ttu-id="61ab6-176">foo_IDList.txt (facultatif)</span><span class="sxs-lookup"><span data-stu-id="61ab6-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="61ab6-177">Ligne facultatif liste séparée par des ID tooredact de face.</span><span class="sxs-lookup"><span data-stu-id="61ab6-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="61ab6-178">Si ce champ est laissé vide, tous les visages sont floutés.</span><span class="sxs-lookup"><span data-stu-id="61ab6-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="61ab6-179">Configuration d’entrée</span><span class="sxs-lookup"><span data-stu-id="61ab6-179">Input config</span></span> |<span data-ttu-id="61ab6-180">Job configuration preset</span><span class="sxs-lookup"><span data-stu-id="61ab6-180">Job configuration preset</span></span> |<span data-ttu-id="61ab6-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="61ab6-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="61ab6-182">Élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-182">Output asset</span></span> |<span data-ttu-id="61ab6-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="61ab6-183">foo_redacted.mp4</span></span> |<span data-ttu-id="61ab6-184">Vidéo avec flou appliqué en fonction des annotations</span><span class="sxs-lookup"><span data-stu-id="61ab6-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="61ab6-185">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-185">Example output</span></span>
<span data-ttu-id="61ab6-186">Il s’agit de sortie hello à partir d’un conjointe avec un code sélectionné.</span><span class="sxs-lookup"><span data-stu-id="61ab6-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="61ab6-187">regarder cette vidéo</span><span class="sxs-lookup"><span data-stu-id="61ab6-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="61ab6-188">Exemple : foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="61ab6-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="61ab6-189">Types de flou</span><span class="sxs-lookup"><span data-stu-id="61ab6-189">Blur types</span></span>

<span data-ttu-id="61ab6-190">Bonjour **combinée** ou **Redact** mode, il existe 5 flou différents modes, vous pouvez choisir parmi via la configuration d’entrée de JSON hello : **faible**, **Med**, **Haute**, **déboguer**, et **noir**.</span><span class="sxs-lookup"><span data-stu-id="61ab6-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="61ab6-191">Par défaut, **Med** (Moyen) est utilisé.</span><span class="sxs-lookup"><span data-stu-id="61ab6-191">By default **Med** is used.</span></span>

<span data-ttu-id="61ab6-192">Vous pouvez trouver les exemples de hello flou types ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="61ab6-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="61ab6-193">Exemple JSON :</span><span class="sxs-lookup"><span data-stu-id="61ab6-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="61ab6-194">Faible</span><span class="sxs-lookup"><span data-stu-id="61ab6-194">Low</span></span>

![Faible](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="61ab6-196">Med (Moyen)</span><span class="sxs-lookup"><span data-stu-id="61ab6-196">Med</span></span>

![Med (Moyen)](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="61ab6-198">Élevé</span><span class="sxs-lookup"><span data-stu-id="61ab6-198">High</span></span>

![Élevé](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="61ab6-200">Déboguer</span><span class="sxs-lookup"><span data-stu-id="61ab6-200">Debug</span></span>

![Déboguer](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="61ab6-202">Noir</span><span class="sxs-lookup"><span data-stu-id="61ab6-202">Black</span></span>

![Noir](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="61ab6-204">Éléments hello JSON du fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="61ab6-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="61ab6-205">Hello rédaction du Pack d’administration fournit la détection de l’emplacement de haute précision face et de suivi permettant de détecter les visages de humaine too64 dans une image vidéo.</span><span class="sxs-lookup"><span data-stu-id="61ab6-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="61ab6-206">Visages de face fournissent hello meilleurs résultats, lors de la face et de petites faces (inférieur ou égal à too24x24 pixels) est difficile.</span><span class="sxs-lookup"><span data-stu-id="61ab6-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="61ab6-207">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="61ab6-207">.NET sample code</span></span>

<span data-ttu-id="61ab6-208">suivant de Hello programme montre comment :</span><span class="sxs-lookup"><span data-stu-id="61ab6-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="61ab6-209">Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="61ab6-210">Créer une tâche avec une tâche de rédaction face basée sur un fichier de configuration qui contient hello suivant présélection de json.</span><span class="sxs-lookup"><span data-stu-id="61ab6-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="61ab6-211">Télécharger les fichiers JSON de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="61ab6-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="61ab6-212">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61ab6-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="61ab6-213">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="61ab6-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="61ab6-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="61ab6-214">Example</span></span>

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
        // Read values from hello App.config file.
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
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

## <a name="next-steps"></a><span data-ttu-id="61ab6-215">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="61ab6-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61ab6-216">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="61ab6-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="61ab6-217">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="61ab6-217">Related links</span></span>
[<span data-ttu-id="61ab6-218">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="61ab6-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="61ab6-219">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="61ab6-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

