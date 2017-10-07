---
title: texte aaaDigitize avec Azure Media Analytique OCR | Documents Microsoft
description: "Azure Media d’Analytique OCR (reconnaissance optique des caractères) vous permet de tooconvert le contenu de texte dans des fichiers vidéo en texte numérique interrogeable modifiable.  Cela vous permet d’extraction de hello tooautomate de métadonnées significatives à partir de signal vidéo de hello de votre support."
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
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="21df2-104">Utiliser le contenu de texte tooconvert Azure Media Analytique dans les fichiers vidéos en texte numérique</span><span class="sxs-lookup"><span data-stu-id="21df2-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="21df2-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="21df2-105">Overview</span></span>
<span data-ttu-id="21df2-106">Si vous devez tooextract texte contenu à partir de vos fichiers vidéo et générez un texte numérique modifiable, la recherche, vous devez utiliser Azure Media Analytique OCR (reconnaissance optique des caractères).</span><span class="sxs-lookup"><span data-stu-id="21df2-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="21df2-107">Ce processeur multimédia Azure détecte le contenu texte de vos fichiers vidéo et génère les fichiers texte à utiliser.</span><span class="sxs-lookup"><span data-stu-id="21df2-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="21df2-108">OCR permet de vous tooautomate hello d’extraction de métadonnées significatives à partir de signal vidéo de hello de votre support.</span><span class="sxs-lookup"><span data-stu-id="21df2-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="21df2-109">Lorsqu’il est utilisé conjointement avec un moteur de recherche, vous pouvez facilement votre support d’index en texte et améliorer la détectabilité hello de votre contenu.</span><span class="sxs-lookup"><span data-stu-id="21df2-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="21df2-110">Cela est particulièrement utile dans une vidéo contenant beaucoup de texte, comme un enregistrement vidéo ou une capture d’écran de diaporama.</span><span class="sxs-lookup"><span data-stu-id="21df2-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="21df2-111">Hello processeur OCR Azure est optimisé pour le texte numérique.</span><span class="sxs-lookup"><span data-stu-id="21df2-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="21df2-112">Hello **Azure Media OCR** processeur multimédia est actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="21df2-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="21df2-113">Cette rubrique fournit des détails sur **Azure Media OCR** et montre comment toouse avec Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="21df2-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="21df2-114">Pour plus d’informations et d’exemples, consultez [ce blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="21df2-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="21df2-115">Fichiers d'entrée OCR</span><span class="sxs-lookup"><span data-stu-id="21df2-115">OCR input files</span></span>
<span data-ttu-id="21df2-116">Fichiers vidéo.</span><span class="sxs-lookup"><span data-stu-id="21df2-116">Video files.</span></span> <span data-ttu-id="21df2-117">Actuellement, hello suivant les formats est pris en charge : MP4 et WMV MOV.</span><span class="sxs-lookup"><span data-stu-id="21df2-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="21df2-118">Configuration de la tâche</span><span class="sxs-lookup"><span data-stu-id="21df2-118">Task configuration</span></span>
<span data-ttu-id="21df2-119">Configuration de la tâche (préconfiguration).</span><span class="sxs-lookup"><span data-stu-id="21df2-119">Task configuration (preset).</span></span> <span data-ttu-id="21df2-120">Lors de la création d’une tâche **Azure Media OCR**, vous devez spécifier une présélection de configuration avec JSON ou XML.</span><span class="sxs-lookup"><span data-stu-id="21df2-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="21df2-121">moteur de reconnaissance optique des caractères Hello n’accepte qu’une région de l’image avec des pixels toomaximum 32000 40 pixels minimale comme une entrée valide dans les deux hauteur/largeur.</span><span class="sxs-lookup"><span data-stu-id="21df2-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="21df2-122">Descriptions des attributs</span><span class="sxs-lookup"><span data-stu-id="21df2-122">Attribute descriptions</span></span>
| <span data-ttu-id="21df2-123">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="21df2-123">Attribute name</span></span> | <span data-ttu-id="21df2-124">Description</span><span class="sxs-lookup"><span data-stu-id="21df2-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="21df2-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="21df2-125">AdvancedOutput</span></span>| <span data-ttu-id="21df2-126">Si vous définissez AdvancedOutput tootrue, la sortie JSON hello contiendra les données positionnelles pour chaque mot (dans Ajout toophrases et régions).</span><span class="sxs-lookup"><span data-stu-id="21df2-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="21df2-127">Si vous ne souhaitez pas toosee ces détails, définissez hello indicateur toofalse.</span><span class="sxs-lookup"><span data-stu-id="21df2-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="21df2-128">valeur par défaut de Hello est false.</span><span class="sxs-lookup"><span data-stu-id="21df2-128">hello default value is false.</span></span> <span data-ttu-id="21df2-129">Pour plus d’informations, consultez [ce blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="21df2-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="21df2-130">language</span><span class="sxs-lookup"><span data-stu-id="21df2-130">Language</span></span> |<span data-ttu-id="21df2-131">(facultatif) décrit le langage hello du texte pour le toolook.</span><span class="sxs-lookup"><span data-stu-id="21df2-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="21df2-132">Hello suivantes : détection automatique (par défaut), arabe, ChineseSimplified, sait, tchèque danois, néerlandais, anglais, finnois, Français, allemand, grec, hongrois, italien, japonais, coréen, norvégien, polonais, portugais, roumain, russe, SerbianCyrillic, SerbianLatin, slovaque, espagnol, suédois, turc.</span><span class="sxs-lookup"><span data-stu-id="21df2-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="21df2-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="21df2-133">TextOrientation</span></span> |<span data-ttu-id="21df2-134">(facultatif) décrit l’orientation de hello du texte pour le toolook.</span><span class="sxs-lookup"><span data-stu-id="21df2-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="21df2-135">« Gauche » signifie que hello en haut de toutes les lettres est pointé vers hello gauche.</span><span class="sxs-lookup"><span data-stu-id="21df2-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="21df2-136">Par défaut, le texte peut être affiché en mode « Up » (comme dans un livre).</span><span class="sxs-lookup"><span data-stu-id="21df2-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="21df2-137">Hello suivantes : détection automatique (par défaut), haut, droite, bas, gauche.</span><span class="sxs-lookup"><span data-stu-id="21df2-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="21df2-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="21df2-138">TimeInterval</span></span> |<span data-ttu-id="21df2-139">(facultatif) décrit le taux d’échantillonnage de hello.</span><span class="sxs-lookup"><span data-stu-id="21df2-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="21df2-140">La valeur par défaut est chaque demie seconde.</span><span class="sxs-lookup"><span data-stu-id="21df2-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="21df2-141">Format JSON – HH:mm:ss.SSS (par défaut : 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="21df2-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="21df2-142">Format XML – durée de la primitive W3C XSD (par défaut PT0.5)</span><span class="sxs-lookup"><span data-stu-id="21df2-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="21df2-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="21df2-143">DetectRegions</span></span> |<span data-ttu-id="21df2-144">(facultatif) Tableau d’objets DetectRegion spécifiant des zones dans les images vidéo hello dans le texte toodetect.</span><span class="sxs-lookup"><span data-stu-id="21df2-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="21df2-145">Un objet DetectRegion est constitué de hello quatre valeurs d’entier suivantes :</span><span class="sxs-lookup"><span data-stu-id="21df2-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="21df2-146">Gauche – pixels à partir de la marge de gauche hello</span><span class="sxs-lookup"><span data-stu-id="21df2-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="21df2-147">Haut – pixels à partir de la marge supérieure hello</span><span class="sxs-lookup"><span data-stu-id="21df2-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="21df2-148">Largeur : la largeur de la région de hello en pixels</span><span class="sxs-lookup"><span data-stu-id="21df2-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="21df2-149">Hauteur – la hauteur de la région de hello en pixels</span><span class="sxs-lookup"><span data-stu-id="21df2-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="21df2-150">Exemple de présélection JSON</span><span class="sxs-lookup"><span data-stu-id="21df2-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="21df2-151">Exemple de présélection XML</span><span class="sxs-lookup"><span data-stu-id="21df2-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="21df2-152">Fichiers de sortie OCR</span><span class="sxs-lookup"><span data-stu-id="21df2-152">OCR output files</span></span>
<span data-ttu-id="21df2-153">sortie Hello de processeur multimédia de OCR hello est un fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="21df2-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="21df2-154">Éléments hello JSON du fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="21df2-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="21df2-155">Hello OCR vidéo sortie fournit des données de temps segmenté sur les caractères de hello ont été trouvés dans votre vidéo.</span><span class="sxs-lookup"><span data-stu-id="21df2-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="21df2-156">Vous pouvez utiliser des attributs tels que la langue ou l’orientation dans toohone exactement les mots hello qui vous intéressent analyse.</span><span class="sxs-lookup"><span data-stu-id="21df2-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="21df2-157">sortie de Hello contient hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="21df2-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="21df2-158">Élément</span><span class="sxs-lookup"><span data-stu-id="21df2-158">Element</span></span> | <span data-ttu-id="21df2-159">Description</span><span class="sxs-lookup"><span data-stu-id="21df2-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21df2-160">Échelle de temps</span><span class="sxs-lookup"><span data-stu-id="21df2-160">Timescale</span></span> |<span data-ttu-id="21df2-161">« cycles » par seconde de la vidéo de hello</span><span class="sxs-lookup"><span data-stu-id="21df2-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="21df2-162">Offset</span><span class="sxs-lookup"><span data-stu-id="21df2-162">Offset</span></span> |<span data-ttu-id="21df2-163">décalage des horodatages.</span><span class="sxs-lookup"><span data-stu-id="21df2-163">time offset for timestamps.</span></span> <span data-ttu-id="21df2-164">Cette valeur sera toujours 0 dans la version 1.0 des API vidéo.</span><span class="sxs-lookup"><span data-stu-id="21df2-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="21df2-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="21df2-165">Framerate</span></span> |<span data-ttu-id="21df2-166">Images par seconde de hello vidéo</span><span class="sxs-lookup"><span data-stu-id="21df2-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="21df2-167">width</span><span class="sxs-lookup"><span data-stu-id="21df2-167">width</span></span> |<span data-ttu-id="21df2-168">largeur de la vidéo en pixels de hello</span><span class="sxs-lookup"><span data-stu-id="21df2-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="21df2-169">height</span><span class="sxs-lookup"><span data-stu-id="21df2-169">height</span></span> |<span data-ttu-id="21df2-170">hauteur de la vidéo en pixels de hello</span><span class="sxs-lookup"><span data-stu-id="21df2-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="21df2-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="21df2-171">Fragments</span></span> |<span data-ttu-id="21df2-172">tableau de segments de durée de vidéo dans le hello métadonnées sont mémorisé en bloc</span><span class="sxs-lookup"><span data-stu-id="21df2-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="21df2-173">start</span><span class="sxs-lookup"><span data-stu-id="21df2-173">start</span></span> |<span data-ttu-id="21df2-174">heure de début d’un fragment en « cycles »</span><span class="sxs-lookup"><span data-stu-id="21df2-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="21df2-175">duration</span><span class="sxs-lookup"><span data-stu-id="21df2-175">duration</span></span> |<span data-ttu-id="21df2-176">durée d’un fragment en « cycles »</span><span class="sxs-lookup"><span data-stu-id="21df2-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="21df2-177">interval</span><span class="sxs-lookup"><span data-stu-id="21df2-177">interval</span></span> |<span data-ttu-id="21df2-178">intervalle de chaque événement dans hello donné fragment</span><span class="sxs-lookup"><span data-stu-id="21df2-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="21df2-179">événements</span><span class="sxs-lookup"><span data-stu-id="21df2-179">events</span></span> |<span data-ttu-id="21df2-180">tableau contenant des régions</span><span class="sxs-lookup"><span data-stu-id="21df2-180">array containing regions</span></span> |
| <span data-ttu-id="21df2-181">region</span><span class="sxs-lookup"><span data-stu-id="21df2-181">region</span></span> |<span data-ttu-id="21df2-182">objet représentant des mots ou expressions détectés</span><span class="sxs-lookup"><span data-stu-id="21df2-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="21df2-183">Langage</span><span class="sxs-lookup"><span data-stu-id="21df2-183">language</span></span> |<span data-ttu-id="21df2-184">langue du texte hello détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="21df2-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="21df2-185">orientation</span><span class="sxs-lookup"><span data-stu-id="21df2-185">orientation</span></span> |<span data-ttu-id="21df2-186">orientation du texte hello détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="21df2-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="21df2-187">lignes</span><span class="sxs-lookup"><span data-stu-id="21df2-187">lines</span></span> |<span data-ttu-id="21df2-188">tableau de lignes de texte détecté dans une région</span><span class="sxs-lookup"><span data-stu-id="21df2-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="21df2-189">texte</span><span class="sxs-lookup"><span data-stu-id="21df2-189">text</span></span> |<span data-ttu-id="21df2-190">texte Hello</span><span class="sxs-lookup"><span data-stu-id="21df2-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="21df2-191">Exemple de sortie JSON</span><span class="sxs-lookup"><span data-stu-id="21df2-191">JSON output example</span></span>
<span data-ttu-id="21df2-192">Hello exemple de sortie suivant contient des informations générales vidéo hello et plusieurs fragments vidéo.</span><span class="sxs-lookup"><span data-stu-id="21df2-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="21df2-193">Dans chaque fragment de vidéo, il contient toutes les régions sont détectée par le Pack d’administration OCR avec le langage de hello et son orientation de texte.</span><span class="sxs-lookup"><span data-stu-id="21df2-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="21df2-194">région de Hello contient également toutes les lignes dans cette zone de texte, position de ligne hello et chaque mot d’informations (contenu word, position et confiance) dans cette ligne de la ligne hello word.</span><span class="sxs-lookup"><span data-stu-id="21df2-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="21df2-195">Hello suit est un exemple et placer des commentaires en ligne.</span><span class="sxs-lookup"><span data-stu-id="21df2-195">hello following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
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

## <a name="net-sample-code"></a><span data-ttu-id="21df2-196">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="21df2-196">.NET sample code</span></span>

<span data-ttu-id="21df2-197">suivant de Hello programme montre comment :</span><span class="sxs-lookup"><span data-stu-id="21df2-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="21df2-198">Créer un élément multimédia et téléchargez un fichier multimédia en ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="21df2-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="21df2-199">Créer un travail avec un fichier de configuration OCR/prédéfini.</span><span class="sxs-lookup"><span data-stu-id="21df2-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="21df2-200">Télécharger les fichiers JSON de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="21df2-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="21df2-201">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21df2-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="21df2-202">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="21df2-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="21df2-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="21df2-203">Example</span></span>

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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="21df2-204">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="21df2-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21df2-205">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="21df2-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="21df2-206">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="21df2-206">Related links</span></span>
[<span data-ttu-id="21df2-207">Vue d’ensemble d’Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="21df2-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

