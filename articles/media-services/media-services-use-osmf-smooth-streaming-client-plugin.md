---
title: aaaSmooth plug-in de diffusion en continu pour hello Open Source Media Framework
description: "Découvrez comment toouse hello Azure Media Services Smooth Streaming de plug-in pour hello Adobe Open Source Media Framework."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Comment tooUse hello Microsoft Smooth Streaming plug-in pour hello Adobe Open Source Media Framework
## <a name="overview"></a>Vue d'ensemble
Hello plug-in de diffusion en continu lisse Microsoft pour Open Source Media Framework 2.0 (SS pour OSMF) étend les fonctionnalités par défaut de hello de OSMF et ajoute toonew de lecture de contenu Microsoft de la diffusion en continu lisse OSMF existant lecteurs. plug-in Hello ajoute également la diffusion en continu lisse lecture fonctionnalités tooStrobe Media Playback (SMP).

SS pour OSMF comprend deux versions du plug-in :

* Plug-in Smooth Streaming statique pour OSMF (.swc)
* Plug-in Smooth Streaming dynamique pour OSMF (.swf)

Ce document suppose que le lecteur de hello a une connaissance de OSMF et OSMF plug-ins. Pour plus d’informations sur OSMF, veuillez consulter la documentation de hello hello [site officiel de OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Plug-in Smooth Streaming pour OSMF 2.0
plug-in Hello prend en charge la lecture du contenu de diffusion en continu à la demande et chargement avec hello suivant de fonctionnalités :

* Lecture Smooth Streaming à la demande (lecture, pause, avance rapide, arrêt)
* Lecture Smooth Streaming en direct (lecture)
* Fonctions DVR en direct (pause, avance rapide, lecture DVR, retour au direct)
* Prise en charge des codecs vidéo - H.264
* Prise en charge des codecs audio - AAC
* Plusieurs langues avec API OSMF intégrées
* Sélection de la qualité de lecture maximale avec API OSMF intégrées
* Sous-titres Sidecar avec plug-in de sous-titres OSMF
* Adobe&reg; Flash&reg; Player 11.4 ou version ultérieure.
* Cette version ne prend en charge qu'OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Fonctionnalités prises en charge et problèmes connus
Pour obtenir une liste complète des fonctionnalités prises en charge, les fonctionnalités prises en charge et les problèmes connus, consultez trop[ce document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Hello de chargement du plug-in
Les plug-ins OSMF peuvent être chargés de façon statique (à la compilation) ou dynamique (à l'exécution). un plug-in de diffusion en continu lisse à Hello pour le téléchargement OSMF inclut des versions statiques et dynamiques.

* Chargement statique : tooload de manière statique, un fichier de bibliothèque statique (SWC) est requis. Plug-ins statiques sont ajoutés en tant que référence toohello projets et fusion à l’intérieur de la sortie finale hello de fichiers au moment de la compilation hello.
* Chargement dynamique : tooload dynamiquement, un fichier (SWF) précompilé est requis. Plug-ins dynamiques sont chargés dans le runtime de hello et pas inclus dans la sortie du projet hello. (Résultat compilé) Les plug-ins dynamiques peuvent être chargés avec les protocoles HTTP ou FILE.

Pour plus d’informations sur le chargement statique et dynamique, consultez officielle de hello [page de plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>Chargement de SS pour OSMF statique
extrait de code Hello ci-dessous montre comment les tooload hello plug-in SS pour OSMF statiquement et lire une vidéo de base à l’aide de la classe de OSMF MediaFactory. Avant d’inclure hello SS pour le code OSMF, assurez-vous que référence de projet hello inclut des plug-in de statique hello « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc ».

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a>Chargement de SS pour OSMF dynamique
extrait de code Hello ci-dessous montre comment les tooload hello dynamiquement les plug-in SS pour OSMF et lire une vidéo de base à l’aide de la classe de OSMF MediaFactory hello. Avant d’inclure hello SS pour le code OSMF, copier dossier du projet toohello hello « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf » plug-in dynamique si vous souhaitez tooload à l’aide du protocole de fichier, ou copiez sous un serveur web pour la charge HTTP. Il n’existe aucun tooinclude besoin « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc » dans les références de projet hello.

package {

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Lecture du média STROBE avec hello plug-in de SS ODMF dynamique
Hello Smooth Streaming pour OSMF les plug-in dynamique est compatible avec [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). Vous pouvez utiliser hello SS pour tooSMP de lecture de contenu de diffusion en continu lisse OSMF plug-in tooadd. toodo, copie « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf » sous un serveur web pour la charge HTTP à l’aide de hello suivant les étapes :

1. Parcourir hello [page Installation de la lecture du média Strobe](http://osmf.org/dev/2.0gm/setup.html). 
2. Permet de définir hello src tooa Smooth Streaming source, (par exemple, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Apporter des modifications de configuration hello souhaité et cliquez sur Afficher un aperçu et mise à jour.
   
   **Remarque** Votre serveur Web de contenu doit disposer d'un fichier crossdomain.xml valide. 
4. Copiez et collez hello code tooa simple page HTML à l’aide de votre éditeur de texte, tels que Bonjour l’exemple suivant :

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. Ajouter toohello du plug-in OSMF de diffusion en continu lisse incorporer le code et l’enregistrer.
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. Enregistrez votre page HTML et publier un serveur web de tooa. Parcourir toohello publié la page web à l’aide de vos favoris Flash&reg; lecteur activé le navigateur Internet (Internet Explorer, Chrome, Firefox, etc.).
3. Accédez au contenu Smooth Streaming dans Adobe&reg; Flash&reg; Player.

Pour plus d’informations sur le développement de OSMF général, consultez officielle de hello [page de développement OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Plug-in de diffusion en continu adaptative Microsoft pour la mise à jour OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

