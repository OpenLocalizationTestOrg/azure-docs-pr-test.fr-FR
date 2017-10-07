---
title: "à l’aide du contenu stratégie d’autorisation de clé aaaConfigure hello portail Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure une stratégie d’autorisation pour une clé de contenu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Configuration de la stratégie d’autorisation de clé de contenu
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services vous permet de toodeliver MPEG-DASH, Smooth Streaming et les flux HTTP Live Streaming (HLS) protégés avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS permet également de vous toodeliver tiret flux chiffrés avec Widevine DRM. PlayReady et Widevine sont chiffrées par hello spécification de chiffrement commun (CENC 23001-7 de norme ISO/IEC).

Media Services fournit également un **Service de remise de clé/licence** à partir desquels les clients peuvent obtenir des clés AES ou PlayReady/Widevine licences tooplay hello contenu chiffré.

Cette rubrique montre comment toouse hello stratégie de contenu d’autorisation de clé hello tooconfigure portail Azure. clé de Hello peut être utilisée ultérieurement toodynamically chiffrer votre contenu. Notez que vous pouvez actuellement chiffrer hello suivant les formats de diffusion en continu : TLS, MPEG DASH et diffusion en continu lisse. Vous ne pouvez pas chiffrer les téléchargements progressifs.

Lorsqu’un lecteur demande le flux de données qui a la valeur toobe dynamiquement chiffré, Media Services utilise hello configuré clé toodynamically chiffrer votre contenu à l’aide du chiffrement AES ou la gestion des droits numériques. flux de données toodecrypt hello, le lecteur hello demande clé de hello de service de distribution de clés hello. toodecide soit ou non d’utilisateur de hello autorisé clé de hello tooget, hello évalue les stratégies d’autorisation hello que vous avez spécifié pour la clé de hello.

Si vous envisagez de toohave plusieurs clés de contenu ou que vous voulez toospecify un **Service de remise de clé/licence** URL de hello service de distribution de clés de Media Services, utilisez Media Services .NET SDK ou des API REST.

[Configurer la stratégie d’autorisation de clé de contenu à l’aide du Kit de développement logiciel (SDK).NET Media Services](media-services-dotnet-configure-content-key-auth-policy.md)

[Configurer la stratégie d’autorisation de clé de contenu à l’aide de l’API REST Media Services](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Certaines considérations s’appliquent :
* Création de votre compte AMS un **par défaut** point de terminaison de diffusion en continu est ajoutée tooyour compte Bonjour **arrêté** état. toostart votre contenu et profitez de l’empaquetage dynamique et chiffrement dynamique, votre point de terminaison de diffusion en continu de diffusion en continu a toobe Bonjour **en cours d’exécution** état. 
* Votre ressource doit contenir un ensemble de MP4 à débit adaptatif ou des fichiers de diffusion en continu lisse à débit adaptatif. Pour plus d'informations, consultez [Encoder une ressource](media-services-encode-asset.md).
* Hello service de fourniture de clé met en cache ContentKeyAuthorizationPolicy et les objets associés (options de stratégie et les restrictions) pendant 15 minutes.  Si vous créez une stratégie ContentKeyAuthorizationPolicy et spécifiez toouse une restriction « Token », puis testez, puis mettre à jour de stratégie de hello trop « ouvrir » restriction, il prendra environ 15 minutes avant hello commutateurs toohello « Ouvert » version de stratégie de la stratégie de hello.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Comment : configurer la stratégie d’autorisation de clé de hello
stratégie d’autorisation de clé de tooconfigure hello, sélectionnez hello **PROTECTION du contenu** page.

Media Services prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé. stratégie d’autorisation de clé contenu de Hello **ouvrir**, **jeton**, ou **IP** restrictions d’autorisation (**IP** peut être configuré avec REST ou .NET SDK).

### <a name="open-restriction"></a>Restriction ouverte
Hello **ouvrir** restriction signifie hello système fournit des tooanyone clé hello qui fait la demande. Cette restriction peut être utile à des fins de test.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Restriction à jeton
jeton de hello toochoose restreint la stratégie, appuyez sur hello **jeton** bouton.

Hello **jeton** stratégie restreint doit être accompagnée d’un jeton émis par une **Service d’émission de jeton sécurisé** (STS). Media Services prend en charge les jetons Bonjour **des jetons Web simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format et **jeton Web JSON** format (JWT). Pour plus d’informations, consultez [Authentification à jeton JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Media Services ne fournit pas de **services de jeton sécurisé**. Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS. Hello STS doit être configuré toocreate un jeton signé avec hello spécifié clé et émettre les revendications que vous avez spécifié dans la configuration de restriction token hello. Hello service de distribution de clés de Media Services renvoie client de toohello clé de chiffrement hello si hello du jeton est valide et hello revendications de jeton de hello correspondent à ceux configurés pour la clé de contenu hello. Pour plus d’informations, consultez [les jetons tooissue utilisation Azure ACS](http://mingfeiy.com/acs-with-key-services).

Lors de la configuration hello **jeton** stratégie restreint, vous devez définir des valeurs pour **clé de vérification**, **émetteur** et **public**. clé de vérification principale Hello contient hello clé que le jeton de hello a été signé avec, l’émetteur est hello sécurisé STS qui émet le jeton de hello. audience Hello (parfois appelé étendue) décrit l’intention de hello du jeton de hello ou autorise l’accès au jeton de hello ressource hello. Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.

### <a name="playready"></a>PlayReady
Lorsque vous protégez votre contenu avec **PlayReady**, un hello choses toospecify dans votre stratégie d’autorisation est une chaîne XML qui définit le modèle de licence PlayReady hello. Par défaut, hello suivant la stratégie est définie :

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices><ContentKey i:type="ContentEncryptionKeyFromHeader" /><LicenseType>Nonpersistent</LicenseType><PlayRight><AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput></PlayRight></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>

Vous pouvez cliquer sur hello **importer le xml de stratégie** bouton et fournir un autre XML conforme toohello schéma XML défini [ici](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Étape suivante
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

