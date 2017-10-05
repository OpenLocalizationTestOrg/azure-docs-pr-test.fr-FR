---
title: "Suivi des performances d’Azure Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="6e2a6-103">Mesures de performances</span><span class="sxs-lookup"><span data-stu-id="6e2a6-103">Performance metrics</span></span>

<span data-ttu-id="6e2a6-104">Les mesures doivent être collectées pour comprendre les performances de votre cluster, et des applications qu’il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="6e2a6-105">Pour les clusters Service Fabric, nous vous recommandons de collecter les compteurs de performances suivants.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="6e2a6-106">Nœuds</span><span class="sxs-lookup"><span data-stu-id="6e2a6-106">Nodes</span></span>

<span data-ttu-id="6e2a6-107">Pour les ordinateurs de votre cluster, veuillez collecter les compteurs de performances suivants afin de mieux comprendre la charge de chaque ordinateur et de prendre les meilleures décisions quant à la mise à l’échelle des clusters.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="6e2a6-108">Catégorie de compteur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-108">Counter Category</span></span> | <span data-ttu-id="6e2a6-109">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6e2a6-110">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-111">Avg.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-111">Avg.</span></span> <span data-ttu-id="6e2a6-112">de file d’attente lecture disque</span><span class="sxs-lookup"><span data-stu-id="6e2a6-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="6e2a6-113">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-114">Avg.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-114">Avg.</span></span> <span data-ttu-id="6e2a6-115">de file d’attente écriture disque</span><span class="sxs-lookup"><span data-stu-id="6e2a6-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="6e2a6-116">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-117">Avg.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-117">Avg.</span></span> <span data-ttu-id="6e2a6-118">Disk sec/Read</span><span class="sxs-lookup"><span data-stu-id="6e2a6-118">Disk sec/Read</span></span> |
| <span data-ttu-id="6e2a6-119">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-120">Avg.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-120">Avg.</span></span> <span data-ttu-id="6e2a6-121">Disk sec/Write</span><span class="sxs-lookup"><span data-stu-id="6e2a6-121">Disk sec/Write</span></span> |
| <span data-ttu-id="6e2a6-122">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-123">Nb d’opérations de lectures de disque/s </span><span class="sxs-lookup"><span data-stu-id="6e2a6-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="6e2a6-124">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-125">Nb d’octets de lecture de disque/s </span><span class="sxs-lookup"><span data-stu-id="6e2a6-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="6e2a6-126">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-127">Nb d’opération d’écriture de disque/s</span><span class="sxs-lookup"><span data-stu-id="6e2a6-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="6e2a6-128">PhysicalDisk(per Disk)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6e2a6-129">Nb d’octets d’écriture de disque/s</span><span class="sxs-lookup"><span data-stu-id="6e2a6-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="6e2a6-130">Mémoire</span><span class="sxs-lookup"><span data-stu-id="6e2a6-130">Memory</span></span> | <span data-ttu-id="6e2a6-131">Nombre d’octets disponibles</span><span class="sxs-lookup"><span data-stu-id="6e2a6-131">Available MBytes</span></span> |
| <span data-ttu-id="6e2a6-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="6e2a6-132">PagingFile</span></span> | <span data-ttu-id="6e2a6-133">% utilisation</span><span class="sxs-lookup"><span data-stu-id="6e2a6-133">% Usage</span></span> |
| <span data-ttu-id="6e2a6-134">Processus (total)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-134">Process(Total)</span></span> | <span data-ttu-id="6e2a6-135">% temps processeur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-135">% Processor Time</span></span> |
| <span data-ttu-id="6e2a6-136">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-136">Process (per service)</span></span> | <span data-ttu-id="6e2a6-137">% temps processeur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-137">% Processor Time</span></span> |
| <span data-ttu-id="6e2a6-138">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-138">Process (per service)</span></span> | <span data-ttu-id="6e2a6-139">Traitement ID</span><span class="sxs-lookup"><span data-stu-id="6e2a6-139">ID Process</span></span> |
| <span data-ttu-id="6e2a6-140">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-140">Process (per service)</span></span> | <span data-ttu-id="6e2a6-141">Octets privés</span><span class="sxs-lookup"><span data-stu-id="6e2a6-141">Private Bytes</span></span> |
| <span data-ttu-id="6e2a6-142">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-142">Process (per service)</span></span> | <span data-ttu-id="6e2a6-143">Nombre de threads</span><span class="sxs-lookup"><span data-stu-id="6e2a6-143">Thread Count</span></span> |
| <span data-ttu-id="6e2a6-144">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-144">Process (per service)</span></span> | <span data-ttu-id="6e2a6-145">Octets virtuels</span><span class="sxs-lookup"><span data-stu-id="6e2a6-145">Virtual Bytes</span></span> |
| <span data-ttu-id="6e2a6-146">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-146">Process (per service)</span></span> | <span data-ttu-id="6e2a6-147">Plage de travail</span><span class="sxs-lookup"><span data-stu-id="6e2a6-147">Working Set</span></span> |
| <span data-ttu-id="6e2a6-148">Processus (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-148">Process (per service)</span></span> | <span data-ttu-id="6e2a6-149">Plage de travail - Privée</span><span class="sxs-lookup"><span data-stu-id="6e2a6-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="6e2a6-150">Applications et services .NET</span><span class="sxs-lookup"><span data-stu-id="6e2a6-150">.NET applications and services</span></span>

<span data-ttu-id="6e2a6-151">Collectez les compteurs suivants si vous déployez des services .NET dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="6e2a6-152">Catégorie de compteur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-152">Counter Category</span></span> | <span data-ttu-id="6e2a6-153">Nom de compteur</span><span class="sxs-lookup"><span data-stu-id="6e2a6-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6e2a6-154">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-155">ID du processus</span><span class="sxs-lookup"><span data-stu-id="6e2a6-155">Process ID</span></span> |
| <span data-ttu-id="6e2a6-156">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-157">Nombre total d’octets dédiés</span><span class="sxs-lookup"><span data-stu-id="6e2a6-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="6e2a6-158">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-159">Nombre total d’octets réservés</span><span class="sxs-lookup"><span data-stu-id="6e2a6-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="6e2a6-160">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-161">Nombre d’octets dans tous les tas</span><span class="sxs-lookup"><span data-stu-id="6e2a6-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="6e2a6-162">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-163">Nombre de collections de génération 0</span><span class="sxs-lookup"><span data-stu-id="6e2a6-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="6e2a6-164">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-165">Nombre de collections de génération 1</span><span class="sxs-lookup"><span data-stu-id="6e2a6-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="6e2a6-166">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-167">Nombre de collections de génération 2</span><span class="sxs-lookup"><span data-stu-id="6e2a6-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="6e2a6-168">.NET CLR Memory (par service)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6e2a6-169">% de temps dans GC</span><span class="sxs-lookup"><span data-stu-id="6e2a6-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="6e2a6-170">Compteurs de performances personnalisés de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e2a6-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="6e2a6-171">Service Fabric génère une quantité importante de compteurs de performance personnalisés.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="6e2a6-172">Si le kit de développement SDK est installé, vous pouvez voir la liste complète sur votre ordinateur Windows dans l’Analyseur de performances (Démarrer > Analyseur de performances).</span><span class="sxs-lookup"><span data-stu-id="6e2a6-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="6e2a6-173">Si vous utilisez Reliable Actors, dans les applications que vous déployez dans votre cluster, ajoutez des compteurs des catégories `Service Fabric Actor` et `Service Fabric Actor Method` (consultez [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)) (Diagnostics Reliable Actors de Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="6e2a6-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="6e2a6-174">Si vous utilisez Reliable Services, nous disposons également de catégories `Service Fabric Service` et `Service Fabric Service Method` desquelles vous devez collecter des compteurs.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="6e2a6-175">Si vous utilisez Reliable Collections, nous vous recommandons d’ajouter `Avg. Transaction ms/Commit` depuis le `Service Fabric Transactional Replicator` pour collecter la latence moyenne de validation par mesure de transaction.</span><span class="sxs-lookup"><span data-stu-id="6e2a6-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6e2a6-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e2a6-176">Next steps</span></span>

* <span data-ttu-id="6e2a6-177">En savoir plus sur la [génération d’événements au niveau de la plateforme](service-fabric-diagnostics-event-generation-infra.md) dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6e2a6-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="6e2a6-178">Collecter des mesures de performances via [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="6e2a6-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
