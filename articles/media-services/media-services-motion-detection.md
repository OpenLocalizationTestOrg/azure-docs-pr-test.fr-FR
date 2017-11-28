---
title: les mouvements aaaDetect avec Azure Media Analytique | Documents Microsoft
description: "Bonjour permet de processeur (MP) détecteur de mouvement de média Azure media tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="91e74-103">Détecter les mouvements avec Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="91e74-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="91e74-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="91e74-104">Overview</span></span>
<span data-ttu-id="91e74-105">Hello **détecteur de mouvement Azure Media** permet de processeur (MP) support tooefficiently de vous identifient des sections d’intérêt dans une vidéo sinon long et se déroule normalement.</span><span class="sxs-lookup"><span data-stu-id="91e74-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="91e74-106">Détection de mouvement peut être utilisée sur caméra statique enregistrements tooidentify sections de la vidéo de hello où se produit le mouvement.</span><span class="sxs-lookup"><span data-stu-id="91e74-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="91e74-107">Il génère un fichier JSON contenant des métadonnées avec les horodateurs et hello englobant la région où l’événement de hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="91e74-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="91e74-108">Cible des flux vidéo de sécurité, cette technologie est mouvement en mesure de toocategorize dans les événements pertinents et des faux positifs, tels que des changements d’éclairage et les ombres.</span><span class="sxs-lookup"><span data-stu-id="91e74-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="91e74-109">Ainsi, vous toogenerate les alertes de sécurité à partir de flux de l’appareil photo sans recevoir des messages indésirables avec les événements non pertinentes sans fin, tout en étant instants tooextract en mesure d’intérêt de vidéos de surveillance très longs.</span><span class="sxs-lookup"><span data-stu-id="91e74-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="91e74-110">Hello **détecteur de mouvement Azure Media** Pack d’administration est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="91e74-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="91e74-111">Cette rubrique fournit des détails sur **détecteur de mouvement Azure Media** et montre comment toouse avec Media Services SDK pour .NET</span><span class="sxs-lookup"><span data-stu-id="91e74-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="91e74-112">Fichiers d’entrée du détecteur de mouvement</span><span class="sxs-lookup"><span data-stu-id="91e74-112">Motion Detector input files</span></span>
<span data-ttu-id="91e74-113">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="91e74-113">Video files.</span></span> <span data-ttu-id="91e74-114">Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.</span><span class="sxs-lookup"><span data-stu-id="91e74-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="91e74-115">Configuration de la tâche (préconfiguration)</span><span class="sxs-lookup"><span data-stu-id="91e74-115">Task configuration (preset)</span></span>
<span data-ttu-id="91e74-116">Lors de la création d’une tâche de vidéo **Azure Media Motion Detector**, vous devez spécifier une présélection de configuration.</span><span class="sxs-lookup"><span data-stu-id="91e74-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="91e74-117">Paramètres</span><span class="sxs-lookup"><span data-stu-id="91e74-117">Parameters</span></span>
<span data-ttu-id="91e74-118">Vous pouvez utiliser hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="91e74-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="91e74-119">Nom</span><span class="sxs-lookup"><span data-stu-id="91e74-119">Name</span></span> | <span data-ttu-id="91e74-120">Options</span><span class="sxs-lookup"><span data-stu-id="91e74-120">Options</span></span> | <span data-ttu-id="91e74-121">Description</span><span class="sxs-lookup"><span data-stu-id="91e74-121">Description</span></span> | <span data-ttu-id="91e74-122">Default</span><span class="sxs-lookup"><span data-stu-id="91e74-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="91e74-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="91e74-123">sensitivityLevel</span></span> |<span data-ttu-id="91e74-124">Chaîne : « low », « medium », « high »</span><span class="sxs-lookup"><span data-stu-id="91e74-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="91e74-125">Définit la sensibilité de hello niveau sur les mouvements est signalée.</span><span class="sxs-lookup"><span data-stu-id="91e74-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="91e74-126">Ajustez ce montant tooadjust de faux positifs.</span><span class="sxs-lookup"><span data-stu-id="91e74-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="91e74-127">« medium »</span><span class="sxs-lookup"><span data-stu-id="91e74-127">'medium'</span></span> |
| <span data-ttu-id="91e74-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="91e74-128">frameSamplingValue</span></span> |<span data-ttu-id="91e74-129">Entier positif</span><span class="sxs-lookup"><span data-stu-id="91e74-129">Positive integer</span></span> |<span data-ttu-id="91e74-130">Définit la fréquence de hello sur lequel s’exécute algorithme.</span><span class="sxs-lookup"><span data-stu-id="91e74-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="91e74-131">1 = chaque trame, 2 = toutes les 2 trames, etc.</span><span class="sxs-lookup"><span data-stu-id="91e74-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="91e74-132">1</span><span class="sxs-lookup"><span data-stu-id="91e74-132">1</span></span> |
| <span data-ttu-id="91e74-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="91e74-133">detectLightChange</span></span> |<span data-ttu-id="91e74-134">Booléen : « True », « False »</span><span class="sxs-lookup"><span data-stu-id="91e74-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="91e74-135">Définit si des changements d’éclairage sont signalés dans les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="91e74-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="91e74-136">« False »</span><span class="sxs-lookup"><span data-stu-id="91e74-136">'False'</span></span> |
| <span data-ttu-id="91e74-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="91e74-137">mergeTimeThreshold</span></span> |<span data-ttu-id="91e74-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="91e74-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="91e74-139">Exemple : 00:00:03</span><span class="sxs-lookup"><span data-stu-id="91e74-139">Example: 00:00:03</span></span> |<span data-ttu-id="91e74-140">Spécifie la fenêtre de temps hello entre les événements de mouvement où 2 événements seront combinées et signalés comme 1.</span><span class="sxs-lookup"><span data-stu-id="91e74-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="91e74-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="91e74-141">00:00:00</span></span> |
| <span data-ttu-id="91e74-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="91e74-142">detectionZones</span></span> |<span data-ttu-id="91e74-143">Tableau de zones de détection :</span><span class="sxs-lookup"><span data-stu-id="91e74-143">An array of detection zones:</span></span><br/><span data-ttu-id="91e74-144">- Zone de détection est un tableau de 3 points ou plus</span><span class="sxs-lookup"><span data-stu-id="91e74-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="91e74-145">-Point est x et y coordonnées de too1 0.</span><span class="sxs-lookup"><span data-stu-id="91e74-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="91e74-146">Décrit la liste hello de détection polygonale zones toobe est utilisé.</span><span class="sxs-lookup"><span data-stu-id="91e74-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="91e74-147">Résultats seront signalés en tant qu’ID, avec hello tout d’abord un est 'id' avec des zones de hello : 0</span><span class="sxs-lookup"><span data-stu-id="91e74-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="91e74-148">Zone unique qui traite de cadre hello dans son intégralité.</span><span class="sxs-lookup"><span data-stu-id="91e74-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="91e74-149">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="91e74-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="91e74-150">Fichiers de sortie du détecteur de mouvement</span><span class="sxs-lookup"><span data-stu-id="91e74-150">Motion Detector output files</span></span>
<span data-ttu-id="91e74-151">Une tâche de détection de mouvement renvoie un fichier JSON de la ressource en sortie hello qui décrit les alertes de mouvement hello, ainsi que leurs catégories, au sein de hello vidéo.</span><span class="sxs-lookup"><span data-stu-id="91e74-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="91e74-152">fichier de Hello contient plus d’informations sur hello et la durée de mouvement détecté dans hello vidéo.</span><span class="sxs-lookup"><span data-stu-id="91e74-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="91e74-153">une fois qu’il existe des objets en mouvement dans une vidéo d’arrière-plan fixe (par exemple, une surveillance vidéo) Hello API de détecteur de mouvement fournit des indicateurs.</span><span class="sxs-lookup"><span data-stu-id="91e74-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="91e74-154">Hello détecteur de mouvement est formé tooreduce fausses alertes, telles que l’éclairage et les modifications de clichés instantanés.</span><span class="sxs-lookup"><span data-stu-id="91e74-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="91e74-155">Limitations actuelles des algorithmes de hello incluent les vidéos de vision de nuit, les objets semi-transparents et les petits objets.</span><span class="sxs-lookup"><span data-stu-id="91e74-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="91e74-156"><a id="output_elements"></a>Éléments hello JSON du fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="91e74-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="91e74-157">Dans la version la plus récente hello, format de sortie JSON hello a changé et peut représenter une modification avec rupture pour certains clients.</span><span class="sxs-lookup"><span data-stu-id="91e74-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="91e74-158">Hello tableau suivant décrit les éléments hello JSON du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="91e74-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="91e74-159">Élément</span><span class="sxs-lookup"><span data-stu-id="91e74-159">Element</span></span> | <span data-ttu-id="91e74-160">Description</span><span class="sxs-lookup"><span data-stu-id="91e74-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91e74-161">Version</span><span class="sxs-lookup"><span data-stu-id="91e74-161">Version</span></span> |<span data-ttu-id="91e74-162">Cela fait référence version toohello Hello vidéo API.</span><span class="sxs-lookup"><span data-stu-id="91e74-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="91e74-163">version actuelle de Hello est 2.</span><span class="sxs-lookup"><span data-stu-id="91e74-163">hello current version is 2.</span></span> |
| <span data-ttu-id="91e74-164">Échelle de temps</span><span class="sxs-lookup"><span data-stu-id="91e74-164">Timescale</span></span> |<span data-ttu-id="91e74-165">« Cycles » par seconde de la vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="91e74-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="91e74-166">Offset</span><span class="sxs-lookup"><span data-stu-id="91e74-166">Offset</span></span> |<span data-ttu-id="91e74-167">décalage de temps Hello des horodatages dans « cycles ».</span><span class="sxs-lookup"><span data-stu-id="91e74-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="91e74-168">Cette valeur sera toujours 0 dans la version 1.0 des API vidéo.</span><span class="sxs-lookup"><span data-stu-id="91e74-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="91e74-169">Cette valeur est susceptible d’être modifiée dans les scénarios pris en charge ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="91e74-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="91e74-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="91e74-170">Framerate</span></span> |<span data-ttu-id="91e74-171">Images par seconde de hello vidéo.</span><span class="sxs-lookup"><span data-stu-id="91e74-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="91e74-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="91e74-172">Width, Height</span></span> |<span data-ttu-id="91e74-173">Fait référence toohello largeur et hauteur de hello vidéo en pixels.</span><span class="sxs-lookup"><span data-stu-id="91e74-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="91e74-174">Démarrer</span><span class="sxs-lookup"><span data-stu-id="91e74-174">Start</span></span> |<span data-ttu-id="91e74-175">Hello démarrer timestamp dans « cycles ».</span><span class="sxs-lookup"><span data-stu-id="91e74-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="91e74-176">Duration</span><span class="sxs-lookup"><span data-stu-id="91e74-176">Duration</span></span> |<span data-ttu-id="91e74-177">longueur de Hello d’événement hello, dans « cycles ».</span><span class="sxs-lookup"><span data-stu-id="91e74-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="91e74-178">Intervalle</span><span class="sxs-lookup"><span data-stu-id="91e74-178">Interval</span></span> |<span data-ttu-id="91e74-179">intervalle de salutation de chaque entrée de l’événement hello, dans « cycles ».</span><span class="sxs-lookup"><span data-stu-id="91e74-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="91e74-180">Événements</span><span class="sxs-lookup"><span data-stu-id="91e74-180">Events</span></span> |<span data-ttu-id="91e74-181">Chaque fragment de l’événement contient un mouvement de hello détecté au sein de cette durée.</span><span class="sxs-lookup"><span data-stu-id="91e74-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="91e74-182">Type</span><span class="sxs-lookup"><span data-stu-id="91e74-182">Type</span></span> |<span data-ttu-id="91e74-183">Dans la version actuelle de hello, il est toujours « 2 » pour le mouvement générique.</span><span class="sxs-lookup"><span data-stu-id="91e74-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="91e74-184">Cette étiquette donne un mouvement de toocategorize vidéo API hello flexibilité dans les futures versions.</span><span class="sxs-lookup"><span data-stu-id="91e74-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="91e74-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="91e74-185">RegionID</span></span> |<span data-ttu-id="91e74-186">Comme expliqué ci-dessus, cette valeur sera toujours « 0 » dans la présente version.</span><span class="sxs-lookup"><span data-stu-id="91e74-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="91e74-187">Cette étiquette donne un mouvement de toofind vidéo API hello flexibilité dans différentes régions dans les futures versions.</span><span class="sxs-lookup"><span data-stu-id="91e74-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="91e74-188">Régions</span><span class="sxs-lookup"><span data-stu-id="91e74-188">Regions</span></span> |<span data-ttu-id="91e74-189">Désigne la zone toohello dans la vidéo où vous vous souciez de mouvement.</span><span class="sxs-lookup"><span data-stu-id="91e74-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="91e74-190">-« id » représente la zone de la région hello : dans cette version il existe un seul ID 0.</span><span class="sxs-lookup"><span data-stu-id="91e74-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="91e74-191">-« type » représente la forme hello de région de hello vous souciez de mouvement.</span><span class="sxs-lookup"><span data-stu-id="91e74-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="91e74-192">Pour l’instant, seules « rectangle » et « polygone » sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="91e74-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="91e74-193">Si vous avez spécifié « rectangle », région de hello possède dimensions X, Y, largeur et hauteur.</span><span class="sxs-lookup"><span data-stu-id="91e74-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="91e74-194">Hello X et Y coordonnées représentent les coordonnées XY hello angle supérieur gauche de région de hello dans une échelle normalisée de too1.0 0.0.</span><span class="sxs-lookup"><span data-stu-id="91e74-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="91e74-195">hauteur et largeur de hello représentent la taille hello de région de hello dans une échelle normalisée de too1.0 0.0.</span><span class="sxs-lookup"><span data-stu-id="91e74-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="91e74-196">Dans la version actuelle de hello, X, Y, largeur et hauteur sont toujours fixes au niveau 0, 0 et 1, 1.</span><span class="sxs-lookup"><span data-stu-id="91e74-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="91e74-197">Si vous avez spécifié « polygone », région de hello possède les dimensions en points.</span><span class="sxs-lookup"><span data-stu-id="91e74-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="91e74-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="91e74-198">Fragments</span></span> |<span data-ttu-id="91e74-199">les métadonnées Hello sont mémorisé en bloc dans différents segments appelés fragments.</span><span class="sxs-lookup"><span data-stu-id="91e74-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="91e74-200">Chaque fragment contient des valeurs de début (start), de durée (duration), un numéro d’intervalle et des événements (event).</span><span class="sxs-lookup"><span data-stu-id="91e74-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="91e74-201">Un fragment sans aucun événement signifie qu’aucun mouvement n’a été détecté pendant cette heure de début et la durée.</span><span class="sxs-lookup"><span data-stu-id="91e74-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="91e74-202">Crochets []</span><span class="sxs-lookup"><span data-stu-id="91e74-202">Brackets []</span></span> |<span data-ttu-id="91e74-203">Chaque support représente un intervalle de l’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="91e74-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="91e74-204">Les crochets vides pour cet intervalle signifient qu’aucun mouvement n’a été détecté.</span><span class="sxs-lookup"><span data-stu-id="91e74-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="91e74-205">emplacements</span><span class="sxs-lookup"><span data-stu-id="91e74-205">locations</span></span> |<span data-ttu-id="91e74-206">Cette nouvelle entrée sous événements répertorie l’emplacement hello où le mouvement de hello s’est produite.</span><span class="sxs-lookup"><span data-stu-id="91e74-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="91e74-207">Il s’agit plus précis que les zones de détection hello.</span><span class="sxs-lookup"><span data-stu-id="91e74-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="91e74-208">Hello Voici un exemple de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="91e74-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="91e74-209">Limites</span><span class="sxs-lookup"><span data-stu-id="91e74-209">Limitations</span></span>
* <span data-ttu-id="91e74-210">Hello pris en charge les formats vidéo d’entrée incluent MP4 et WMV MOV.</span><span class="sxs-lookup"><span data-stu-id="91e74-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="91e74-211">La détection de mouvement est optimisée pour les vidéos dont l’arrière-plan est fixe.</span><span class="sxs-lookup"><span data-stu-id="91e74-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="91e74-212">algorithme de Hello se concentre sur la réduction de fausses alertes, telles que des changements d’éclairage et les ombres.</span><span class="sxs-lookup"><span data-stu-id="91e74-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="91e74-213">Certains mouvement peut ne pas être détecté en raison de problèmes de tootechnical ; par exemple, vidéos de vision de nuit, les objets semi-transparents et petits objets.</span><span class="sxs-lookup"><span data-stu-id="91e74-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="91e74-214">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="91e74-214">.NET sample code</span></span>

<span data-ttu-id="91e74-215">suivant de Hello programme montre comment :</span><span class="sxs-lookup"><span data-stu-id="91e74-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="91e74-216">Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="91e74-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="91e74-217">Créer une tâche avec une tâche de détection de mouvement vidéo basée sur un fichier de configuration qui contient hello suivant présélection de json.</span><span class="sxs-lookup"><span data-stu-id="91e74-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="91e74-218">Télécharger les fichiers JSON de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="91e74-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="91e74-219">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91e74-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="91e74-220">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="91e74-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="91e74-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="91e74-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="91e74-222">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="91e74-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91e74-223">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="91e74-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="91e74-224">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="91e74-224">Related links</span></span>
[<span data-ttu-id="91e74-225">Blog Azure Media Services Motion Detector</span><span class="sxs-lookup"><span data-stu-id="91e74-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="91e74-226">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="91e74-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="91e74-227">Démonstrations Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="91e74-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

