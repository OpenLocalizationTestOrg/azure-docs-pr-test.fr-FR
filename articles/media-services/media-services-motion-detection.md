---
title: "Détecter les mouvements avec Azure Media Analytics | Microsoft Docs"
description: "Le processeur multimédia Azure Media Motion Detector vous permet d’identifier efficacement les passages intéressants dans une vidéo qui, autrement, serait longue et monotone."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="dd81e-103">Détecter les mouvements avec Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="dd81e-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="dd81e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dd81e-104">Overview</span></span>
<span data-ttu-id="dd81e-105">Le processeur multimédia **Azure Media Motion Detector** vous permet d’identifier efficacement les passages intéressants dans une vidéo qui, autrement, serait longue et monotone.</span><span class="sxs-lookup"><span data-stu-id="dd81e-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="dd81e-106">La détection de mouvement peut être utilisée sur des séquences d’une caméra fixe pour identifier les passages de la vidéo où un mouvement se produit.</span><span class="sxs-lookup"><span data-stu-id="dd81e-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="dd81e-107">Elle génère un fichier JSON contenant des métadonnées avec des horodateurs et le cadre de limitation de la vidéo où s’est produit l’événement.</span><span class="sxs-lookup"><span data-stu-id="dd81e-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="dd81e-108">Ciblant les vidéos de surveillance, cette technologie est en mesure de classer les mouvements en événements pertinents et en faux positifs, tels que les ombres et les variations d’éclairage.</span><span class="sxs-lookup"><span data-stu-id="dd81e-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="dd81e-109">Cela vous permet de générer des alertes de sécurité à partir de séquences vidéo sans perdre de temps avec d’innombrables faux positifs, et tout en accédant rapidement aux moments clés dans des vidéos de surveillance extrêmement longues.</span><span class="sxs-lookup"><span data-stu-id="dd81e-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="dd81e-110">Le processeur multimédia **Azure Media Motion Detector** est uniquement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="dd81e-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="dd81e-111">Cette rubrique fournit des informations détaillées sur **Azure Media Motion Detector** et illustre son utilisation avec le SDK Media Services pour .NET.</span><span class="sxs-lookup"><span data-stu-id="dd81e-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="dd81e-112">Fichiers d’entrée du détecteur de mouvement</span><span class="sxs-lookup"><span data-stu-id="dd81e-112">Motion Detector input files</span></span>
<span data-ttu-id="dd81e-113">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-113">Video files.</span></span> <span data-ttu-id="dd81e-114">Les formats suivants sont actuellement pris en charge : MP4, MOV et WMV.</span><span class="sxs-lookup"><span data-stu-id="dd81e-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="dd81e-115">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="dd81e-115">Task configuration (preset)</span></span>
<span data-ttu-id="dd81e-116">Lors de la création d’une tâche de vidéo **Azure Media Motion Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="dd81e-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="dd81e-117">Paramètres</span><span class="sxs-lookup"><span data-stu-id="dd81e-117">Parameters</span></span>
<span data-ttu-id="dd81e-118">Vous pouvez utiliser les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="dd81e-118">You can use the following parameters:</span></span>

