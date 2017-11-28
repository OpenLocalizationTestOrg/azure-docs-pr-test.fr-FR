---
title: "aaaDetect émotion avec Azure Media Analytique et Face | Documents Microsoft"
description: "Cette rubrique montre comment toodetect fait face et émotions avec Azure Media Analytique."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="6cc2e-103">Détection des visages et des émotions avec Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="6cc2e-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="6cc2e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6cc2e-104">Overview</span></span>
<span data-ttu-id="6cc2e-105">Hello **Azure Media Face détecteur** le processeur multimédia (MP) vous permet de toocount, les mouvements de suivi et même la participation jauge audience et réaction via des expressions visages.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="6cc2e-106">Ce service présente deux fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="6cc2e-106">This service contains two features:</span></span> 

* <span data-ttu-id="6cc2e-107">**Détection faciale**</span><span class="sxs-lookup"><span data-stu-id="6cc2e-107">**Face detection**</span></span>
  
    <span data-ttu-id="6cc2e-108">La détection faciale détecte et suit les visages humains au sein d’une vidéo.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="6cc2e-109">Plusieurs polices peuvent être détectées et par la suite être suivis comme ils sont en déplacement, avec hello heure et l’emplacement des métadonnées retournées dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="6cc2e-110">Lors du suivi, il va tenter de toogive un toohello ID cohérent même sont confrontés lors de la personne de hello tourne autour de l’écran, même s’ils sont coupés ou laisser brièvement les frames de hello.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6cc2e-111">Ce service n’effectue pas la reconnaissance faciale.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="6cc2e-112">Une personne qui laisse le frame de hello ou devienne coupée pour trop longtemps recevra un nouvel ID lorsqu’elles retournent.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="6cc2e-113">**Détection d’émotions**</span><span class="sxs-lookup"><span data-stu-id="6cc2e-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="6cc2e-114">Détection d’émotion est un composant facultatif de hello processeur multimédia de détection Face qui renvoie analysis sur plusieurs attributs émotionnels à partir de face hello détecté, y compris bonheur, leur, peur, colère et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="6cc2e-115">Hello **Azure Media Face détecteur** Pack d’administration est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="6cc2e-116">Cette rubrique fournit des détails sur **Azure Media Face détecteur** et montre comment toouse avec Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="6cc2e-117">Fichiers d’entrée du détecteur facial</span><span class="sxs-lookup"><span data-stu-id="6cc2e-117">Face Detector input files</span></span>
