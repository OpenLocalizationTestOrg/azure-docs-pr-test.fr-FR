---
title: "à l’aide des stratégies de protection du contenu aaaConfiguring hello portail Azure | Documents Microsoft"
description: "Cet article explique comment toouse hello des stratégies de protection du contenu tooconfigure portail Azure. Hello article également montre comment le chiffrement dynamique tooenable pour vos ressources."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Configuration des stratégies de protection du contenu à l’aide de hello portail Azure
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Vue d'ensemble
Microsoft Azure Media Services (AMS) permet de vous toosecure votre média à partir de l’heure hello qu'il quitte votre ordinateur via le stockage, le traitement et la remise. Media Services vous permet de toodeliver votre contenu chiffré dynamiquement avec Advanced Encryption Standard (AES) (à l’aide de clés de chiffrement 128 bits), chiffrement commun (CENC) à l’aide de PlayReady et/ou Widevine DRM et FairPlay d’Apple. 

AMS fournit un service de fourniture de licences DRM et les clients tooauthorized de clés en clair AES. Hello portail Azure vous permet de toocreate un **stratégie d’autorisation de clé/licence** pour tous les types de chiffrements.

Cet article explique comment tooconfigure avec hello portail Azure, les stratégies de protection de contenu. Hello article également montre comment actifs de tooyour tooapply chiffrement dynamique.


