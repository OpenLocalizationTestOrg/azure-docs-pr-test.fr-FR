---
title: "Incorporation d’une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js | Microsoft Docs"
description: "Cette rubrique montre comment incorporer une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js."
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
ms.openlocfilehash: 27ce6325773ba1f9fd9cd9ab9e07ea9f5e2488ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="6c7a3-103">Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js</span><span class="sxs-lookup"><span data-stu-id="6c7a3-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="6c7a3-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c7a3-104">Overview</span></span>
<span data-ttu-id="6c7a3-105">MPEG-DASH est une norme ISO pour la diffusion en continu adaptative de contenu vidéo, qui offre des avantages significatifs pour ceux qui souhaitent proposer un résultat de diffusion vidéo en continu adaptative de haute qualité.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-105">MPEG-DASH is an ISO standard for the adaptive streaming of video content, which offers significant benefits for those who wish to deliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="6c7a3-106">Avec MPEG-DASH, le flux vidéo est automatiquement ramené à une définition inférieure quand le réseau est encombré.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-106">With MPEG-DASH, the video stream will automatically drop to a lower definition when the network becomes congested.</span></span> <span data-ttu-id="6c7a3-107">Cela réduit le risque pour un utilisateur de voir une vidéo « interrompue » pendant que le lecteur télécharge les quelques secondes suivantes à lire (également appelée mise en mémoire tampon).</span><span class="sxs-lookup"><span data-stu-id="6c7a3-107">This reduces the likelihood of the viewer seeing a "paused" video while the player downloads the next few seconds to play (aka buffering).</span></span> <span data-ttu-id="6c7a3-108">À mesure que l'encombrement du réseau diminue, le lecteur vidéo renvoie à son tour un flux de qualité supérieure.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-108">As network congestion reduces, the video player will in turn return to a higher quality stream.</span></span> <span data-ttu-id="6c7a3-109">Cette capacité d'adaptation de la bande passante requise entraîne également un temps de départ plus rapide pour la vidéo.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-109">This ability to adapt the bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="6c7a3-110">Cela signifie que les premières secondes peuvent être lues dans un segment de moindre qualité rapide à télécharger, puis que la qualité s'améliore une fois le contenu suffisant mis en mémoire tampon.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-110">That means that the first few seconds can be played in a fast-to-download lower quality segment and then step up to a higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="6c7a3-111">Dash.js est un lecteur de vidéo MPEG-DASH open source écrit en JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="6c7a3-112">Son objectif est de fournir un lecteur robuste, inter-plateformes qui peut être réutilisé librement dans les applications qui requièrent une lecture vidéo.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-112">Its goal is to provide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="6c7a3-113">Il assure la lecture MPEG-DASH dans n’importe quel navigateur prenant en charge W3C Media Source Extensions (MSE) aujourd’hui, à savoir Chrome, Microsoft Edge et IE11 (d’autres navigateurs ont indiqué leur intention de prendre en charge MSE).</span><span class="sxs-lookup"><span data-stu-id="6c7a3-113">It provides MPEG-DASH playback in any browser that supports the W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent to support MSE).</span></span> <span data-ttu-id="6c7a3-114">Pour plus d'informations sur DASH.js, consultez le référentiel dash.js GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-114">For more information about DASH.js, js see the GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="6c7a3-115">Création d'un lecteur vidéo de diffusion en continu basé sur le navigateur</span><span class="sxs-lookup"><span data-stu-id="6c7a3-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="6c7a3-116">Pour créer une page web simple qui affiche un lecteur vidéo avec les contrôles courants comme Lecture, Pause, Retour rapide, etc., vous devez effectuer les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-116">To create a simple web page that displays a video player with the expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="6c7a3-117">Créer une page HTML</span><span class="sxs-lookup"><span data-stu-id="6c7a3-117">Create an HTML page</span></span>
2. <span data-ttu-id="6c7a3-118">Ajouter la balise vidéo</span><span class="sxs-lookup"><span data-stu-id="6c7a3-118">Add the video tag</span></span>
3. <span data-ttu-id="6c7a3-119">Ajouter le lecteur dash.js</span><span class="sxs-lookup"><span data-stu-id="6c7a3-119">Add the dash.js player</span></span>
4. <span data-ttu-id="6c7a3-120">Initialiser le lecteur</span><span class="sxs-lookup"><span data-stu-id="6c7a3-120">Initialize the player</span></span>
5. <span data-ttu-id="6c7a3-121">Ajouter un style CSS</span><span class="sxs-lookup"><span data-stu-id="6c7a3-121">Add some CSS style</span></span>
6. <span data-ttu-id="6c7a3-122">Afficher les résultats dans un navigateur qui implémente MSE</span><span class="sxs-lookup"><span data-stu-id="6c7a3-122">View the results in a browser that implements MSE</span></span>

