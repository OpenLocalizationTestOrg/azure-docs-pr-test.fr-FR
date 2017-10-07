---
title: "échecs d’aaaSimulate dans Azure microservices | Documents Microsoft"
description: "Cet article traite sur les actions de testabilité hello trouvées dans Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="a2098-103">Actions de testabilité</span><span class="sxs-lookup"><span data-stu-id="a2098-103">Testability actions</span></span>
<span data-ttu-id="a2098-104">Dans l’ordre toosimulate une infrastructure fiable, Azure Service Fabric fournit, hello pour le développeur toosimulate de façons différentes défaillances réelles et les transitions d’état.</span><span class="sxs-lookup"><span data-stu-id="a2098-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="a2098-105">Elles sont exposées en tant qu’actions de testabilité.</span><span class="sxs-lookup"><span data-stu-id="a2098-105">These are exposed as testability actions.</span></span> <span data-ttu-id="a2098-106">actions de Hello sont hello API de bas niveau qui provoquent une injection d’erreurs spécifiques, la transition d’état ou la validation.</span><span class="sxs-lookup"><span data-stu-id="a2098-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="a2098-107">En combinant ces actions, vous êtes en mesure d’écrire des scénarios de test complets pour vos services.</span><span class="sxs-lookup"><span data-stu-id="a2098-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="a2098-108">Service Fabric fournit en standard des scénarios courants de test, constitués de ces actions.</span><span class="sxs-lookup"><span data-stu-id="a2098-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="a2098-109">Nous recommandons vivement que vous utilisez ces scénarios intégrés, qui sont choisies avec soin les transitions d’état commun tootest et cas d’échec.</span><span class="sxs-lookup"><span data-stu-id="a2098-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="a2098-110">Toutefois, les actions peuvent être des scénarios de test personnalisée toocreate utilisé lorsque vous souhaitez que la couverture du tooadd pour les scénarios qui ne relèvent pas des scénarios intégrés hello encore ou qui sont personnalisés adaptés à votre application.</span><span class="sxs-lookup"><span data-stu-id="a2098-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="a2098-111">Les implémentations c# des actions de hello sont trouvent dans hello System.Fabric.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="a2098-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="a2098-112">module PowerShell de l’infrastructure de système de Hello se trouve dans hello Microsoft.ServiceFabric.Powershell.dll assembly.</span><span class="sxs-lookup"><span data-stu-id="a2098-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="a2098-113">Dans le cadre de l’installation du runtime, hello module ServiceFabric PowerShell est installé tooallow de facilité d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="a2098-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="a2098-114">Actions d’erreurs avec et sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="a2098-115">Les actions de testabilité sont répertoriées en deux groupes principaux :</span><span class="sxs-lookup"><span data-stu-id="a2098-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="a2098-116">Erreurs avec perte de données : ces erreurs simulent des défaillances comme les redémarrages de machines ou les incidents de processus.</span><span class="sxs-lookup"><span data-stu-id="a2098-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="a2098-117">Dans ce cas d’échecs, contexte d’exécution hello du processus s’arrête brusquement.</span><span class="sxs-lookup"><span data-stu-id="a2098-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="a2098-118">Cela signifie qu'aucun nettoyage de l’état de hello ne peut s’exécuter avant l’application hello redémarre.</span><span class="sxs-lookup"><span data-stu-id="a2098-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="a2098-119">Erreurs sans perte de données : ces erreurs simulent des actions comme des déplacements ou des abandons de réplicas provoqués par l’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="a2098-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="a2098-120">Dans ce cas, service de hello Obtient une notification de hello fermer et pouvez nettoyer l’état de hello avant de quitter.</span><span class="sxs-lookup"><span data-stu-id="a2098-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="a2098-121">Pour la validation de meilleure qualité, exécuter le service de hello et charge de travail entreprise tout en INDUISANT différents normale et anormal des erreurs.</span><span class="sxs-lookup"><span data-stu-id="a2098-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="a2098-122">Erreurs anormal couvrir des scénarios où hello service processus s’arrête brusquement au milieu de hello de certains flux de travail.</span><span class="sxs-lookup"><span data-stu-id="a2098-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="a2098-123">Ce test chemin de récupération hello une fois que le réplica de service hello est restaurée par l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="a2098-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="a2098-124">Cela permet de tester la cohérence des données et si l’état du service hello est maintenue correctement après des incidents.</span><span class="sxs-lookup"><span data-stu-id="a2098-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="a2098-125">Hello autre ensemble d’échecs (hello normale) tester que le service de hello réagit correctement tooreplicas déplacés ce par l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="a2098-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="a2098-126">Cette commande teste la gestion de l’annulation dans la méthode de RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="a2098-127">service de Hello doit toocheck pour hello annulation jeton qui est défini correctement enregistrer son état et quitte la méthode de RunAsync hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="a2098-128">Liste des actions de testabilité</span><span class="sxs-lookup"><span data-stu-id="a2098-128">Testability actions list</span></span>
| <span data-ttu-id="a2098-129">Action</span><span class="sxs-lookup"><span data-stu-id="a2098-129">Action</span></span> | <span data-ttu-id="a2098-130">Description</span><span class="sxs-lookup"><span data-stu-id="a2098-130">Description</span></span> | <span data-ttu-id="a2098-131">API gérée</span><span class="sxs-lookup"><span data-stu-id="a2098-131">Managed API</span></span> | <span data-ttu-id="a2098-132">Applet de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2098-132">PowerShell cmdlet</span></span> | <span data-ttu-id="a2098-133">Erreurs sans/avec perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a2098-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="a2098-134">CleanTestState</span></span> |<span data-ttu-id="a2098-135">Supprime tous les États de test hello cluster hello en cas d’un arrêt incorrect du pilote de test hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="a2098-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-136">CleanTestStateAsync</span></span> |<span data-ttu-id="a2098-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="a2098-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="a2098-138">Non applicable</span><span class="sxs-lookup"><span data-stu-id="a2098-138">Not applicable</span></span> |
| <span data-ttu-id="a2098-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="a2098-139">InvokeDataLoss</span></span> |<span data-ttu-id="a2098-140">Provoque une perte de données dans une partition de service.</span><span class="sxs-lookup"><span data-stu-id="a2098-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="a2098-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="a2098-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="a2098-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="a2098-143">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-143">Graceful</span></span> |
| <span data-ttu-id="a2098-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="a2098-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="a2098-145">Entraîne une perte de quorum dans une partition considérée de service avec état.</span><span class="sxs-lookup"><span data-stu-id="a2098-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="a2098-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="a2098-147">Invoke-ServiceFabricQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="a2098-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="a2098-148">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-148">Graceful</span></span> |
| <span data-ttu-id="a2098-149">MovePrimary</span><span class="sxs-lookup"><span data-stu-id="a2098-149">Move Primary</span></span> |<span data-ttu-id="a2098-150">Déplace hello spécifié le réplica principal d’un nœud de cluster spécifié toohello service avec état.</span><span class="sxs-lookup"><span data-stu-id="a2098-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="a2098-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-151">MovePrimaryAsync</span></span> |<span data-ttu-id="a2098-152">Move-ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="a2098-153">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-153">Graceful</span></span> |
| <span data-ttu-id="a2098-154">MoveSecondary</span><span class="sxs-lookup"><span data-stu-id="a2098-154">Move Secondary</span></span> |<span data-ttu-id="a2098-155">Déplace le réplica secondaire de hello actuel d’un nœud de cluster différent tooa service avec état.</span><span class="sxs-lookup"><span data-stu-id="a2098-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="a2098-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="a2098-157">Move-ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="a2098-158">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-158">Graceful</span></span> |
| <span data-ttu-id="a2098-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-159">RemoveReplica</span></span> |<span data-ttu-id="a2098-160">Simule une défaillance de réplica en supprimant un réplica d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="a2098-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="a2098-161">Cela ferme le réplica de hello et il passera toorole 'None', supprimant tous de l’état du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="a2098-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="a2098-163">Remove-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="a2098-164">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-164">Graceful</span></span> |
| <span data-ttu-id="a2098-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="a2098-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="a2098-166">Simule une défaillance de processus de package de code en redémarrant un package de code déployé sur un nœud de cluster.</span><span class="sxs-lookup"><span data-stu-id="a2098-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="a2098-167">Cela annule les processus du package de code hello, qui va redémarrer tous les réplicas de service d’utilisateur hello hébergés dans ce processus.</span><span class="sxs-lookup"><span data-stu-id="a2098-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="a2098-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="a2098-169">Restart-ServiceFabricDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="a2098-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="a2098-170">Avec perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-170">Ungraceful</span></span> |
| <span data-ttu-id="a2098-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="a2098-171">RestartNode</span></span> |<span data-ttu-id="a2098-172">Simule la défaillance d’un nœud de cluster Service Fabric en redémarrant un nœud.</span><span class="sxs-lookup"><span data-stu-id="a2098-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="a2098-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-173">RestartNodeAsync</span></span> |<span data-ttu-id="a2098-174">Restart-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a2098-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="a2098-175">Avec perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-175">Ungraceful</span></span> |
| <span data-ttu-id="a2098-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="a2098-176">RestartPartition</span></span> |<span data-ttu-id="a2098-177">Simule un scénario d’indisponibilité de centre de données ou de cluster en redémarrant certains des réplicas d’une partition, ou tous ces réplicas.</span><span class="sxs-lookup"><span data-stu-id="a2098-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="a2098-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-178">RestartPartitionAsync</span></span> |<span data-ttu-id="a2098-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="a2098-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="a2098-180">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-180">Graceful</span></span> |
| <span data-ttu-id="a2098-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-181">RestartReplica</span></span> |<span data-ttu-id="a2098-182">Simule un échec de réplication par le redémarrage d’un réplica persistant dans un cluster, fermeture de réplica de hello et puis de le rouvrir.</span><span class="sxs-lookup"><span data-stu-id="a2098-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="a2098-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-183">RestartReplicaAsync</span></span> |<span data-ttu-id="a2098-184">Restart-ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="a2098-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="a2098-185">Sans perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-185">Graceful</span></span> |
| <span data-ttu-id="a2098-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="a2098-186">StartNode</span></span> |<span data-ttu-id="a2098-187">Démarre un nœud dans un cluster déjà arrêté.</span><span class="sxs-lookup"><span data-stu-id="a2098-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="a2098-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-188">StartNodeAsync</span></span> |<span data-ttu-id="a2098-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a2098-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="a2098-190">Non applicable</span><span class="sxs-lookup"><span data-stu-id="a2098-190">Not applicable</span></span> |
| <span data-ttu-id="a2098-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="a2098-191">StopNode</span></span> |<span data-ttu-id="a2098-192">Simule une défaillance de nœud en arrêtant un nœud dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="a2098-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="a2098-193">nœud de Hello restera vers le bas jusqu'à ce que StartNode est appelée.</span><span class="sxs-lookup"><span data-stu-id="a2098-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="a2098-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-194">StopNodeAsync</span></span> |<span data-ttu-id="a2098-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="a2098-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="a2098-196">Avec perte de données</span><span class="sxs-lookup"><span data-stu-id="a2098-196">Ungraceful</span></span> |
| <span data-ttu-id="a2098-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="a2098-197">ValidateApplication</span></span> |<span data-ttu-id="a2098-198">Valide l’intégrité de tous les services de l’infrastructure de Service dans une application, généralement après induire des erreurs dans le système de hello et la disponibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="a2098-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="a2098-200">Test-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="a2098-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="a2098-201">Non applicable</span><span class="sxs-lookup"><span data-stu-id="a2098-201">Not applicable</span></span> |
| <span data-ttu-id="a2098-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="a2098-202">ValidateService</span></span> |<span data-ttu-id="a2098-203">Valide la disponibilité de hello et l’intégrité d’un service Service Fabric, généralement après induire des erreurs dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="a2098-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="a2098-204">ValidateServiceAsync</span></span> |<span data-ttu-id="a2098-205">Test-ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="a2098-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="a2098-206">Non applicable</span><span class="sxs-lookup"><span data-stu-id="a2098-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="a2098-207">Exécution d’une action de testabilité à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2098-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="a2098-208">Ce didacticiel vous montre comment toorun une action de test à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2098-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="a2098-209">Vous allez apprendre comment toorun une action de test par rapport à un cluster (une case) local ou un cluster Azure.</span><span class="sxs-lookup"><span data-stu-id="a2098-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="a2098-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric module PowerShell--est installé automatiquement lorsque vous installez hello MSI de l’infrastructure de Service de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a2098-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="a2098-211">module de Hello est chargé automatiquement lorsque vous ouvrez une invite de commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2098-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="a2098-212">Sections du didacticiel :</span><span class="sxs-lookup"><span data-stu-id="a2098-212">Tutorial segments:</span></span>

