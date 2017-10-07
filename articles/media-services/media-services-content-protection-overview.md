---
title: aaaProtect votre contenu avec Azure Media Services | Documents Microsoft
description: "Cet article donne une vue d’ensemble de la protection du contenu avec Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Vue d’ensemble de la protection du contenu
Microsoft Azure Media Services permet de vous toosecure votre média à partir de l’heure hello qu'il quitte votre ordinateur via le stockage, le traitement et la remise. Media Services vous permet de toodeliver votre direct et à la demande le contenu chiffré dynamiquement avec chiffrement AES (Advanced Standard) (à l’aide de clés de chiffrement 128 bits) ou l’une des hello DRMs principales : Microsoft PlayReady, Google Widevine et Apple FairPlay. Media Services fournit également un service de fourniture de clés AES et tooauthorized clients des licences DRM (PlayReady, Widevine et FairPlay). 

Hello suivant image montre hello protection du contenu des flux de travail qui prend en charge de AMS. 

![Protéger avec PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart de diffusion en continu de votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, hello de point de terminaison de diffusion en continu à partir de laquelle vous souhaitez que le contenu toostream a toobe Bonjour **en cours d’exécution** état. 

Cette rubrique explique [concepts et terminologie](media-services-content-protection-overview.md) protection du contenu avec AMS toounderstanding pertinentes. Hello présente également les [liens](media-services-content-protection-overview.md#common-scenarios) tootopics qui montrent comment tooachieve les tâches de protection de contenu. 

## <a name="dynamic-encryption"></a>Chiffrement dynamique
Microsoft Azure Media Services vous permet de toodeliver votre contenu chiffré dynamiquement avec la clé en clair AES ou le chiffrement de la gestion des droits numériques : Microsoft PlayReady, Google Widevine et FairPlay d’Apple.

Actuellement, vous pouvez chiffrer hello suivant les formats de diffusion en continu : TLS, MPEG DASH et diffusion en continu lisse. Vous ne pouvez pas chiffrer les téléchargements progressifs.

Si vous souhaitez un élément multimédia pour tooencrypt de Media Services, vous devez tooassociate une clé de chiffrement (CommonEncryption ou EnvelopeEncryption) avec votre élément multimédia et également configurer les stratégies d’autorisation pour la clé de hello.

Vous devez également la stratégie de livraison de l’actif tooconfigure hello. Si vous voulez toostream un élément multimédia chiffré de stockage, assurez-vous que toospecify comment vous souhaitez que toodeliver il en configurant la stratégie de livraison des actifs.

Lorsqu’un flux de données est demandée par un lecteur, Media Services utilise hello spécifié toodynamically clé chiffrer votre contenu à l’aide de la clé en clair AES ou le chiffrement de la gestion des droits numériques. flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello. toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.


## <a name="storage-encryption"></a>Chiffrement du stockage
Utilisez tooencrypt de chiffrement de stockage de votre contenu en clair localement à l’aide du chiffrement AES 256 bits, puis le télécharger tooAzure Storage où il est stocké et chiffré au repos. Les éléments multimédias protégés par chiffrement de stockage sont automatiquement déchiffrés et placés dans un tooencoding préalable de système de fichiers chiffrés et éventuellement RE-chiffrée toouploading préalable comme un nouvel élément multimédia de sortie. Hello est principalement utilisé pour le chiffrement de stockage lorsque vous souhaitez toosecure vos fichiers multimédias d’entrée de haute qualité avec un chiffrement renforcé au reste sur le disque.

Dans l’ordre toodeliver un élément multimédia chiffré de stockage, vous devez configurer la stratégie de remise de hello actif afin que Media Services sache comment vous souhaitez que toodeliver votre contenu. Avant que votre élément multimédia peut être transmis en continu, hello de diffusion en continu flux et chiffrement de stockage de serveur supprime hello votre contenu à l’aide de hello spécifié de stratégie de remise (par exemple, AES, chiffrement commun ou aucun chiffrement).

## <a name="common-encryption-cenc"></a>Chiffrement commun (CENC)
Le chiffrement commun est utilisé pour chiffrer votre contenu avec PlayReady ou/et Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Utilisation du chiffrement cbcs-aapl
cbcs-aapl est utilisé pour chiffrer votre contenu avec FairPlay.

## <a name="envelope-encryption"></a>Chiffrement d’enveloppe
Utilisez cette option si vous souhaitez tooprotect votre contenu avec la clé en clair AES-128. Si vous souhaitez une option plus sécurisée, choisissez l’une des hello DRMs répertoriées dans cette rubrique. 

## <a name="licenses-and-keys-delivery-service"></a>Service de remise de licences et de clés
Media Services fournit un service de fourniture de licences DRM (PlayReady, Widevine, FairPlay) et les clients tooauthorized de clés en clair AES. Vous pouvez utiliser [hello portail Azure](media-services-portal-protect-content.md), API REST ou Media Services SDK pour .NET tooconfigure authentifications et les stratégies pour les licences et les clés.

## <a name="token-restriction"></a>Restriction à jeton
Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : ouvrir ou de restriction de jeton. stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité). Media Services prend en charge les jetons dans les formats de jetons SWT (Simple Web Tokens) hello et JSON Web Token (JWT). Media Services ne fournit pas de services de jeton sécurisé. Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS. Hello STS doit être configuré toocreate un jeton signé avec hello spécifié clé et émettre les revendications que vous avez spécifié dans la configuration de restriction token hello. les revendications Hello Media Services, service de distribution de clés renvoie hello demandé hello et clé (ou licence) client toohello si hello jeton est valide dans hello jeton correspondent à celles configurées pour la clé de hello (ou licence).

Lorsque vous configurez la stratégie de restriction token hello, vous devez spécifier la clé de vérification principale hello, l’émetteur et paramètres de l’audience. clé de vérification principale Hello contient hello clé que le jeton de hello a été signé avec, l’émetteur est hello sécurisé STS qui émet le jeton de hello. audience Hello (parfois appelé étendue) décrit l’intention de hello du jeton de hello ou autorise l’accès au jeton de hello ressource hello. Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.

## <a name="streaming-urls"></a>URL de diffusion
Si votre élément multimédia a été chiffré avec plusieurs DRM, vous devez utiliser une balise de chiffrement dans les URL de diffusion en continu de hello : (format = 'm3u8-aapl', chiffrement = 'xxx').

Hello suivant considérations s’appliquent :

* Seul zéro ou un type de chiffrement peut être spécifié.
* Type de chiffrement ne dispose pas toobe spécifié dans les url de hello si seul un chiffrement a été appliqué toohello actif.
* Le type de chiffrement ne tient pas compte de la casse.
* Hello, les types de chiffrement suivants peut être spécifié :  
  * **cenc** : chiffrement commun (Playready ou Widevine)
  * **des CBC-aapl**: Fairplay
  * **cbc**: chiffrement de l’enveloppe AES.

## <a name="common-scenarios"></a>Scénarios courants
Hello les rubriques suivantes montrent comment tooprotect le contenu dans le stockage, fournir dynamiquement chiffré de diffusion multimédia en continu, utiliser le service de remise de clé/licence AMS

* [Offrir une protection basée sur AES](media-services-protect-with-aes128.md) 
* [Protection avec PlayReady et/ou Widevine ](media-services-protect-with-drm.md)
* [Diffuser en continu votre contenu HLS protégé avec Apple FairPlay et/ou PlayReady](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Autres cas de figure
* [Comment toointegrate la licence PlayReady Azure service avec votre propre chiffreur/serveur de diffusion](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [À l’aide de tooAzure de licences DRM castLabs toodeliver Media Services](media-services-castlabs-integration.md)

>[!NOTE]
>Les scénarios où vous utilisez un serveur (ou une technologie) DRM externe et un flux provenant d’AMS ne sont pas pris en charge pour le moment.


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Liens connexes
[Annonce de PlayReady en tant que service et du chiffrement AES dynamique avec Azure Media Services](http://mingfeiy.com/playready)

[Explication de la tarification de la remise de licences PlayReady d’Azure Media Services](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Mode de chiffrement de flux de données dans Azure Media Services toodebug pour AES](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Authentification par jeton JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Intégration d'une application Azure Media Services basée sur OWIN MVC avec Azure Active Directory et une remise de clé de contenu basée sur les revendications JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/)

[Utilisez les jetons ACS Azure tooissue](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
