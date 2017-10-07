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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js
## <a name="overview"></a>Vue d'ensemble
MPEG-DASH est une norme ISO pour hello adaptative de diffusion en continu de contenu vidéo, qui offre des avantages significatifs pour ceux qui souhaitent vidéo haute qualité, adaptive toodeliver sortie de diffusion en continu. Avec MPEG-DASH, les flux vidéo hello supprimera automatiquement définition inférieure de tooa lorsque le réseau de hello devienne encombré. Cela réduit la probabilité de hello de visionneuse hello voir une vidéo « suspendue » pendant que le lecteur hello télécharge hello ensuite quelques secondes tooplay (également appelé mise en mémoire tampon). Comme réduit la congestion du réseau, le lecteur vidéo hello retourne à son tour tooa supérieure qualité de flux. Cette possibilité tooadapt hello la bande passante requise entraîne également une heure de début plus rapide pour la vidéo. Que signifie que hello quelques secondes peut être lus dans un segment de qualité inférieure rapide au téléchargement et puis intensifier tooa une qualité supérieure, une fois que le contenu suffisamment a été mis en mémoire tampon.

Dash.js est un lecteur de vidéo MPEG-DASH open source écrit en JavaScript. Son objectif est tooprovide un lecteur robust, inter-plateformes qui peut être réutilisé librement dans les applications qui nécessitent la lecture vidéo. Il fournit la lecture MPEG-DASH dans n’importe quel navigateur prenant en charge hello W3C Media Source Extensions (MSE), c'est-à-dire aujourd'hui Chrome, Microsoft Edge et IE11 (d’autres navigateurs ont indiqué leur intention toosupport MSE). Pour plus d’informations sur DASH.js, js voir référentiel dash.js de GitHub hello.

## <a name="creating-a-browser-based-streaming-video-player"></a>Création d'un lecteur vidéo de diffusion en continu basé sur le navigateur
toocreate une page web simple qui affiche un lecteur vidéo avec hello attendu contrôle ces lecture, pause, rembobiner, etc., vous devez :

1. Créer une page HTML
2. Ajoutez la balise vidéo de hello
3. Ajouter le lecteur hello dash.js
4. Initialiser le lecteur hello
5. Ajouter un style CSS
6. Afficher les résultats dans un navigateur qui implémente MSE hello

L’initialisation du lecteur de hello peut être effectué en quelques lignes de code JavaScript. À l’aide de dash.js, il est réellement que la vidéo simple tooembed MPEG-DASH dans vos applications basées sur un navigateur.

## <a name="creating-hello-html-page"></a>Création de hello HTML Page
première étape de Hello est page toocreate un code HTML standard contenant hello **vidéo** élément, enregistrez ce fichier sous basicPlayer.html, en tant que hello l’exemple suivant illustre :

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Ajout de hello DASH.js lecteur
tooadd hello dash.js implémentation toohello d’application de référence, vous aurez besoin de fichier de dash.all.js hello toograb à partir de la version 1.0 de hello du projet de dash.js. Il doit être enregistré dans le dossier de JavaScript hello de votre application. Ce fichier est un fichier pratique qui regroupe tout le code hello dash.js nécessaires dans un seul fichier. Si vous disposez d’un coup de œil autour de référentiel dash.js de hello, vous allez trouver hello des fichiers individuels, le code de test et bien plus encore, mais si vous souhaitez toodo est utiliser dash.js, fichier de dash.all.js hello est ce dont vous avez besoin.

tooadd hello dash.js tooyour des applications de lecteur, ajoutez une section script balise toohello head de basicPlayer.html :

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Ensuite, créez un lecteur de hello tooinitialize fonction lorsque le chargement de la page hello. Ajoutez hello script suivant après la ligne hello dans lequel vous chargez dash.all.js :

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

Cette fonction crée d'abord un DashContext. Il s’agit d’application de hello tooconfigure utilisés pour un environnement d’exécution spécifique. À partir d’un point de vue technique, il définit hello classes hello infrastructure d’injection de dépendance doivent utiliser lors de la construction d’application hello. Dans la plupart des cas, vous utiliserez Dash.di.DashContext.

Ensuite, instancier la classe principale de hello du framework dash.js de hello, MediaPlayer. Cette classe contient core hello méthodes nécessaires telles que lire et suspendre, gère les relation hello avec un élément de vidéo hello et gère également interprétation hello du fichier de Description de présentation multimédia (MPD) hello qui décrit hello vidéo toobe est lu.

Hello startup() Hello MediaPlayer classe est appelée tooensure joueur hello est prêt tooplay vidéo. Entre autres, cette fonction permet de s’assurer que toutes les classes nécessaires hello (comme défini par le contexte de hello) ont été chargés. Une fois que le lecteur hello est prêt, vous pouvez attacher hello tooit d’élément vidéo à l’aide de la fonction de attachView() hello. Ainsi les flux vidéo de hello MediaPlayer tooinject hello en élément de hello et également contrôler la lecture en tant que nécessaire.

Passer des URL hello de hello MPD fichier toohello MediaPlayer, afin qu’il connaît hello vidéo est censé venez de créer (fonction) setupVideo() tooplay.hello devez toobe exécuté une fois la page de hello a complètement chargé. Cela à l’aide d’événements d’onload hello de l’élément de corps hello. Remplacez votre élément <body> par :

    <body onload="setupVideo()">

Enfin, définissez taille hello d’élément de vidéo hello à l’aide de CSS. Dans un environnement de diffusion en continu ADAPTATIF, cela est particulièrement important car taille hello Hello vidéo en cours de lecture peut changer que la lecture s’adapte toochanging les conditions de réseau. Dans cette démonstration simple simplement forcer hello élément vidéo toobe 80 % de la fenêtre du navigateur disponible hello en ajoutant hello suivant toohello principal la section CSS de la page de hello :

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Lecture d'une vidéo
tooplay une vidéo, pointez votre navigateur dans le fichier de basicPlayback.html hello et cliquez sur Lire sur le lecteur vidéo hello affiché.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Développement d'applications de lecteur vidéo](media-services-develop-video-players.md)

[Référentiel dash.js GitHub](https://github.com/Dash-Industry-Forum/dash.js) 

