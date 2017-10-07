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
# <a name="inserting-ads-on-hello-client-side"></a>Insertion de publicités côté client de hello
Cette rubrique contient des informations sur la façon de tooinsert différents types de publicités côté client de hello.

Pour en savoir plus sur la prise en charge du sous-titrage codé et des publicités dans les vidéos en flux live, consultez la page [Normes de sous-titrage codé et d’insertion de publicités prises en charge](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Actuellement, Azure Media Player ne prend pas en charge les publicités.
> 
> 

## <a id="insert_ads_into_media"></a>Insertion de publicités dans vos supports
Azure Media Services assure la prise en charge pour l’insertion de publicités via hello plateforme Windows Media : Player Frameworks. Des infrastructures de lecteur avec prise en charge des publicités sont disponibles pour les périphériques Windows 8, Silverlight, Windows Phone 8 et iOS. Chaque player framework contient des exemples de code qui vous montre comment tooimplement une application de lecteur. Il existe trois sortes de publicités, que vous pouvez insérer dans votre liste multimédia.

* **Linéaire** – total des annonces frame suspendre la vidéo principale de hello.
* **Non linéaires** : publicité superposée qui s’affiche pendant la lecture de la vidéo principale hello, généralement un logo ou autre image statique placé dans le lecteur hello.
* **Le Guide** – annonces qui s’affichent en dehors du lecteur de hello.

Les publicités peuvent être placées à n’importe quel point dans la chronologie de la vidéo principale hello. Vous devez indiquer le lecteur hello lorsque tooplay hello ad et qui tooplay de publicités. Cela s’effectue via un ensemble de fichiers XML standard : Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) et Digital Video Player Ad Interface Definition (VPAID). Les fichiers VAST spécifient quels toodisplay de publicités. Fichiers VMAP indiquent quand tooplay différentes publicités et contient du code XML VAST. Les fichiers MAST sont des publicités toosequence façon un autre contenant aussi du code XML VAST. Les fichiers VPAID définissent une interface entre le lecteur vidéo hello et Active Directory de hello ou serveur Active Directory.

Chaque infrastructure de lecteur fonctionne différemment et fera l’objet d’une rubrique distincte. Cette rubrique décrit les publicités tooinsert hello mécanismes de base utilisés. Les applications de lecteur vidéo demande publicités à partir d’un serveur Active Directory. serveur Hello peut répondre de plusieurs façons :

* renvoyer un fichier VAST ;
* renvoyer un fichier VMAP (avec VAST incorporé) ;
* renvoyer un fichier MAST (avec VAST incorporé) ;
* renvoyer un fichier VAST avec des publicités VPAID.

### <a name="using-a-video-ad-service-template-vast-file"></a>Utilisation d’un fichier VAST (Video Ad Service Template)
Un fichier VAST indique l’ou les publicités toodisplay. Hello XML suivant est un exemple de fichier VAST pour une publicité linéaire :

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

publicité linéaire de Hello est décrite par hello <**linéaire**> élément. Il spécifie la durée hello d’annonce de hello, événements de suivi, cliquez sur via, cliquez sur le suivi et un nombre de **MediaFile** éléments. Événements de suivi sont spécifiés dans hello <**TrackingEvents**> élément et permettre une tootrack de serveur ad différents événements qui se produisent lors de l’affichage d’annonce de hello. Dans ce cas hello début, milieu, complète et développez événements suivis. événement de début Hello se produit lorsque hello publicité est affichée. événement de milieu Hello se produit lorsqu’au moins 50 % de la chronologie de la publicité hello a été affiché. événement Hello se produit lorsque hello publicité a été visionnée toohello fin. événement de développement Hello se produit lorsque l’utilisateur de hello développe écran toofull de lecteur vidéo hello. Clics publicitaires sont spécifiés avec une <**générés interactifs**> élément au sein d’un <**VideoClicks**> élément et spécifie un toodisplay de ressource URI tooa lorsque les utilisateur hello clique sur ad de hello. Clics est spécifié dans un <**clics**> élément et également dans hello <**VideoClicks**> élément et spécifie une ressource de hello lecteur toorequest suivi clic hello utilisateur sur hello ad.hello <**MediaFile**> éléments spécifient des informations sur l’encodage spécifique d’une annonce. Lorsqu’il existe plusieurs <**MediaFile**> élément, le lecteur vidéo hello peut choisir de hello meilleur encodage pour la plateforme de hello. 

