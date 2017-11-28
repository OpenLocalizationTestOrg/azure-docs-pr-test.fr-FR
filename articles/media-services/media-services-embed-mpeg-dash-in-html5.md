---
title: "aaaEmbedding une vidéo de diffusion en continu adaptative MPEG-DASH dans une Application HTML5 avec DASH.js | Documents Microsoft"
description: "Cette rubrique montre comment tooembed une vidéo de diffusion en continu adaptative MPEG-DASH dans une Application HTML5 avec DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="d8bd1-103">Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js</span><span class="sxs-lookup"><span data-stu-id="d8bd1-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="d8bd1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d8bd1-104">Overview</span></span>
<span data-ttu-id="d8bd1-105">MPEG-DASH est une norme ISO pour hello adaptative de diffusion en continu de contenu vidéo, qui offre des avantages significatifs pour ceux qui souhaitent vidéo haute qualité, adaptive toodeliver sortie de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="d8bd1-106">Avec MPEG-DASH, les flux vidéo hello supprimera automatiquement définition inférieure de tooa lorsque le réseau de hello devienne encombré.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="d8bd1-107">Cela réduit la probabilité de hello de visionneuse hello voir une vidéo « suspendue » pendant que le lecteur hello télécharge hello ensuite quelques secondes tooplay (également appelé mise en mémoire tampon).</span><span class="sxs-lookup"><span data-stu-id="d8bd1-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="d8bd1-108">Comme réduit la congestion du réseau, le lecteur vidéo hello retourne à son tour tooa supérieure qualité de flux.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="d8bd1-109">Cette possibilité tooadapt hello la bande passante requise entraîne également une heure de début plus rapide pour la vidéo.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="d8bd1-110">Que signifie que hello quelques secondes peut être lus dans un segment de qualité inférieure rapide au téléchargement et puis intensifier tooa une qualité supérieure, une fois que le contenu suffisamment a été mis en mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="d8bd1-111">Dash.js est un lecteur de vidéo MPEG-DASH open source écrit en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="d8bd1-112">Son objectif est tooprovide un lecteur robust, inter-plateformes qui peut être réutilisé librement dans les applications qui nécessitent la lecture vidéo.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="d8bd1-113">Il fournit la lecture MPEG-DASH dans n’importe quel navigateur prenant en charge hello W3C Media Source Extensions (MSE), c'est-à-dire aujourd'hui Chrome, Microsoft Edge et IE11 (d’autres navigateurs ont indiqué leur intention toosupport MSE).</span><span class="sxs-lookup"><span data-stu-id="d8bd1-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="d8bd1-114">Pour plus d’informations sur DASH.js, js voir référentiel dash.js de GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="d8bd1-115">Création d'un lecteur vidéo de diffusion en continu basé sur le navigateur</span><span class="sxs-lookup"><span data-stu-id="d8bd1-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="d8bd1-116">toocreate une page web simple qui affiche un lecteur vidéo avec hello attendu contrôle ces lecture, pause, rembobiner, etc., vous devez :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="d8bd1-117">Créer une page HTML</span><span class="sxs-lookup"><span data-stu-id="d8bd1-117">Create an HTML page</span></span>
2. <span data-ttu-id="d8bd1-118">Ajoutez la balise vidéo de hello</span><span class="sxs-lookup"><span data-stu-id="d8bd1-118">Add hello video tag</span></span>
3. <span data-ttu-id="d8bd1-119">Ajouter le lecteur hello dash.js</span><span class="sxs-lookup"><span data-stu-id="d8bd1-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="d8bd1-120">Initialiser le lecteur hello</span><span class="sxs-lookup"><span data-stu-id="d8bd1-120">Initialize hello player</span></span>
5. <span data-ttu-id="d8bd1-121">Ajouter un style CSS</span><span class="sxs-lookup"><span data-stu-id="d8bd1-121">Add some CSS style</span></span>
6. <span data-ttu-id="d8bd1-122">Afficher les résultats dans un navigateur qui implémente MSE hello</span><span class="sxs-lookup"><span data-stu-id="d8bd1-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="d8bd1-123">L’initialisation du lecteur de hello peut être effectué en quelques lignes de code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="d8bd1-124">À l’aide de dash.js, il est réellement que la vidéo simple tooembed MPEG-DASH dans vos applications basées sur un navigateur.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="d8bd1-125">Création de hello HTML Page</span><span class="sxs-lookup"><span data-stu-id="d8bd1-125">Creating hello HTML Page</span></span>
<span data-ttu-id="d8bd1-126">première étape de Hello est page toocreate un code HTML standard contenant hello **vidéo** élément, enregistrez ce fichier sous basicPlayer.html, en tant que hello l’exemple suivant illustre :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="d8bd1-127">Ajout de hello DASH.js lecteur</span><span class="sxs-lookup"><span data-stu-id="d8bd1-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="d8bd1-128">tooadd hello dash.js implémentation toohello d’application de référence, vous aurez besoin de fichier de dash.all.js hello toograb à partir de la version 1.0 de hello du projet de dash.js.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="d8bd1-129">Il doit être enregistré dans le dossier de JavaScript hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="d8bd1-130">Ce fichier est un fichier pratique qui regroupe tout le code hello dash.js nécessaires dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="d8bd1-131">Si vous disposez d’un coup de œil autour de référentiel dash.js de hello, vous allez trouver hello des fichiers individuels, le code de test et bien plus encore, mais si vous souhaitez toodo est utiliser dash.js, fichier de dash.all.js hello est ce dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="d8bd1-132">tooadd hello dash.js tooyour des applications de lecteur, ajoutez une section script balise toohello head de basicPlayer.html :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="d8bd1-133">Ensuite, créez un lecteur de hello tooinitialize fonction lorsque le chargement de la page hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="d8bd1-134">Ajoutez hello script suivant après la ligne hello dans lequel vous chargez dash.all.js :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="d8bd1-135">Cette fonction crée d'abord un DashContext.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-135">This function first creates a DashContext.</span></span> <span data-ttu-id="d8bd1-136">Il s’agit d’application de hello tooconfigure utilisés pour un environnement d’exécution spécifique.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="d8bd1-137">À partir d’un point de vue technique, il définit hello classes hello infrastructure d’injection de dépendance doivent utiliser lors de la construction d’application hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="d8bd1-138">Dans la plupart des cas, vous utiliserez Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="d8bd1-139">Ensuite, instancier la classe principale de hello du framework dash.js de hello, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="d8bd1-140">Cette classe contient core hello méthodes nécessaires telles que lire et suspendre, gère les relation hello avec un élément de vidéo hello et gère également interprétation hello du fichier de Description de présentation multimédia (MPD) hello qui décrit hello vidéo toobe est lu.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="d8bd1-141">Hello startup() Hello MediaPlayer classe est appelée tooensure joueur hello est prêt tooplay vidéo.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="d8bd1-142">Entre autres, cette fonction permet de s’assurer que toutes les classes nécessaires hello (comme défini par le contexte de hello) ont été chargés.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="d8bd1-143">Une fois que le lecteur hello est prêt, vous pouvez attacher hello tooit d’élément vidéo à l’aide de la fonction de attachView() hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="d8bd1-144">Ainsi les flux vidéo de hello MediaPlayer tooinject hello en élément de hello et également contrôler la lecture en tant que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="d8bd1-145">Passer des URL hello de hello MPD fichier toohello MediaPlayer, afin qu’il connaît hello vidéo est censé venez de créer (fonction) setupVideo() tooplay.hello devez toobe exécuté une fois la page de hello a complètement chargé.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="d8bd1-146">Cela à l’aide d’événements d’onload hello de l’élément de corps hello.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="d8bd1-147">Remplacez votre élément <body> par :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="d8bd1-148">Enfin, définissez taille hello d’élément de vidéo hello à l’aide de CSS.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="d8bd1-149">Dans un environnement de diffusion en continu ADAPTATIF, cela est particulièrement important car taille hello Hello vidéo en cours de lecture peut changer que la lecture s’adapte toochanging les conditions de réseau.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="d8bd1-150">Dans cette démonstration simple simplement forcer hello élément vidéo toobe 80 % de la fenêtre du navigateur disponible hello en ajoutant hello suivant toohello principal la section CSS de la page de hello :</span><span class="sxs-lookup"><span data-stu-id="d8bd1-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="d8bd1-151">Lecture d'une vidéo</span><span class="sxs-lookup"><span data-stu-id="d8bd1-151">Playing a Video</span></span>
<span data-ttu-id="d8bd1-152">tooplay une vidéo, pointez votre navigateur dans le fichier de basicPlayback.html hello et cliquez sur Lire sur le lecteur vidéo hello affiché.</span><span class="sxs-lookup"><span data-stu-id="d8bd1-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d8bd1-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d8bd1-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d8bd1-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d8bd1-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="d8bd1-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d8bd1-155">See Also</span></span>
[<span data-ttu-id="d8bd1-156">Développement d'applications de lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="d8bd1-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="d8bd1-157">Référentiel dash.js GitHub</span><span class="sxs-lookup"><span data-stu-id="d8bd1-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

