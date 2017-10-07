---
title: "aaaTroubleshooting avec le suivi d’événements | Documents Microsoft"
description: "problèmes courants de Hello rencontrés lors du déploiement des services sur Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="2907e-103">Résoudre les problèmes courants rencontrés pendant le déploiement de services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2907e-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="2907e-104">Lorsque vous exécutez des services sur votre ordinateur de développement, il est facile toouse [outils de débogage de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="2907e-104">When you're running services on your developer computer, it is easy toouse [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="2907e-105">Pour les clusters à distance, [rapports d’intégrité](service-fabric-view-entities-aggregated-health.md) sont toujours un toostart parfait.</span><span class="sxs-lookup"><span data-stu-id="2907e-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place toostart.</span></span> <span data-ttu-id="2907e-106">Hello plus simple tooaccess façons ces rapports sont via PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2907e-106">hello easiest ways tooaccess these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="2907e-107">Cet article suppose que vous déboguez un cluster distant et que vous avez une connaissance de base toouse une de ces outils.</span><span class="sxs-lookup"><span data-stu-id="2907e-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how toouse either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="2907e-108">Blocage d'application</span><span class="sxs-lookup"><span data-stu-id="2907e-108">Application crash</span></span>
<span data-ttu-id="2907e-109">Hello » Partition est inférieure à cibler le nombre de réplica ou l’instance « rapport est une bonne indication que votre service est en panne.</span><span class="sxs-lookup"><span data-stu-id="2907e-109">hello "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="2907e-110">toofind out où votre service est en panne prend un examen peu plus approfondi.</span><span class="sxs-lookup"><span data-stu-id="2907e-110">toofind out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="2907e-111">Lors d’une exécution de votre service à grande l'échelle, votre meilleur ami est un ensemble de traces bien planifiées.</span><span class="sxs-lookup"><span data-stu-id="2907e-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="2907e-112">Nous vous suggérons d’essayer de [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) pour collecter les traces et à l’aide d’une solution comme [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) pour l’affichage et recherche les traces hello.</span><span class="sxs-lookup"><span data-stu-id="2907e-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching hello traces.</span></span>

![Intégrité de la partition SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="2907e-114">Au cours de l’initialisation du service ou de l’acteur</span><span class="sxs-lookup"><span data-stu-id="2907e-114">During service or actor initialization</span></span>
<span data-ttu-id="2907e-115">Toutes les exceptions avant l’initialisation du type de service hello entraîne hello processus toocrash.</span><span class="sxs-lookup"><span data-stu-id="2907e-115">Any exceptions before hello service type is initialized will cause hello process toocrash.</span></span> <span data-ttu-id="2907e-116">Pour ces types de pannes, journal des événements application hello affiche erreur hello à partir de votre service.</span><span class="sxs-lookup"><span data-stu-id="2907e-116">For these types of crashes, hello application event log will show hello error from your service.</span></span>
<span data-ttu-id="2907e-117">Il s’agit de hello courants exceptions toosee avant l’initialisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="2907e-117">These are hello most common exceptions toosee before hello service is initialized.</span></span>

<span data-ttu-id="2907e-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="2907e-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="2907e-119">Cette erreur est souvent en raison des dépendances d’assembly toomissing.</span><span class="sxs-lookup"><span data-stu-id="2907e-119">This error is often due toomissing assembly dependencies.</span></span> <span data-ttu-id="2907e-120">Vérifiez la propriété CopyLocal hello dans Visual Studio ou hello global assembly cache pour le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="2907e-120">Check hello CopyLocal property in Visual Studio or hello global assembly cache for hello node.</span></span>

<span data-ttu-id="2907e-121">***System.Runtime.InteropServices.COMException*** *à System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="2907e-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="2907e-122">Cela indique que ce nom de type hello service inscrit ne correspond pas au manifeste de service hello.</span><span class="sxs-lookup"><span data-stu-id="2907e-122">This indicates that hello registered service type name does not match hello service manifest.</span></span>

<span data-ttu-id="2907e-123">[Diagnostics Azure](service-fabric-diagnostics-how-to-setup-wad.md) peut être un journal des événements application hello tooupload configuré pour tous les nœuds de votre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2907e-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured tooupload hello application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="2907e-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="2907e-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="2907e-125">Si l’incident de hello se produit lors de l’initialisation de hello ou en cours d’exécution de votre type de service inscrit ou un acteur, hello exception sera interceptée par Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2907e-125">If hello crash happens during hello initialization or running of your registered service type or actor, hello exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="2907e-126">Vous pouvez afficher à partir des fournisseurs de EventSource hello détaillées dans la section « Étapes suivantes » de hello.</span><span class="sxs-lookup"><span data-stu-id="2907e-126">You can view these from hello EventSource providers detailed in hello "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2907e-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2907e-127">Next steps</span></span>
<span data-ttu-id="2907e-128">En savoir plus sur les diagnostics existants fournis par Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="2907e-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="2907e-129">Diagnostics Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2907e-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="2907e-130">Diagnostics Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2907e-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

