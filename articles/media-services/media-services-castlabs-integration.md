---
title: "Utilisation de castLabs pour fournir des licences Widevine à Azure Media Services | Microsoft Docs"
description: "Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir un flux chiffré dynamiquement par AMS avec des DRM PlayReady et Widevine. La licence PlayReady provient du serveur de licences Media Services PlayReady et la licence Widevine est délivrée par le serveur de licences castLabs."
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
ms.openlocfilehash: 5b69e804809f834e81221fb2787a997a52dbe286
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-castlabs-to-deliver-widevine-licenses-to-azure-media-services"></a>Utilisation de castLabs pour fournir des licences Widevine à Azure Media Services
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment vous pouvez utiliser Azure Media Services (AMS) pour fournir un flux chiffré dynamiquement par AMS avec des DRM PlayReady et Widevine. La licence PlayReady provient du serveur de licences Media Services PlayReady et la licence Widevine est délivrée par le serveur de licences **castLabs** .

Pour lire un contenu en streaming protégé par CENC (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Pour plus d’informations, consultez le [document AMP](http://amp.azure.net/libs/amp/latest/docs/) .

Le diagramme suivant représente une architecture qui intègre Azure Media Services et castLabs.

![intégration](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Configuration système classique
* Le contenu multimédia est stocké dans AMS.
* Les ID des clés de contenu sont stockées à la fois dans castLabs et AMS.
* castLabs et AMS intègrent une authentification par jeton. Les sections suivantes décrivent les jetons d'authentification. 
* Quand un client demande à diffuser en continu la vidéo, le contenu est chiffré dynamiquement par **chiffrement commun** (CENC) et empaqueté dynamiquement par AMS en Smooth Streaming ou DASH. Nous offrons également un chiffrement de flux élémentaire PlayReady M2TS pour le protocole de diffusion en continu HLS.
* La licence PlayReady est récupérée auprès du serveur de licences AMS et licence Widevine est récupérée auprès du serveur de licences castLabs. 
* Media Player détermine automatiquement quelles licences récupérer en fonction de la capacité de la plateforme client. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Génération de jetons d'authentification pour l'obtention d'une licence
AMS et castLabs prennent en charge le format de jeton JWT (jeton web JSON) utilisé pour autoriser une licence. 

### <a name="jwt-token-in-ams"></a>Jeton JWT dans AMS
Le tableau suivant décrit le jeton JWT dans AMS. 

| Émetteur | Chaîne d'émetteur issue du service de jeton sécurisé (STS) choisi |
| --- | --- |
| Public ciblé |Chaîne de public issue du STS utilisé |
| Revendications |Ensemble de revendications |
| NotBefore |Début de validité du jeton |
| Expires |Fin de validité du jeton |
| SigningCredentials |Clé partagée entre le serveur de licences PlayReady, le serveur de licences castLabs et le STS. Elle peut être symétrique ou asymétrique. |

### <a name="jwt-token-in-castlabs"></a>Jeton JWT dans castLabs
Le tableau suivant décrit le jeton JWT dans castLabs. 

| Nom | Description |
| --- | --- |
| optData |Chaîne JSON contenant des informations sur vous. |
| crt |Chaîne JSON contenant des informations sur l'élément multimédia, ses informations de licence et ses droits de lecture. |
| iat |Date/heure actuelle de l'époque. |
| jti |Identificateur unique relatif à ce jeton (chaque jeton peut être utilisé une seule fois dans le système castLabs). |

## <a name="sample-solution-set-up"></a>Exemple de configuration de solution
L' [exemple de solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) se compose de deux projets :

* Une application console qui peut être utilisée pour définir des restrictions DRM sur un élément multimédia déjà ingéré, à la fois pour PlayReady et Widevine.
* Une application web qui délivre les jetons, qui peut être considérée comme une version TRÈS SIMPLIFIÉE d'un STS.

Pour utiliser l'application console :

1. Modifiez le fichier app.config pour configurer les informations d'identification AMS, les informations d'identification castLabs, la configuration du STS et la clé partagée.
2. Téléchargez un élément multimédia dans AMS.
3. Obtenez l'UUID de l'élément multimédia téléchargé et modifiez la ligne 32 dans le fichier Program.cs :
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Utilisez un AssetId pour nommer l'élément multimédia dans le système castLabs (ligne 44 dans le fichier Program.cs).
   
   Vous devez définir AssetId pour **castLabs**; il doit s'agir d'une chaîne alphanumérique unique.
5. Exécutez le programme.

Pour utiliser l'application web (STS) :

1. Modifiez le fichier web.config pour configurer l'ID du prestataire castlabs, le STS et la clé partagée.
2. Déployez-le sur des sites web Azure.
3. Accédez au site web.

## <a name="playing-back-a-video"></a>Lecture d'une vidéo
Pour lire une vidéo chiffrée par chiffrement commun (PlayReady et/ou Widevine), vous pouvez utiliser [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Pendant l'exécution de l'application console, l'ID de la clé de contenu et l'URL du manifeste sont renvoyés.

1. Ouvrez un nouvel onglet et lancez votre STS : http://[nom_sts].azurewebsites.net/api/token/assetid/[id_élément_multimédia_castlabs]/contentkeyid/[id_clé_contenu].
2. Accédez à [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Collez l'URL de diffusion en continu.
4. Cochez la case **Options avancées** .
5. Dans la liste déroulante **Protection** , sélectionnez PlayReady et/ou Widevine.
6. Collez le jeton que vous avez obtenu de votre STS dans la zone de texte Jeton. 
   
   Le serveur de licences castLab n'a pas besoin du préfixe « Bearer= » devant le jeton. Par conséquent, supprimez-le avant d'envoyer le jeton.
7. Mettez à jour le lecteur.
8. La vidéo doit pouvoir être lue.

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

