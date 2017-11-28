---
title: aaaAzure analyse des performances de Service Fabric | Documents Microsoft
description: En savoir plus sur les compteurs de performances pour le suivi et le diagnostic des clusters Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="86d61-103">Mesures de performances</span><span class="sxs-lookup"><span data-stu-id="86d61-103">Performance metrics</span></span>

<span data-ttu-id="86d61-104">Métriques doivent être collectées toounderstand hello de performance de votre cluster ainsi que les applications de hello en cours d’exécution qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="86d61-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="86d61-105">Pour les clusters de l’infrastructure de Service, nous vous recommandons de hello suivant des compteurs de performance de collecte.</span><span class="sxs-lookup"><span data-stu-id="86d61-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="86d61-106">Nœuds</span><span class="sxs-lookup"><span data-stu-id="86d61-106">Nodes</span></span>

<span data-ttu-id="86d61-107">Pour les ordinateurs hello dans votre cluster, envisagez de hello suivant toobetter comprendre hello charge sur chaque ordinateur et de rendre le cluster approprié de mise à l’échelle des décisions les compteurs de performance de collecte.</span><span class="sxs-lookup"><span data-stu-id="86d61-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="86d61-108">Catégorie de compteur</span><span class="sxs-lookup"><span data-stu-id="86d61-108">Counter Category</span></span> | <span data-ttu-id="86d61-109">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="86d61-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="86d61-110">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-111">Avg. de file d’attente lecture disque</span><span class="sxs-lookup"><span data-stu-id="86d61-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="86d61-112">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-113">Avg. de file d’attente écriture disque</span><span class="sxs-lookup"><span data-stu-id="86d61-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="86d61-114">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-115">Avg. Disk sec/Read</span><span class="sxs-lookup"><span data-stu-id="86d61-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="86d61-116">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-117">Avg. Disk sec/Write</span><span class="sxs-lookup"><span data-stu-id="86d61-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="86d61-118">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-119">Nb d’opérations de lectures de disque/s </span><span class="sxs-lookup"><span data-stu-id="86d61-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="86d61-120">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-121">Nb d’octets de lecture de disque/s </span><span class="sxs-lookup"><span data-stu-id="86d61-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="86d61-122">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-123">Nb d’opération d’écriture de disque/s</span><span class="sxs-lookup"><span data-stu-id="86d61-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="86d61-124">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="86d61-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="86d61-125">Nb d’octets d’écriture de disque/s</span><span class="sxs-lookup"><span data-stu-id="86d61-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="86d61-126">Mémoire</span><span class="sxs-lookup"><span data-stu-id="86d61-126">Memory</span></span> | <span data-ttu-id="86d61-127">Nombre d’octets disponibles</span><span class="sxs-lookup"><span data-stu-id="86d61-127">Available MBytes</span></span> |
| <span data-ttu-id="86d61-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="86d61-128">PagingFile</span></span> | <span data-ttu-id="86d61-129">% utilisation</span><span class="sxs-lookup"><span data-stu-id="86d61-129">% Usage</span></span> |
| <span data-ttu-id="86d61-130">Processus (total)</span><span class="sxs-lookup"><span data-stu-id="86d61-130">Process(Total)</span></span> | <span data-ttu-id="86d61-131">% temps processeur</span><span class="sxs-lookup"><span data-stu-id="86d61-131">% Processor Time</span></span> |
| <span data-ttu-id="86d61-132">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-132">Process (per service)</span></span> | <span data-ttu-id="86d61-133">% temps processeur</span><span class="sxs-lookup"><span data-stu-id="86d61-133">% Processor Time</span></span> |
| <span data-ttu-id="86d61-134">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-134">Process (per service)</span></span> | <span data-ttu-id="86d61-135">Traitement ID</span><span class="sxs-lookup"><span data-stu-id="86d61-135">ID Process</span></span> |
| <span data-ttu-id="86d61-136">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-136">Process (per service)</span></span> | <span data-ttu-id="86d61-137">Octets privés</span><span class="sxs-lookup"><span data-stu-id="86d61-137">Private Bytes</span></span> |
| <span data-ttu-id="86d61-138">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-138">Process (per service)</span></span> | <span data-ttu-id="86d61-139">Nombre de threads</span><span class="sxs-lookup"><span data-stu-id="86d61-139">Thread Count</span></span> |
| <span data-ttu-id="86d61-140">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-140">Process (per service)</span></span> | <span data-ttu-id="86d61-141">Octets virtuels</span><span class="sxs-lookup"><span data-stu-id="86d61-141">Virtual Bytes</span></span> |
| <span data-ttu-id="86d61-142">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-142">Process (per service)</span></span> | <span data-ttu-id="86d61-143">Plage de travail</span><span class="sxs-lookup"><span data-stu-id="86d61-143">Working Set</span></span> |
| <span data-ttu-id="86d61-144">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-144">Process (per service)</span></span> | <span data-ttu-id="86d61-145">Plage de travail - Privée</span><span class="sxs-lookup"><span data-stu-id="86d61-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="86d61-146">Applications et services .NET</span><span class="sxs-lookup"><span data-stu-id="86d61-146">.NET applications and services</span></span>

