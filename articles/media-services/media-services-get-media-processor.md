---
title: "tooCreate aaaHow un processeur multimédia à l’aide hello Azure Media Services SDK pour .NET | Documents Microsoft"
description: "Découvrez comment toocreate un tooencode de composant de processeur multimédia, convertir le format de chiffrer ou déchiffrer le contenu multimédia pour Azure Media Services. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a>Obtention d’une instance de processeur multimédia
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia. Vous généralement créez un processeur multimédia lorsque vous créez une tâche tooencode, chiffrez ou convertissez le format hello du contenu multimédia.

## <a name="azure-media-processors"></a>Processeurs multimédias Azure 

Hello rubrique suivante fournit des listes de processeurs multimédias :

* [Processeurs multimédias d’encodage](scenarios-and-availability.md#encoding-media-processors)
* [Processeurs multimédias Analytics](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a>Obtention d'un processeur multimédia

Hello suivant de méthode montre comment tooget une instance de processeur multimédia. exemple de code Hello suppose l’utilisation de hello d’une variable au niveau du module nommée **contexte _de_données** tooreference contexte hello du serveur comme décrit dans la section de hello [Comment : se connecter tooMedia Services par programmation](media-services-use-aad-auth-to-access-ams-api.md).

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous savez comment tooget une instance de processeur multimédia, accédez toohello [comment tooEncode un élément multimédia](media-services-dotnet-encode-with-media-encoder-standard.md) rubrique qui vous indique comment toouse hello tooencode Media Encoder Standard, un élément multimédia.

