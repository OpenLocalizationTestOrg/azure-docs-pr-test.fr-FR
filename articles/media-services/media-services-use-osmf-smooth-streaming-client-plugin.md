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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="6c1d2-103">Comment tooUse hello Microsoft Smooth Streaming plug-in pour hello Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="6c1d2-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="6c1d2-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c1d2-104">Overview</span></span>
<span data-ttu-id="6c1d2-105">Hello plug-in de diffusion en continu lisse Microsoft pour Open Source Media Framework 2.0 (SS pour OSMF) étend les fonctionnalités par défaut de hello de OSMF et ajoute toonew de lecture de contenu Microsoft de la diffusion en continu lisse OSMF existant lecteurs.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="6c1d2-106">plug-in Hello ajoute également la diffusion en continu lisse lecture fonctionnalités tooStrobe Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="6c1d2-107">SS pour OSMF comprend deux versions du plug-in :</span><span class="sxs-lookup"><span data-stu-id="6c1d2-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="6c1d2-108">Plug-in Smooth Streaming statique pour OSMF (.swc)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="6c1d2-109">Plug-in Smooth Streaming dynamique pour OSMF (.swf)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="6c1d2-110">Ce document suppose que le lecteur de hello a une connaissance de OSMF et OSMF plug-ins. Pour plus d’informations sur OSMF, veuillez consulter la documentation de hello hello [site officiel de OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="6c1d2-111">Plug-in Smooth Streaming pour OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="6c1d2-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="6c1d2-112">plug-in Hello prend en charge la lecture du contenu de diffusion en continu à la demande et chargement avec hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="6c1d2-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="6c1d2-113">Lecture Smooth Streaming à la demande (lecture, pause, avance rapide, arrêt)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="6c1d2-114">Lecture Smooth Streaming en direct (lecture)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="6c1d2-115">Fonctions DVR en direct (pause, avance rapide, lecture DVR, retour au direct)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="6c1d2-116">Prise en charge des codecs vidéo - H.264</span><span class="sxs-lookup"><span data-stu-id="6c1d2-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="6c1d2-117">Prise en charge des codecs audio - AAC</span><span class="sxs-lookup"><span data-stu-id="6c1d2-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="6c1d2-118">Plusieurs langues avec API OSMF intégrées</span><span class="sxs-lookup"><span data-stu-id="6c1d2-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="6c1d2-119">Sélection de la qualité de lecture maximale avec API OSMF intégrées</span><span class="sxs-lookup"><span data-stu-id="6c1d2-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="6c1d2-120">Sous-titres Sidecar avec plug-in de sous-titres OSMF</span><span class="sxs-lookup"><span data-stu-id="6c1d2-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="6c1d2-121">Adobe&reg; Flash&reg; Player 11.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="6c1d2-122">Cette version ne prend en charge qu'OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="6c1d2-123">Fonctionnalités prises en charge et problèmes connus</span><span class="sxs-lookup"><span data-stu-id="6c1d2-123">Supported features and known issues</span></span>
<span data-ttu-id="6c1d2-124">Pour obtenir une liste complète des fonctionnalités prises en charge, les fonctionnalités prises en charge et les problèmes connus, consultez trop[ce document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="6c1d2-125">Hello de chargement du plug-in</span><span class="sxs-lookup"><span data-stu-id="6c1d2-125">Loading hello Plugin</span></span>
<span data-ttu-id="6c1d2-126">Les plug-ins OSMF peuvent être chargés de façon statique (à la compilation) ou dynamique (à l'exécution).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="6c1d2-127">un plug-in de diffusion en continu lisse à Hello pour le téléchargement OSMF inclut des versions statiques et dynamiques.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="6c1d2-128">Chargement statique : tooload de manière statique, un fichier de bibliothèque statique (SWC) est requis.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="6c1d2-129">Plug-ins statiques sont ajoutés en tant que référence toohello projets et fusion à l’intérieur de la sortie finale hello de fichiers au moment de la compilation hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="6c1d2-130">Chargement dynamique : tooload dynamiquement, un fichier (SWF) précompilé est requis.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="6c1d2-131">Plug-ins dynamiques sont chargés dans le runtime de hello et pas inclus dans la sortie du projet hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="6c1d2-132">(Résultat compilé) Les plug-ins dynamiques peuvent être chargés avec les protocoles HTTP ou FILE.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="6c1d2-133">Pour plus d’informations sur le chargement statique et dynamique, consultez officielle de hello [page de plug-in OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="6c1d2-134">Chargement de SS pour OSMF statique</span><span class="sxs-lookup"><span data-stu-id="6c1d2-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="6c1d2-135">extrait de code Hello ci-dessous montre comment les tooload hello plug-in SS pour OSMF statiquement et lire une vidéo de base à l’aide de la classe de OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="6c1d2-136">Avant d’inclure hello SS pour le code OSMF, assurez-vous que référence de projet hello inclut des plug-in de statique hello « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc ».</span><span class="sxs-lookup"><span data-stu-id="6c1d2-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="6c1d2-137">Chargement de SS pour OSMF dynamique</span><span class="sxs-lookup"><span data-stu-id="6c1d2-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="6c1d2-138">extrait de code Hello ci-dessous montre comment les tooload hello dynamiquement les plug-in SS pour OSMF et lire une vidéo de base à l’aide de la classe de OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="6c1d2-139">Avant d’inclure hello SS pour le code OSMF, copier dossier du projet toohello hello « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf » plug-in dynamique si vous souhaitez tooload à l’aide du protocole de fichier, ou copiez sous un serveur web pour la charge HTTP.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="6c1d2-140">Il n’existe aucun tooinclude besoin « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc » dans les références de projet hello.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="6c1d2-141">package {</span><span class="sxs-lookup"><span data-stu-id="6c1d2-141">package {</span></span>

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
<span data-ttu-id="6c1d2-142">}</span><span class="sxs-lookup"><span data-stu-id="6c1d2-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="6c1d2-143">Lecture du média STROBE avec hello plug-in de SS ODMF dynamique</span><span class="sxs-lookup"><span data-stu-id="6c1d2-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="6c1d2-144">Hello Smooth Streaming pour OSMF les plug-in dynamique est compatible avec [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="6c1d2-145">Vous pouvez utiliser hello SS pour tooSMP de lecture de contenu de diffusion en continu lisse OSMF plug-in tooadd.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="6c1d2-146">toodo, copie « MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf » sous un serveur web pour la charge HTTP à l’aide de hello suivant les étapes :</span><span class="sxs-lookup"><span data-stu-id="6c1d2-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="6c1d2-147">Parcourir hello [page Installation de la lecture du média Strobe](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="6c1d2-148">Permet de définir hello src tooa Smooth Streaming source, (par exemple, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="6c1d2-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="6c1d2-149">Apporter des modifications de configuration hello souhaité et cliquez sur Afficher un aperçu et mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="6c1d2-150">**Remarque** Votre serveur Web de contenu doit disposer d'un fichier crossdomain.xml valide.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="6c1d2-151">Copiez et collez hello code tooa simple page HTML à l’aide de votre éditeur de texte, tels que Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c1d2-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

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



1. <span data-ttu-id="6c1d2-152">Ajouter toohello du plug-in OSMF de diffusion en continu lisse incorporer le code et l’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
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
2. <span data-ttu-id="6c1d2-153">Enregistrez votre page HTML et publier un serveur web de tooa.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="6c1d2-154">Parcourir toohello publié la page web à l’aide de vos favoris Flash&reg; lecteur activé le navigateur Internet (Internet Explorer, Chrome, Firefox, etc.).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="6c1d2-155">Accédez au contenu Smooth Streaming dans Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="6c1d2-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="6c1d2-156">Pour plus d’informations sur le développement de OSMF général, consultez officielle de hello [page de développement OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="6c1d2-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6c1d2-157">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="6c1d2-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c1d2-158">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="6c1d2-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="6c1d2-159">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="6c1d2-159">See Also</span></span>
[<span data-ttu-id="6c1d2-160">Plug-in de diffusion en continu adaptative Microsoft pour la mise à jour OSMF</span><span class="sxs-lookup"><span data-stu-id="6c1d2-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

