---
title: "Gérer la rapidité et la simultanéité de votre encodage avec Azure Media Services | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="b1b04-103">Gérer la vitesse et la simultanéité de votre encodage</span><span class="sxs-lookup"><span data-stu-id="b1b04-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="b1b04-104">Cet article donne un bref aperçu de la manière dont vous pouvez gérer la rapidité et la simultanéité de vos travaux/tâches d’encodage.</span><span class="sxs-lookup"><span data-stu-id="b1b04-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="b1b04-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="b1b04-105">Overview</span></span>

<span data-ttu-id="b1b04-106">Dans Media Services, un **Type d’unité réservée** détermine la vitesse à laquelle vos tâches de traitement multimédia sont traitées.</span><span class="sxs-lookup"><span data-stu-id="b1b04-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="b1b04-107">Vous pouvez choisir entre les types d’unités réservées suivantes : **S1**, **S2** ou **S3**.</span><span class="sxs-lookup"><span data-stu-id="b1b04-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="b1b04-108">Par exemple, un même travail d’encodage s’exécute plus rapidement quand vous utilisez le type d’unité réservée **S2** que le type **S1**.</span><span class="sxs-lookup"><span data-stu-id="b1b04-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="b1b04-109">La rubrique relative à la [mise à l’échelle des unités d’encodage](media-services-scale-media-processing-overview.md) contient un tableau qui vous aide à prendre une décision lors du choix entre les différentes vitesses d’encodage.</span><span class="sxs-lookup"><span data-stu-id="b1b04-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="b1b04-110">En plus de spécifier le type d’unité réservée, vous pouvez approvisionner votre compte avec des **unités réservées**.</span><span class="sxs-lookup"><span data-stu-id="b1b04-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="b1b04-111">Le nombre d’unités réservées approvisionnées détermine le nombre de tâches de média qui peuvent être traitées simultanément dans un compte donné.</span><span class="sxs-lookup"><span data-stu-id="b1b04-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="b1b04-112">Si, par exemple, votre compte a cinq unités réservées, les cinq tâches multimédias sont exécutées simultanément tant qu’il y a des tâches à traiter.</span><span class="sxs-lookup"><span data-stu-id="b1b04-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="b1b04-113">Les autres tâches restent dans la file d'attente et sont sélectionnées séquentiellement pour le traitement quand l'exécution d'une tâche se termine.</span><span class="sxs-lookup"><span data-stu-id="b1b04-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="b1b04-114">Si aucune unité réservée n'est approvisionnée pour un compte donné, les tâches sont sélectionnées séquentiellement.</span><span class="sxs-lookup"><span data-stu-id="b1b04-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="b1b04-115">Dans ce cas, le temps d'attente entre l'achèvement d'une tâche et le démarrage de la suivante dépend de la disponibilité des ressources dans le système.</span><span class="sxs-lookup"><span data-stu-id="b1b04-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="b1b04-116">Pour obtenir des informations détaillées et des exemples sur la manière de mettre à l’échelle les unités d’encodage, consultez [cette rubrique](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b1b04-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="b1b04-117">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b1b04-117">Next step</span></span>

[<span data-ttu-id="b1b04-118">Mise à l’échelle des unités d’encodage</span><span class="sxs-lookup"><span data-stu-id="b1b04-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="b1b04-119">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="b1b04-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b1b04-120">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="b1b04-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

