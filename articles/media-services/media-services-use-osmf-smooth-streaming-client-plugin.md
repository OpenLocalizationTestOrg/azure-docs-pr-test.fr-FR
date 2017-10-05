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
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="a4627-103">Utilisation du plug-in Microsoft Smooth Streaming pour Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="a4627-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="a4627-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a4627-104">Overview</span></span>
<span data-ttu-id="a4627-105">Le plug-in Microsoft Smooth Streaming pour Open Source Media Framework 2.0 (SS pour OSMF) étend les capacités par défaut d'OSMF et ajoute la lecture de contenu Microsoft Smooth Streaming aux lecteurs OSMF, qu'ils soient nouveaux ou existants.</span><span class="sxs-lookup"><span data-stu-id="a4627-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="a4627-106">Il ajoute également la fonction de lecture Smooth Streaming à Strobe Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="a4627-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="a4627-107">SS pour OSMF comprend deux versions du plug-in :</span><span class="sxs-lookup"><span data-stu-id="a4627-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="a4627-108">Plug-in Smooth Streaming statique pour OSMF (.swc)</span><span class="sxs-lookup"><span data-stu-id="a4627-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="a4627-109">Plug-in Smooth Streaming dynamique pour OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="a4627-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="a4627-110">Ce document part du principe que l'utilisateur a une expérience d'utilisation d'OSMF et des plug-ins OSMF. Pour plus d'informations sur OSMF, consultez la documentation sur le [site OSMF officiel](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="a4627-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="a4627-111">Plug-in Smooth Streaming pour OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="a4627-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="a4627-112">Le plug-in prend en charge le chargement et la lecture de contenu Smooth Streaming à la demande, avec les fonctions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a4627-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="a4627-113">Lecture Smooth Streaming à la demande (lecture, pause, avance rapide, arrêt)</span><span class="sxs-lookup"><span data-stu-id="a4627-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="a4627-114">Lecture Smooth Streaming en direct (lecture)</span><span class="sxs-lookup"><span data-stu-id="a4627-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="a4627-115">Fonctions DVR en direct (pause, avance rapide, lecture DVR, retour au direct)</span><span class="sxs-lookup"><span data-stu-id="a4627-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="a4627-116">Prise en charge des codecs vidéo - H.264</span><span class="sxs-lookup"><span data-stu-id="a4627-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="a4627-117">Prise en charge des codecs audio - AAC</span><span class="sxs-lookup"><span data-stu-id="a4627-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="a4627-118">Plusieurs langues avec API OSMF intégrées</span><span class="sxs-lookup"><span data-stu-id="a4627-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="a4627-119">Sélection de la qualité de lecture maximale avec API OSMF intégrées</span><span class="sxs-lookup"><span data-stu-id="a4627-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="a4627-120">Sous-titres Sidecar avec plug-in de sous-titres OSMF</span><span class="sxs-lookup"><span data-stu-id="a4627-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="a4627-121">Adobe&reg; Flash&reg; Player 11.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a4627-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="a4627-122">Cette version ne prend en charge qu'OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="a4627-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="a4627-123">Fonctionnalités prises en charge et problèmes connus</span><span class="sxs-lookup"><span data-stu-id="a4627-123">Supported features and known issues</span></span>
<span data-ttu-id="a4627-124">Pour obtenir une liste complète des fonctionnalités prises en charge, des fonctionnalités non prises en charge et des problèmes connus, consultez [ce document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="a4627-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="a4627-125">Chargement du plug-in</span><span class="sxs-lookup"><span data-stu-id="a4627-125">Loading the Plugin</span></span>
<span data-ttu-id="a4627-126">Les plug-ins OSMF peuvent être chargés de façon statique (à la compilation) ou dynamique (à l'exécution).</span><span class="sxs-lookup"><span data-stu-id="a4627-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="a4627-127">Le téléchargement du plug-in Smooth Streaming pour OSMF comprend les deux versions, statique et dynamique.</span><span class="sxs-lookup"><span data-stu-id="a4627-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="a4627-128">Chargement statique : pour le chargement statique, un fichier de bibliothèque statique (SWC) est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a4627-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="a4627-129">Les plug-ins statiques sont ajoutés comme référence aux projets et sont intégrés au fichier de résultat final au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="a4627-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="a4627-130">Chargement dynamique : pour le chargement dynamique, un fichier précompilé (SWF) est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a4627-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="a4627-131">Les plug-ins dynamiques sont chargés dans le runtime et ne sont pas intégrés au résultat du projet.</span><span class="sxs-lookup"><span data-stu-id="a4627-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="a4627-132">(Résultat compilé) Les plug-ins dynamiques peuvent être chargés avec les protocoles HTTP ou FILE.</span><span class="sxs-lookup"><span data-stu-id="a4627-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="a4627-133">Pour plus d'informations sur le chargement statique et dynamique, consultez la page [Plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="a4627-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="a4627-134">Chargement de SS pour OSMF statique</span><span class="sxs-lookup"><span data-stu-id="a4627-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="a4627-135">L'extrait de code qui suit montre comment charger le plug-in SS de façon statique pour OSMF et lire une vidéo simple à l'aide de la classe OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="a4627-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="a4627-136">Avant d'inclure le code SS pour OSMF, assurez-vous que la référence de projet comprend le plug-in statique « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc ».</span><span class="sxs-lookup"><span data-stu-id="a4627-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="a4627-137">Chargement de SS pour OSMF dynamique</span><span class="sxs-lookup"><span data-stu-id="a4627-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="a4627-138">L'extrait de code qui suit montre comment charger le plug-in SS de façon dynamique pour OSMF et lire une vidéo simple à l'aide de la classe OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="a4627-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="a4627-139">Avant d'ajouter le code SS pour OSMF, copiez le plug-in dynamique MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf dans le dossier du projet si vous voulez effectuer le chargement avec le protocole FILE ou bien copiez-le sur un serveur Web pour le chargement HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4627-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="a4627-140">Il n'est pas nécessaire d'inclure MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc dans les références du projet.</span><span class="sxs-lookup"><span data-stu-id="a4627-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="a4627-141">package {</span><span class="sxs-lookup"><span data-stu-id="a4627-141">package {</span></span>

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
<span data-ttu-id="a4627-142">}</span><span class="sxs-lookup"><span data-stu-id="a4627-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="a4627-143">Lecture Strobe Media Playback avec le plug-in dynamique SS OSMF</span><span class="sxs-lookup"><span data-stu-id="a4627-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="a4627-144">Le plug-in dynamique Smooth Streaming pour OSMF est compatible avec [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="a4627-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="a4627-145">Vous pouvez utiliser le plug-in SS pour OSMF pour ajouter la lecture Smooth Streaming à SMP.</span><span class="sxs-lookup"><span data-stu-id="a4627-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="a4627-146">Pour cela, copiez MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf sur un serveur Web pour le chargement HTTP, en appliquant la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="a4627-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="a4627-147">Accédez à la page d'installation de [Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="a4627-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="a4627-148">Définissez src sur une source Smooth Streaming (par exemple http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="a4627-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="a4627-149">Appliquez les modifications souhaitées à la configuration, puis cliquez sur Preview and Update.</span><span class="sxs-lookup"><span data-stu-id="a4627-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="a4627-150">**Remarque** Votre serveur Web de contenu doit disposer d'un fichier crossdomain.xml valide.</span><span class="sxs-lookup"><span data-stu-id="a4627-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="a4627-151">Copiez et collez le code dans une page HTML à l'aide de votre éditeur de texte, comme dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="a4627-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="a4627-152">Ajoutez le plug-in Smooth Streaming OSMF au code intégré, puis enregistrez.</span><span class="sxs-lookup"><span data-stu-id="a4627-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="a4627-153">Enregistrez votre page HTML et publiez-la sur un serveur Web.</span><span class="sxs-lookup"><span data-stu-id="a4627-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="a4627-154">Accédez à la page web publiée à l'aide de votre navigateur Internet compatible avec Flash&reg; Player (Internet Explorer, Chrome, Firefox, etc.).</span><span class="sxs-lookup"><span data-stu-id="a4627-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="a4627-155">Accédez au contenu Smooth Streaming dans Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="a4627-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="a4627-156">Pour plus d'informations sur le développement avec OSMF, consultez la page officielle [sur le développement pour OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="a4627-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="a4627-157">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a4627-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a4627-158">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a4627-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a4627-159">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a4627-159">See Also</span></span>
[<span data-ttu-id="a4627-160">Plug-in de diffusion en continu adaptative Microsoft pour la mise à jour OSMF</span><span class="sxs-lookup"><span data-stu-id="a4627-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

