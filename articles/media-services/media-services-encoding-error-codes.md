---
title: "codes d’erreur de codage de média aaaAzure | Documents Microsoft"
description: "Cette rubrique répertorie les codes d’erreur qui peut être renvoyés au cas où une erreur est survenue pendant hello encodage d’exécution de la tâche..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>Codes d’erreur d’encodage

Hello tableau suivant répertorie les codes d’erreur qui peut être renvoyés au cas où une erreur est survenue pendant hello exécution de la tâche de codage.  Détails de l’erreur tooget dans votre code .NET, utilisez hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe. Détails de l’erreur tooget dans votre code reste, utilisez hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API REST.

| ErrorDetail.Code | Causes possibles de l’erreur |
| --- | --- |
| Unknown |Erreur inconnue lors de l’exécution de tâche hello |
| ErrorDownloadingInputAssetMalformedContent |Catégorie d’erreurs se produisant lors du téléchargement d’éléments multimédias d’entrée : noms de fichier incorrects, fichiers de longueur nulle, formats incorrects, etc. |
| ErrorDownloadingInputAssetServiceFailure |Catégorie d’erreurs qui traite des problèmes sur le côté du service hello - pour les exemples d’erreurs réseau ou de stockage lors du téléchargement. |
| ErrorParsingConfiguration |Catégorie d’erreurs de tâches où <see cref="MediaTask.PrivateData"/> (configuration) n’est pas valide, par exemple la configuration de hello n’est pas un système valide prédéfini ou il contient du code XML non valide. |
| ErrorExecutingTaskMalformedContent |Catégorie d’erreurs lors de l’exécution de hello de tâche hello où problèmes à l’intérieur de hello d’entrée des fichiers multimédias de provoquer un échec. |
| ErrorExecutingTaskUnsupportedFormat |Catégorie d’erreurs où processeur multimédia de hello ne peut pas traiter les fichiers hello fournis - format de média non pris en charge ou ne correspond pas à la Configuration de hello. Par exemple, la tentative de tooproduce une sortie audio uniquement à partir d’une ressource qui a uniquement les vidéos |
| ErrorProcessingTask |Catégorie d’autres erreurs hello processeur multimédia rencontre lors du traitement de hello de tâche hello qui sont toocontent non liée. |
| ErrorUploadingOutputAsset |Catégorie d’erreurs lors du chargement de la ressource en sortie hello |
| ErrorCancelingTask |Catégorie d’erreurs toocover échecs lors de la tentative de toocancel hello tâche |
| TransientError |Catégorie d’erreurs toocover problèmes temporaires (par exemple). problèmes réseau temporaires avec Azure Storage) |

aide tooget hello **Media Services** équipe, ouvrez un [ticket de support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Articles connexes
* [Exécution de tâches d’encodage avancées via la personnalisation des présélections Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Quotas et limitations](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