<span data-ttu-id="6c7a3-123">L'initialisation du lecteur peut être effectuée en seulement quelques lignes de code JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-123">Initializing the player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="6c7a3-124">À l'aide de dash.js, il est vraiment très simple d'incorporer une vidéo MPEG-DASH dans vos applications basées sur le navigateur.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-124">Using dash.js, it really is that simple to embed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-the-html-page"></a><span data-ttu-id="6c7a3-125">Création de la page HTML</span><span class="sxs-lookup"><span data-stu-id="6c7a3-125">Creating the HTML Page</span></span>
<span data-ttu-id="6c7a3-126">La première étape consiste à créer une page HTML standard qui contient l’élément **video**, à enregistrer ce fichier sous basicPlayer.html, comme l’illustre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-126">The first step is to create a standard HTML page containing the **video** element, save this file as basicPlayer.html, as the following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-the-dashjs-player"></a><span data-ttu-id="6c7a3-127">Ajout du lecteur DASH.js</span><span class="sxs-lookup"><span data-stu-id="6c7a3-127">Adding the DASH.js Player</span></span>
<span data-ttu-id="6c7a3-128">Pour ajouter l'implémentation de référence dash.js à l'application, vous devez extraire le fichier dash.all.js de la version 1.0 du projet dash.js.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-128">To add the dash.js reference implementation to the application, you’ll need to grab the dash.all.js file from the 1.0 release of dash.js project.</span></span> <span data-ttu-id="6c7a3-129">Celui-ci doit être enregistré dans le dossier JavaScript de votre application.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-129">This should be saved in the JavaScript folder of your application.</span></span> <span data-ttu-id="6c7a3-130">Ce fichier est un fichier de convenance qui rassemble tout le code dash.js requis dans un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-130">This file is a convenience file that pulls together all the necessary dash.js code into a single file.</span></span> <span data-ttu-id="6c7a3-131">En examinant le contenu du référentiel dash.js, vous trouverez les fichiers individuels, le code de test, entre autres, mais si vous voulez seulement utiliser dash.js, alors c'est du fichier dash.all.js dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-131">If you have a look around the dash.js repository, you will find the individual files, test code and much more, but if all you want to do is use dash.js, then the dash.all.js file is what you need.</span></span>

<span data-ttu-id="6c7a3-132">Pour ajouter le lecteur dash.js à vos applications, ajoutez une balise de script à la section d'en-tête de basicPlayer.html :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-132">To add the dash.js player to your applications, add a script tag to the head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="6c7a3-133">Ensuite, créez une fonction pour initialiser le lecteur pendant le chargement de la page.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-133">Next, create a function to initialize the player when the page loads.</span></span> <span data-ttu-id="6c7a3-134">Ajoutez le script suivant après la ligne dans laquelle vous chargez dash.all.js :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-134">Add the following script after the line in which you load dash.all.js:</span></span>

    <script>
    // setup the video element and attach it to the Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="6c7a3-135">Cette fonction crée d'abord un DashContext.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-135">This function first creates a DashContext.</span></span> <span data-ttu-id="6c7a3-136">Celui-ci permet de configurer l'application pour un environnement d'exécution spécifique.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-136">This is used to configure the application for a specific runtime environment.</span></span> <span data-ttu-id="6c7a3-137">D'un point de vue technique, il définit les classes que l'infrastructure d'injection de dépendance doit utiliser pour construire l'application.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-137">From a technical point of view, it defines the classes that the dependency injection framework should use when constructing the application.</span></span> <span data-ttu-id="6c7a3-138">Dans la plupart des cas, vous utiliserez Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="6c7a3-139">Ensuite, instanciez la classe principale de l'infrastructure dash.js, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-139">Next, instantiate the primary class of the dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="6c7a3-140">Cette classe contient les principales méthodes requises telles que la lecture et la mise en pause, gère la relation avec l'élément vidéo et gère également l'interprétation du fichier MPD (Media Presentation Description) qui décrit la vidéo à lire.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-140">This class contains the core methods needed such as play and pause, manages the relationship with the video element and also manages the interpretation of the Media Presentation Description (MPD) file which describes the video to be played.</span></span>

