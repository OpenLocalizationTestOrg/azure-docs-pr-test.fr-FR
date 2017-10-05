---
title: "Azure App Service : Mise à l’échelle des applications d’App Service"
description: "Découvrez les tenants et les aboutissants de la mise à l’échelle d’application dans App Service."
keywords: "app service, azure app service, mise à l'échelle, évolutif, plan app service, coût d'app service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="e3aa7-104">Azure App Service : Mise à l’échelle des applications d’App Service</span><span class="sxs-lookup"><span data-stu-id="e3aa7-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="e3aa7-105">Les applications hébergées dans Azure App Service peuvent [être mises à l’échelle massivement](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="e3aa7-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="e3aa7-106">Toutefois, la mise à l’échelle d’une application est un problème complexe pour lequel il n’existe pas de solution universelle.</span><span class="sxs-lookup"><span data-stu-id="e3aa7-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="e3aa7-107">Pour mettre à l’échelle correctement votre application, il convient de prendre en compte 3 domaines clés :</span><span class="sxs-lookup"><span data-stu-id="e3aa7-107">To correctly scale your application there are 3 key areas that will contribute to your applications success:</span></span>

1. <span data-ttu-id="e3aa7-108">Comprendre l’architecture de votre application et ses faiblesses.</span><span class="sxs-lookup"><span data-stu-id="e3aa7-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="e3aa7-109">Votre application est-elle avec état ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-109">Is your Application Stateful?</span></span> <span data-ttu-id="e3aa7-110">Sans état ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-110">Stateless?</span></span>
   * <span data-ttu-id="e3aa7-111">Quels sont les composants de votre application ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-111">What are all the components of your application?</span></span>
     * <span data-ttu-id="e3aa7-112">Où se trouvent les goulots d’étranglement dans l’application ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-112">Where are the bottlenecks in the application?</span></span>
   * <span data-ttu-id="e3aa7-113">Lors de l’application de la charge à votre application, qu’est-ce qui s’arrête en premier ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-113">When load is applied to your app, what will break first?</span></span>
2. <span data-ttu-id="e3aa7-114">Comprendre les exigences de performances et de charge attendues.</span><span class="sxs-lookup"><span data-stu-id="e3aa7-114">Understanding the expected load and performance requirements.</span></span>
   * <span data-ttu-id="e3aa7-115">L’application doit-elle répondre à 1 000 ou à un million d’utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-115">Does the application need to serve one thousand users? or one million?</span></span>
   * <span data-ttu-id="e3aa7-116">Le trafic provient-il d’un seul emplacement géographique ou du monde entier ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="e3aa7-117">Existe-t-il des variations saisonnières ? Des pics de trafic ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="e3aa7-118">À quelle vitesse, l’application doit-elle répondre ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-118">How fast should the app respond?</span></span> <span data-ttu-id="e3aa7-119">1 seconde ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-119">1 second?</span></span> <span data-ttu-id="e3aa7-120">1 milliseconde ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-120">1 millisecond?</span></span>
3. <span data-ttu-id="e3aa7-121">Comprendre et exploiter correctement la plateforme d’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="e3aa7-121">Understanding and correctly leverage the platform hosting your app.</span></span>
   * <span data-ttu-id="e3aa7-122">Quelles fonctionnalités dois-je utiliser pour atteindre mes objectifs de mise à l’échelle ?</span><span class="sxs-lookup"><span data-stu-id="e3aa7-122">What features should I leverage to achieve my scale goals?</span></span>

<span data-ttu-id="e3aa7-123">Cette section vous aidera à comprendre tous les facteurs et à concevoir une stratégie tirant parti des fonctionnalités d’App Service nécessaires pour atteindre vos objectifs d’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="e3aa7-123">This section will help you understand all the factors and help you devise a strategy that takes advantage of the necessary App Service features to achieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

