---
title: aaaScale de diffusion en continu des points de terminaison avec hello portail Azure | Documents Microsoft
description: "Ce didacticiel vous guide tout au long des étapes hello de mise à l’échelle des points de terminaison de diffusion en continu avec hello portail Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a>Mettre à l’échelle des points de terminaison de diffusion en continu avec hello portail Azure
## <a name="overview"></a>Vue d'ensemble

> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Les points de terminaison de streaming **Premium** sont conçus pour les charges de travail avancées et fournissent une capacité de bande passante dédiée et évolutive. Les clients disposant d’un point de terminaison de streaming **Premium** ont par défaut une unité de streaming. point de terminaison de diffusion en continu de Hello peut être monté en ajoutant SUs. Chaque appel à SU fournit l’application de toohello de capacité de la bande passante supplémentaire. Pour plus d’informations sur la configuration CDN et les types de point de terminaison de diffusion en continu, consultez hello [vue d’ensemble du point de terminaison de diffusion en continu](media-services-portal-manage-streaming-endpoints.md) rubrique.
 
Cette rubrique montre comment tooscale un point de terminaison de diffusion en continu.

Pour des informations détaillées sur la tarification, consultez la page [Détails de la tarification des services de média](http://go.microsoft.com/fwlink/?LinkId=275107).

## <a name="scale-streaming-endpoints"></a>Mettre à l’échelle les points de terminaison de streaming

nombre de hello toochange d’unités de diffusion en continu, hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.
2. Bonjour **paramètres** fenêtre, sélectionnez **points de terminaison de diffusion en continu**.
3. Cliquez sur le point de terminaison de diffusion en continu hello que tooscale. 

    [!NOTE] Vous pouvez uniquement mettre à l’échelle les points de terminaison de streaming **Premium**.

4. Déplacer hello curseur toospecify hello nombre d’unités de diffusion en continu.

    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a>Étapes suivantes
Consultez les parcours d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

