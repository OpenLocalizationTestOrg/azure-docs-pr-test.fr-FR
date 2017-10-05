---
title: "Détection des visages et des émotions avec Azure Media Analytics | Microsoft Docs"
description: "Cette rubrique illustre la détection faciale et d’émotions avec Azure Media Analytics."
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="3aa26-103">Détection des visages et des émotions avec Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="3aa26-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="3aa26-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3aa26-104">Overview</span></span>
<span data-ttu-id="3aa26-105">Le processeur multimédia **Azure Media Face Detector** vous permet de compter, de suivre le mouvement, voire de mesurer la participation du public ainsi que ses réactions en analysant les expressions faciales.</span><span class="sxs-lookup"><span data-stu-id="3aa26-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="3aa26-106">Ce service présente deux fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="3aa26-106">This service contains two features:</span></span> 

* <span data-ttu-id="3aa26-107">**Détection faciale**</span><span class="sxs-lookup"><span data-stu-id="3aa26-107">**Face detection**</span></span>
  
    <span data-ttu-id="3aa26-108">La détection faciale détecte et suit les visages humains au sein d’une vidéo.</span><span class="sxs-lookup"><span data-stu-id="3aa26-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="3aa26-109">Plusieurs visages peuvent être détectés et, par la suite, suivis dans leurs mouvements ; les métadonnées d’horodatage et de localisation seront retournées dans un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="3aa26-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="3aa26-110">Lors du suivi, la fonctionnalité tente d’attribuer un identificateur cohérent à un visage en mouvement, même si ce dernier quitte momentanément l’image ou s’il est caché.</span><span class="sxs-lookup"><span data-stu-id="3aa26-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3aa26-111">Ce service n’effectue pas la reconnaissance faciale.</span><span class="sxs-lookup"><span data-stu-id="3aa26-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="3aa26-112">Une personne qui quitte l’image ou dont le visage est caché pendant une période prolongée se voit attribuer un nouvel identifiant à son retour.</span><span class="sxs-lookup"><span data-stu-id="3aa26-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="3aa26-113">**Détection d’émotions**</span><span class="sxs-lookup"><span data-stu-id="3aa26-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="3aa26-114">La détection d’émotions est un composant facultatif du processeur multimédia de détection faciale, qui analyse plusieurs caractéristiques émotionnelles sur les visages détectés, telles que le bonheur, la tristesse, la peur, la colère et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="3aa26-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="3aa26-115">Le processeur multimédia **Azure Media Face Detector** est uniquement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="3aa26-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="3aa26-116">Cette rubrique donne des informations détaillées sur **Azure Media Face Detector** et illustre son utilisation avec le SDK Media Services pour .NET.</span><span class="sxs-lookup"><span data-stu-id="3aa26-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="3aa26-117">Fichiers d’entrée du détecteur facial</span><span class="sxs-lookup"><span data-stu-id="3aa26-117">Face Detector input files</span></span>