Les publicités linéaires peuvent être affichées dans un ordre bien précis. toodo, ajouter d’autres <Ad> éléments toohello VAST fichier et spécifiez la commande hello d’attribut de séquence hello. Bonjour à l’exemple suivant illustre ce comportement :

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

Les publicités non linéaires sont également spécifiées dans un élément <Creative>. Hello suivant montre l’exemple un <Creative> élément qui décrit une publicité.

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


Hello <**NonLinearAds**> élément peut contenir un ou plusieurs <**non-linéaire**> éléments, chacun d’eux peut décrire une publicité. Hello <**non-linéaire**> élément spécifie la ressource hello pour publicité hello. Hello ressource peut être une <**StaticResouce**>, <**IFrameResource**>, ou <**HTMLResouce**>. <**StaticResource**> décrit une ressource non-HTML et définit un attribut creativeType qui spécifie la façon dont les ressources hello s’affiche :

Image/gif, image/jpeg, image/png : ressource de hello est affichée dans un élément HTML <**img**> balise.

Application/x-javascript : ressource de hello s’affiche dans le code HTML <**script**> balise.

Application/x-shockwave-flash : ressource de hello s’affiche dans un lecteur Flash.

**IFrameResource** décrit une ressource HTML qui peut être affichée dans un IFrame. **HTMLREsource** décrit un fragment de code HTML qui peut être inséré dans une page web. **TrackingEvents** spécifier les événements de suivi et hello URI toorequest lorsque hello événement se produit. Bonjour de cet exemple, les événements acceptInvitation et de réduction sont suivies. Pour plus d’informations sur hello **NonLinearAds** élément et ses enfants, consultez IAB.NET/vast. Notez que hello **TrackingEvents** élément se trouve dans hello **NonLinearAds** élément plutôt que hello **non-linéaire** élément.

