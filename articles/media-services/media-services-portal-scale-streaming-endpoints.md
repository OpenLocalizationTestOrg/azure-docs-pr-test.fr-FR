---
title: "Mettre à l’échelle des points de terminaison de streaming avec le Portail Azure | Microsoft Docs"
description: "Ce didacticiel vous guide à travers les étapes de mise à l’échelle des points de terminaison de streaming avec le Portail Azure."
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
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="fb70d-103">Mettre à l’échelle des points de terminaison de streaming avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="fb70d-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="fb70d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fb70d-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="fb70d-105">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fb70d-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="fb70d-106">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb70d-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="fb70d-107">Les points de terminaison de streaming **Premium** sont conçus pour les charges de travail avancées et fournissent une capacité de bande passante dédiée et évolutive.</span><span class="sxs-lookup"><span data-stu-id="fb70d-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="fb70d-108">Les clients disposant d’un point de terminaison de streaming **Premium** ont par défaut une unité de streaming.</span><span class="sxs-lookup"><span data-stu-id="fb70d-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="fb70d-109">Le point de terminaison de streaming peut être adapté avec l’ajout d’unités de streaming.</span><span class="sxs-lookup"><span data-stu-id="fb70d-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="fb70d-110">Chaque unité de streaming fournit une capacité de bande passante supplémentaire à l’application.</span><span class="sxs-lookup"><span data-stu-id="fb70d-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="fb70d-111">Pour plus d’informations sur les types de point de terminaison de streaming et la configuration du CDN, consultez la rubrique [Vue d’ensemble des points de terminaison de streaming](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="fb70d-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="fb70d-112">Cette rubrique montre comment mettre à l’échelle un point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="fb70d-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="fb70d-113">Pour des informations détaillées sur la tarification, consultez la page [Détails de la tarification des services de média](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="fb70d-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="fb70d-114">Mettre à l’échelle les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="fb70d-114">Scale streaming endpoints</span></span>

<span data-ttu-id="fb70d-115">Pour modifier le nombre d’unités de streaming, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fb70d-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="fb70d-116">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="fb70d-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="fb70d-117">Dans la fenêtre **Paramètres**, sélectionnez **Points de terminaison de diffusion en continu**.</span><span class="sxs-lookup"><span data-stu-id="fb70d-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="fb70d-118">Cliquez sur le point de terminaison de streaming que vous souhaitez mettre à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="fb70d-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="fb70d-119">Vous pouvez uniquement mettre à l’échelle les points de terminaison de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="fb70d-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="fb70d-120">Déplacez le curseur pour spécifier le nombre d’unités de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="fb70d-120">Move the slider to specify the number of streaming units.</span></span>

    ![point de terminaison de diffusion en continu](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="fb70d-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb70d-122">Next steps</span></span>
<span data-ttu-id="fb70d-123">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="fb70d-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fb70d-124">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="fb70d-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