<span data-ttu-id="86d61-147">Collecter hello suivant compteurs si vous déployez un cluster de tooyour services .NET.</span><span class="sxs-lookup"><span data-stu-id="86d61-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="86d61-148">Catégorie de compteur</span><span class="sxs-lookup"><span data-stu-id="86d61-148">Counter Category</span></span> | <span data-ttu-id="86d61-149">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="86d61-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="86d61-150">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-151">ID du processus</span><span class="sxs-lookup"><span data-stu-id="86d61-151">Process ID</span></span> |
| <span data-ttu-id="86d61-152">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-153">Nombre total d’octets dédiés</span><span class="sxs-lookup"><span data-stu-id="86d61-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="86d61-154">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-155">Nombre total d’octets réservés</span><span class="sxs-lookup"><span data-stu-id="86d61-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="86d61-156">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-157">Nombre d’octets dans tous les tas</span><span class="sxs-lookup"><span data-stu-id="86d61-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="86d61-158">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-159">Nombre de collections de génération 0</span><span class="sxs-lookup"><span data-stu-id="86d61-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="86d61-160">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-161">Nombre de collections de génération 1</span><span class="sxs-lookup"><span data-stu-id="86d61-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="86d61-162">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-163">Nombre de collections de génération 2</span><span class="sxs-lookup"><span data-stu-id="86d61-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="86d61-164">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="86d61-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="86d61-165">% de temps dans GC</span><span class="sxs-lookup"><span data-stu-id="86d61-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="86d61-166">Compteurs de performances personnalisés de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="86d61-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="86d61-167">Service Fabric génère une quantité importante de compteurs de performance personnalisés.</span><span class="sxs-lookup"><span data-stu-id="86d61-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="86d61-168">Si vous avez hello SDK installé, vous pouvez voir la liste complète de hello sur votre ordinateur Windows dans votre application de l’Analyseur de performances (Démarrer > Analyseur de performances).</span><span class="sxs-lookup"><span data-stu-id="86d61-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="86d61-169">Dans les applications de hello vous déployez tooyour cluster, si vous utilisez Reliable Actors, ajoutez des countes de `Service Fabric Actor` et `Service Fabric Actor Method` catégories (consultez [Service Fabric fiable acteurs Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="86d61-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="86d61-170">Si vous utilisez Reliable Services, nous disposons également de catégories `Service Fabric Service` et `Service Fabric Service Method` desquelles vous devez collecter des compteurs.</span><span class="sxs-lookup"><span data-stu-id="86d61-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="86d61-171">Si vous utilisez des Collections fiable, nous vous recommandons d’ajouter hello `Avg. Transaction ms/Commit` de hello `Service Fabric Transactional Replicator` toocollect la latence moyenne de validation hello par mesure de la transaction.</span><span class="sxs-lookup"><span data-stu-id="86d61-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="86d61-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86d61-172">Next steps</span></span>

* <span data-ttu-id="86d61-173">En savoir plus sur [génération des événements au niveau de plate-forme hello](service-fabric-diagnostics-event-generation-infra.md) dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="86d61-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="86d61-174">Collecter des mesures de performances via [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="86d61-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
