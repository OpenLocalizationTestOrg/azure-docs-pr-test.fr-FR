---
title: "vitesse de gérer aaa et l’accès simultané de votre encodage avec Azure Media Services | Documents Microsoft"
description: "Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage avec Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="b3383-103">Gérer la vitesse et la simultanéité de votre encodage</span><span class="sxs-lookup"><span data-stu-id="b3383-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="b3383-104">Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="b3383-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="b3383-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b3383-105">Overview</span></span>

<span data-ttu-id="b3383-106">Dans Media Services, un **Type d’unité réservée** détermine la vitesse de hello avec lequel votre média, les tâches de traitement est traités.</span><span class="sxs-lookup"><span data-stu-id="b3383-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="b3383-107">Vous pouvez choisir parmi les éléments suivants de hello réservé de types d’unités : **S1**, **S2**, ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="b3383-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="b3383-108">Par exemple, les hello même travail d’encodage s’exécute plus rapidement lorsque vous utilisez hello **S2** type d’unité réservée comparer toohello **S1** type.</span><span class="sxs-lookup"><span data-stu-id="b3383-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="b3383-109">Hello [mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md) rubrique illustre une table qui vous permet de prendre de décision lors du choix entre différentes vitesses de codage.</span><span class="sxs-lookup"><span data-stu-id="b3383-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="b3383-110">En outre toospecifying hello réservé type d’unité, vous pouvez spécifier tooprovision votre compte avec **unités réservées**.</span><span class="sxs-lookup"><span data-stu-id="b3383-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="b3383-111">nombre Hello d’unités réservées configurées détermine le nombre hello de tâches multimédia qui peuvent être traitées simultanément dans un compte donné.</span><span class="sxs-lookup"><span data-stu-id="b3383-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="b3383-112">Par exemple, si votre compte dispose de cinq unités réservées, puis les tâches de cinq support exécuter simultanément à condition qu’il sont toobe tâches traitée.</span><span class="sxs-lookup"><span data-stu-id="b3383-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="b3383-113">les tâches restantes Hello attendent dans la file d’attente hello et sont collectées de manière séquentielle pour traitement lorsqu’une tâche en cours d’exécution se termine.</span><span class="sxs-lookup"><span data-stu-id="b3383-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="b3383-114">Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="b3383-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="b3383-115">Dans ce cas, hello délai entre une fin de tâche et hello ensuite démarrage dépendront de disponibilité hello des ressources dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="b3383-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="b3383-116">Pour plus d’informations et des exemples qui montrent comment les unités d’encodage tooscale, consultez [cela](media-services-scale-media-processing-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="b3383-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="b3383-117">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b3383-117">Next step</span></span>

[<span data-ttu-id="b3383-118">Mise à l’échelle des unités d’encodage</span><span class="sxs-lookup"><span data-stu-id="b3383-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="b3383-119">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="b3383-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b3383-120">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b3383-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