<span data-ttu-id="6c7a3-141">La fonction startup() de la classe MediaPlayer est appelée pour s'assurer que le lecteur est prêt à lire la vidéo.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-141">The startup() function of the MediaPlayer class is called to ensure that the player is ready to play video.</span></span> <span data-ttu-id="6c7a3-142">Entre autres choses, cette fonction garantit que toutes les classes nécessaires (comme défini par le contexte) ont été chargées.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-142">Amongst other things this function ensures that all the necessary classes (as defined by the context) have been loaded.</span></span> <span data-ttu-id="6c7a3-143">Une fois que le lecteur est prêt, vous pouvez y associer l'élément vidéo à l'aide de la fonction attachView().</span><span class="sxs-lookup"><span data-stu-id="6c7a3-143">Once the player is ready, you can attach the video element to it using the attachView() function.</span></span> <span data-ttu-id="6c7a3-144">Cela permet à MediaPlayer d'injecter le flux vidéo dans l'élément et également de contrôler la lecture si besoin.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-144">This enables the MediaPlayer to inject the video stream into the element and also control playback as necessary.</span></span>

<span data-ttu-id="6c7a3-145">Passez l'URL du fichier MPD à MediaPlayer pour l'informer sur la vidéo à lire. La fonction setupVideo() tout juste créée devra être exécutée une fois la page entièrement chargée.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-145">Pass the URL of the MPD file to the MediaPlayer so that it knows about the video it is expected to play.The setupVideo() function just created will need to be executed once the page has fully loaded.</span></span> <span data-ttu-id="6c7a3-146">Pour cela, utilisez l'événement onload de l'élément body.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-146">Do this by using the onload event of the body element.</span></span> <span data-ttu-id="6c7a3-147">Remplacez votre élément <body> par :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="6c7a3-148">Enfin, définissez la taille de l'élément vidéo à l'aide de CSS.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-148">Finally, set the size of the video element using CSS.</span></span> <span data-ttu-id="6c7a3-149">Dans un environnement de diffusion en continu adaptative, cela s'avère particulièrement important car la taille de la vidéo lue peut changer au gré de l'adaptation de la lecture aux conditions changeantes du réseau.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-149">In an adaptive streaming environment, this is especially important because the size of the video being played may change as playback adapts to changing network conditions.</span></span> <span data-ttu-id="6c7a3-150">Cette démonstration simple force l'élément vidéo à constituer 80 % de la fenêtre de navigateur disponible en ajoutant le fichier CSS suivant à la section head de la page :</span><span class="sxs-lookup"><span data-stu-id="6c7a3-150">In this simple demo simply force the video element to be 80% of the available browser window by adding the following CSS to the head section of the page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="6c7a3-151">Lecture d'une vidéo</span><span class="sxs-lookup"><span data-stu-id="6c7a3-151">Playing a Video</span></span>
<span data-ttu-id="6c7a3-152">Pour lire une vidéo, pointez votre navigateur sur le fichier basicPlayback.html et cliquez sur Lire sur le lecteur vidéo affiché.</span><span class="sxs-lookup"><span data-stu-id="6c7a3-152">To play a video, point your browser at the basicPlayback.html file and click play on the video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6c7a3-153">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="6c7a3-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c7a3-154">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="6c7a3-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6c7a3-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6c7a3-155">See Also</span></span>
[<span data-ttu-id="6c7a3-156">Développement d'applications de lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="6c7a3-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="6c7a3-157">Référentiel dash.js GitHub</span><span class="sxs-lookup"><span data-stu-id="6c7a3-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

