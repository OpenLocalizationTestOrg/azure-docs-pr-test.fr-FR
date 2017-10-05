---
title: "Différences Azure Service Fabric entre Linux et Windows | Microsoft Docs"
description: "Différences entre la version préliminaire d’Azure Service Fabric sur Linux et Azure Service Fabric sur Windows."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7b80bb7d4a4e6a1b4cf47ce87200f47339785c53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="2497d-103">Différences entre Service Fabric sur Linux (version préliminaire) et Windows (mise à la disposition générale)</span><span class="sxs-lookup"><span data-stu-id="2497d-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="2497d-104">Étant donné que Service Fabric sur Linux est une version préliminaire, certaines fonctionnalités sont prises en charge sur Windows, mais pas encore sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2497d-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="2497d-105">Les ensembles de fonctionnalités seront identiques lors de la mise à disposition générale de Service Fabric sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2497d-105">Eventually, the feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="2497d-106">Avec les versions à venir, cet écart de fonctionnalités sera réduit.</span><span class="sxs-lookup"><span data-stu-id="2497d-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="2497d-107">Les différences suivantes existent entre les versions les plus récentes disponibles (c’est-à-dire entre la version 5.6 pour Windows et la version 5.5 pour Linux) :</span><span class="sxs-lookup"><span data-stu-id="2497d-107">The following differences exist between the latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="2497d-108">Les collections fiables (et les services avec état fiable)</span><span class="sxs-lookup"><span data-stu-id="2497d-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="2497d-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="2497d-109">ReverseProxy</span></span> 
* <span data-ttu-id="2497d-110">Le programme d’installation autonome</span><span class="sxs-lookup"><span data-stu-id="2497d-110">Standalone installer</span></span> 
* <span data-ttu-id="2497d-111">La validation de schéma XML pour les fichiers de manifeste</span><span class="sxs-lookup"><span data-stu-id="2497d-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="2497d-112">La redirection de la console</span><span class="sxs-lookup"><span data-stu-id="2497d-112">Console redirection</span></span> 
* <span data-ttu-id="2497d-113">Le service d’analyse des erreurs</span><span class="sxs-lookup"><span data-stu-id="2497d-113">The Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="2497d-114">Docker Compose et les pilotes de journalisation et de volume pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="2497d-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="2497d-115">La gestion des ressources pour les conteneurs et les services</span><span class="sxs-lookup"><span data-stu-id="2497d-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="2497d-116">Service DNS</span><span class="sxs-lookup"><span data-stu-id="2497d-116">DNS service</span></span>
* <span data-ttu-id="2497d-117">La prise en charge d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2497d-117">Azure Active Directory support</span></span>
* <span data-ttu-id="2497d-118">Des équivalents de commandes d’interface de ligne de commande de certaines commandes Powershell</span><span class="sxs-lookup"><span data-stu-id="2497d-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="2497d-119">Seul un sous-ensemble de commandes Powershell peut être exécuté sur un cluster Linux (comme expliqué en détail dans la section suivante).</span><span class="sxs-lookup"><span data-stu-id="2497d-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in the next section).</span></span>

>[!NOTE]
><span data-ttu-id="2497d-120">La redirection de console n’est pas prise en charge dans les clusters de production, même sur Windows.</span><span class="sxs-lookup"><span data-stu-id="2497d-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="2497d-121">Les outils de développement sont également différents entre Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="2497d-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="2497d-122">VisualStudio, Powershell, VSTS et ETW sont utilisés sur Windows, tandis que Yeoman, Eclipse, Jenkins et LTTng sont utilisés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2497d-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="2497d-123">Applets de commande PowerShell ne fonctionnant pas sur un cluster Linux Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2497d-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="2497d-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="2497d-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="2497d-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="2497d-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="2497d-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="2497d-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="2497d-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="2497d-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="2497d-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="2497d-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="2497d-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="2497d-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="2497d-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="2497d-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="2497d-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="2497d-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="2497d-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="2497d-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="2497d-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="2497d-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="2497d-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="2497d-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="2497d-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="2497d-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="2497d-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="2497d-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="2497d-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="2497d-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="2497d-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="2497d-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="2497d-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="2497d-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="2497d-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="2497d-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="2497d-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="2497d-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="2497d-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="2497d-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="2497d-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="2497d-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="2497d-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="2497d-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="2497d-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="2497d-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="2497d-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="2497d-146">Cmd</span></span>
* <span data-ttu-id="2497d-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="2497d-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="2497d-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="2497d-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="2497d-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="2497d-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="2497d-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="2497d-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="2497d-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="2497d-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="2497d-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="2497d-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="2497d-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="2497d-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="2497d-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="2497d-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="2497d-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="2497d-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="2497d-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="2497d-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="2497d-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="2497d-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="2497d-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="2497d-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="2497d-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="2497d-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="2497d-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="2497d-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="2497d-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="2497d-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="2497d-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="2497d-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="2497d-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="2497d-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="2497d-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="2497d-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="2497d-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="2497d-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="2497d-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="2497d-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="2497d-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="2497d-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="2497d-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="2497d-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="2497d-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="2497d-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2497d-177">Next steps</span></span>
* [<span data-ttu-id="2497d-178">Préparer votre environnement de développement sur Linux</span><span class="sxs-lookup"><span data-stu-id="2497d-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="2497d-179">Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)</span><span class="sxs-lookup"><span data-stu-id="2497d-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="2497d-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide de Yeoman)</span><span class="sxs-lookup"><span data-stu-id="2497d-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="2497d-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide du plug-in Service Fabric pour Eclipse)</span><span class="sxs-lookup"><span data-stu-id="2497d-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="2497d-182">Create your first Java application on Linux (Créer votre première application Java sur Linux)</span><span class="sxs-lookup"><span data-stu-id="2497d-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="2497d-183">Utilisez l’interface de ligne de commande Service Fabric pour gérer vos applications</span><span class="sxs-lookup"><span data-stu-id="2497d-183">Use the Service Fabric CLI to manage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