| <span data-ttu-id="dd81e-119">Nom</span><span class="sxs-lookup"><span data-stu-id="dd81e-119">Name</span></span> | <span data-ttu-id="dd81e-120">Options</span><span class="sxs-lookup"><span data-stu-id="dd81e-120">Options</span></span> | <span data-ttu-id="dd81e-121">Description</span><span class="sxs-lookup"><span data-stu-id="dd81e-121">Description</span></span> | <span data-ttu-id="dd81e-122">Default</span><span class="sxs-lookup"><span data-stu-id="dd81e-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dd81e-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="dd81e-123">sensitivityLevel</span></span> |<span data-ttu-id="dd81e-124">Chaîne : « low », « medium », « high »</span><span class="sxs-lookup"><span data-stu-id="dd81e-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="dd81e-125">Définit le niveau de sensibilité auquel les mouvements sont signalés.</span><span class="sxs-lookup"><span data-stu-id="dd81e-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="dd81e-126">Réglez cette option pour ajuster la quantité de faux positifs.</span><span class="sxs-lookup"><span data-stu-id="dd81e-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="dd81e-127">« medium »</span><span class="sxs-lookup"><span data-stu-id="dd81e-127">'medium'</span></span> |
| <span data-ttu-id="dd81e-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="dd81e-128">frameSamplingValue</span></span> |<span data-ttu-id="dd81e-129">Entier positif</span><span class="sxs-lookup"><span data-stu-id="dd81e-129">Positive integer</span></span> |<span data-ttu-id="dd81e-130">Définit la fréquence d’exécution de l’algorithme.</span><span class="sxs-lookup"><span data-stu-id="dd81e-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="dd81e-131">1 = chaque trame, 2 = toutes les 2 trames, etc.</span><span class="sxs-lookup"><span data-stu-id="dd81e-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="dd81e-132">1</span><span class="sxs-lookup"><span data-stu-id="dd81e-132">1</span></span> |
| <span data-ttu-id="dd81e-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="dd81e-133">detectLightChange</span></span> |<span data-ttu-id="dd81e-134">Booléen : « True », « False »</span><span class="sxs-lookup"><span data-stu-id="dd81e-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="dd81e-135">Définit si des changements d’éclairage sont signalés dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="dd81e-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="dd81e-136">« False »</span><span class="sxs-lookup"><span data-stu-id="dd81e-136">'False'</span></span> |
| <span data-ttu-id="dd81e-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="dd81e-137">mergeTimeThreshold</span></span> |<span data-ttu-id="dd81e-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="dd81e-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="dd81e-139">Exemple : 00:00:03</span><span class="sxs-lookup"><span data-stu-id="dd81e-139">Example: 00:00:03</span></span> |<span data-ttu-id="dd81e-140">Spécifie la fenêtre de temps entre les événements de mouvement lorsque 2 événements sont combinés et signalés comme 1.</span><span class="sxs-lookup"><span data-stu-id="dd81e-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="dd81e-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="dd81e-141">00:00:00</span></span> |
| <span data-ttu-id="dd81e-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="dd81e-142">detectionZones</span></span> |<span data-ttu-id="dd81e-143">Tableau de zones de détection :</span><span class="sxs-lookup"><span data-stu-id="dd81e-143">An array of detection zones:</span></span><br/><span data-ttu-id="dd81e-144">- Zone de détection est un tableau de 3 points ou plus</span><span class="sxs-lookup"><span data-stu-id="dd81e-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="dd81e-145">- Point est une coordonnée x et y de 0 à 1.</span><span class="sxs-lookup"><span data-stu-id="dd81e-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="dd81e-146">Décrit la liste des zones de détection polygonale à utiliser.</span><span class="sxs-lookup"><span data-stu-id="dd81e-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="dd81e-147">Les résultats seront signalés avec les zones en tant qu’ID, la première étant « id » :0.</span><span class="sxs-lookup"><span data-stu-id="dd81e-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="dd81e-148">Zone unique couvrant la trame entière.</span><span class="sxs-lookup"><span data-stu-id="dd81e-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="dd81e-149">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="dd81e-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="dd81e-150">Fichiers de sortie du détecteur de mouvement</span><span class="sxs-lookup"><span data-stu-id="dd81e-150">Motion Detector output files</span></span>
<span data-ttu-id="dd81e-151">Une tâche de détection de mouvement renvoie un fichier JSON dans l’élément multimédia de sortie qui décrit les alertes de mouvement et leurs catégories dans la vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="dd81e-152">Le fichier contient des informations sur l’heure et la durée du mouvement détecté dans la vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="dd81e-153">L’API de détecteur de mouvement indique lorsqu’un mouvement a été détecté dans une vidéo d’arrière-plan fixe (par exemple, une vidéo de surveillance).</span><span class="sxs-lookup"><span data-stu-id="dd81e-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="dd81e-154">Le détecteur de mouvement est optimisé pour réduire au minimum les fausses alertes, telles que les ombres et les variations d’éclairage.</span><span class="sxs-lookup"><span data-stu-id="dd81e-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="dd81e-155">Les limitations actuelles des algorithmes incluent les vidéos en vision nocturne, les objets semi-transparents et les petits objets.</span><span class="sxs-lookup"><span data-stu-id="dd81e-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="dd81e-156"><a id="output_elements"></a>Éléments du fichier de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="dd81e-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="dd81e-157">Dans la dernière version, le format de sortie JSON a été modifié et peut représenter une rupture pour certains clients.</span><span class="sxs-lookup"><span data-stu-id="dd81e-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="dd81e-158">Le tableau suivant décrit les éléments du fichier de sortie JSON.</span><span class="sxs-lookup"><span data-stu-id="dd81e-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="dd81e-159">Élément</span><span class="sxs-lookup"><span data-stu-id="dd81e-159">Element</span></span> | <span data-ttu-id="dd81e-160">Description</span><span class="sxs-lookup"><span data-stu-id="dd81e-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dd81e-161">Version</span><span class="sxs-lookup"><span data-stu-id="dd81e-161">Version</span></span> |<span data-ttu-id="dd81e-162">Cela vaut pour la version de l’API vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="dd81e-163">La version actuelle est 2.</span><span class="sxs-lookup"><span data-stu-id="dd81e-163">The current version is 2.</span></span> |
| <span data-ttu-id="dd81e-164">Échelle de temps</span><span class="sxs-lookup"><span data-stu-id="dd81e-164">Timescale</span></span> |<span data-ttu-id="dd81e-165">« Cycles » par seconde de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="dd81e-166">Offset</span><span class="sxs-lookup"><span data-stu-id="dd81e-166">Offset</span></span> |<span data-ttu-id="dd81e-167">Le décalage des horodatages en « cycles ».</span><span class="sxs-lookup"><span data-stu-id="dd81e-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="dd81e-168">Cette valeur sera toujours 0 dans la version 1.0 des API vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="dd81e-169">Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="dd81e-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="dd81e-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="dd81e-170">Framerate</span></span> |<span data-ttu-id="dd81e-171">Images par seconde de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="dd81e-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="dd81e-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="dd81e-172">Width, Height</span></span> |<span data-ttu-id="dd81e-173">Fait référence à la largeur et à la hauteur de la vidéo en pixels.</span><span class="sxs-lookup"><span data-stu-id="dd81e-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="dd81e-174">Démarrer</span><span class="sxs-lookup"><span data-stu-id="dd81e-174">Start</span></span> |<span data-ttu-id="dd81e-175">L’horodatage de début en « cycles ».</span><span class="sxs-lookup"><span data-stu-id="dd81e-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="dd81e-176">Durée</span><span class="sxs-lookup"><span data-stu-id="dd81e-176">Duration</span></span> |<span data-ttu-id="dd81e-177">La durée de l’événement en « cycles ».</span><span class="sxs-lookup"><span data-stu-id="dd81e-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="dd81e-178">Intervalle</span><span class="sxs-lookup"><span data-stu-id="dd81e-178">Interval</span></span> |<span data-ttu-id="dd81e-179">L’intervalle de chaque entrée dans l’événement en « cycles ».</span><span class="sxs-lookup"><span data-stu-id="dd81e-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="dd81e-180">Événements</span><span class="sxs-lookup"><span data-stu-id="dd81e-180">Events</span></span> |<span data-ttu-id="dd81e-181">Chaque fragment d’événement contient le mouvement détecté pendant cette durée.</span><span class="sxs-lookup"><span data-stu-id="dd81e-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="dd81e-182">Type</span><span class="sxs-lookup"><span data-stu-id="dd81e-182">Type</span></span> |<span data-ttu-id="dd81e-183">Dans la version actuelle, cette valeur est toujours de « 2 » pour le mouvement générique.</span><span class="sxs-lookup"><span data-stu-id="dd81e-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="dd81e-184">Ce libellé permet aux API vidéo de classer le mouvement dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="dd81e-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="dd81e-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="dd81e-185">RegionID</span></span> |<span data-ttu-id="dd81e-186">Comme expliqué ci-dessus, cette valeur sera toujours « 0 » dans la présente version.</span><span class="sxs-lookup"><span data-stu-id="dd81e-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="dd81e-187">Ce libellé permet aux API vidéo de détecter du mouvement dans différentes régions dans les versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="dd81e-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="dd81e-188">Régions</span><span class="sxs-lookup"><span data-stu-id="dd81e-188">Regions</span></span> |<span data-ttu-id="dd81e-189">Fait référence à la zone dans la vidéo où un mouvement est susceptible de vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="dd81e-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="dd81e-190">-« id » représente la zone de la région ; dans cette version, la seule valeur existante est ID 0.</span><span class="sxs-lookup"><span data-stu-id="dd81e-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="dd81e-191">-« type » représente la forme de la région où un mouvement est susceptible de vous intéresser.</span><span class="sxs-lookup"><span data-stu-id="dd81e-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="dd81e-192">Pour l’instant, seules « rectangle » et « polygone » sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="dd81e-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="dd81e-193">Si vous avez indiqué « rectangle », les dimensions de la région sont X, Y, Width et Height.</span><span class="sxs-lookup"><span data-stu-id="dd81e-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="dd81e-194">Les coordonnées X et Y représentent les coordonnées XY de l’angle supérieur gauche de la région sur une échelle normalisée de 0,0 à 1,0.</span><span class="sxs-lookup"><span data-stu-id="dd81e-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="dd81e-195">La largeur et la hauteur représentent la taille de la région sur une échelle normalisée de 0,0 à 1,0.</span><span class="sxs-lookup"><span data-stu-id="dd81e-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="dd81e-196">Dans la version actuelle, X, Y, Width et Height sont toujours fixés à 0, 0 et 1, 1.</span><span class="sxs-lookup"><span data-stu-id="dd81e-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="dd81e-197">Si vous avez indiqué « polygone », les dimensions de la région sont en points.</span><span class="sxs-lookup"><span data-stu-id="dd81e-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="dd81e-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="dd81e-198">Fragments</span></span> |<span data-ttu-id="dd81e-199">Les métadonnées sont mémorisées dans différents segments appelés fragments.</span><span class="sxs-lookup"><span data-stu-id="dd81e-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="dd81e-200">Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event).</span><span class="sxs-lookup"><span data-stu-id="dd81e-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="dd81e-201">Un fragment sans aucun événement signifie qu’aucun mouvement n’a été détecté pendant cette heure de début et la durée.</span><span class="sxs-lookup"><span data-stu-id="dd81e-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="dd81e-202">Crochets []</span><span class="sxs-lookup"><span data-stu-id="dd81e-202">Brackets []</span></span> |<span data-ttu-id="dd81e-203">Chaque crochet représente un intervalle dans l’événement.</span><span class="sxs-lookup"><span data-stu-id="dd81e-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="dd81e-204">Les crochets vides pour cet intervalle signifient qu’aucun mouvement n’a été détecté.</span><span class="sxs-lookup"><span data-stu-id="dd81e-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="dd81e-205">emplacements</span><span class="sxs-lookup"><span data-stu-id="dd81e-205">locations</span></span> |<span data-ttu-id="dd81e-206">Cette nouvelle entrée sous les événements répertorie l’emplacement dans lequel le mouvement s’est produit.</span><span class="sxs-lookup"><span data-stu-id="dd81e-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="dd81e-207">Cette entrée est plus précise que les zones de détection.</span><span class="sxs-lookup"><span data-stu-id="dd81e-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="dd81e-208">Voici un exemple de sortie JSON :</span><span class="sxs-lookup"><span data-stu-id="dd81e-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="dd81e-209">Limites</span><span class="sxs-lookup"><span data-stu-id="dd81e-209">Limitations</span></span>
* <span data-ttu-id="dd81e-210">Les formats de fichier vidéo d’entrée pris en charge incluent WMV, MOV et MP4.</span><span class="sxs-lookup"><span data-stu-id="dd81e-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="dd81e-211">La détection de mouvement est optimisée pour les vidéos dont l’arrière-plan est fixe.</span><span class="sxs-lookup"><span data-stu-id="dd81e-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="dd81e-212">L’algorithme est axé sur la réduction des fausses alertes, telles que les variations d’éclairage et les ombres.</span><span class="sxs-lookup"><span data-stu-id="dd81e-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="dd81e-213">Certains mouvements peuvent ne pas être détectés en raison de défis techniques ; par exemple, des vidéos en vision nocturne, les objets semi-transparents et les petits objets.</span><span class="sxs-lookup"><span data-stu-id="dd81e-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="dd81e-214">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="dd81e-214">.NET sample code</span></span>

<span data-ttu-id="dd81e-215">Le programme suivant montre comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd81e-215">The following program shows how to:</span></span>

1. <span data-ttu-id="dd81e-216">Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="dd81e-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="dd81e-217">Créer un travail avec une tâche de détection du mouvement vidéo basée sur un fichier de configuration qui contient la présélection json suivante.</span><span class="sxs-lookup"><span data-stu-id="dd81e-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="dd81e-218">Télécharger les fichiers JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="dd81e-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="dd81e-219">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd81e-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="dd81e-220">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="dd81e-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="dd81e-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="dd81e-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="dd81e-222">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="dd81e-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="dd81e-223">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="dd81e-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="dd81e-224">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="dd81e-224">Related links</span></span>
[<span data-ttu-id="dd81e-225">Blog Azure Media Services Motion Detector</span><span class="sxs-lookup"><span data-stu-id="dd81e-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="dd81e-226">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="dd81e-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="dd81e-227">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="dd81e-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

