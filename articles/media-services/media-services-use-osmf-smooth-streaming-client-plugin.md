---
title: Plug-in Smooth Streaming pour Open Source Media Framework
description: "Apprenez à utiliser le plug-in Smooth Streaming d'Azure Media Services pour Adobe Open Source Media Framework."
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a>Utilisation du plug-in Microsoft Smooth Streaming pour Adobe Open Source Media Framework
## <a name="overview"></a>Vue d'ensemble
Le plug-in Microsoft Smooth Streaming pour Open Source Media Framework 2.0 (SS pour OSMF) étend les capacités par défaut d'OSMF et ajoute la lecture de contenu Microsoft Smooth Streaming aux lecteurs OSMF, qu'ils soient nouveaux ou existants. Il ajoute également la fonction de lecture Smooth Streaming à Strobe Media Playback (SMP).

SS pour OSMF comprend deux versions du plug-in :

* Plug-in Smooth Streaming statique pour OSMF (.swc)
* Plug-in Smooth Streaming dynamique pour OSMF (.swf)

Ce document part du principe que l'utilisateur a une expérience d'utilisation d'OSMF et des plug-ins OSMF. Pour plus d'informations sur OSMF, consultez la documentation sur le [site OSMF officiel](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Plug-in Smooth Streaming pour OSMF 2.0
Le plug-in prend en charge le chargement et la lecture de contenu Smooth Streaming à la demande, avec les fonctions suivantes :

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
Pour obtenir une liste complète des fonctionnalités prises en charge, des fonctionnalités non prises en charge et des problèmes connus, consultez [ce document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-the-plugin"></a>Chargement du plug-in
Les plug-ins OSMF peuvent être chargés de façon statique (à la compilation) ou dynamique (à l'exécution). Le téléchargement du plug-in Smooth Streaming pour OSMF comprend les deux versions, statique et dynamique.

* Chargement statique : pour le chargement statique, un fichier de bibliothèque statique (SWC) est nécessaire. Les plug-ins statiques sont ajoutés comme référence aux projets et sont intégrés au fichier de résultat final au moment de la compilation.
* Chargement dynamique : pour le chargement dynamique, un fichier précompilé (SWF) est nécessaire. Les plug-ins dynamiques sont chargés dans le runtime et ne sont pas intégrés au résultat du projet. (Résultat compilé) Les plug-ins dynamiques peuvent être chargés avec les protocoles HTTP ou FILE.

Pour plus d'informations sur le chargement statique et dynamique, consultez la page [Plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>Chargement de SS pour OSMF statique
L'extrait de code qui suit montre comment charger le plug-in SS de façon statique pour OSMF et lire une vidéo simple à l'aide de la classe OSMF MediaFactory. Avant d'inclure le code SS pour OSMF, assurez-vous que la référence de projet comprend le plug-in statique « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc ».

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a>Chargement de SS pour OSMF dynamique
L'extrait de code qui suit montre comment charger le plug-in SS de façon dynamique pour OSMF et lire une vidéo simple à l'aide de la classe OSMF MediaFactory. Avant d'ajouter le code SS pour OSMF, copiez le plug-in dynamique MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf dans le dossier du projet si vous voulez effectuer le chargement avec le protocole FILE ou bien copiez-le sur un serveur Web pour le chargement HTTP. Il n'est pas nécessaire d'inclure MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc dans les références du projet.

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


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a>Lecture Strobe Media Playback avec le plug-in dynamique SS OSMF
Le plug-in dynamique Smooth Streaming pour OSMF est compatible avec [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). Vous pouvez utiliser le plug-in SS pour OSMF pour ajouter la lecture Smooth Streaming à SMP. Pour cela, copiez MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf sur un serveur Web pour le chargement HTTP, en appliquant la procédure suivante :

1. Accédez à la page d'installation de [Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html). 
2. Définissez src sur une source Smooth Streaming (par exemple http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Appliquez les modifications souhaitées à la configuration, puis cliquez sur Preview and Update.
   
   **Remarque** Votre serveur Web de contenu doit disposer d'un fichier crossdomain.xml valide. 
4. Copiez et collez le code dans une page HTML à l'aide de votre éditeur de texte, comme dans cet exemple :

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



1. Ajoutez le plug-in Smooth Streaming OSMF au code intégré, puis enregistrez.
   
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
2. Enregistrez votre page HTML et publiez-la sur un serveur Web. Accédez à la page web publiée à l'aide de votre navigateur Internet compatible avec Flash&reg; Player (Internet Explorer, Chrome, Firefox, etc.).
3. Accédez au contenu Smooth Streaming dans Adobe&reg; Flash&reg; Player.

Pour plus d'informations sur le développement avec OSMF, consultez la page officielle [sur le développement pour OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Plug-in de diffusion en continu adaptative Microsoft pour la mise à jour OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

