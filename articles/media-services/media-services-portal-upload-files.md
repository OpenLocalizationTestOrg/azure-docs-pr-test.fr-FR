---
title: "AAA » télécharger des fichiers dans un compte de service de média à l’aide de hello portail Azure | Documents Microsoft »"
description: "Ce didacticiel vous guide à travers les étapes de hello de téléchargement de fichiers dans un compte de service de média à l’aide de hello portail Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>Télécharger des fichiers dans un compte de service de média à l’aide de hello portail Azure
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 


Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource. Hello actif peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.) Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.


## <a name="upload-files"></a>Charger des fichiers

>[!NOTE]
>Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services. Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.
>

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Sur hello **paramètres** panneau, cliquez sur **actifs**.
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. Cliquez sur hello **télécharger** bouton.
   
    Hello **télécharger un élément multimédia vidéo** fenêtre s’affiche.
   
   > [!NOTE]
   > Il n’existe aucune limite de taille de fichier.
   > 
   > 
4. Parcourir vidéo toohello souhaité sur votre ordinateur, sélectionnez-le, puis appuyez sur OK.  
   
    téléchargement de Hello démarre et vous pouvez voir la progression hello sous le nom de fichier hello.  

Une fois le téléchargement de hello terminé, vous verrez hello un nouveau composant répertorié dans hello **actifs** fenêtre. 

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez désormais encoder vos éléments multimédias téléchargés. Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).

Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré. Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