> [!NOTE]
> Si vous avez utilisé des stratégies de protection toocreate de portail classique Azure hello, les stratégies de hello ne peuvent pas apparaître dans hello [portail Azure](https://portal.azure.com/). Toutefois, hello toutes les anciennes stratégies toujours existe. Vous pouvez les examiner à l’aide de hello Azure Media Services .NET SDK ou hello [-Media--Explorateur des Services Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) outil (stratégies de hello toosee, avec le bouton droit sur l’élément multimédia de hello -> Affichage des informations (F4) -> cliquez sur l’onglet -> clés de contenu Cliquez sur la clé de hello). 
> 
> Si vous souhaitez tooencrypt votre élément multimédia à l’aide des nouvelles stratégies, configurez-les avec hello portail Azure, cliquez sur Enregistrer et appliquer le chiffrement dynamique. 
> 
> 

## <a name="start-configuring-content-protection"></a>Commencer à configurer la protection de contenu
les toostart portail hello toouse configuration de la protection de contenu, tooyour global AMS compte, procédez comme hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Sélectionnez **Paramètres** > **Protection du contenu**.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>stratégie d’autorisation de clé/licence
AMS prend en charge plusieurs méthodes d’authentification des utilisateurs effectuant des demandes de clé ou de licence. stratégie d’autorisation de clé contenu de Hello doit être configurée par vous et appliquée par votre client pour hello clé/licence toobe toohello delived client. Hello contenu clé peut avoir une ou plusieurs restrictions d’autorisation : **ouvrir** ou **jeton** restriction.

Hello portail Azure vous permet de toocreate un **stratégie d’autorisation de clé/licence** pour tous les types de chiffrements.

### <a name="open"></a>Ouverts
Restriction Open signifie que hello système fournit des tooanyone clé hello qui fait la demande. Cette restriction peut être utile à des fins de test. 

### <a name="token"></a>Jeton
stratégie de restriction token Hello doit être accompagné d’un jeton émis par un Service (jeton de sécurité). Media Services prend en charge les jetons dans les formats de jetons SWT (Simple Web Tokens) hello et JSON Web Token (JWT). Media Services ne fournit pas de services de jeton sécurisé. Vous pouvez créer un STS personnalisé ou tirer parti des jetons de tooissue Microsoft Azure ACS. Hello STS doit être configuré toocreate un jeton signé avec hello spécifié clé et émettre les revendications que vous avez spécifié dans la configuration de restriction token hello. les revendications Hello Media Services, service de distribution de clés renvoie hello demandé hello et clé (ou licence) client toohello si hello jeton est valide dans hello jeton correspondent à celles configurées pour la clé de hello (ou licence).

Lorsque vous configurez la stratégie de restriction token hello, vous devez spécifier la clé de vérification principale hello, l’émetteur et des paramètres de l’audience. clé de vérification principale Hello contient hello clé que le jeton de hello a été signé avec, l’émetteur est hello sécurisé STS qui émet le jeton de hello. audience Hello (parfois appelé étendue) décrit l’intention de hello du jeton de hello ou autorise l’accès au jeton de hello ressource hello. Hello service de distribution de clés de Media Services valide que ces valeurs dans le jeton de hello correspondent aux valeurs hello modèle de hello.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Modèle de droits PlayReady
Pour obtenir des informations détaillées sur le modèle de droits hello PlayReady, consultez [vue d’ensemble du modèle de licence PlayReady Media Services](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Non persistante
Si vous configurez la licence comme non persistant, il est uniquement conservée en mémoire pendant que le lecteur hello est à l’aide de licence de hello.  

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Persistante
Si vous configurez la licence de hello comme persistant, il est enregistré dans un stockage persistant sur le client de hello.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Modèle de droits Widevine
Pour obtenir des informations détaillées sur le modèle de droits Widevine hello, consultez [vue d’ensemble des modèles de licence Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>De base
Lorsque vous sélectionnez **base**, hello modèle sera créé avec toutes les valeurs par défaut.

### <a name="advanced"></a>Avancé
Pour obtenir une explication détaillée sur l’option avancée des configurations Widevine, consultez [cette](media-services-widevine-license-template-overview.md) rubrique.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Configuration de FairPlay
le chiffrement FairPlay tooenable, vous avez besoin tooprovide hello certificat de l’application et la clé de Secret d’Application (demandez) via hello option de Configuration de FairPlay. Pour obtenir des informations détaillées sur la configuration de FairPlay et de la configuration requise, consultez [cet](media-services-protect-hls-with-fairplay.md) article.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Appliquer asset tooyour de chiffrement dynamique
tootake parti du chiffrement dynamique, vous devez tooencode votre fichier source en un ensemble de fichiers MP4 à débit adaptatif.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Sélectionnez un élément multimédia que vous souhaitez tooencrypt
sélectionner de tous vos actifs, toosee **paramètres** > **actifs**.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Chiffrer avec AES ou DRM
Quand vous appuyez sur **Chiffrer** sur un élément multimédia, deux options s’offrent à vous : **AES** ou **DRM**. 

#### <a name="aes"></a>AES
Le chiffrement de clé en clair est activé sur tous les protocoles de diffusion en continu : Smooth Streaming, HLS et MPEG-DASH.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Lorsque vous sélectionnez hello DRM onglet, vous sont présentées avec différents choix de stratégies de protection du contenu (qui, vous devez configurer à ce stade) + d’un ensemble de protocoles de diffusion en continu.

* **PlayReady et Widevine avec MPEG-DASH** : chiffre dynamiquement votre flux MPEG-DASH avec les DRM PlayReady et Widevine.
* **PlayReady et Widevine avec MPEG-DASH+ FairPlay avec HLS** : chiffre dynamiquement votre flux MPEG-DASH avec les DRM PlayReady et Widevine. Chiffre également vos flux HLS avec FairPlay.
* **PlayReady uniquement avec Smooth Streaming, HLS et MPEG-DASH** : chiffre dynamiquement les flux Smooth Streaming, HLS, MPEG-DASH avec la DRM PlayReady.
* **Widevine uniquement avec MPEG-DASH** : chiffre dynamiquement votre MPEG-DASH avec la DRM Widevine.
* **FairPlay uniquement avec HLS** : chiffre dynamiquement votre flux HLS avec FairPlay.

le chiffrement FairPlay tooenable, vous avez besoin tooprovide hello certificat de l’application et la clé de Secret d’Application (demandez) via hello option FairPlay Configuration du Panneau de paramètres de Protection du contenu hello.

![Protéger du contenu](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Une fois votre sélection du chiffrement hello, appuyez sur **appliquer**.

>[!NOTE] 
>Si vous envisagez de tooplay une AES chiffrée TLS dans Safari, consultez [ce billet de blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

