---
title: "vue d’ensemble du traitement multimédia aaaScaling | Documents Microsoft"
description: "Cette rubrique est une présentation de la mise à l’échelle du traitement multimédia avec Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 780ef5c2-3bd6-4261-8540-6dee77041387
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: d17531f79d4c1e0d0fa544c4fb5c083684e706fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-media-processing-overview"></a>Vue d’ensemble de la mise à l’échelle du traitement multimédia
Cette page fournit une vue d’ensemble de comment et pourquoi le traitement tooscale media. 

## <a name="overview"></a>Vue d'ensemble
Un compte Media Services est associé à un Type d’unité réservée, qui détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités. Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**. Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type. Pour plus d’informations, consultez hello [Types d’unités réservées](https://azure.microsoft.com/blog/high-speed-encoding-with-azure-media-services/).

En outre toospecifying hello réservé type d’unité, vous pouvez spécifier des votre compte de tooprovision avec des unités réservées. nombre Hello d’unités réservées configurées détermine le nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné. Par exemple, si votre compte dispose de cinq unités réservées, puis les tâches de cinq support exécuter simultanément à condition qu’il sont toobe tâches traitée. les tâches restantes Hello attendent dans la file d’attente hello et sont collectées de manière séquentielle pour traitement lorsqu’une tâche en cours d’exécution se termine. Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement. Dans ce cas, hello délai entre une fin de tâche et hello ensuite démarrage dépendront de disponibilité hello des ressources dans le système de hello.

## <a name="choosing-between-different-reserved-unit-types"></a>Choix entre les différents types d’unités réservées
Hello tableau suivant vous permet de prendre de décision lors du choix entre différentes vitesses de codage. Également, elle fournit quelques cas de test d’évaluation et fournit des URL de SAP que vous pouvez utiliser les vidéos toodownload sur lequel vous pouvez effectuer vos propres tests :

| Scénarios | **S1** | **S2** | **S3** |
| --- | --- | --- | --- |
| Cas d’utilisation prévue |Encodage à débit binaire unique. <br/>Fichiers avec une résolution SD ou inférieure, insensibles à l’heure, à moindre coût. |Encodage à débit binaire unique et à débit binaire multiple.<br/>Utilisation normale de l’encodage SD et HD. |Encodage à débit binaire unique et à débit binaire multiple.<br/>Vidéos avec une résolution HD complète et 4K. Encodage sensible à l’heure, plus rapide. |
| Référence |[Fichier d’entrée : durée de 5 minutes 640x360p à 29,97 images/seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_360p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D).<br/><br/>Encodage de fichier MP4 à débit unique tooa à hello même résolution, prend environ 11 minutes. |[Fichier d’entrée : durée de 5 minutes 1280x720p à 29,97 images/seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_720p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D)<br/><br/>L’encodage avec la présélection « H264 – Vitesse de transmission simple – 720p » prend environ 5 minutes.<br/><br/>L’encodage avec la présélection « H264 – Vitesse de transmission multiple – 720p » prend environ 11,5 minutes. |[Fichier d’entrée : durée de 5 minutes 1920x1080p à 29,97 images/seconde](https://wamspartners.blob.core.windows.net/for-long-term-share/Whistler_5min_1080p30.mp4?sr=c&si=AzureDotComReadOnly&sig=OY0TZ%2BP2jLK7vmcQsCTAWl33GIVCu67I02pgarkCTNw%3D). <br/><br/>L’encodage avec la présélection « H264 à débit binaire simple 1080p » prend environ 2,7 minutes.<br/><br/>L’encodage avec la présélection « H264 à débit binaire multiple 1080p » prend environ 5,7 minutes. |

## <a name="considerations"></a>Considérations
> [!IMPORTANT]
> Passez en revue les considérations décrites dans cette section.  
> 
> 

* Les unités réservées fonctionnent pour la mise en parallèle de tout le traitement multimédia, notamment les travaux à l'aide de l'Indexeur multimédia Azure.  Toutefois, contrairement à l’encodage, l’indexation des travaux n’est pas plus rapide avec des unités réservées plus rapides.
* Si vous utilisez hello partagé pool, autrement dit, sans les unités réservées, puis vos tâches d’encodage ont hello les mêmes performances comme avec S1 RUs. Toutefois, limite supérieure toohello ne subit aucun vos tâches peuvent passer dans l’état en file d’attente, et à un moment donné, au plus qu’une seule tâche exécutera.
* Hello suivant des centres de données n’offre pas hello **S2** type d’unité réservé : Brésil Sud et ouest de l’Inde.
* Hello centre de données suivant n’offre pas hello **S3** type d’unité réservé : Inde-ouest.

## <a name="billing"></a>Facturation

Vous êtes facturé en fonction des minutes réelles d’utilisation des unités réservées Multimédia. Pour plus d’informations, voir section hello FAQ hello [tarification de Media Services](https://azure.microsoft.com/pricing/details/media-services/) page.   

## <a name="quotas-and-limitations"></a>Quotas et limitations
Pour plus d’informations sur les quotas et limitations et tooopen un ticket de support, voir [Quotas et limitations](media-services-quotas-and-limitations.md).

## <a name="next-step"></a>Étape suivante
Atteindre hello media tâche avec l’une de ces technologies de traitement de mise à l’échelle : 

> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portail](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

