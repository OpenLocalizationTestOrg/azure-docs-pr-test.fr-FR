---
title: "applications de lecteur vidéo aaaDevelop"
description: "rubrique de Hello fournit des liens tooPlayer infrastructures et plug-ins que vous pouvez utiliser toodevelop vos propres applications clientes qui peuvent consommer de diffusion multimédia en continu de Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Développement d’applications de lecteur vidéo
## <a name="overview"></a>Vue d'ensemble
Azure Media Services fournit des outils hello vous devez toocreate riche, les applications de lecteur client dynamiques pour la plupart des plateformes, y compris : iOS, appareils, les appareils Android, Windows, Windows Phone, Xbox et décodeurs boîtes. Cette rubrique fournit également des liens tooSDKs et des infrastructures de lecteur que vous pouvez utiliser toodevelop vos propres applications clientes qui peuvent consommer de diffusion multimédia en continu à partir d’Azure Media Services.

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) un lecteur vidéo web repose tooplay précédent contenu multimédia à partir de Microsoft Azure Media Services sur un large éventail de navigateurs et périphériques. Azure Media Player utilise des normes industrielles telles que HTML5, Media Source Extensions (MSE) et les Extensions de média chiffré (EME) tooprovide une expérience de diffusion en continu adaptative enrichie. Lorsque ces normes ne sont pas disponibles sur un périphérique ou dans un navigateur, Azure Media Player utilise Flash et Silverlight comme technologies de secours. Quelle que soit la technologie de lecture hello utilisée, les développeurs auront un tooaccess d’interface unifiée JavaScript API. Cela permet de contenu pris en charge par toobe Azure Media Services lu sur un large éventail d’appareils et navigateurs sans effort supplémentaire.

Microsoft Azure Media Services permet toobe contenu pris en charge avec DASH, Smooth Streaming et HLS tooplay de formats de diffusion en continu sauvegarder le contenu. Azure Media Player prend en compte ces différents formats et automatiquement joué par hello lien meilleures en fonction des capacités de plateforme/navigateur hello. Microsoft Azure Media Services assure également le chiffrement dynamique des ressources avec le chiffrement PlayReady ou le chiffrement d’enveloppe AES 128 bits. Lorsqu’il est configuré de manière appropriée, Azure Media Player permet le déchiffrement du contenu chiffré avec PlayReady et AES 128 bits. 

Pour plus d'informations :

* [Azure Media Player](http://aka.ms/ampinfo)
* [Documentation d’Azure Media Player](http://aka.ms/ampdocs) 
* [Blog de prise en main d’Azure Media Player](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [S’inscrire toostay des toodate avec hello plus récentes à partir d’Azure Media Player](http://aka.ms/ampsignup)
* [Ajouter de nouvelles demandes de fonctionnalités, des idées et des commentaires](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Autres outils pour la création d’applications de lecteur
Vous pouvez également utiliser une des hello suivant des kits de développement logiciel :

* [Kit de développement logiciel (SDK) de client de diffusion en continu lisse](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Didacticiel d’application Windows Store de diffusion en continu lisse](media-services-build-smooth-streaming-apps.md)
* [Plateforme multimédia Microsoft : infrastructure de lecteur](http://playerframework.codeplex.com/) 
* [Documentation de l’infrastructure de lecteur HTML5](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Plug-in de diffusion en continu lisse Microsoft pour OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licence du kit de portage du client de diffusion en continu lisse Microsoft®](http://aka.ms/sspk) 
* [Développement d’applications vidéo pour XBOX](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Publicité
Azure Media Services assure la prise en charge pour l’insertion de publicités via hello plateforme Windows Media : Player Frameworks. Des infrastructures de lecteur avec prise en charge des publicités sont disponibles pour les périphériques Windows 8, Silverlight, Windows Phone 8 et iOS. Chaque player framework contient des exemples de code qui vous montre comment tooimplement une application de lecteur. Il existe trois sortes de publicités différentes que vous pouvez insérer dans votre contenu multimédia :

Linéaire : publicité en plein cadre qui interrompent la vidéo principale de hello

Non-linéaire : publicité superposée qui s’affichent lorsque la lecture de la vidéo principale hello, généralement un logo ou autre image statique est placé dans le lecteur hello

Compagnon : publicité qui s’affichent en dehors du lecteur de hello

Les publicités peuvent être placées à n’importe quel point dans la chronologie de la vidéo principale hello. Vous devez indiquer le lecteur hello lorsque tooplay hello ad et qui tooplay de publicités. Cela s’effectue via un ensemble de fichiers XML standard : Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) et Digital Video Player Ad Interface Definition (VPAID). Les fichiers VAST spécifient quels toodisplay de publicités. Fichiers VMAP indiquent quand tooplay différentes publicités et contient du code XML VAST. Les fichiers MAST sont des publicités toosequence façon un autre contenant aussi du code XML VAST. Les fichiers VPAID définissent une interface entre le lecteur vidéo hello et Active Directory de hello ou serveur Active Directory. Pour plus d’informations, consultez la page [Insertion de publicités](https://msdn.microsoft.com/library/dn387398.aspx).

Pour en savoir plus sur la prise en charge du sous-titrage et des publicités dans les vidéos en flux continu, consultez la page [Normes de sous-titrage et d’insertion de publicités prises en charge](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Voir aussi
[Incorporation d'une vidéo de diffusion en continu adaptative MPEG-DASH dans une application HTML5 avec DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Référentiel dash.js GitHub](https://github.com/Dash-Industry-Forum/dash.js)

