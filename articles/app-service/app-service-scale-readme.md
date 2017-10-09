---
title: "Azure App Service : Mise à l’échelle des applications d’App Service"
description: "Découvrez hello coulisses de mise à l’échelle d’Application dans le Service d’applications."
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
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="11b34-104">Azure App Service : Mise à l’échelle des applications d’App Service</span><span class="sxs-lookup"><span data-stu-id="11b34-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="11b34-105">Les applications hébergées dans Azure App Service peuvent [être mises à l’échelle massivement](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="11b34-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="11b34-106">Toutefois, la mise à l’échelle d’une application est un problème complexe pour lequel il n’existe pas de solution universelle.</span><span class="sxs-lookup"><span data-stu-id="11b34-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="11b34-107">toocorrectly l’échelle votre application il existe 3 domaines clés qui contribueront réussite des applications tooyour :</span><span class="sxs-lookup"><span data-stu-id="11b34-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="11b34-108">Comprendre l’architecture de votre application et ses faiblesses.</span><span class="sxs-lookup"><span data-stu-id="11b34-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="11b34-109">Votre application est-elle avec état ?</span><span class="sxs-lookup"><span data-stu-id="11b34-109">Is your Application Stateful?</span></span> <span data-ttu-id="11b34-110">Sans état ?</span><span class="sxs-lookup"><span data-stu-id="11b34-110">Stateless?</span></span>
   * <span data-ttu-id="11b34-111">Quels sont les composants hello de votre application ?</span><span class="sxs-lookup"><span data-stu-id="11b34-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="11b34-112">Où sont les goulots d’étranglement de hello dans l’application hello ?</span><span class="sxs-lookup"><span data-stu-id="11b34-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="11b34-113">Lorsque la charge est appliquée tooyour application, ce qui interrompt premier ?</span><span class="sxs-lookup"><span data-stu-id="11b34-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="11b34-114">Hello de présentation des attendu des exigences de performances et de charge.</span><span class="sxs-lookup"><span data-stu-id="11b34-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="11b34-115">Application hello doit-elle tooserve mille utilisateurs ? ou d’un million ?</span><span class="sxs-lookup"><span data-stu-id="11b34-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="11b34-116">Le trafic provient-il d’un seul emplacement géographique ou du monde entier ?</span><span class="sxs-lookup"><span data-stu-id="11b34-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="11b34-117">Existe-t-il des variations saisonnières ? Des pics de trafic ?</span><span class="sxs-lookup"><span data-stu-id="11b34-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="11b34-118">La vitesse à laquelle l’application hello doit répondre ?</span><span class="sxs-lookup"><span data-stu-id="11b34-118">How fast should hello app respond?</span></span> <span data-ttu-id="11b34-119">1 seconde ?</span><span class="sxs-lookup"><span data-stu-id="11b34-119">1 second?</span></span> <span data-ttu-id="11b34-120">1 milliseconde ?</span><span class="sxs-lookup"><span data-stu-id="11b34-120">1 millisecond?</span></span>
3. <span data-ttu-id="11b34-121">Présentation et correctement tirer parti de la plateforme de hello qui héberge votre application.</span><span class="sxs-lookup"><span data-stu-id="11b34-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="11b34-122">Les fonctionnalités doivent exploiter tooachieve mes objectifs de mise à l’échelle ?</span><span class="sxs-lookup"><span data-stu-id="11b34-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="11b34-123">Cette section vous aidera à comprendre tous les facteurs de hello et aide vous concevoir une stratégie qui tire parti de hello nécessaires du Service d’applications fonctionnalités tooachieve vos objectifs d’évolutivité.</span><span class="sxs-lookup"><span data-stu-id="11b34-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

