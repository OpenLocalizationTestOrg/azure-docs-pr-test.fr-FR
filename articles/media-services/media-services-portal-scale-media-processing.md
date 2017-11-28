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
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="b070d-103">Type d’unité de modification hello réservé</span><span class="sxs-lookup"><span data-stu-id="b070d-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b070d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b070d-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="b070d-105">Portail</span><span class="sxs-lookup"><span data-stu-id="b070d-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="b070d-106">REST</span><span class="sxs-lookup"><span data-stu-id="b070d-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="b070d-107">Java</span><span class="sxs-lookup"><span data-stu-id="b070d-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="b070d-108">PHP</span><span class="sxs-lookup"><span data-stu-id="b070d-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="b070d-109">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b070d-109">Overview</span></span>

<span data-ttu-id="b070d-110">Un compte Media Services est associé à un Type d’unité réservée, qui détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités.</span><span class="sxs-lookup"><span data-stu-id="b070d-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="b070d-111">Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="b070d-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="b070d-112">Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type.</span><span class="sxs-lookup"><span data-stu-id="b070d-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="b070d-113">En outre toospecifying hello réservé type d’unité, vous pouvez spécifier tooprovision votre compte avec **unités réservées** (RUs).</span><span class="sxs-lookup"><span data-stu-id="b070d-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="b070d-114">nombre de Hello de configuré RUs détermine nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné.</span><span class="sxs-lookup"><span data-stu-id="b070d-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="b070d-115">Les unités réservées fonctionnent pour la mise en parallèle de tout le traitement multimédia, notamment les travaux d’indexation qui utilisent Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="b070d-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="b070d-116">Toutefois, contrairement à l’encodage, l’indexation des travaux n’est pas plus rapide avec des unités réservées plus rapides.</span><span class="sxs-lookup"><span data-stu-id="b070d-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b070d-117">Assurez-vous que tooreview hello [vue d’ensemble](media-services-scale-media-processing-overview.md) rubrique tooget plus d’informations sur la mise à l’échelle de media du traitement de rubrique.</span><span class="sxs-lookup"><span data-stu-id="b070d-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="b070d-118">Mise à l’échelle du traitement multimédia</span><span class="sxs-lookup"><span data-stu-id="b070d-118">Scale media processing</span></span>
<span data-ttu-id="b070d-119">toochange hello réservé unité type hello et le nombre d’unités réservées, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b070d-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="b070d-120">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b070d-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b070d-121">Bonjour **paramètres** fenêtre, sélectionnez **unités réservées multimédia**.</span><span class="sxs-lookup"><span data-stu-id="b070d-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="b070d-122">nombre de hello de toochange d’unités réservées pour hello sélectionné le type d’unité réservée, utilisez hello **unités de média pris en charge** curseur.</span><span class="sxs-lookup"><span data-stu-id="b070d-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="b070d-123">toochange hello **TYPE d’unité réservée**, appuyez sur S1, S2 ou S3.</span><span class="sxs-lookup"><span data-stu-id="b070d-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Page Processors](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="b070d-125">Hello de presse enregistrer bouton toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b070d-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="b070d-126">unités réservées de Hello nouvelle sont allouées lorsque vous appuyez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="b070d-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b070d-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b070d-127">Next steps</span></span>
<span data-ttu-id="b070d-128">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="b070d-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b070d-129">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b070d-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

