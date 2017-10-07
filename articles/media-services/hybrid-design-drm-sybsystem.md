---
title: "conception d’aaaHybrid d’un ou plusieurs sous-systèmes DRM à l’aide d’Azure Media Services | Documents Microsoft"
description: "Cette rubrique explique comment concevoir des modèles hybrides de sous-systèmes de gestion des droits numériques (DRM) à l’aide d’Azure Media Services."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>Conception de modèles hybrides de sous-systèmes de DRM

Cette rubrique explique comment concevoir des modèles hybrides de sous-systèmes de gestion des droits numériques (DRM) à l’aide d’Azure Media Services.

## <a name="overview"></a>Vue d'ensemble

Azure Media Services prend en charge hello suivant trois système :

* PlayReady
* Widevine (Modular)
* FairPlay

prise en charge de la gestion des droits numériques Hello inclut le chiffrement de gestion des droits numériques (chiffrement dynamique) et de remise de licences, avec Azure Media Player prenant en charge tous les 3 DRMs comme un lecteur de navigateur Kit de développement logiciel.

Pour une description détaillée de la conception du sous-système DRM/CENC et d’implémentation, consultez le document intitulé hello [CENC avec Multi-DRM et contrôle d’accès](media-services-cenc-with-multidrm-access-control.md).

Même si nous offrent une prise en charge complète pour les trois systèmes DRM, parfois, les clients doivent toouse différentes parties de leurs propre infrastructure/sous-systèmes addition tooAzure Media Services toobuild un sous-système DRM hybride.

Voici quelques-unes des questions que les clients nous posent souvent :

* « Puis-je utiliser mes propres serveurs de licences DRM ? » (Dans ce cas, les clients ont investi dans une batterie de serveurs de licences DRM avec une logique métier incorporée.)
* « Puis-je utiliser votre service de remise de licence DRM sans héberger de contenu dans Azure Media Services ? »

## <a name="modularity-of-hello-ams-drm-platform"></a>Modularité de hello plate-forme AMS DRM

Partie intégrante d’une plateforme vidéo cloud complète, le système de DRM d’Azure Media Services a été conçu dans un souci de flexibilité et de modularité. Vous pouvez utiliser Azure Media Services avec les hello suivant différentes combinaisons décrites dans le tableau hello ci-dessous (notation hello utilisée dans la table de hello est décrit ci-dessous). 

|**Hébergement et origine du contenu**|**Chiffrement du contenu**|**Remise de licence DRM**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|Tiers|
|AMS|Tiers|AMS|
|AMS|Tiers|Tiers|
|Tiers|Tiers|AMS|

### <a name="content-hosting--origin"></a>Hébergement et origine du contenu

* AMS : la ressource vidéo est hébergée dans AMS et la diffusion en continu se fait via les points de terminaison de streaming d’AMS (mais pas nécessairement l’empaquetage dynamique).
* Tiers : la vidéo est hébergée et diffusée sur une plateforme de streaming tierce en dehors d’AMS.

### <a name="content-encryption"></a>Chiffrement du contenu

* AMS : le chiffrement du contenu est effectué dynamiquement/à la demande à l’aide du chiffrement dynamique d’AMS.
* Tiers : le chiffrement du contenu est effectué en dehors d’AMS à l’aide d’un workflow de prétraitement.

### <a name="drm-license-delivery"></a>Remise de licence DRM

* AMS : la licence DRM est distribuée par le service de remise de licence d’AMS.
* Tiers : la licence DRM est distribuée par un serveur de licences DRM tiers en dehors d’AMS.

## <a name="configure-based-on-your-hybrid-scenario"></a>Configuration en fonction de votre scénario hybride

### <a name="content-key"></a>Clé de contenu

Étapes de configuration d’une clé de contenu, vous pouvez contrôler hello suivant des attributs de chiffrement dynamique de AMS et service de remise de licences AMS :

