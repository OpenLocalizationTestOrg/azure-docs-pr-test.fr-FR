---
title: "Résolution des problèmes avec le suivi d’événements | Microsoft Docs"
description: "Problèmes les plus courants rencontrés lors du déploiement de services sur Microsoft Azure Service Fabric."
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
ms.openlocfilehash: e60bd4b9291cb2fc748921e42f11f54bb545984f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="cda0e-103">Résoudre les problèmes courants rencontrés pendant le déploiement de services dans Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cda0e-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="cda0e-104">Lors de l'exécution de services sur votre ordinateur de développement, il est facile d’utiliser les [outils de dépannage de Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="cda0e-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="cda0e-105">Pour les clusters à distance, [les rapports d'intégrité](service-fabric-view-entities-aggregated-health.md) sont toujours un bon point de départ.</span><span class="sxs-lookup"><span data-stu-id="cda0e-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="cda0e-106">Le plus simple pour accéder à ces rapports est de passer par PowerShell ou [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cda0e-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="cda0e-107">Cet article suppose que vous résolvez les problèmes d’un cluster à distance et que vous avez des notions de base concernant l'utilisation de l’un de ces outils.</span><span class="sxs-lookup"><span data-stu-id="cda0e-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="cda0e-108">Blocage d'application</span><span class="sxs-lookup"><span data-stu-id="cda0e-108">Application crash</span></span>
<span data-ttu-id="cda0e-109">Le rapport « La partition présente un nombre de réplicas ou d’instances inférieur à la valeur cible » est un bon moyen de savoir que votre service se bloque.</span><span class="sxs-lookup"><span data-stu-id="cda0e-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="cda0e-110">Pour savoir où votre service se bloque, cela demande un peu plus d’investigation.</span><span class="sxs-lookup"><span data-stu-id="cda0e-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="cda0e-111">Lors d’une exécution de votre service à grande l'échelle, votre meilleur ami est un ensemble de traces bien planifiées.</span><span class="sxs-lookup"><span data-stu-id="cda0e-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="cda0e-112">Nous vous suggérons d’essayer les [diagnostics Azure](service-fabric-diagnostics-how-to-setup-wad.md) pour collecter ces traces et d’utiliser une solution comme [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) pour afficher et rechercher les traces.</span><span class="sxs-lookup"><span data-stu-id="cda0e-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![Intégrité de la partition SFX](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="cda0e-114">Au cours de l’initialisation du service ou de l’acteur</span><span class="sxs-lookup"><span data-stu-id="cda0e-114">During service or actor initialization</span></span>
<span data-ttu-id="cda0e-115">Toutes les exceptions qui surviennent avant l’initialisation du type de service entraînent le blocage du processus.</span><span class="sxs-lookup"><span data-stu-id="cda0e-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="cda0e-116">Pour ces types de blocage, le journal d’événements des applications affiche l'erreur à partir de votre service.</span><span class="sxs-lookup"><span data-stu-id="cda0e-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="cda0e-117">Il s'agit des exceptions les plus courantes qui se produisent avant l’initialisation du service.</span><span class="sxs-lookup"><span data-stu-id="cda0e-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="cda0e-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="cda0e-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="cda0e-119">Cette erreur est souvent due à des dépendances d'assembly manquantes.</span><span class="sxs-lookup"><span data-stu-id="cda0e-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="cda0e-120">Vérifiez la propriété CopyLocal dans Visual Studio ou dans le Global Assembly Cache (GAC) pour le nœud.</span><span class="sxs-lookup"><span data-stu-id="cda0e-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="cda0e-121">***System.Runtime.InteropServices.COMException*** *à System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="cda0e-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="cda0e-122">Cette erreur indique que le nom du type de service inscrit ne correspond pas au manifeste du service.</span><span class="sxs-lookup"><span data-stu-id="cda0e-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="cda0e-123">[diagnostics Azure](service-fabric-diagnostics-how-to-setup-wad.md) peuvent être configurés pour télécharger le journal d’événements des applications pour tous les nœuds automatiquement.</span><span class="sxs-lookup"><span data-stu-id="cda0e-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="cda0e-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="cda0e-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="cda0e-125">Si le blocage se produit pendant l'initialisation ou l'exécution de votre type de service ou acteur inscrit, l'exception est interceptée par Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cda0e-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="cda0e-126">Vous pouvez l’afficher à partir des fournisseurs EventSource détaillés dans la section « Étapes suivantes ».</span><span class="sxs-lookup"><span data-stu-id="cda0e-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cda0e-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cda0e-127">Next steps</span></span>
<span data-ttu-id="cda0e-128">En savoir plus sur les diagnostics existants fournis par Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="cda0e-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="cda0e-129">Diagnostics Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="cda0e-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="cda0e-130">Diagnostics Reliable Services</span><span class="sxs-lookup"><span data-stu-id="cda0e-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)