<span data-ttu-id="3aa26-118">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="3aa26-118">Video files.</span></span> <span data-ttu-id="3aa26-119">Les formats suivants sont actuellement pris en charge : MP4, MOV et WMV.</span><span class="sxs-lookup"><span data-stu-id="3aa26-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="3aa26-120">Fichiers de sortie du détecteur facial</span><span class="sxs-lookup"><span data-stu-id="3aa26-120">Face Detector output files</span></span>
<span data-ttu-id="3aa26-121">L’API de détection et de suivi facial permet une détection d’emplacement et un suivi de visage très précis ; elle peut détecter jusqu’à 64 visages humains dans une vidéo.</span><span class="sxs-lookup"><span data-stu-id="3aa26-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="3aa26-122">Les visages filmés de face donnent les meilleurs résultats ; les visages filmés de côté ou les visages de taille réduite (24 x 24 pixels ou moins) peuvent ne pas être aussi précis.</span><span class="sxs-lookup"><span data-stu-id="3aa26-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="3aa26-123">Les visages détectés et suivis sont retournés avec les coordonnées (point gauche et supérieur, largeur, hauteur) indiquant l’emplacement des visages dans l’image en pixels, mais aussi un numéro d’identification pour chaque visage, indiquant le suivi de cette personne.</span><span class="sxs-lookup"><span data-stu-id="3aa26-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="3aa26-124">Les numéros d’identification des visages peuvent être réinitialisés dans des cas où le visage filmé de face sort de l’image ou si un élément vient se superposer ; certaines personnes peuvent ainsi se voir attribuer plusieurs identifiants.</span><span class="sxs-lookup"><span data-stu-id="3aa26-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="3aa26-125"><a id="output_elements"></a>Éléments du fichier de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="3aa26-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="3aa26-126">Face Detector utilise des techniques de fragmentation (où les métadonnées peuvent être divisées en segments temporels, et vous téléchargez uniquement ce dont vous avez besoin) et de segmentation (où les événements sont fractionnés s’ils sont trop larges).</span><span class="sxs-lookup"><span data-stu-id="3aa26-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="3aa26-127">Des calculs simples peuvent vous aider à transformer les données.</span><span class="sxs-lookup"><span data-stu-id="3aa26-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="3aa26-128">Par exemple, si un événement a démarré à 6 300 (cycles), avec une échelle de temps de 2 997 (cycles par seconde) et si la fréquence d’images est de 29,97 (images par seconde), alors :</span><span class="sxs-lookup"><span data-stu-id="3aa26-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="3aa26-129">Démarrage/Échelle de temps = 2,1 secondes</span><span class="sxs-lookup"><span data-stu-id="3aa26-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="3aa26-130">Secondes x fréquence d'images = 63 images</span><span class="sxs-lookup"><span data-stu-id="3aa26-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="3aa26-131">Exemple d’entrée et de sortie de détection faciale</span><span class="sxs-lookup"><span data-stu-id="3aa26-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3aa26-132">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="3aa26-132">Input video</span></span>
[<span data-ttu-id="3aa26-133">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="3aa26-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3aa26-134">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="3aa26-134">Task configuration (preset)</span></span>
<span data-ttu-id="3aa26-135">Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="3aa26-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3aa26-136">La présélection de configuration suivante est uniquement valable pour la détection faciale.</span><span class="sxs-lookup"><span data-stu-id="3aa26-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="3aa26-137">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="3aa26-137">Attribute descriptions</span></span>
| <span data-ttu-id="3aa26-138">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="3aa26-138">Attribute name</span></span> | <span data-ttu-id="3aa26-139">Description</span><span class="sxs-lookup"><span data-stu-id="3aa26-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3aa26-140">Mode</span><span class="sxs-lookup"><span data-stu-id="3aa26-140">Mode</span></span> |<span data-ttu-id="3aa26-141">Fast : traitement rapide, mais moins précis (par défaut).</span><span class="sxs-lookup"><span data-stu-id="3aa26-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="3aa26-142">Sortie JSON</span><span class="sxs-lookup"><span data-stu-id="3aa26-142">JSON output</span></span>
<span data-ttu-id="3aa26-143">L’exemple suivant de sortie JSON a été tronqué.</span><span class="sxs-lookup"><span data-stu-id="3aa26-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="3aa26-144">Exemple d’entrée et de sortie de détection d’émotion</span><span class="sxs-lookup"><span data-stu-id="3aa26-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3aa26-145">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="3aa26-145">Input video</span></span>
[<span data-ttu-id="3aa26-146">Vidéo d’entrée</span><span class="sxs-lookup"><span data-stu-id="3aa26-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3aa26-147">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="3aa26-147">Task configuration (preset)</span></span>
<span data-ttu-id="3aa26-148">Lors de la création d’une tâche de vidéo **Azure Media Face Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="3aa26-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3aa26-149">La présélection de configuration suivante spécifie la création d’un JSON en fonction de la détection d’émotion.</span><span class="sxs-lookup"><span data-stu-id="3aa26-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="3aa26-150">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="3aa26-150">Attribute descriptions</span></span>
| <span data-ttu-id="3aa26-151">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="3aa26-151">Attribute name</span></span> | <span data-ttu-id="3aa26-152">Description</span><span class="sxs-lookup"><span data-stu-id="3aa26-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3aa26-153">Mode</span><span class="sxs-lookup"><span data-stu-id="3aa26-153">Mode</span></span> |<span data-ttu-id="3aa26-154">Faces : détection faciale uniquement.</span><span class="sxs-lookup"><span data-stu-id="3aa26-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="3aa26-155">PerFaceEmotion : retourne les valeurs d’émotion indépendamment pour chaque détection faciale.</span><span class="sxs-lookup"><span data-stu-id="3aa26-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="3aa26-156">AggregateEmotion : retourne les valeurs d’émotion moyennes pour tous les visages dans l’image.</span><span class="sxs-lookup"><span data-stu-id="3aa26-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="3aa26-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3aa26-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3aa26-158">Utilisez cet attribut si le mode AggregateEmotion est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3aa26-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3aa26-159">Spécifie la longueur de la vidéo utilisée pour produire chaque résultat agrégé, en millisecondes.</span><span class="sxs-lookup"><span data-stu-id="3aa26-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="3aa26-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3aa26-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3aa26-161">Utilisez cet attribut si le mode AggregateEmotion est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3aa26-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3aa26-162">Spécifie à quelle fréquence les résultats agrégés doivent être produits.</span><span class="sxs-lookup"><span data-stu-id="3aa26-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="3aa26-163">Valeurs d'agrégation par défaut</span><span class="sxs-lookup"><span data-stu-id="3aa26-163">Aggregate defaults</span></span>
<span data-ttu-id="3aa26-164">Les valeurs ci-dessous sont des valeurs recommandées pour les paramètres de fenêtre et d’intervalle d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="3aa26-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="3aa26-165">La valeur AggregateEmotionWindowMs doit être supérieure à AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="3aa26-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="3aa26-166">Valeur(s) par défaut</span><span class="sxs-lookup"><span data-stu-id="3aa26-166">Defaults(s)</span></span> | <span data-ttu-id="3aa26-167">Valeur(s) min</span><span class="sxs-lookup"><span data-stu-id="3aa26-167">Min(s)</span></span> | <span data-ttu-id="3aa26-168">Valeur(s) max</span><span class="sxs-lookup"><span data-stu-id="3aa26-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="3aa26-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3aa26-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3aa26-170">0.5</span><span class="sxs-lookup"><span data-stu-id="3aa26-170">0.5</span></span> |<span data-ttu-id="3aa26-171">2</span><span class="sxs-lookup"><span data-stu-id="3aa26-171">2</span></span> |<span data-ttu-id="3aa26-172">0,25</span><span class="sxs-lookup"><span data-stu-id="3aa26-172">0.25</span></span>|
| <span data-ttu-id="3aa26-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3aa26-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3aa26-174">0.5</span><span class="sxs-lookup"><span data-stu-id="3aa26-174">0.5</span></span> |<span data-ttu-id="3aa26-175">1</span><span class="sxs-lookup"><span data-stu-id="3aa26-175">1</span></span> |<span data-ttu-id="3aa26-176">0,25</span><span class="sxs-lookup"><span data-stu-id="3aa26-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="3aa26-177">Sortie JSON</span><span class="sxs-lookup"><span data-stu-id="3aa26-177">JSON output</span></span>
<span data-ttu-id="3aa26-178">Sortie JSON pour l’émotion agrégée (tronquée) :</span><span class="sxs-lookup"><span data-stu-id="3aa26-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="3aa26-179">Limitations</span><span class="sxs-lookup"><span data-stu-id="3aa26-179">Limitations</span></span>
* <span data-ttu-id="3aa26-180">Les formats de fichier vidéo d’entrée pris en charge incluent WMV, MOV et MP4.</span><span class="sxs-lookup"><span data-stu-id="3aa26-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="3aa26-181">Les visages sont détectables selon une plage de tailles allant de 24 x 24 à 2 048 x 2 048 pixels.</span><span class="sxs-lookup"><span data-stu-id="3aa26-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="3aa26-182">Les visages en dehors de cette plage ne sont pas détectés.</span><span class="sxs-lookup"><span data-stu-id="3aa26-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="3aa26-183">Pour chaque vidéo, le nombre maximal de visages retourné est de 64.</span><span class="sxs-lookup"><span data-stu-id="3aa26-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="3aa26-184">Certains visages peuvent ne pas être détectés en raison de défis techniques, par exemple, les prises très rapprochées (portrait) et les occlusions importantes</span><span class="sxs-lookup"><span data-stu-id="3aa26-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="3aa26-185">Les prises frontales et quasi-frontales produisent les meilleurs résultats.</span><span class="sxs-lookup"><span data-stu-id="3aa26-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="3aa26-186">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="3aa26-186">.NET sample code</span></span>

<span data-ttu-id="3aa26-187">Le programme suivant montre comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="3aa26-187">The following program shows how to:</span></span>

1. <span data-ttu-id="3aa26-188">Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="3aa26-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="3aa26-189">Créer un travail avec une tâche de détection faciale basée sur un fichier de configuration qui contient la présélection JSON suivante.</span><span class="sxs-lookup"><span data-stu-id="3aa26-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="3aa26-190">Télécharger les fichiers JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="3aa26-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3aa26-191">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3aa26-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3aa26-192">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3aa26-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="3aa26-193">Exemple</span><span class="sxs-lookup"><span data-stu-id="3aa26-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="3aa26-194">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="3aa26-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3aa26-195">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="3aa26-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="3aa26-196">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="3aa26-196">Related links</span></span>
[<span data-ttu-id="3aa26-197">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="3aa26-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="3aa26-198">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="3aa26-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