* clé de contenu Hello utilisé pour le chiffrement de DRM dynamique.
* Toobe de contenu de licences DRM fournis par les services de livraison de licence : clé de contenu, des droits et des restrictions.
* Le type de **restriction de la stratégie d’autorisation de clé de contenu** : restriction ouverte, IP ou par jeton.
* Si **jeton** le type de **sert de restriction de la stratégie d’autorisation de clé contenu**, hello **restriction de la stratégie d’autorisation de clé de contenu** doivent être remplies avant l’émission d’une licence.

### <a name="asset-delivery-policy"></a>Stratégie de remise d’élément multimédia

Via la configuration d’une stratégie de remise actif, vous pouvez contrôler hello suivant des attributs utilisés par l’outil d’empaquetage dynamique AMS et chiffrement dynamique d’un point de terminaison de diffusion en continu de AMS :

* L’association d’un protocole de diffusion en continu et d’un chiffrement DRM, telle que DASH sous CENC (PlayReady et Widevine), la diffusion en continu lisse sous PlayReady, ou encore HLS sous Widevine ou PlayReady.
* URL par défaut/incorporé Hello licence remise pour chacun des hello impliqués DRMs.
* Si les URL d’acquisition de licence (LA_URL) dans un fichier DASH MPD ou une playlist HLS contiennent une chaîne de requête d’ID de clé (KID) pour Widevine et FairPlay, respectivement.

## <a name="scenarios-and-samples"></a>Scénarios et exemples

Selon les explications hello dans la section précédente de hello, hello suivant cinq scénarios hybrides utiliser respectifs **clé de contenu**-**stratégie de livraison des actifs** (hello les combinaisons de configurations suivent la table de hello exemples mentionnés dans la dernière colonne de hello) :

|**Hébergement et origine du contenu**|**Chiffrement DRM**|**Remise de licence DRM**|**Configuration de la clé de contenu**|**Configurer une stratégie de distribution d’éléments multimédias**|**Exemple**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|Oui|Oui|Exemple 1|
|AMS|AMS|Tiers|Oui|Oui|Exemple 2|
|AMS|Tiers|AMS|Oui|Non|Exemple 3|
|AMS|Tiers|Extérieur|Non|Non|Exemple 4|
|Tiers|Tiers|AMS|Oui|Non|    

Dans les exemples de hello, la protection PlayReady fonctionne pour tiret et la diffusion en continu lisse. Hello vidéo URL ci-dessous sont les URL de diffusion en continu lisses. tooget hello URL tiret correspondantes, qu’il suffit d’ajouter « (format = mpd-heure-csf) ». Vous pouvez utiliser hello [azure media player de test](http://aka.ms/amtest) tootest dans un navigateur. Il vous permet de tooconfigure qui toouse de protocole, sous les techniques de diffusion en continu. IE11 et MS Edge sur Windows 10 prennent en charge PlayReady via EME. Pour plus d’informations, consultez [plus d’informations sur hello tester l’outil](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).

### <a name="sample-1"></a>Exemple 1

* URL source (de base) : https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* LA_URL PlayReady (DASH et diffusion en continu lisse) : https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* LA_URL Widevine (DASH) : https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* LA_URL FairPlay (TLS) : https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>Exemple 2

* URL source (de base) : http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* LA_URL PlayReady (DASH et diffusion en continu lisse) : http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>Exemple 3

* URL source : https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* LA_URL PlayReady (DASH et diffusion en continu lisse) : https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>Exemple 4

* URL source : https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* LA_URL PlayReady (DASH et diffusion en continu lisse) : https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>Résumé

En résumé, les composants DRM d’Azure Media Services sont flexibles, vous pouvez les utiliser dans un scénario hybride en configurant correctement la clé de contenu et la stratégie de remise de ressources, comme indiqué dans cette rubrique.

## <a name="next-steps"></a>Étapes suivantes
Afficher les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

