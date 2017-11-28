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
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="0b3c5-103">Mettre à l’échelle des points de terminaison de diffusion en continu avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0b3c5-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="0b3c5-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0b3c5-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="0b3c5-105">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="0b3c5-106">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b3c5-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="0b3c5-107">Les points de terminaison de streaming **Premium** sont conçus pour les charges de travail avancées et fournissent une capacité de bande passante dédiée et évolutive.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="0b3c5-108">Les clients disposant d’un point de terminaison de streaming **Premium** ont par défaut une unité de streaming.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="0b3c5-109">point de terminaison de diffusion en continu de Hello peut être monté en ajoutant SUs.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="0b3c5-110">Chaque appel à SU fournit l’application de toohello de capacité de la bande passante supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="0b3c5-111">Pour plus d’informations sur la configuration CDN et les types de point de terminaison de diffusion en continu, consultez hello [vue d’ensemble du point de terminaison de diffusion en continu](media-services-portal-manage-streaming-endpoints.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="0b3c5-112">Cette rubrique montre comment tooscale un point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="0b3c5-113">Pour des informations détaillées sur la tarification, consultez la page [Détails de la tarification des services de média](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="0b3c5-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="0b3c5-114">Mettre à l’échelle les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="0b3c5-114">Scale streaming endpoints</span></span>

<span data-ttu-id="0b3c5-115">nombre de hello toochange d’unités de diffusion en continu, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="0b3c5-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="0b3c5-116">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="0b3c5-117">Bonjour **paramètres** fenêtre, sélectionnez **points de terminaison de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="0b3c5-118">Cliquez sur le point de terminaison de diffusion en continu hello que tooscale.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="0b3c5-119">Vous pouvez uniquement mettre à l’échelle les points de terminaison de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="0b3c5-120">Déplacer hello curseur toospecify hello nombre d’unités de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="0b3c5-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b3c5-122">Next steps</span></span>
<span data-ttu-id="0b3c5-123">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="0b3c5-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b3c5-124">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="0b3c5-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