Les publicités d'accompagnement sont définies dans un élément <CompanionAds>. Hello <CompanionAds> élément peut contenir un ou plusieurs <Companion> éléments. Chaque <Companion> élément décrit une publicité d’accompagnement et peut contenir un <StaticResource>, <IFrameResource>, ou <HTMLResource> qui sont spécifié dans hello la même façon que dans une publicité. Un fichier VAST peut contenir plusieurs publicités d’accompagnement et application de lecteur hello peut choisir hello plus appropriée annonce toodisplay. Pour plus d'informations sur VAST, consultez [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Utilisation d’un fichier VMAP (Video Multiple Ad Playlist)
Un fichier VMAP vous permet de toospecify ad sauts, la durée pendant laquelle chaque saut de ligne est, combien d’annonces peut être affichées dans un saut et les types de publicités peuvent être affichées pendant une coupure. Hello suivant dans un exemple de fichier VMAP qui définit une coupure publicitaire unique :

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

Un fichier VMAP commence par un élément <VMAP> qui contient un ou plusieurs éléments <AdBreak>, chacun définissant une coupure publicitaire. Chaque coupure publicitaire spécifie un type de coupure, un identificateur et une durée de décalage. attribut de Hello breakType Spécifie le type hello de publicité pouvant être diffusée pendant l’arrêt de hello : linéaire, non linéaire ou d’affichage. Afficher les annonces mappent les publicités d’accompagnement tooVAST. Plusieurs types de publicités peuvent être spécifiés dans une liste séparée par des virgules (sans espaces). attribut breakID de Hello est un identificateur facultatif pour Active Directory de hello. attribut timeOffset de Hello spécifie quand les ad hello doit être affiché. Il peut être spécifié dans un des hello suivant façons :

1. Durée : au format hh:mm:ss ou hh:mm:ss.mmm, où .mmm représente des millisecondes. valeur Hello de cet attribut spécifie l’heure hello à partir du début de hello du début de toohello hello chronologie de la vidéo de publicitaire hello.
2. Pourcentage – format % n, où n est le pourcentage de hello de hello chronologie vidéo tooplay avant de lire l’annonce de hello
3. Début/fin : Spécifie qu’une publicité doit être affichée avant ou après avoir affiché les vidéo hello
4. Position : Spécifie l’ordre hello des coupures publicitaires lorsque minutage hello des coupures publicitaires de hello est inconnu, comme lors de la diffusion en continu. commande Hello de chaque coupure publicitaire est spécifié au format hello #n où n est un entier de 1 ou supérieur. 1 signifie hello publicité doit être affichée à la première occasion de hello, 2 signifie une publicité de hello doit être affichée à l’opportunité de deuxième hello et ainsi de suite.

Au sein de hello <**AdBreak**> élément il peut être <**ADsource par celle**> élément. Hello <**ADsource par celle**> élément contient hello suivant d’attributs :

1. ID : Spécifie l’identificateur pour la source de hello ad
2. allowMultipleAds : valeur booléenne qui spécifie si plusieurs publicités peuvent être affichées pendant publicitaire hello
3. followRedirects : valeur booléenne facultative qui spécifie si le lecteur vidéo hello doit respecter redirige dans une réponse publicitaire

Hello <**ADsource par celle**> élément fournit le lecteur hello une réponse publicitaire insérée ou une réponse de référence tooan Active Directory. Il peut contenir un des hello suivant d’éléments :

* <VASTAdData>Indique qu’une réponse publicitaire VAST est incorporée dans le fichier VMAP de hello
* <AdTagURI> : URI qui fait référence à une réponse publicitaire émanant d’un autre système.
* <CustomAdData> : chaîne arbitraire qui représente une réponse non-VAST.

Dans cet exemple, une réponse publicitaire insérée est spécifiée avec un élément <VASTAdData> qui contient une réponse publicitaire VAST. Pour plus d’informations sur hello autres éléments, consultez [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Hello <**AdBreak**> peut également contenir un <**TrackingEvents**> élément. Hello <**TrackingEvents**> élément vous permet de démarrer de hello tootrack ou à la fin d’une coupure publicitaire ou si une erreur s’est produite pendant la coupure publicitaire hello. Hello <**TrackingEvents**> élément contient un ou plusieurs <**suivi**> éléments, dont chacun spécifie un événement de suivi et un URI de suivi. événements de suivi possibles Hello sont :

1. breakStart : effectue le suivi de début hello d’une coupure publicitaire
2. breakEnd : fin de hello de suivi d’une coupure publicitaire
3. effectue le suivi de l’erreur : une erreur s’est produite pendant la coupure publicitaire hello

Bonjour à l’exemple suivant montre un fichier VMAP qui spécifie les événements de suivi

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

Pour plus d’informations sur hello <**TrackingEvents**> élément et ses enfants, consultez http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Utilisation d’un fichier MAST (Media Abstract Sequencing Template)
Un fichier MAST vous permet de toospecify les déclencheurs qui définissent quand une publicité est affichée. Hello Voici un exemple de fichier MAST qui contient des déclencheurs pour une publicité de versions antérieures, une publicité mi-bande et une publicité.

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



Un fichier MAST commence par un élément **MAST** qui contient un élément **triggers**. Hello <triggers> élément contient un ou plusieurs **déclencheur** éléments qui définissent quand une publicité doit être affichée. 

Hello **déclencheur** élément contient un **startConditions** élément qui spécifient quand une publicité doit commencer tooplay. Hello **startConditions** élément contient un ou plusieurs <condition> éléments. Lorsque chaque <condition> tootrue un déclencheur est lancé ou révoqué, selon s’il prend la valeur hello <condition> est contenue dans un **startConditions** ou **endConditions** élément respectivement. Lorsque plusieurs <condition> éléments sont présents, ils sont traités comme un ou implicite, n’importe quelle condition d’évaluation tootrue entraîne hello déclencheur tooinitiate. Les éléments <condition> peuvent être imbriqués. Lorsque enfant <condition> éléments sont prédéfinies, elles sont traitées comme un opérateur AND implicit, toutes les conditions doivent évaluer tootrue pour hello déclencheur tooinitiate. Hello <condition> élément contient hello suivant des attributs qui définissent la condition de hello : 

1. **type** – Spécifie le type de hello de condition, événement ou la propriété
2. **nom** hello – nom de hello toobe propriété ou un événement utilisé lors de l’évaluation
3. **valeur** – hello valeur qui est évaluée par rapport à une propriété
4. **opérateur** – hello opération toouse lors de l’évaluation : EQ (égal à), NEQ (différent de), GTR (supérieur à), GEQ (supérieur ou égal à), LT (inférieur à), LEQ (inférieur ou égal à), MOD (modulo)

**&lt;endConditions&gt;** contient également des éléments <condition>. Lorsqu’une condition a déclencheur de hello tootrue est reset.hello <trigger> élément contient également un <sources> élément qui contient un ou plusieurs <source> éléments. Hello <source> éléments définissent la réponse de hello URI toohello Active Directory et de type hello de réponse publicitaire. Dans cet exemple, un URI est fourni réponse VAST de tooa. 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Utilisation de VPAID (Video Player-Ad Interface Definition)
VPAID est une API pour l’activation de toocommunicate d’unités de publicité exécutable avec un lecteur vidéo. Cela permet d’offrir une expérience publicitaire hautement interactive. utilisateur de Hello peut interagir avec ad de hello et hello pouvant répondre tooactions effectuées par la visionneuse de hello. Par exemple, une publicité peut afficher les boutons qui permettent à hello utilisateur tooview plus d’informations ou une version plus longue de publicité de hello. le lecteur vidéo Hello doit prendre en charge hello API VPAID et publicité exécutable de hello doit implémenter les API hello. Lorsqu’un lecteur demande une publicité à partir d’un serveur hello du serveur Active Directory peut répondre avec une réponse VAST contenant une publicité vpaid.

Une publicité exécutable est créée dans un code qui doit être exécuté dans un environnement d’exécution, tel qu’Adobe Flash™ ou JavaScript, pouvant être exécuté dans un navigateur web. Lorsqu’un serveur publicitaire retourne une réponse VAST contenant une publicité vpaid, hello la valeur de l’attribut apiFramework de hello Bonjour <MediaFile> l’élément doit être « VPAID ». Cet attribut spécifie qu’ad hello contenue est une publicité vpaid exécutable. attribut de type Hello doit être définie type MIME de toohello Hello exécutable, telles que « application/x-shockwave-flash » ou « application/x-javascript ». Hello extrait de code XML suivant montre hello <MediaFile> élément à partir d’une réponse VAST contenant une publicité vpaid exécutable. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Une publicité exécutable peut être initialisée à l’aide de hello <AdParameters> élément hello <Linear> ou <NonLinear> éléments dans une réponse VAST. Pour plus d’informations sur hello <AdParameters> élément, consultez [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Pour plus d’informations sur hello API VPAID, consultez [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Implémentation d’un lecteur Windows ou Windows Phone 8 avec prise en charge de publicités
Hello plateforme multimédia Microsoft : Player Framework pour Windows 8 et Windows Phone 8 contient une collection d’exemples d’applications qui vous montrent comment une application de lecteur vidéo à l’aide de tooimplement hello framework. Vous pouvez télécharger des exemples de Player Framework et hello hello de [Player Framework pour Windows 8 et Windows Phone 8](https://playerframework.codeplex.com).

Lorsque vous ouvrez la solution Microsoft.PlayerFramework.Xaml.Samples de hello, vous verrez un nombre de dossiers dans le projet de hello. dossier de publicité Hello contient toocreating pertinentes de code exemple hello un lecteur vidéo avec prise en charge d’Active Directory. Dossier de publicité à l’intérieur hello est un nombre de XAML/cs des fichiers chaque émission comment tooinsert les publicités d’une manière différente. Hello suivant liste décrit chaque fichier :

* AdPodPage.xaml montre comment les zones de toodisplay une publicité.
* AdSchedulingPage.xaml montre comment les publicités tooschedule.
* FreeWheelPage.xaml montre comment toouse hello FreeWheel plug-in tooschedule annonces.
* MastPage.xaml montre comment tooschedule des publicités avec un fichier MAST.
* ProgrammaticAdPage.xaml montre comment tooprogrammatically planifier des publicités dans une vidéo.
* ScheduleClipPage.xaml montre comment tooschedule une publicité sans fichier VAST.
* VastLinearCompanionPage.xaml montre comment tooinsert linéaire et publicité d’accompagnement.
* VastNonLinearPage.xaml montre comment tooinsert une publicité non linéaire.
* VmapPage.xaml montre comment toospecify des publicités avec un fichier VMAP.

Chacun de ces exemples utilise la classe de MediaPlayer hello défini par l’infrastructure de lecteur hello. La plupart des exemples utilisent des plug-ins qui apportent une prise en charge de différents formats de réponses publicitaires. Hello, exemple ProgrammaticAdPage interagit par programmation avec une instance MediaPlayer.

### <a name="adpodpage-sample"></a>Exemple AdPodPage
Cet exemple utilise hello AdSchedulerPlugin toodefine lorsque toodisplay une publicité. Dans cet exemple, une publicité mi-bande est planifiée toobe lu après 5 secondes. bloc publicitaire Hello (il s’agit d’un groupe de toodisplay de publicités dans l’ordre) est spécifié dans un fichier VAST retourné à partir d’un serveur Active Directory. le fichier VAST Hello URI toohello est spécifié dans hello <RemoteAdSource> élément.

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

Pour plus d’informations sur hello AdSchedulerPlugin, consultez [publicité Bonjour Player Framework sous Windows 8 et Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
Cet exemple utilise également hello AdSchedulerPlugin. Il planifie trois publicités, une publicité de début de bande, une publicité mi-bande et une publicité de fin de bande. Hello URI toohello VAST pour chaque publicité est spécifiée dans un <RemoteAdSource> élément.

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


### <a name="freewheelpage"></a>FreeWheelPage
Cet exemple utilise hello FreeWheelPlugin qui spécifie un attribut Source qui spécifie un URI ce fichier SmartXML tooa points Spécifie le contenu de l’annonce, ainsi que des informations de planification d’Active Directory.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Cet exemple utilise hello MastSchedulerPlugin qui vous permet de toouse un fichier MAST. attribut de Source de Hello Spécifie l’emplacement hello du fichier MAST de hello.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
Cet exemple interagit par programmation avec hello MediaPlayer. fichier de Hello ProgrammaticAdPage.xaml instancie hello MediaPlayer :

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

fichier de Hello ProgrammaticAdPage.xaml.cs crée un AdHandlerPlugin, ajoute un toospecify TimelineMarker lorsqu’une publicité doit être affichée, puis ajoute un gestionnaire pour l’événement MarkerReached hello qui charge une RemoteAdSource spécification d’un fichier de grande tooa URI et le lit annonce de Hello.

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

### <a name="scheduleclippage"></a>ScheduleClipPage
Cet exemple utilise hello AdSchedulerPlugin tooschedule une publicité mi-bande en spécifiant un fichier .wmv qui contient les ad hello.

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

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
Cet exemple illustre comment toouse hello AdSchedulerPlugin tooschedule un mi-bande linéaire avec une publicité d’accompagnement. Hello <RemoteAdSource> élément spécifie l’emplacement de hello du fichier VAST de hello.

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

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Cet exemple utilise hello AdSchedulerPlugin tooschedule linéaire et une publicité non linéaire. Hello emplacement du fichier VAST est spécifié avec hello <RemoteAdSource> élément.

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

### <a name="vmappage"></a>VMAPPage
Cet exemple utilise des annonces de tooschedule hello VmapSchedulerPlugin à l’aide d’un fichier VMAP. le fichier Hello URI toohello VMAP est spécifié dans l’attribut de Source de hello Hello <VmapSchedulerPlugin> élément.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Implémentation d'un lecteur vidéo iOS avec prise en charge de publicités
Hello plateforme multimédia Microsoft : Player Framework pour iOS contient une collection d’exemples d’applications qui vous montrent comment une application de lecteur vidéo à l’aide de tooimplement hello framework. Vous pouvez télécharger des exemples de Player Framework et hello hello de [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). Hello page github comporte un tooa lien Wiki qui contient des informations supplémentaires sur l’infrastructure de lecteur hello et un exemple de lecteur introduction toohello : [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Planification de publicités avec VMAP
Hello suivant montre l’exemple de comment tooschedule les publicités à l’aide d’un fichier VMAP.

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

### <a name="scheduling-ads-with-vast"></a>Planification de publicités avec VAST
exemple Hello suivant illustre comment tooschedule une publicité VAST à liaison tardive.

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

   exemple Hello suivant illustre comment tooschedule une publicité VAST à liaison anticipée.
Planification d’exemple : 4 un hello de //Download publicitaire VAST liaison anticipée VAST fichier si ( ! [[ framework.adResolver downloadManifest : & manifeste withURL : [NSURL URLWithString : @ « http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml »]]) {[logFrameworkError personnel] ;} else {adLinearTime.startTime = 7 ; adLinearTime.duration = 0 ;

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

exemple Hello suivant illustre comment tooinsert une annonce à l’aide d’approximative Couper modification (RCE)

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

Hello suivant montre comment les zones de tooschedule une publicité.

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

Hello suivant montre l’exemple de comment tooschedule une publicité mi-bande non répétitive. Une publicité non répétitive est diffusée une fois, indépendamment de toute recherche hello visionne.

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

Hello suivant montre l’exemple de comment tooschedule une publicité mi-bande répétitive. Une publicité répétitive s’affichera chaque fois hello spécifié point sur la chronologie de la vidéo hello est atteint.

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


exemple Hello suivant illustre comment tooschedule une publicité.

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

exemple Hello suivant illustre comment tooschedule une publicité.

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

Hello suivant l’exemple montre comment tooschedule un mi-bande superposition ad.

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



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Développement d'applications de lecteur vidéo](media-services-develop-video-players.md)

