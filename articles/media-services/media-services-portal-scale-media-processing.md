---
title: "support aaaScale à l’aide de traitement hello portail Azure | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello de support de mise à l’échelle le traitement à l’aide de hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Type d’unité de modification hello réservé
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portail](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Vue d'ensemble

Un compte Media Services est associé à un Type d’unité réservée, qui détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités. Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**. Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type.

En outre toospecifying hello réservé type d’unité, vous pouvez spécifier tooprovision votre compte avec **unités réservées** (RUs). nombre de Hello de configuré RUs détermine nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné.

>[!NOTE]
>Les unités réservées fonctionnent pour la mise en parallèle de tout le traitement multimédia, notamment les travaux d’indexation qui utilisent Azure Media Indexer. Toutefois, contrairement à l’encodage, l’indexation des travaux n’est pas plus rapide avec des unités réservées plus rapides.

> [!IMPORTANT]
> Assurez-vous que tooreview hello [vue d’ensemble](media-services-scale-media-processing-overview.md) rubrique tooget plus d’informations sur la mise à l’échelle de media du traitement de rubrique.
> 
> 

## <a name="scale-media-processing"></a>Mise à l’échelle du traitement multimédia
toochange hello réservé unité type hello et le nombre d’unités réservées, hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** fenêtre, sélectionnez **unités réservées multimédia**.
   
    nombre de hello de toochange d’unités réservées pour hello sélectionné le type d’unité réservée, utilisez hello **unités de média pris en charge** curseur.
   
    toochange hello **TYPE d’unité réservée**, appuyez sur S1, S2 ou S3.
   
    ![Page Processors](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Hello de presse enregistrer bouton toosave vos modifications.
   
    unités réservées de Hello nouvelle sont allouées lorsque vous appuyez sur Enregistrer.

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

