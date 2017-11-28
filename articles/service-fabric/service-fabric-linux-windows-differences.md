---
title: "aaaAzure Service Fabric différences entre Linux et Windows | Documents Microsoft"
description: "Différences entre hello Azure Service Fabric aperçu sur Linux et Azure Service Fabric sur Windows."
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
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="9ea1e-103">Différences entre Service Fabric sur Linux (version préliminaire) et Windows (mise à la disposition générale)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="9ea1e-104">Étant donné que Service Fabric sur Linux est une version préliminaire, certaines fonctionnalités sont prises en charge sur Windows, mais pas encore sur Linux.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="9ea1e-105">Finalement, ensembles de fonctionnalités hello sera à parité quand Service Fabric sur Linux devient disponible.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="9ea1e-106">Avec les versions à venir, cet écart de fonctionnalités sera réduit.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="9ea1e-107">Hello différences suivantes existent entre hello dernières releases disponibles (autrement dit, entre la version 5.6 sur Windows et la version 5.5 sur Linux) :</span><span class="sxs-lookup"><span data-stu-id="9ea1e-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="9ea1e-108">Les collections fiables (et les services avec état fiable)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="9ea1e-109">ReverseProxy</span><span class="sxs-lookup"><span data-stu-id="9ea1e-109">ReverseProxy</span></span> 
* <span data-ttu-id="9ea1e-110">Le programme d’installation autonome</span><span class="sxs-lookup"><span data-stu-id="9ea1e-110">Standalone installer</span></span> 
* <span data-ttu-id="9ea1e-111">La validation de schéma XML pour les fichiers de manifeste</span><span class="sxs-lookup"><span data-stu-id="9ea1e-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="9ea1e-112">La redirection de la console</span><span class="sxs-lookup"><span data-stu-id="9ea1e-112">Console redirection</span></span> 
* <span data-ttu-id="9ea1e-113">Hello erreur Analysis Service (FAS)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="9ea1e-114">Docker Compose et les pilotes de journalisation et de volume pour les conteneurs</span><span class="sxs-lookup"><span data-stu-id="9ea1e-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="9ea1e-115">La gestion des ressources pour les conteneurs et les services</span><span class="sxs-lookup"><span data-stu-id="9ea1e-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="9ea1e-116">Service DNS</span><span class="sxs-lookup"><span data-stu-id="9ea1e-116">DNS service</span></span>
* <span data-ttu-id="9ea1e-117">La prise en charge d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ea1e-117">Azure Active Directory support</span></span>
* <span data-ttu-id="9ea1e-118">Des équivalents de commandes d’interface de ligne de commande de certaines commandes Powershell</span><span class="sxs-lookup"><span data-stu-id="9ea1e-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="9ea1e-119">Seul un sous-ensemble des commandes Powershell peut être exécuté sur un cluster Linux (tel qu’il est développé dans la section suivante de hello).</span><span class="sxs-lookup"><span data-stu-id="9ea1e-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="9ea1e-120">La redirection de console n’est pas prise en charge dans les clusters de production, même sur Windows.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="9ea1e-121">Les outils de développement sont également différents entre Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="9ea1e-122">VisualStudio, Powershell, VSTS et ETW sont utilisés sur Windows, tandis que Yeoman, Eclipse, Jenkins et LTTng sont utilisés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="9ea1e-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="9ea1e-123">Applets de commande PowerShell ne fonctionnant pas sur un cluster Linux Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9ea1e-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="9ea1e-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="9ea1e-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="9ea1e-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="9ea1e-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="9ea1e-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="9ea1e-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="9ea1e-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="9ea1e-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="9ea1e-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="9ea1e-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="9ea1e-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="9ea1e-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="9ea1e-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="9ea1e-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="9ea1e-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="9ea1e-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="9ea1e-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="9ea1e-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="9ea1e-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="9ea1e-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="9ea1e-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="9ea1e-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="9ea1e-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="9ea1e-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="9ea1e-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="9ea1e-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="9ea1e-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="9ea1e-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="9ea1e-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="9ea1e-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="9ea1e-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="9ea1e-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="9ea1e-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="9ea1e-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="9ea1e-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="9ea1e-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="9ea1e-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="9ea1e-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="9ea1e-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="9ea1e-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="9ea1e-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="9ea1e-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="9ea1e-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="9ea1e-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="9ea1e-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="9ea1e-146">Cmd</span></span>
* <span data-ttu-id="9ea1e-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="9ea1e-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="9ea1e-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="9ea1e-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="9ea1e-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="9ea1e-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="9ea1e-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="9ea1e-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="9ea1e-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="9ea1e-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="9ea1e-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="9ea1e-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="9ea1e-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="9ea1e-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="9ea1e-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="9ea1e-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="9ea1e-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="9ea1e-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="9ea1e-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="9ea1e-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="9ea1e-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="9ea1e-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="9ea1e-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="9ea1e-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="9ea1e-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="9ea1e-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="9ea1e-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="9ea1e-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="9ea1e-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="9ea1e-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="9ea1e-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="9ea1e-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="9ea1e-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="9ea1e-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="9ea1e-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="9ea1e-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="9ea1e-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="9ea1e-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="9ea1e-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="9ea1e-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="9ea1e-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="9ea1e-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="9ea1e-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="9ea1e-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="9ea1e-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="9ea1e-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ea1e-177">Next steps</span></span>
* [<span data-ttu-id="9ea1e-178">Préparer votre environnement de développement sur Linux</span><span class="sxs-lookup"><span data-stu-id="9ea1e-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="9ea1e-179">Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="9ea1e-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide de Yeoman)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-180">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="9ea1e-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide du plug-in Service Fabric pour Eclipse)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-181">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="9ea1e-182">Create your first Java application on Linux (Créer votre première application Java sur Linux)</span><span class="sxs-lookup"><span data-stu-id="9ea1e-182">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="9ea1e-183">Utiliser hello Service Fabric CLI toomanage vos applications</span><span class="sxs-lookup"><span data-stu-id="9ea1e-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
