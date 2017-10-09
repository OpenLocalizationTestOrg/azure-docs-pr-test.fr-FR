---
title: aaaAzure Forum aux questions de Media Services | Documents Microsoft
description: Forum Aux Questions (FAQ)
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Forum Aux Questions

Cet article répond aux questions fréquemment posées déclenchées par la Communauté d’utilisateurs hello Azure Media Services (AMS).

## <a name="general-ams-faqs"></a>Forum Aux Questions - Généralités AMS
Q : comment mettre à l’échelle l’indexation ?

A: unités de hello réservé sont hello même pour l’encodage et l’indexation des tâches. Suivez les instructions de [comment unités réservées d’encodage tooScale](media-services-scale-media-processing-overview.md). **Remarque** : le fonctionnement de l’indexeur n’est pas affecté par le type d’unité réservée.

Q : j’ai chargé, encodé et publié une vidéo. Quel serait vidéo de hello raison hello n’est pas lu lors de le toostream il ?

R : un des hello des raisons de la plus courante est inutile de hello de diffusion en continu de point de terminaison à partir de laquelle vous essayez de tooplayback Bonjour **en cours d’exécution** état.  

Q : la composition d’un flux dynamique est-elle possible ?

R : la composition de flux live est actuellement pas disponible dans Azure Media Services, et vous devez donc toopre-composer sur votre ordinateur.

Q : puis-je utiliser le CDN Azure avec la vidéo en flux continu ?

R : Media Services prend en charge l’intégration à Azure CDN (pour plus d’informations, consultez [comment tooManage points de terminaison de diffusion en continu dans un compte Media Services](media-services-portal-manage-streaming-endpoints.md)).  Vous pouvez utiliser la vidéo en flux continu avec le CDN. Azure Media Services fournit des sorties aux formats Smooth Streaming, HLS et MPEG-DASH. Tous ces formats utilisent le protocole HTTP pour transférer les données et bénéficient des avantages de la mise en cache HTTP. Dynamique de diffusion en continu des données audio/vidéo réelles est divisé toofragments et des fragments mis en cache dans le CDN. Uniquement les toobe besoins données actualisées donnée hello manifeste. CDN actualise régulièrement les données de manifeste.

Q : le stockage des images est-il pris en charge par Azure Media Services ?

R : Si vous souhaitez simplement toostore JPEG ou des images PNG, vous devez conserver celles figurant dans le stockage d’objets Blob Azure. Il n’existe aucun tooputting avantage dans vos Services de support compte sauf si vous souhaitez tookeep que les associé à vos vidéo ou Audio. Ou si vous pouvez avoir un toouse besoin hello images comme superpositions dans un encodeur vidéo de hello. Media Encoder Standard prend en charge les images de superposition par-dessus les vidéos, et c’est qu’il répertorie JPEG et PNG pris en charge d’entrée de formats. Pour plus d’informations, consultez la page [Création de superpositions](media-services-advanced-encoding-with-mes.md#overlay).

Q : Comment puis-je copier des ressources à partir d’un tooanother de compte Media Services.

R : toocopy des ressources à partir d’un tooanother de compte Media Services à l’aide de .NET, utilisez [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) méthode d’extension disponible dans hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) référentiel. Pour plus d’informations, consultez [cette publication de forum](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) .

Q : quelles sont les hello caractères pris en charge pour nommer les fichiers lorsque vous travaillez avec AMS ?

R : Media Services utilise la valeur hello hello IAssetFile.Name propriété lors de la génération d’URL pour hello de diffusion en continu de contenu (par exemple, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Pour cette raison, l’encodage par pourcentage n’est pas autorisé. Hello valeur Hello **nom** propriété ne peut pas avoir un des éléments suivants de hello [% réservés d’encodage de caractères](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): ! *' () ; : @& = + $, / ? % # [] ». En outre, il ne peut exister qu’un seul « . » pour l’extension de nom de fichier hello.

Q : comment tooconnect à l’aide de REST ?

R : pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services. Vous devez effectuer les appels suivants toohello nouvel URI. 

Q : Comment puis-je pivoter une vidéo pendant hello processus de codage.

R : hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) prend en charge de la rotation par les angles de 90/180/270. comportement par défaut de Hello est « Auto », où il tente de métadonnées de rotation toodetect hello dans le fichier MP4/MOV entrant hello et compensation. Suivants de hello **Sources** tooone élément des présélections de json hello défini [ici](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
