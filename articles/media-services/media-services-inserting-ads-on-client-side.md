---
title: "les publicités côté client de hello aaaInserting | Documents Microsoft"
description: "Cette rubrique montre comment les publicités tooinsert hello côté client."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="f57fa-103">Insertion de publicités côté client de hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="f57fa-104">Cette rubrique contient des informations sur la façon de tooinsert différents types de publicités côté client de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="f57fa-105">Pour en savoir plus sur la prise en charge du sous-titrage codé et des publicités dans les vidéos en flux live, consultez la page [Normes de sous-titrage codé et d’insertion de publicités prises en charge](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="f57fa-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="f57fa-106">Actuellement, Azure Media Player ne prend pas en charge les publicités.</span><span class="sxs-lookup"><span data-stu-id="f57fa-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="f57fa-107"><a id="insert_ads_into_media"></a>Insertion de publicités dans vos supports</span><span class="sxs-lookup"><span data-stu-id="f57fa-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="f57fa-108">Azure Media Services assure la prise en charge pour l’insertion de publicités via hello plateforme Windows Media : Player Frameworks.</span><span class="sxs-lookup"><span data-stu-id="f57fa-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="f57fa-109">Des infrastructures de lecteur avec prise en charge des publicités sont disponibles pour les périphériques Windows 8, Silverlight, Windows Phone 8 et iOS.</span><span class="sxs-lookup"><span data-stu-id="f57fa-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="f57fa-110">Chaque player framework contient des exemples de code qui vous montre comment tooimplement une application de lecteur. Il existe trois sortes de publicités, que vous pouvez insérer dans votre liste multimédia.</span><span class="sxs-lookup"><span data-stu-id="f57fa-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="f57fa-111">**Linéaire** – total des annonces frame suspendre la vidéo principale de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="f57fa-112">**Non linéaires** : publicité superposée qui s’affiche pendant la lecture de la vidéo principale hello, généralement un logo ou autre image statique placé dans le lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="f57fa-113">**Le Guide** – annonces qui s’affichent en dehors du lecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="f57fa-114">Les publicités peuvent être placées à n’importe quel point dans la chronologie de la vidéo principale hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="f57fa-115">Vous devez indiquer le lecteur hello lorsque tooplay hello ad et qui tooplay de publicités.</span><span class="sxs-lookup"><span data-stu-id="f57fa-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="f57fa-116">Cela s’effectue via un ensemble de fichiers XML standard : Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) et Digital Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="f57fa-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="f57fa-117">Les fichiers VAST spécifient quels toodisplay de publicités.</span><span class="sxs-lookup"><span data-stu-id="f57fa-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="f57fa-118">Fichiers VMAP indiquent quand tooplay différentes publicités et contient du code XML VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="f57fa-119">Les fichiers MAST sont des publicités toosequence façon un autre contenant aussi du code XML VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="f57fa-120">Les fichiers VPAID définissent une interface entre le lecteur vidéo hello et Active Directory de hello ou serveur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="f57fa-121">Chaque infrastructure de lecteur fonctionne différemment et fera l’objet d’une rubrique distincte.</span><span class="sxs-lookup"><span data-stu-id="f57fa-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="f57fa-122">Cette rubrique décrit les publicités tooinsert hello mécanismes de base utilisés. Les applications de lecteur vidéo demande publicités à partir d’un serveur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="f57fa-123">serveur Hello peut répondre de plusieurs façons :</span><span class="sxs-lookup"><span data-stu-id="f57fa-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="f57fa-124">renvoyer un fichier VAST ;</span><span class="sxs-lookup"><span data-stu-id="f57fa-124">Return a VAST file</span></span>
* <span data-ttu-id="f57fa-125">renvoyer un fichier VMAP (avec VAST incorporé) ;</span><span class="sxs-lookup"><span data-stu-id="f57fa-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="f57fa-126">renvoyer un fichier MAST (avec VAST incorporé) ;</span><span class="sxs-lookup"><span data-stu-id="f57fa-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="f57fa-127">renvoyer un fichier VAST avec des publicités VPAID.</span><span class="sxs-lookup"><span data-stu-id="f57fa-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="f57fa-128">Utilisation d’un fichier VAST (Video Ad Service Template)</span><span class="sxs-lookup"><span data-stu-id="f57fa-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="f57fa-129">Un fichier VAST indique l’ou les publicités toodisplay.</span><span class="sxs-lookup"><span data-stu-id="f57fa-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="f57fa-130">Hello XML suivant est un exemple de fichier VAST pour une publicité linéaire :</span><span class="sxs-lookup"><span data-stu-id="f57fa-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

<span data-ttu-id="f57fa-131">publicité linéaire de Hello est décrite par hello <**linéaire**> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="f57fa-132">Il spécifie la durée hello d’annonce de hello, événements de suivi, cliquez sur via, cliquez sur le suivi et un nombre de **MediaFile** éléments.</span><span class="sxs-lookup"><span data-stu-id="f57fa-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="f57fa-133">Événements de suivi sont spécifiés dans hello <**TrackingEvents**> élément et permettre une tootrack de serveur ad différents événements qui se produisent lors de l’affichage d’annonce de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="f57fa-134">Dans ce cas hello début, milieu, complète et développez événements suivis.</span><span class="sxs-lookup"><span data-stu-id="f57fa-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="f57fa-135">événement de début Hello se produit lorsque hello publicité est affichée.</span><span class="sxs-lookup"><span data-stu-id="f57fa-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="f57fa-136">événement de milieu Hello se produit lorsqu’au moins 50 % de la chronologie de la publicité hello a été affiché.</span><span class="sxs-lookup"><span data-stu-id="f57fa-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="f57fa-137">événement Hello se produit lorsque hello publicité a été visionnée toohello fin.</span><span class="sxs-lookup"><span data-stu-id="f57fa-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="f57fa-138">événement de développement Hello se produit lorsque l’utilisateur de hello développe écran toofull de lecteur vidéo hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="f57fa-139">Clics publicitaires sont spécifiés avec une <**générés interactifs**> élément au sein d’un <**VideoClicks**> élément et spécifie un toodisplay de ressource URI tooa lorsque les utilisateur hello clique sur ad de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="f57fa-140">Clics est spécifié dans un <**clics**> élément et également dans hello <**VideoClicks**> élément et spécifie une ressource de hello lecteur toorequest suivi clic hello utilisateur sur hello ad.hello <**MediaFile**> éléments spécifient des informations sur l’encodage spécifique d’une annonce.</span><span class="sxs-lookup"><span data-stu-id="f57fa-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="f57fa-141">Lorsqu’il existe plusieurs <**MediaFile**> élément, le lecteur vidéo hello peut choisir de hello meilleur encodage pour la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="f57fa-142">Les publicités linéaires peuvent être affichées dans un ordre bien précis.</span><span class="sxs-lookup"><span data-stu-id="f57fa-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="f57fa-143">toodo, ajouter d’autres <Ad> éléments toohello VAST fichier et spécifiez la commande hello d’attribut de séquence hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="f57fa-144">Bonjour à l’exemple suivant illustre ce comportement :</span><span class="sxs-lookup"><span data-stu-id="f57fa-144">hello following example illustrates this:</span></span>

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

<span data-ttu-id="f57fa-145">Les publicités non linéaires sont également spécifiées dans un élément <Creative>.</span><span class="sxs-lookup"><span data-stu-id="f57fa-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="f57fa-146">Hello suivant montre l’exemple un <Creative> élément qui décrit une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


<span data-ttu-id="f57fa-147">Hello <**NonLinearAds**> élément peut contenir un ou plusieurs <**non-linéaire**> éléments, chacun d’eux peut décrire une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="f57fa-148">Hello <**non-linéaire**> élément spécifie la ressource hello pour publicité hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="f57fa-149">Hello ressource peut être une <**StaticResouce**>, <**IFrameResource**>, ou <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="f57fa-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="f57fa-150"> <**StaticResource**> décrit une ressource non-HTML et définit un attribut creativeType qui spécifie la façon dont les ressources hello s’affiche :</span><span class="sxs-lookup"><span data-stu-id="f57fa-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="f57fa-151">Image/gif, image/jpeg, image/png : ressource de hello est affichée dans un élément HTML <**img**> balise.</span><span class="sxs-lookup"><span data-stu-id="f57fa-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="f57fa-152">Application/x-javascript : ressource de hello s’affiche dans le code HTML <**script**> balise.</span><span class="sxs-lookup"><span data-stu-id="f57fa-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="f57fa-153">Application/x-shockwave-flash : ressource de hello s’affiche dans un lecteur Flash.</span><span class="sxs-lookup"><span data-stu-id="f57fa-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="f57fa-154">**IFrameResource** décrit une ressource HTML qui peut être affichée dans un IFrame.</span><span class="sxs-lookup"><span data-stu-id="f57fa-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="f57fa-155">**HTMLREsource** décrit un fragment de code HTML qui peut être inséré dans une page web.</span><span class="sxs-lookup"><span data-stu-id="f57fa-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="f57fa-156">**TrackingEvents** spécifier les événements de suivi et hello URI toorequest lorsque hello événement se produit.</span><span class="sxs-lookup"><span data-stu-id="f57fa-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="f57fa-157">Bonjour de cet exemple, les événements acceptInvitation et de réduction sont suivies.</span><span class="sxs-lookup"><span data-stu-id="f57fa-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="f57fa-158">Pour plus d’informations sur hello **NonLinearAds** élément et ses enfants, consultez IAB.NET/vast.</span><span class="sxs-lookup"><span data-stu-id="f57fa-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="f57fa-159">Notez que hello **TrackingEvents** élément se trouve dans hello **NonLinearAds** élément plutôt que hello **non-linéaire** élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="f57fa-160">Les publicités d'accompagnement sont définies dans un élément <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="f57fa-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="f57fa-161">Hello <CompanionAds> élément peut contenir un ou plusieurs <Companion> éléments.</span><span class="sxs-lookup"><span data-stu-id="f57fa-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="f57fa-162">Chaque <Companion> élément décrit une publicité d’accompagnement et peut contenir un <StaticResource>, <IFrameResource>, ou <HTMLResource> qui sont spécifié dans hello la même façon que dans une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="f57fa-163">Un fichier VAST peut contenir plusieurs publicités d’accompagnement et application de lecteur hello peut choisir hello plus appropriée annonce toodisplay.</span><span class="sxs-lookup"><span data-stu-id="f57fa-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="f57fa-164">Pour plus d'informations sur VAST, consultez [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="f57fa-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="f57fa-165">Utilisation d’un fichier VMAP (Video Multiple Ad Playlist)</span><span class="sxs-lookup"><span data-stu-id="f57fa-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="f57fa-166">Un fichier VMAP vous permet de toospecify ad sauts, la durée pendant laquelle chaque saut de ligne est, combien d’annonces peut être affichées dans un saut et les types de publicités peuvent être affichées pendant une coupure.</span><span class="sxs-lookup"><span data-stu-id="f57fa-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="f57fa-167">Hello suivant dans un exemple de fichier VMAP qui définit une coupure publicitaire unique :</span><span class="sxs-lookup"><span data-stu-id="f57fa-167">hello following in an example VMAP file that defines a single ad break:</span></span>

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

<span data-ttu-id="f57fa-168">Un fichier VMAP commence par un élément <VMAP> qui contient un ou plusieurs éléments <AdBreak>, chacun définissant une coupure publicitaire.</span><span class="sxs-lookup"><span data-stu-id="f57fa-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="f57fa-169">Chaque coupure publicitaire spécifie un type de coupure, un identificateur et une durée de décalage.</span><span class="sxs-lookup"><span data-stu-id="f57fa-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="f57fa-170">attribut de Hello breakType Spécifie le type hello de publicité pouvant être diffusée pendant l’arrêt de hello : linéaire, non linéaire ou d’affichage.</span><span class="sxs-lookup"><span data-stu-id="f57fa-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="f57fa-171">Afficher les annonces mappent les publicités d’accompagnement tooVAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="f57fa-172">Plusieurs types de publicités peuvent être spécifiés dans une liste séparée par des virgules (sans espaces).</span><span class="sxs-lookup"><span data-stu-id="f57fa-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="f57fa-173">attribut breakID de Hello est un identificateur facultatif pour Active Directory de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="f57fa-174">attribut timeOffset de Hello spécifie quand les ad hello doit être affiché.</span><span class="sxs-lookup"><span data-stu-id="f57fa-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="f57fa-175">Il peut être spécifié dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="f57fa-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="f57fa-176">Durée : au format hh:mm:ss ou hh:mm:ss.mmm, où .mmm représente des millisecondes.</span><span class="sxs-lookup"><span data-stu-id="f57fa-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="f57fa-177">valeur Hello de cet attribut spécifie l’heure hello à partir du début de hello du début de toohello hello chronologie de la vidéo de publicitaire hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="f57fa-178">Pourcentage – format % n, où n est le pourcentage de hello de hello chronologie vidéo tooplay avant de lire l’annonce de hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="f57fa-179">Début/fin : Spécifie qu’une publicité doit être affichée avant ou après avoir affiché les vidéo hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="f57fa-180">Position : Spécifie l’ordre hello des coupures publicitaires lorsque minutage hello des coupures publicitaires de hello est inconnu, comme lors de la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="f57fa-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="f57fa-181">commande Hello de chaque coupure publicitaire est spécifié au format hello #n où n est un entier de 1 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="f57fa-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="f57fa-182">1 signifie hello publicité doit être affichée à la première occasion de hello, 2 signifie une publicité de hello doit être affichée à l’opportunité de deuxième hello et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="f57fa-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="f57fa-183">Au sein de hello <**AdBreak**> élément il peut être <**ADsource par celle**> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="f57fa-184">Hello <**ADsource par celle**> élément contient hello suivant d’attributs :</span><span class="sxs-lookup"><span data-stu-id="f57fa-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="f57fa-185">ID : Spécifie l’identificateur pour la source de hello ad</span><span class="sxs-lookup"><span data-stu-id="f57fa-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="f57fa-186">allowMultipleAds : valeur booléenne qui spécifie si plusieurs publicités peuvent être affichées pendant publicitaire hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="f57fa-187">followRedirects : valeur booléenne facultative qui spécifie si le lecteur vidéo hello doit respecter redirige dans une réponse publicitaire</span><span class="sxs-lookup"><span data-stu-id="f57fa-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="f57fa-188">Hello <**ADsource par celle**> élément fournit le lecteur hello une réponse publicitaire insérée ou une réponse de référence tooan Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="f57fa-189">Il peut contenir un des hello suivant d’éléments :</span><span class="sxs-lookup"><span data-stu-id="f57fa-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="f57fa-190"><VASTAdData>Indique qu’une réponse publicitaire VAST est incorporée dans le fichier VMAP de hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="f57fa-191"><AdTagURI> : URI qui fait référence à une réponse publicitaire émanant d’un autre système.</span><span class="sxs-lookup"><span data-stu-id="f57fa-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="f57fa-192"><CustomAdData> : chaîne arbitraire qui représente une réponse non-VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="f57fa-193">Dans cet exemple, une réponse publicitaire insérée est spécifiée avec un élément <VASTAdData> qui contient une réponse publicitaire VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="f57fa-194">Pour plus d’informations sur hello autres éléments, consultez [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="f57fa-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="f57fa-195">Hello <**AdBreak**> peut également contenir un <**TrackingEvents**> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="f57fa-196">Hello <**TrackingEvents**> élément vous permet de démarrer de hello tootrack ou à la fin d’une coupure publicitaire ou si une erreur s’est produite pendant la coupure publicitaire hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="f57fa-197">Hello <**TrackingEvents**> élément contient un ou plusieurs <**suivi**> éléments, dont chacun spécifie un événement de suivi et un URI de suivi.</span><span class="sxs-lookup"><span data-stu-id="f57fa-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="f57fa-198">événements de suivi possibles Hello sont :</span><span class="sxs-lookup"><span data-stu-id="f57fa-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="f57fa-199">breakStart : effectue le suivi de début hello d’une coupure publicitaire</span><span class="sxs-lookup"><span data-stu-id="f57fa-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="f57fa-200">breakEnd : fin de hello de suivi d’une coupure publicitaire</span><span class="sxs-lookup"><span data-stu-id="f57fa-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="f57fa-201">effectue le suivi de l’erreur : une erreur s’est produite pendant la coupure publicitaire hello</span><span class="sxs-lookup"><span data-stu-id="f57fa-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="f57fa-202">Bonjour à l’exemple suivant montre un fichier VMAP qui spécifie les événements de suivi</span><span class="sxs-lookup"><span data-stu-id="f57fa-202">hello following example shows a VMAP file that specifies tracking events</span></span>

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

<span data-ttu-id="f57fa-203">Pour plus d’informations sur hello <**TrackingEvents**> élément et ses enfants, consultez http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="f57fa-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="f57fa-204">Utilisation d’un fichier MAST (Media Abstract Sequencing Template)</span><span class="sxs-lookup"><span data-stu-id="f57fa-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="f57fa-205">Un fichier MAST vous permet de toospecify les déclencheurs qui définissent quand une publicité est affichée.</span><span class="sxs-lookup"><span data-stu-id="f57fa-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="f57fa-206">Hello Voici un exemple de fichier MAST qui contient des déclencheurs pour une publicité de versions antérieures, une publicité mi-bande et une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



<span data-ttu-id="f57fa-207">Un fichier MAST commence par un élément **MAST** qui contient un élément **triggers**.</span><span class="sxs-lookup"><span data-stu-id="f57fa-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="f57fa-208">Hello <triggers> élément contient un ou plusieurs **déclencheur** éléments qui définissent quand une publicité doit être affichée.</span><span class="sxs-lookup"><span data-stu-id="f57fa-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="f57fa-209">Hello **déclencheur** élément contient un **startConditions** élément qui spécifient quand une publicité doit commencer tooplay.</span><span class="sxs-lookup"><span data-stu-id="f57fa-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="f57fa-210">Hello **startConditions** élément contient un ou plusieurs <condition> éléments.</span><span class="sxs-lookup"><span data-stu-id="f57fa-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="f57fa-211">Lorsque chaque <condition> tootrue un déclencheur est lancé ou révoqué, selon s’il prend la valeur hello <condition> est contenue dans un **startConditions** ou **endConditions** élément respectivement.</span><span class="sxs-lookup"><span data-stu-id="f57fa-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="f57fa-212">Lorsque plusieurs <condition> éléments sont présents, ils sont traités comme un ou implicite, n’importe quelle condition d’évaluation tootrue entraîne hello déclencheur tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="f57fa-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="f57fa-213">Les éléments <condition> peuvent être imbriqués.</span><span class="sxs-lookup"><span data-stu-id="f57fa-213"><condition> elements can be nested.</span></span> <span data-ttu-id="f57fa-214">Lorsque enfant <condition> éléments sont prédéfinies, elles sont traitées comme un opérateur AND implicit, toutes les conditions doivent évaluer tootrue pour hello déclencheur tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="f57fa-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="f57fa-215">Hello <condition> élément contient hello suivant des attributs qui définissent la condition de hello :</span><span class="sxs-lookup"><span data-stu-id="f57fa-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="f57fa-216">**type** – Spécifie le type de hello de condition, événement ou la propriété</span><span class="sxs-lookup"><span data-stu-id="f57fa-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="f57fa-217">**nom** hello – nom de hello toobe propriété ou un événement utilisé lors de l’évaluation</span><span class="sxs-lookup"><span data-stu-id="f57fa-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="f57fa-218">**valeur** – hello valeur qui est évaluée par rapport à une propriété</span><span class="sxs-lookup"><span data-stu-id="f57fa-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="f57fa-219">**opérateur** – hello opération toouse lors de l’évaluation : EQ (égal à), NEQ (différent de), GTR (supérieur à), GEQ (supérieur ou égal à), LT (inférieur à), LEQ (inférieur ou égal à), MOD (modulo)</span><span class="sxs-lookup"><span data-stu-id="f57fa-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="f57fa-220">**&lt;endConditions&gt;** contient également des éléments <condition>.</span><span class="sxs-lookup"><span data-stu-id="f57fa-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="f57fa-221">Lorsqu’une condition a déclencheur de hello tootrue est reset.hello <trigger> élément contient également un <sources> élément qui contient un ou plusieurs <source> éléments.</span><span class="sxs-lookup"><span data-stu-id="f57fa-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="f57fa-222">Hello <source> éléments définissent la réponse de hello URI toohello Active Directory et de type hello de réponse publicitaire.</span><span class="sxs-lookup"><span data-stu-id="f57fa-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="f57fa-223">Dans cet exemple, un URI est fourni réponse VAST de tooa.</span><span class="sxs-lookup"><span data-stu-id="f57fa-223">In this example a URI is given tooa VAST response.</span></span> 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="f57fa-224">Utilisation de VPAID (Video Player-Ad Interface Definition)</span><span class="sxs-lookup"><span data-stu-id="f57fa-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="f57fa-225">VPAID est une API pour l’activation de toocommunicate d’unités de publicité exécutable avec un lecteur vidéo.</span><span class="sxs-lookup"><span data-stu-id="f57fa-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="f57fa-226">Cela permet d’offrir une expérience publicitaire hautement interactive.</span><span class="sxs-lookup"><span data-stu-id="f57fa-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="f57fa-227">utilisateur de Hello peut interagir avec ad de hello et hello pouvant répondre tooactions effectuées par la visionneuse de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="f57fa-228">Par exemple, une publicité peut afficher les boutons qui permettent à hello utilisateur tooview plus d’informations ou une version plus longue de publicité de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="f57fa-229">le lecteur vidéo Hello doit prendre en charge hello API VPAID et publicité exécutable de hello doit implémenter les API hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="f57fa-230">Lorsqu’un lecteur demande une publicité à partir d’un serveur hello du serveur Active Directory peut répondre avec une réponse VAST contenant une publicité vpaid.</span><span class="sxs-lookup"><span data-stu-id="f57fa-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="f57fa-231">Une publicité exécutable est créée dans un code qui doit être exécuté dans un environnement d’exécution, tel qu’Adobe Flash™ ou JavaScript, pouvant être exécuté dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="f57fa-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="f57fa-232">Lorsqu’un serveur publicitaire retourne une réponse VAST contenant une publicité vpaid, hello la valeur de l’attribut apiFramework de hello Bonjour <MediaFile> l’élément doit être « VPAID ».</span><span class="sxs-lookup"><span data-stu-id="f57fa-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="f57fa-233">Cet attribut spécifie qu’ad hello contenue est une publicité vpaid exécutable.</span><span class="sxs-lookup"><span data-stu-id="f57fa-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="f57fa-234">attribut de type Hello doit être définie type MIME de toohello Hello exécutable, telles que « application/x-shockwave-flash » ou « application/x-javascript ».</span><span class="sxs-lookup"><span data-stu-id="f57fa-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="f57fa-235">Hello extrait de code XML suivant montre hello <MediaFile> élément à partir d’une réponse VAST contenant une publicité vpaid exécutable.</span><span class="sxs-lookup"><span data-stu-id="f57fa-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="f57fa-236">Une publicité exécutable peut être initialisée à l’aide de hello <AdParameters> élément hello <Linear> ou <NonLinear> éléments dans une réponse VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="f57fa-237">Pour plus d’informations sur hello <AdParameters> élément, consultez [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="f57fa-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="f57fa-238">Pour plus d’informations sur hello API VPAID, consultez [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="f57fa-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="f57fa-239">Implémentation d’un lecteur Windows ou Windows Phone 8 avec prise en charge de publicités</span><span class="sxs-lookup"><span data-stu-id="f57fa-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="f57fa-240">Hello plateforme multimédia Microsoft : Player Framework pour Windows 8 et Windows Phone 8 contient une collection d’exemples d’applications qui vous montrent comment une application de lecteur vidéo à l’aide de tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="f57fa-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="f57fa-241">Vous pouvez télécharger des exemples de Player Framework et hello hello de [Player Framework pour Windows 8 et Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="f57fa-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="f57fa-242">Lorsque vous ouvrez la solution Microsoft.PlayerFramework.Xaml.Samples de hello, vous verrez un nombre de dossiers dans le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="f57fa-243">dossier de publicité Hello contient toocreating pertinentes de code exemple hello un lecteur vidéo avec prise en charge d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="f57fa-244">Dossier de publicité à l’intérieur hello est un nombre de XAML/cs des fichiers chaque émission comment tooinsert les publicités d’une manière différente.</span><span class="sxs-lookup"><span data-stu-id="f57fa-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="f57fa-245">Hello suivant liste décrit chaque fichier :</span><span class="sxs-lookup"><span data-stu-id="f57fa-245">hello following list describes each:</span></span>

* <span data-ttu-id="f57fa-246">AdPodPage.xaml montre comment les zones de toodisplay une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="f57fa-247">AdSchedulingPage.xaml montre comment les publicités tooschedule.</span><span class="sxs-lookup"><span data-stu-id="f57fa-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="f57fa-248">FreeWheelPage.xaml montre comment toouse hello FreeWheel plug-in tooschedule annonces.</span><span class="sxs-lookup"><span data-stu-id="f57fa-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="f57fa-249">MastPage.xaml montre comment tooschedule des publicités avec un fichier MAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="f57fa-250">ProgrammaticAdPage.xaml montre comment tooprogrammatically planifier des publicités dans une vidéo.</span><span class="sxs-lookup"><span data-stu-id="f57fa-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="f57fa-251">ScheduleClipPage.xaml montre comment tooschedule une publicité sans fichier VAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="f57fa-252">VastLinearCompanionPage.xaml montre comment tooinsert linéaire et publicité d’accompagnement.</span><span class="sxs-lookup"><span data-stu-id="f57fa-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="f57fa-253">VastNonLinearPage.xaml montre comment tooinsert une publicité non linéaire.</span><span class="sxs-lookup"><span data-stu-id="f57fa-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="f57fa-254">VmapPage.xaml montre comment toospecify des publicités avec un fichier VMAP.</span><span class="sxs-lookup"><span data-stu-id="f57fa-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="f57fa-255">Chacun de ces exemples utilise la classe de MediaPlayer hello défini par l’infrastructure de lecteur hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="f57fa-256">La plupart des exemples utilisent des plug-ins qui apportent une prise en charge de différents formats de réponses publicitaires.</span><span class="sxs-lookup"><span data-stu-id="f57fa-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="f57fa-257">Hello, exemple ProgrammaticAdPage interagit par programmation avec une instance MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="f57fa-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="f57fa-258">Exemple AdPodPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-258">AdPodPage Sample</span></span>
<span data-ttu-id="f57fa-259">Cet exemple utilise hello AdSchedulerPlugin toodefine lorsque toodisplay une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="f57fa-260">Dans cet exemple, une publicité mi-bande est planifiée toobe lu après 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="f57fa-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="f57fa-261">bloc publicitaire Hello (il s’agit d’un groupe de toodisplay de publicités dans l’ordre) est spécifié dans un fichier VAST retourné à partir d’un serveur Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="f57fa-262">le fichier VAST Hello URI toohello est spécifié dans hello <RemoteAdSource> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

<span data-ttu-id="f57fa-263">Pour plus d’informations sur hello AdSchedulerPlugin, consultez [publicité Bonjour Player Framework sous Windows 8 et Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="f57fa-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="f57fa-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-264">AdSchedulingPage</span></span>
<span data-ttu-id="f57fa-265">Cet exemple utilise également hello AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="f57fa-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="f57fa-266">Il planifie trois publicités, une publicité de début de bande, une publicité mi-bande et une publicité de fin de bande.</span><span class="sxs-lookup"><span data-stu-id="f57fa-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="f57fa-267">Hello URI toohello VAST pour chaque publicité est spécifiée dans un <RemoteAdSource> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a><span data-ttu-id="f57fa-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-268">FreeWheelPage</span></span>
<span data-ttu-id="f57fa-269">Cet exemple utilise hello FreeWheelPlugin qui spécifie un attribut Source qui spécifie un URI ce fichier SmartXML tooa points Spécifie le contenu de l’annonce, ainsi que des informations de planification d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f57fa-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="f57fa-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-270">MastPage</span></span>
<span data-ttu-id="f57fa-271">Cet exemple utilise hello MastSchedulerPlugin qui vous permet de toouse un fichier MAST.</span><span class="sxs-lookup"><span data-stu-id="f57fa-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="f57fa-272">attribut de Source de Hello Spécifie l’emplacement hello du fichier MAST de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="f57fa-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="f57fa-274">Cet exemple interagit par programmation avec hello MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="f57fa-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="f57fa-275">fichier de Hello ProgrammaticAdPage.xaml instancie hello MediaPlayer :</span><span class="sxs-lookup"><span data-stu-id="f57fa-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="f57fa-276">fichier de Hello ProgrammaticAdPage.xaml.cs crée un AdHandlerPlugin, ajoute un toospecify TimelineMarker lorsqu’une publicité doit être affichée, puis ajoute un gestionnaire pour l’événement MarkerReached hello qui charge une RemoteAdSource spécification d’un fichier de grande tooa URI et le lit annonce de Hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a><span data-ttu-id="f57fa-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-277">ScheduleClipPage</span></span>
<span data-ttu-id="f57fa-278">Cet exemple utilise hello AdSchedulerPlugin tooschedule une publicité mi-bande en spécifiant un fichier .wmv qui contient les ad hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="f57fa-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="f57fa-280">Cet exemple illustre comment toouse hello AdSchedulerPlugin tooschedule un mi-bande linéaire avec une publicité d’accompagnement.</span><span class="sxs-lookup"><span data-stu-id="f57fa-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="f57fa-281">Hello <RemoteAdSource> élément spécifie l’emplacement de hello du fichier VAST de hello.</span><span class="sxs-lookup"><span data-stu-id="f57fa-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="f57fa-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="f57fa-283">Cet exemple utilise hello AdSchedulerPlugin tooschedule linéaire et une publicité non linéaire.</span><span class="sxs-lookup"><span data-stu-id="f57fa-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="f57fa-284">Hello emplacement du fichier VAST est spécifié avec hello <RemoteAdSource> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a><span data-ttu-id="f57fa-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="f57fa-285">VMAPPage</span></span>
<span data-ttu-id="f57fa-286">Cet exemple utilise des annonces de tooschedule hello VmapSchedulerPlugin à l’aide d’un fichier VMAP.</span><span class="sxs-lookup"><span data-stu-id="f57fa-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="f57fa-287">le fichier Hello URI toohello VMAP est spécifié dans l’attribut de Source de hello Hello <VmapSchedulerPlugin> élément.</span><span class="sxs-lookup"><span data-stu-id="f57fa-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="f57fa-288">Implémentation d'un lecteur vidéo iOS avec prise en charge de publicités</span><span class="sxs-lookup"><span data-stu-id="f57fa-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="f57fa-289">Hello plateforme multimédia Microsoft : Player Framework pour iOS contient une collection d’exemples d’applications qui vous montrent comment une application de lecteur vidéo à l’aide de tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="f57fa-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="f57fa-290">Vous pouvez télécharger des exemples de Player Framework et hello hello de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="f57fa-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="f57fa-291">Hello page github comporte un tooa lien Wiki qui contient des informations supplémentaires sur l’infrastructure de lecteur hello et un exemple de lecteur introduction toohello : [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="f57fa-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="f57fa-292">Planification de publicités avec VMAP</span><span class="sxs-lookup"><span data-stu-id="f57fa-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="f57fa-293">Hello suivant montre l’exemple de comment tooschedule les publicités à l’aide d’un fichier VMAP.</span><span class="sxs-lookup"><span data-stu-id="f57fa-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="f57fa-294">Planification de publicités avec VAST</span><span class="sxs-lookup"><span data-stu-id="f57fa-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="f57fa-295">exemple Hello suivant illustre comment tooschedule une publicité VAST à liaison tardive.</span><span class="sxs-lookup"><span data-stu-id="f57fa-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   <span data-ttu-id="f57fa-296">exemple Hello suivant illustre comment tooschedule une publicité VAST à liaison anticipée.</span><span class="sxs-lookup"><span data-stu-id="f57fa-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="f57fa-297">Planification d’exemple : 4 un hello de //Download publicitaire VAST liaison anticipée VAST fichier si ( ! [[ framework.adResolver downloadManifest : & manifeste withURL : [NSURL URLWithString : @ « http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml »]]) {[logFrameworkError personnel] ;} else {adLinearTime.startTime = 7 ; adLinearTime.duration = 0 ;</span><span class="sxs-lookup"><span data-stu-id="f57fa-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

<span data-ttu-id="f57fa-298">exemple Hello suivant illustre comment tooinsert une annonce à l’aide d’approximative Couper modification (RCE)</span><span class="sxs-lookup"><span data-stu-id="f57fa-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="f57fa-299">Hello suivant montre comment les zones de tooschedule une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-299">hello following example shows how tooschedule an ad pod.</span></span>

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="f57fa-300">Hello suivant montre l’exemple de comment tooschedule une publicité mi-bande non répétitive.</span><span class="sxs-lookup"><span data-stu-id="f57fa-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="f57fa-301">Une publicité non répétitive est diffusée une fois, indépendamment de toute recherche hello visionne.</span><span class="sxs-lookup"><span data-stu-id="f57fa-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="f57fa-302">Hello suivant montre l’exemple de comment tooschedule une publicité mi-bande répétitive.</span><span class="sxs-lookup"><span data-stu-id="f57fa-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="f57fa-303">Une publicité répétitive s’affichera chaque fois hello spécifié point sur la chronologie de la vidéo hello est atteint.</span><span class="sxs-lookup"><span data-stu-id="f57fa-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


<span data-ttu-id="f57fa-304">exemple Hello suivant illustre comment tooschedule une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="f57fa-305">exemple Hello suivant illustre comment tooschedule une publicité.</span><span class="sxs-lookup"><span data-stu-id="f57fa-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

<span data-ttu-id="f57fa-306">Hello suivant l’exemple montre comment tooschedule un mi-bande superposition ad.</span><span class="sxs-lookup"><span data-stu-id="f57fa-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a><span data-ttu-id="f57fa-307">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f57fa-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f57fa-308">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f57fa-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f57fa-309">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f57fa-309">See Also</span></span>
[<span data-ttu-id="f57fa-310">Développement d'applications de lecteur vidéo</span><span class="sxs-lookup"><span data-stu-id="f57fa-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

