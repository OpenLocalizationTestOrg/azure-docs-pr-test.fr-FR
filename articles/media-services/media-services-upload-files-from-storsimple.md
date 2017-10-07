---
title: fichiers aaaUpload dans un compte Azure Media Services, Azure StorSimple | Documents Microsoft
description: "Cet article donne une brève vue d’ensemble d’Azure StorSimple Data Manager. article de Hello contient également des liens tootutorials qui vous montrent comment les données tooextract de StorSimple et le télécharger en tant que ressources tooan compte Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>Charger des fichiers dans un compte Azure Media Services à partir d’Azure StorSimple

Cet article donne une brève vue d’ensemble d’Azure StorSimple Data Manager. article de Hello contient également des liens tootutorials qui vous montrent comment les données tooextract de StorSimple et charger ces données en tant que ressources tooan compte d’Azure Media Services (AMS).

> 
> [!NOTE]
> Azure StorSimple Data Manager est actuellement disponible en version préliminaire privée. 
> 

## <a name="overview"></a>Vue d'ensemble

Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource. Hello actif peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.) Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) utilise le stockage cloud comme une extension de hello solution locale et reconnaît automatiquement les données sur un stockage local hello et de stockage cloud. l’appareil StorSimple Hello dedupes et compresse les données avant de les envoyer cloud toohello rend très efficace pour l’envoi de cloud de toohello des fichiers volumineux. Hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service fournit des API que vous tooextract les données à partir de StorSimple et de les présentent comme des ressources AMS.

## <a name="get-started"></a>Prise en main

1. [Créer un compte Media Services](media-services-portal-create-account.md) dans lequel vous souhaitez actifs de hello tootransfer.
2. S’inscrire pour l’aperçu du Gestionnaire de données, comme décrit dans hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) l’article.
3. Créez un compte StorSimple Data Manager.
4. Créez un travail de transformation de données qui extrait des données d’un appareil StorSimple et les transfère vers un compte AMS en tant que ressources. 

    Lors de la tâche de hello commence à s’exécuter, une file d’attente de stockage est créé. Cette file d’attente est renseignée avec des messages sur les objets blob transformés, au fur et à mesure de leur mise à disposition. nom de Hello de cette file d’attente est hello identique au nom de la définition de la tâche hello hello. Vous pouvez utiliser cette toodetermine de file d’attente lorsque comme élément multimédia est prêt et appeler votre toorun d’opération Media Services souhaitée sur celle-ci. Par exemple, vous pouvez utiliser cette tootrigger de file d’attente une fonction d’Azure qui contient du code de Media Services nécessaire hello qu’elle contient.

## <a name="see-also"></a>Voir aussi

[Utilisez hello .net SDK travaux tootrigger Bonjour Data Manager](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez désormais encoder vos éléments multimédias téléchargés. Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).