<span data-ttu-id="6cc2e-118">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-118">Video files.</span></span> <span data-ttu-id="6cc2e-119">Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="6cc2e-120">Fichiers de sortie du détecteur facial</span><span class="sxs-lookup"><span data-stu-id="6cc2e-120">Face Detector output files</span></span>
<span data-ttu-id="6cc2e-121">API de détection et le suivi de la face Hello fournit la détection de l’emplacement de haute précision face et de suivi permettant de détecter les visages de humaine too64 dans une vidéo.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="6cc2e-122">Hello meilleurs résultats, lors de la face et de petites faces fournissent des visages de face (inférieur ou égal à too24x24 pixels) ne peut pas être aussi précises.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="6cc2e-123">Hello faces détectés et de suivi sont retournées par les coordonnées (gauche, haut, largeur et hauteur) indiquant l’emplacement hello des faces dans l’image de hello en pixels, ainsi que pour un ID face numéro indiquant hello suivi de cette personne.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="6cc2e-124">Les numéros d’identification face sont tooreset susceptible d’engendrer des circonstances quand un visage de face hello est perdu ou superposée dans le cadre de hello, aboutissant à certaines personnes plusieurs ID lors de l’attribution.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="6cc2e-125"><a id="output_elements"></a>Éléments hello JSON du fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="6cc2e-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="6cc2e-126">Détecteur de face utilise des techniques de fragmentation (où hello métadonnées peuvent être divisées en plusieurs segments de temps, vous pouvez télécharger ce que vous devez uniquement) et la segmentation (où les événements hello sont classifiées dans le cas où ils obtenir trop grandes).</span><span class="sxs-lookup"><span data-stu-id="6cc2e-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="6cc2e-127">Des calculs simples, vous peuvent transformer les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="6cc2e-128">Par exemple, si un événement a démarré à 6 300 (cycles), avec une échelle de temps de 2 997 (cycles par seconde) et si la fréquence d’images est de 29,97 (images par seconde), alors :</span><span class="sxs-lookup"><span data-stu-id="6cc2e-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="6cc2e-129">Démarrage/Échelle de temps = 2,1 secondes</span><span class="sxs-lookup"><span data-stu-id="6cc2e-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="6cc2e-130">Secondes x fréquence d'images = 63 images</span><span class="sxs-lookup"><span data-stu-id="6cc2e-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="6cc2e-131">Exemple d’entrée et de sortie de détection faciale</span><span class="sxs-lookup"><span data-stu-id="6cc2e-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="6cc2e-132">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="6cc2e-132">Input video</span></span>
[<span data-ttu-id="6cc2e-133">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="6cc2e-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="6cc2e-134">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="6cc2e-134">Task configuration (preset)</span></span>
<span data-ttu-id="6cc2e-135">Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="6cc2e-136">Hello suivant présélection de configuration est uniquement pour la détection de visage.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="6cc2e-137">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-137">Attribute descriptions</span></span>
| <span data-ttu-id="6cc2e-138">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="6cc2e-138">Attribute name</span></span> | <span data-ttu-id="6cc2e-139">Description</span><span class="sxs-lookup"><span data-stu-id="6cc2e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cc2e-140">Mode</span><span class="sxs-lookup"><span data-stu-id="6cc2e-140">Mode</span></span> |<span data-ttu-id="6cc2e-141">Fast : traitement rapide, mais moins précis (par défaut).</span><span class="sxs-lookup"><span data-stu-id="6cc2e-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="6cc2e-142">Sortie JSON</span><span class="sxs-lookup"><span data-stu-id="6cc2e-142">JSON output</span></span>
<span data-ttu-id="6cc2e-143">Hello, exemple de sortie JSON suivant a été tronquée.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="6cc2e-144">Exemple d’entrée et de sortie de détection d’émotion</span><span class="sxs-lookup"><span data-stu-id="6cc2e-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="6cc2e-145">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="6cc2e-145">Input video</span></span>
[<span data-ttu-id="6cc2e-146">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="6cc2e-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="6cc2e-147">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="6cc2e-147">Task configuration (preset)</span></span>
<span data-ttu-id="6cc2e-148">Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="6cc2e-149">Hello suivant présélection de configuration spécifie toocreate que JSON en fonction de détection d’émotion hello.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="6cc2e-150">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-150">Attribute descriptions</span></span>
| <span data-ttu-id="6cc2e-151">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="6cc2e-151">Attribute name</span></span> | <span data-ttu-id="6cc2e-152">Description</span><span class="sxs-lookup"><span data-stu-id="6cc2e-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6cc2e-153">Mode</span><span class="sxs-lookup"><span data-stu-id="6cc2e-153">Mode</span></span> |<span data-ttu-id="6cc2e-154">Faces : détection faciale uniquement.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="6cc2e-155">PerFaceEmotion : retourne les valeurs d’émotion indépendamment pour chaque détection faciale.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="6cc2e-156">AggregateEmotion : retourne les valeurs d’émotion moyennes pour tous les visages dans l’image.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="6cc2e-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="6cc2e-158">Utilisez cet attribut si le mode AggregateEmotion est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="6cc2e-159">Spécifie hello vidéo tooproduce utilisé chaque résultat d’agrégation, en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="6cc2e-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="6cc2e-161">Utilisez cet attribut si le mode AggregateEmotion est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="6cc2e-162">Spécifie quel agrégat tooproduce de fréquence des résultats.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="6cc2e-163">Valeurs d'agrégation par défaut</span><span class="sxs-lookup"><span data-stu-id="6cc2e-163">Aggregate defaults</span></span>
<span data-ttu-id="6cc2e-164">Ci-dessous sont valeurs recommandées pour l’agrégation hello et les paramètres d’intervalle.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="6cc2e-165">La valeur AggregateEmotionWindowMs doit être supérieure à AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="6cc2e-166">Valeur(s) par défaut</span><span class="sxs-lookup"><span data-stu-id="6cc2e-166">Defaults(s)</span></span> | <span data-ttu-id="6cc2e-167">Valeur(s) min</span><span class="sxs-lookup"><span data-stu-id="6cc2e-167">Min(s)</span></span> | <span data-ttu-id="6cc2e-168">Valeur(s) max</span><span class="sxs-lookup"><span data-stu-id="6cc2e-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="6cc2e-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="6cc2e-170">0.5</span><span class="sxs-lookup"><span data-stu-id="6cc2e-170">0.5</span></span> |<span data-ttu-id="6cc2e-171">2</span><span class="sxs-lookup"><span data-stu-id="6cc2e-171">2</span></span> |<span data-ttu-id="6cc2e-172">0,25</span><span class="sxs-lookup"><span data-stu-id="6cc2e-172">0.25</span></span>|
| <span data-ttu-id="6cc2e-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="6cc2e-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="6cc2e-174">0.5</span><span class="sxs-lookup"><span data-stu-id="6cc2e-174">0.5</span></span> |<span data-ttu-id="6cc2e-175">1</span><span class="sxs-lookup"><span data-stu-id="6cc2e-175">1</span></span> |<span data-ttu-id="6cc2e-176">0,25</span><span class="sxs-lookup"><span data-stu-id="6cc2e-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="6cc2e-177">Sortie JSON</span><span class="sxs-lookup"><span data-stu-id="6cc2e-177">JSON output</span></span>
<span data-ttu-id="6cc2e-178">Sortie JSON pour l’émotion agrégée (tronquée) :</span><span class="sxs-lookup"><span data-stu-id="6cc2e-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="6cc2e-179">Limites</span><span class="sxs-lookup"><span data-stu-id="6cc2e-179">Limitations</span></span>
* <span data-ttu-id="6cc2e-180">Hello pris en charge les formats vidéo d’entrée incluent MP4 et WMV MOV.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="6cc2e-181">plage de tailles de police détectables Hello est 24 x 24 too2048x2048 pixels.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="6cc2e-182">faces Hello en dehors de cette plage ne sont pas détectées.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="6cc2e-183">Pour chaque vidéo, le nombre maximal de hello des faces retourné est 64.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="6cc2e-184">Certaines faces peut ne pas être détectés en raison de problèmes de tootechnical ; par exemple, très grandes face angles (head-pose) et occlusion volumineuse.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="6cc2e-185">Faces frontales et près frontal ont des résultats optimaux hello.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="6cc2e-186">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="6cc2e-186">.NET sample code</span></span>

<span data-ttu-id="6cc2e-187">suivant de Hello programme montre comment :</span><span class="sxs-lookup"><span data-stu-id="6cc2e-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="6cc2e-188">Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="6cc2e-189">Créer une tâche avec une tâche de détection de visage basée sur un fichier de configuration qui contient hello suivant présélection de json.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="6cc2e-190">Télécharger les fichiers JSON de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="6cc2e-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6cc2e-191">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cc2e-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="6cc2e-192">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6cc2e-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="6cc2e-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="6cc2e-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="6cc2e-194">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="6cc2e-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6cc2e-195">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="6cc2e-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6cc2e-196">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="6cc2e-196">Related links</span></span>
[<span data-ttu-id="6cc2e-197">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="6cc2e-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="6cc2e-198">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="6cc2e-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

