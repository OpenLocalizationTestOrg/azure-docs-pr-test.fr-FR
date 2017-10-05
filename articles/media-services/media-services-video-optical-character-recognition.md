---
title: "Numériser du texte avec Azure Media Analytics OCR | Microsoft Docs"
description: "Azure Media Analytics OCR (reconnaissance optique de caractères) vous permet de convertir le contenu texte de fichiers vidéo en un texte numérique modifiable et pouvant faire l’objet d’une recherche.  Vous pouvez ainsi automatiser l’extraction de métadonnées explicites à partir du signal vidéo de votre contenu multimédia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="b7629-104">Utilisation d’Azure Media Analytics pour convertir le contenu texte de fichiers vidéo en texte numérique</span><span class="sxs-lookup"><span data-stu-id="b7629-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="b7629-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b7629-105">Overview</span></span>
<span data-ttu-id="b7629-106">Si vous devez extraire le contenu texte de vos fichiers vidéo et générer un texte numérique modifiable et pouvant faire l’objet d’une recherche, vous devez utiliser Azure Media Analytics OCR (reconnaissance optique de caractères).</span><span class="sxs-lookup"><span data-stu-id="b7629-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="b7629-107">Ce processeur multimédia Azure détecte le contenu texte de vos fichiers vidéo et génère les fichiers texte à utiliser.</span><span class="sxs-lookup"><span data-stu-id="b7629-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="b7629-108">La reconnaissance optique de caractères vous permet d’automatiser l’extraction de métadonnées explicites à partir du signal vidéo de votre contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="b7629-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="b7629-109">Lorsque vous l’utilisez conjointement avec un moteur de recherche, vous pouvez facilement indexer vos données multimédia par texte et améliorer ainsi la détectabilité du contenu.</span><span class="sxs-lookup"><span data-stu-id="b7629-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="b7629-110">Cela est particulièrement utile dans une vidéo contenant beaucoup de texte, comme un enregistrement vidéo ou une capture d’écran de diaporama.</span><span class="sxs-lookup"><span data-stu-id="b7629-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="b7629-111">Le processeur multimédia Azure OCR est optimisé pour le texte numérique.</span><span class="sxs-lookup"><span data-stu-id="b7629-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="b7629-112">Le processeur multimédia **Azure Media OCR** est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="b7629-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="b7629-113">Cette rubrique donne des informations détaillées sur **Azure Media OCR** et montre comment l’utiliser avec le SDK Media Services pour .NET.</span><span class="sxs-lookup"><span data-stu-id="b7629-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="b7629-114">Pour plus d’informations et d’exemples, consultez [ce blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="b7629-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="b7629-115">Fichiers d'entrée OCR</span><span class="sxs-lookup"><span data-stu-id="b7629-115">OCR input files</span></span>
<span data-ttu-id="b7629-116">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="b7629-116">Video files.</span></span> <span data-ttu-id="b7629-117">Les formats suivants sont actuellement pris en charge : MP4, MOV et WMV.</span><span class="sxs-lookup"><span data-stu-id="b7629-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="b7629-118">Configuration de la tâche</span><span class="sxs-lookup"><span data-stu-id="b7629-118">Task configuration</span></span>
<span data-ttu-id="b7629-119">Configuration de la tâche (préconfiguration).</span><span class="sxs-lookup"><span data-stu-id="b7629-119">Task configuration (preset).</span></span> <span data-ttu-id="b7629-120">Lors de la création d’une tâche **Azure Media OCR**, vous devez spécifier une présélection de configuration avec JSON ou XML.</span><span class="sxs-lookup"><span data-stu-id="b7629-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="b7629-121">Le moteur de reconnaissance optique de caractères prend une zone d’image avec au minimum 40 pixels et au maximum 32000 pixels comme entrée valide pour la hauteur et la largeur.</span><span class="sxs-lookup"><span data-stu-id="b7629-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="b7629-122">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="b7629-122">Attribute descriptions</span></span>
| <span data-ttu-id="b7629-123">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="b7629-123">Attribute name</span></span> | <span data-ttu-id="b7629-124">Description</span><span class="sxs-lookup"><span data-stu-id="b7629-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="b7629-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="b7629-125">AdvancedOutput</span></span>| <span data-ttu-id="b7629-126">Si vous définissez AdvancedOutput sur true, le résultat JSON contient les données sur la position de chaque mot unique (en plus des régions et des expressions).</span><span class="sxs-lookup"><span data-stu-id="b7629-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="b7629-127">Si vous ne souhaitez pas voir ces détails, définissez l’indicateur sur False.</span><span class="sxs-lookup"><span data-stu-id="b7629-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="b7629-128">La valeur par défaut est false.</span><span class="sxs-lookup"><span data-stu-id="b7629-128">The default value is false.</span></span> <span data-ttu-id="b7629-129">Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="b7629-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="b7629-130">language</span><span class="sxs-lookup"><span data-stu-id="b7629-130">Language</span></span> |<span data-ttu-id="b7629-131">(facultatif) indique la langue du texte à rechercher.</span><span class="sxs-lookup"><span data-stu-id="b7629-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="b7629-132">Une des valeurs suivantes : AutoDetect (par défaut), Arabic, ChineseSimplified, ChineseTraditional, Czech, Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span><span class="sxs-lookup"><span data-stu-id="b7629-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="b7629-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="b7629-133">TextOrientation</span></span> |<span data-ttu-id="b7629-134">(facultatif) indique l’orientation du texte à rechercher.</span><span class="sxs-lookup"><span data-stu-id="b7629-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="b7629-135">« Left » signifie que la partie supérieure de toutes les lettres pointe vers la gauche.</span><span class="sxs-lookup"><span data-stu-id="b7629-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="b7629-136">Par défaut, le texte peut être affiché en mode « Up » (comme dans un livre).</span><span class="sxs-lookup"><span data-stu-id="b7629-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="b7629-137">Une des valeurs suivantes : AutoDetect (par défaut), Up, Right, Down, Left.</span><span class="sxs-lookup"><span data-stu-id="b7629-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="b7629-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="b7629-138">TimeInterval</span></span> |<span data-ttu-id="b7629-139">(facultatif) décrit le taux d’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="b7629-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="b7629-140">La valeur par défaut est chaque demie seconde.</span><span class="sxs-lookup"><span data-stu-id="b7629-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="b7629-141">Format JSON – HH:mm:ss.SSS (par défaut : 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="b7629-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="b7629-142">Format XML – durée de la primitive W3C XSD (par défaut PT0.5)</span><span class="sxs-lookup"><span data-stu-id="b7629-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="b7629-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="b7629-143">DetectRegions</span></span> |<span data-ttu-id="b7629-144">(facultatif) Tableau d’objets DetectRegion spécifiant des zones au sein de l’image vidéo dans lesquelles détecter le texte.</span><span class="sxs-lookup"><span data-stu-id="b7629-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="b7629-145">Un objet DetectRegion est constitué de quatre valeurs entières suivantes :</span><span class="sxs-lookup"><span data-stu-id="b7629-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="b7629-146">Gauche – pixels à partir de la marge de gauche</span><span class="sxs-lookup"><span data-stu-id="b7629-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="b7629-147">Haut – pixels à partir de la marge supérieure</span><span class="sxs-lookup"><span data-stu-id="b7629-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="b7629-148">Largeur – largeur de la zone en pixels</span><span class="sxs-lookup"><span data-stu-id="b7629-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="b7629-149">Height – hauteur de la zone en pixels</span><span class="sxs-lookup"><span data-stu-id="b7629-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="b7629-150">Exemple de présélection JSON</span><span class="sxs-lookup"><span data-stu-id="b7629-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="b7629-151">Exemple de présélection XML</span><span class="sxs-lookup"><span data-stu-id="b7629-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="b7629-152">Fichiers de sortie OCR</span><span class="sxs-lookup"><span data-stu-id="b7629-152">OCR output files</span></span>
<span data-ttu-id="b7629-153">La sortie du processeur multimédia OCR est un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="b7629-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="b7629-154">Éléments du fichier de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="b7629-154">Elements of the output JSON file</span></span>
<span data-ttu-id="b7629-155">La sortie vidéo OCR fournit des données temporelles segmentées sur les caractères présents dans votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="b7629-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="b7629-156">Vous pouvez utiliser des attributs tels que la langue ou l’orientation pour cibler exactement les mots que vous souhaitez analyser.</span><span class="sxs-lookup"><span data-stu-id="b7629-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="b7629-157">La sortie contient les attributs suivants :</span><span class="sxs-lookup"><span data-stu-id="b7629-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="b7629-158">Élément</span><span class="sxs-lookup"><span data-stu-id="b7629-158">Element</span></span> | <span data-ttu-id="b7629-159">Description</span><span class="sxs-lookup"><span data-stu-id="b7629-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b7629-160">Échelle de temps</span><span class="sxs-lookup"><span data-stu-id="b7629-160">Timescale</span></span> |<span data-ttu-id="b7629-161">« cycles » par seconde de la vidéo</span><span class="sxs-lookup"><span data-stu-id="b7629-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="b7629-162">Offset</span><span class="sxs-lookup"><span data-stu-id="b7629-162">Offset</span></span> |<span data-ttu-id="b7629-163">décalage des horodatages.</span><span class="sxs-lookup"><span data-stu-id="b7629-163">time offset for timestamps.</span></span> <span data-ttu-id="b7629-164">Cette valeur sera toujours 0 dans la version 1.0 des API vidéo.</span><span class="sxs-lookup"><span data-stu-id="b7629-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="b7629-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="b7629-165">Framerate</span></span> |<span data-ttu-id="b7629-166">Images par seconde de la vidéo</span><span class="sxs-lookup"><span data-stu-id="b7629-166">Frames per second of the video</span></span> |
| <span data-ttu-id="b7629-167">width</span><span class="sxs-lookup"><span data-stu-id="b7629-167">width</span></span> |<span data-ttu-id="b7629-168">largeur de la vidéo en pixels</span><span class="sxs-lookup"><span data-stu-id="b7629-168">width of the video in pixels</span></span> |
| <span data-ttu-id="b7629-169">height</span><span class="sxs-lookup"><span data-stu-id="b7629-169">height</span></span> |<span data-ttu-id="b7629-170">hauteur de la vidéo en pixels</span><span class="sxs-lookup"><span data-stu-id="b7629-170">height of the video in pixels</span></span> |
| <span data-ttu-id="b7629-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="b7629-171">Fragments</span></span> |<span data-ttu-id="b7629-172">tableau de segments de temps de vidéo dans lequel les métadonnées sont mémorisées en bloc</span><span class="sxs-lookup"><span data-stu-id="b7629-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="b7629-173">start</span><span class="sxs-lookup"><span data-stu-id="b7629-173">start</span></span> |<span data-ttu-id="b7629-174">heure de début d’un fragment en « cycles »</span><span class="sxs-lookup"><span data-stu-id="b7629-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b7629-175">duration</span><span class="sxs-lookup"><span data-stu-id="b7629-175">duration</span></span> |<span data-ttu-id="b7629-176">durée d’un fragment en « cycles »</span><span class="sxs-lookup"><span data-stu-id="b7629-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b7629-177">interval</span><span class="sxs-lookup"><span data-stu-id="b7629-177">interval</span></span> |<span data-ttu-id="b7629-178">intervalle de chaque événement dans le fragment donné</span><span class="sxs-lookup"><span data-stu-id="b7629-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="b7629-179">événements</span><span class="sxs-lookup"><span data-stu-id="b7629-179">events</span></span> |<span data-ttu-id="b7629-180">tableau contenant des régions</span><span class="sxs-lookup"><span data-stu-id="b7629-180">array containing regions</span></span> |
| <span data-ttu-id="b7629-181">region</span><span class="sxs-lookup"><span data-stu-id="b7629-181">region</span></span> |<span data-ttu-id="b7629-182">objet représentant des mots ou expressions détectés</span><span class="sxs-lookup"><span data-stu-id="b7629-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="b7629-183">Langage</span><span class="sxs-lookup"><span data-stu-id="b7629-183">language</span></span> |<span data-ttu-id="b7629-184">langue du texte détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="b7629-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="b7629-185">orientation</span><span class="sxs-lookup"><span data-stu-id="b7629-185">orientation</span></span> |<span data-ttu-id="b7629-186">orientation du texte détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="b7629-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="b7629-187">lignes</span><span class="sxs-lookup"><span data-stu-id="b7629-187">lines</span></span> |<span data-ttu-id="b7629-188">tableau de lignes de texte détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="b7629-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="b7629-189">texte</span><span class="sxs-lookup"><span data-stu-id="b7629-189">text</span></span> |<span data-ttu-id="b7629-190">le texte réel</span><span class="sxs-lookup"><span data-stu-id="b7629-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="b7629-191">Exemple de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="b7629-191">JSON output example</span></span>
<span data-ttu-id="b7629-192">L’exemple de sortie suivant contient des informations générales sur la vidéo et plusieurs fragments vidéo.</span><span class="sxs-lookup"><span data-stu-id="b7629-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="b7629-193">Chaque fragment vidéo contient toutes les régions détectées par le processeur multimédia OCR selon la langue et l’orientation du texte choisies.</span><span class="sxs-lookup"><span data-stu-id="b7629-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="b7629-194">La région contient également chaque ligne de mot dans cette région, avec le texte et la position de cette ligne, et toutes les informations sur ce mot (contenu, position et niveau de confiance du mot).</span><span class="sxs-lookup"><span data-stu-id="b7629-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="b7629-195">En voici un exemple (avec mes commentaires).</span><span class="sxs-lookup"><span data-stu-id="b7629-195">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="b7629-196">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="b7629-196">.NET sample code</span></span>

<span data-ttu-id="b7629-197">Le programme suivant montre comment effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="b7629-197">The following program shows how to:</span></span>

1. <span data-ttu-id="b7629-198">Créer un élément multimédia et charger un fichier multimédia dans l’élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="b7629-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="b7629-199">Créer un travail avec un fichier de configuration OCR/prédéfini.</span><span class="sxs-lookup"><span data-stu-id="b7629-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="b7629-200">Télécharger les fichiers JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="b7629-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b7629-201">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7629-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b7629-202">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="b7629-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="b7629-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="b7629-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="b7629-204">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="b7629-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b7629-205">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b7629-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b7629-206">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="b7629-206">Related links</span></span>
[<span data-ttu-id="b7629-207">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="b7629-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

