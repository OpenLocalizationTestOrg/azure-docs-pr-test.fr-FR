---
title: aaaUsing castLabs toodeliver Widevine licences tooAzure Media Services | Documents Microsoft
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs. la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par le serveur de licences castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>À l’aide de tooAzure de licences Widevine castLabs toodeliver Media Services
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) toodeliver un flux qui est chiffré dynamiquement par AMS avec PlayReady et Widevine DRMs. la licence PlayReady Hello est fourni à partir du serveur de licences PlayReady de Media Services et les licences Widevine sont remis par **castLabs** serveur de licences.

tooplayback de diffusion en continu de contenu protégé par CENC (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Pour plus d’informations, consultez le [document AMP](http://amp.azure.net/libs/amp/latest/docs/) .

Hello suivant schéma montre une architecture d’intégration Azure Media Services et castLabs globale.

![intégration](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Configuration système classique
* Le contenu multimédia est stocké dans AMS.
* Les ID des clés de contenu sont stockées à la fois dans castLabs et AMS.
* castLabs et AMS intègrent une authentification par jeton. Hello les sections suivantes traite des jetons d’authentification. 
* Lorsqu’un client demande vidéo de hello toostream, hello le contenu est dynamiquement chiffré avec **chiffrement commun** (CENC) et de façon dynamique AMS tooSmooth tiret et diffusion en continu. Nous offrons également un chiffrement de flux élémentaire PlayReady M2TS pour le protocole de diffusion en continu HLS.
* La licence PlayReady est récupérée auprès du serveur de licences AMS et licence Widevine est récupérée auprès du serveur de licences castLabs. 
* Media Player décide automatiquement le toofetch de licence en fonction de la capacité de plate-forme client hello. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Génération de jetons d'authentification pour l'obtention d'une licence
CastLabs et AMS prend en charge de JWT (JSON Web Token) format de jeton utilisée tooauthorize une licence. 

### <a name="jwt-token-in-ams"></a>Jeton JWT dans AMS
Hello tableau suivant décrit le jeton JWT dans AMS. 

| Émetteur | Chaîne de l’émetteur hello choisi Service (jeton de sécurité) |
| --- | --- |
| Public ciblé |Chaîne d’audience à partir de hello utilisé STS |
| Revendications |Ensemble de revendications |
| NotBefore |Démarrer la validité du jeton de hello |
| Expires |Validité de fin du jeton de hello |
| SigningCredentials |clé Hello qui est partagé entre le serveur de licences PlayReady, castLabs serveur de licences et STS, il peut être la clé symétrique ou asymétrique. |

### <a name="jwt-token-in-castlabs"></a>Jeton JWT dans castLabs
Hello tableau suivant décrit le jeton JWT dans castLabs. 

| Nom | Description |
| --- | --- |
| optData |Chaîne JSON contenant des informations sur vous. |
| crt |Une JSON chaîne contenant des informations sur les actifs de hello, ses droits de lecture et les informations de licence. |
| iat |Hello date/heure actuelle dans une époque déterminée. |
| jti |Un identificateur unique sur ce jeton (chaque jeton peut uniquement servir une fois dans le système de castLabs hello). |

## <a name="sample-solution-set-up"></a>Exemple de configuration de solution
Hello [exemple de solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) se compose de deux projets :

* Une application console qui peut être des restrictions de DRM tooset utilisé sur un élément multimédia déjà réceptionné, PlayReady et Widevine.
* Une application web qui délivre les jetons, qui peut être considérée comme une version TRÈS SIMPLIFIÉE d'un STS.

application de console toouse hello :

1. Modifier les informations d’identification de hello app.config toosetup AMS, informations d’identification castLabs, configuration du service STS et une clé partagée.
2. Téléchargez un élément multimédia dans AMS.
3. Get hello UUID de hello téléchargé Asset et modifiez 32 de ligne dans le fichier Program.cs de hello :
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Utiliser un AssetId pour nommer des ressources de hello dans le système de castLabs hello (44 de ligne dans le fichier Program.cs de hello).
   
   Vous devez définir AssetId pour **castLabs**; il doit toobe une chaîne alphanumérique unique.
5. Exécutez le programme de hello.

toouse hello Web Application (STS) :

1. Vendeur de modification hello web.config toosetup castlabs ID, configuration du service STS hello et la clé partagée de hello.
2. Déployer tooAzure sites Web.
3. Accédez du site Web toohello.

## <a name="playing-back-a-video"></a>Lecture d'une vidéo
tooplayback une vidéo chiffrées avec un chiffrement commun (PlayReady et/ou Widevine), vous pouvez utiliser hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Lorsque vous exécutez l’application de console hello, hello ID de clé de contenu et hello URL de manifeste sont renvoyées.

1. Ouvrez un nouvel onglet et lancez votre STS : http://[nom_sts].azurewebsites.net/api/token/assetid/[id_élément_multimédia_castlabs]/contentkeyid/[id_clé_contenu].
2. Accédez trop[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Collez hello URL de diffusion en continu.
4. Cliquez sur hello **Options avancées** case à cocher.
5. Bonjour **Protection** liste déroulante, sélectionnez PlayReady et/ou Widevine.
6. Collez le jeton hello que vous avez obtenu votre STS dans la zone de texte de jeton hello. 
   
   serveur de licences Hello castLab n’a pas besoin hello « support = « préfixe devant le jeton de hello. Par conséquent, veuillez supprimer avant d’envoyer le jeton de hello.
7. Mettre à jour le lecteur hello.
8. Hello vidéo doit jouer.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