* [<span data-ttu-id="a2098-213">Exécuter une action dans un cluster à boîtier unique</span><span class="sxs-lookup"><span data-stu-id="a2098-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="a2098-214">Exécuter une action dans un cluster Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a2098-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="a2098-215">Exécuter une action dans un cluster à boîtier unique</span><span class="sxs-lookup"><span data-stu-id="a2098-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="a2098-216">toorun une action de test par rapport à un cluster local, connectez-vous d’abord toohello cluster et l’invite de commandes PowerShell hello ouvert en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="a2098-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="a2098-217">Examinons hello **ServiceFabricNode de redémarrage** action.</span><span class="sxs-lookup"><span data-stu-id="a2098-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="a2098-218">Ici hello action **ServiceFabricNode de redémarrage** est en cours d’exécution sur un nœud nommé « Node1 ».</span><span class="sxs-lookup"><span data-stu-id="a2098-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="a2098-219">mode de saisie semi-automatique Hello Spécifie qu’il ne doit pas vérifier si action de redémarrage-nœud hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="a2098-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="a2098-220">Mode de saisie semi-automatique hello en spécifiant en tant que « Vérifier » entraînera tooverify si l’action de redémarrage hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="a2098-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="a2098-221">Au lieu de spécifier directement le nœud de hello par son nom, vous pouvez spécifier via un type de clé et hello partition du réplica, comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2098-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="a2098-222">**Redémarrage-ServiceFabricNode** doit être toorestart utilisé un nœud de l’infrastructure de Service dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="a2098-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="a2098-223">Cette commande arrête le processus de Fabric.exe hello, qui va redémarrer tous hello système utilisateur et service service réplicas hébergés sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="a2098-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="a2098-224">Votre service à l’aide de cette tootest API permet de découvrir des bogues sur les chemins de récupération de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="a2098-225">Il permet de simuler des défaillances de nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="a2098-226">Hello capture d’écran suivante montre hello **ServiceFabricNode de redémarrage** commande testabilité en action.</span><span class="sxs-lookup"><span data-stu-id="a2098-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="a2098-227">Hello de sortie de hello tout d’abord **Get-ServiceFabricNode** (une applet de commande du module PowerShell de l’infrastructure de Service de hello) indique que le cluster local hello comporte cinq nœuds : Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="a2098-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="a2098-228">Après l’action de testabilité hello (applet de commande) **ServiceFabricNode de redémarrage** est exécutée sur le nœud de hello, nommé Node.4, nous voyons les temps de fonctionnement de ce nœud hello a été réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="a2098-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="a2098-229">Exécuter une action dans un cluster Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a2098-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="a2098-230">Exécute une action de testabilité (à l’aide de PowerShell) par rapport à un cluster Azure est la même action de hello toorunning par rapport à un cluster local.</span><span class="sxs-lookup"><span data-stu-id="a2098-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="a2098-231">Hello seule différence est que, avant de pouvoir exécuter action hello, au lieu de la connexion cluster local toohello, vous devez tooconnect toohello Azure tout d’abord de cluster.</span><span class="sxs-lookup"><span data-stu-id="a2098-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="a2098-232">Exécution d’une action de testabilité à l’aide de C&#35;</span><span class="sxs-lookup"><span data-stu-id="a2098-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="a2098-233">toorun une action de test à l’aide de c#, vous devez tooconnect toohello cluster à l’aide de fabricclient ne.</span><span class="sxs-lookup"><span data-stu-id="a2098-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="a2098-234">Puis obtenir hello paramètres nécessaires toorun hello action.</span><span class="sxs-lookup"><span data-stu-id="a2098-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="a2098-235">Différents paramètres peuvent être utilisés toorun hello même action.</span><span class="sxs-lookup"><span data-stu-id="a2098-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="a2098-236">Consulte hello action RestartServiceFabricNode, toorun monodirectionnelle, il est à l’aide des informations sur les nœuds hello (nom de nœud et ID d’instance de nœud) dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="a2098-237">Explications de paramètres :</span><span class="sxs-lookup"><span data-stu-id="a2098-237">Parameter explanation:</span></span>

* <span data-ttu-id="a2098-238">**CompleteMode** Spécifie que le mode hello ne doit pas vérifier si action de redémarrage hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="a2098-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="a2098-239">Mode de saisie semi-automatique hello en spécifiant en tant que « Vérifier » entraînera tooverify si l’action de redémarrage hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="a2098-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="a2098-240">**OperationTimeout** jeux hello laps de temps hello opération toofinish avant qu’une exception TimeoutException est levée.</span><span class="sxs-lookup"><span data-stu-id="a2098-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="a2098-241">**CancellationToken** permet un toobe en attente d’appel annulé.</span><span class="sxs-lookup"><span data-stu-id="a2098-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="a2098-242">Au lieu de spécifier directement le nœud de hello par son nom, vous pouvez spécifier via un type de clé et hello de partition de réplica.</span><span class="sxs-lookup"><span data-stu-id="a2098-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="a2098-243">Pour plus d’informations, consultez la section [Sélecteur de partitions et sélecteur de réplicas](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="a2098-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="a2098-244">Sélecteur de partitions et sélecteur de réplicas</span><span class="sxs-lookup"><span data-stu-id="a2098-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="a2098-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="a2098-245">PartitionSelector</span></span>
<span data-ttu-id="a2098-246">PartitionSelector est une application d’assistance exposée dans la testabilité et est utilisé tooselect spécifique de partition sur le tooperform une des actions de testabilité hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="a2098-247">Il peut être utilisé tooselect une partition spécifique si les ID de partition hello est connu au préalable.</span><span class="sxs-lookup"><span data-stu-id="a2098-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="a2098-248">Ou, vous pouvez fournir la clé de partition hello et opération de hello peut résoudre les ID de partition hello en interne.</span><span class="sxs-lookup"><span data-stu-id="a2098-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="a2098-249">Vous avez également option hello de sélection d’une partition aléatoire.</span><span class="sxs-lookup"><span data-stu-id="a2098-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="a2098-250">toouse ce programme d’assistance, créer l’objet de PartitionSelector hello et sélectionnez hello partition en utilisant l’une des méthodes de hello Select *.</span><span class="sxs-lookup"><span data-stu-id="a2098-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="a2098-251">Passez dans hello PartitionSelector objet toohello API qui le requiert.</span><span class="sxs-lookup"><span data-stu-id="a2098-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="a2098-252">Si aucune option n’est sélectionnée, la valeur par défaut partition aléatoire de tooa.</span><span class="sxs-lookup"><span data-stu-id="a2098-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="a2098-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="a2098-253">ReplicaSelector</span></span>
<span data-ttu-id="a2098-254">ReplicaSelector est une application d’assistance exposée dans la testabilité et est utilisé toohelp sélectionnez un réplica sur le tooperform une des actions de testabilité hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="a2098-255">Il peut être utilisé tooselect un réplica spécifique si les ID de réplica hello est connu au préalable.</span><span class="sxs-lookup"><span data-stu-id="a2098-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="a2098-256">En outre, vous pouvez hello en sélectionnant un réplica principal ou secondaire aléatoire.</span><span class="sxs-lookup"><span data-stu-id="a2098-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="a2098-257">ReplicaSelector dérive PartitionSelector, donc vous devez tooselect deux hello hello et réplica de partition sur laquelle vous souhaitez l’opération de testabilité tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="a2098-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="a2098-258">toouse ce programme d’assistance, créez un objet de ReplicaSelector et définissez hello librement tooselect hello réplica et hello partition.</span><span class="sxs-lookup"><span data-stu-id="a2098-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="a2098-259">Vous pouvez puis passez-la dans hello API qui le requiert.</span><span class="sxs-lookup"><span data-stu-id="a2098-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="a2098-260">Si aucune option n’est sélectionnée, la valeur par défaut réplica aléatoire de tooa et partition aléatoire.</span><span class="sxs-lookup"><span data-stu-id="a2098-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="a2098-261">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2098-261">Next steps</span></span>
* [<span data-ttu-id="a2098-262">Scénarios de testabilité</span><span class="sxs-lookup"><span data-stu-id="a2098-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="a2098-263">Comment tootest votre service</span><span class="sxs-lookup"><span data-stu-id="a2098-263">How tootest your service</span></span>
  * [<span data-ttu-id="a2098-264">Simuler des défaillances au cours des charges de travail de services</span><span class="sxs-lookup"><span data-stu-id="a2098-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="a2098-265">Échecs de communication de service à service</span><span class="sxs-lookup"><span data-stu-id="a2098-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

