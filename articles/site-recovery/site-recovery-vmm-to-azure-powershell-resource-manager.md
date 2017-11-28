---
title: "Réplication de machines virtuelles Hyper-V dans des clouds VMM à l’aide d’Azure Site Recovery et de PowerShell (Resource Manager) | Microsoft Docs"
description: "Réplication de machines virtuelles Hyper-V dans des clouds VMM à l'aide d'Azure Site Recovery et PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: 34086044db752f09f1282517b59856091e85c2fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="b56cb-103">Réplication vers Azure de machines virtuelles Hyper-V hébergées dans des clouds VMM à l’aide de PowerShell et d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b56cb-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b56cb-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b56cb-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="b56cb-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b56cb-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="b56cb-106">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="b56cb-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="b56cb-107">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="b56cb-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="b56cb-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b56cb-108">Overview</span></span>
<span data-ttu-id="b56cb-109">Azure Site Recovery contribue à mettre en œuvre la stratégie de continuité des activités et de récupération d'urgence de votre entreprise en coordonnant la réplication, le basculement et la récupération de machines virtuelles dans divers scénarios de déploiement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-109">Azure Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="b56cb-110">Pour obtenir la liste complète des scénarios de déploiement, consultez la [Vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b56cb-110">For a full list of deployment scenarios see the [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="b56cb-111">Cet article vous montre comment utiliser PowerShell pour automatiser les tâches courantes à effectuer lorsque vous configurez Azure Site Recovery pour répliquer des machines virtuelles Hyper-V dans des clouds System Center VMM vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-111">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to Azure storage.</span></span>

<span data-ttu-id="b56cb-112">L’article inclut la configuration requise pour le scénario et décrit les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b56cb-112">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="b56cb-113">Configuration d’un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b56cb-113">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="b56cb-114">Installation du fournisseur Azure Site Recovery sur le serveur VMM source</span><span class="sxs-lookup"><span data-stu-id="b56cb-114">Install the Azure Site Recovery Provider on the source VMM server</span></span>
* <span data-ttu-id="b56cb-115">Inscription du serveur dans le coffre, ajout d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b56cb-115">Register the server in the vault, add an Azure storage account</span></span>
* <span data-ttu-id="b56cb-116">Installation de l’agent Azure Recovery Services sur les serveurs Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b56cb-116">Install the Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="b56cb-117">Configuration des paramètres de protection des clouds VMM qui seront appliqués à toutes les machines virtuelles protégées</span><span class="sxs-lookup"><span data-stu-id="b56cb-117">Configure protection settings for VMM clouds, that will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="b56cb-118">Activation de la protection de ces machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b56cb-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="b56cb-119">Test du basculement pour s’assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="b56cb-119">Test the fail-over to make sure everything's working as expected.</span></span>

<span data-ttu-id="b56cb-120">Si vous rencontrez des problèmes pour mettre en œuvre ce scénario, posez vos questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b56cb-120">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="b56cb-121">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b56cb-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b56cb-122">Cet article traite de l’utilisation du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b56cb-122">This article covers using the Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="b56cb-123">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b56cb-123">Before you start</span></span>
<span data-ttu-id="b56cb-124">Assurez-vous que les conditions préalables sont remplies :</span><span class="sxs-lookup"><span data-stu-id="b56cb-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="b56cb-125">Conditions préalables pour Azure</span><span class="sxs-lookup"><span data-stu-id="b56cb-125">Azure prerequisites</span></span>
* <span data-ttu-id="b56cb-126">Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="b56cb-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="b56cb-127">Si vous n’en avez pas, commencez avec un [compte gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="b56cb-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="b56cb-128">Vous pouvez aussi consulter la [Tarification d’Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="b56cb-128">In addition, you can read about the [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="b56cb-129">Vous avez besoin d’un abonnement Fournisseur de solutions cloud si vous essayez une réplication vers un abonnement de ce type.</span><span class="sxs-lookup"><span data-stu-id="b56cb-129">You'll need a CSP subscription if you are trying out the replication to a CSP subscription scenario.</span></span> <span data-ttu-id="b56cb-130">Pour en savoir plus sur le programme Fournisseur de solutions cloud, consultez [S’inscrire au programme Fournisseur de solutions cloud](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="b56cb-130">Learn more about the CSP program in [how to enroll in the CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="b56cb-131">Vous avez besoin d’un compte de stockage Azure v2 (Resource Manager) pour stocker les données répliquées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-131">You'll need an Azure v2 storage (Resource Manager) account to store data replicated to Azure.</span></span> <span data-ttu-id="b56cb-132">La géo-réplication doit être activée pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="b56cb-132">The account needs geo-replication enabled.</span></span> <span data-ttu-id="b56cb-133">Ce dernier doit se trouver dans la même région que le service Azure Site Recovery et être associé au même abonnement ou à l’abonnement Fournisseur de solutions cloud.</span><span class="sxs-lookup"><span data-stu-id="b56cb-133">It should be in the same region as the Azure Site Recovery service, and be associated with the same subscription or the CSP subscription.</span></span> <span data-ttu-id="b56cb-134">Pour en savoir plus sur la configuration d’Azure Storage, consultez [Introduction à Microsoft Azure Storage](../storage/common/storage-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="b56cb-134">To learn more about setting up Azure storage, see the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="b56cb-135">Vous devez vous assurer que les machines virtuelles que vous voulez protéger sont conformes à la [configuration requise des machines virtuelles Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="b56cb-135">You'll need to make sure that virtual machines you want to protect comply with the [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="b56cb-136">Actuellement, seules les opérations au niveau de la machine virtuelle sont possibles par le biais de Powershell.</span><span class="sxs-lookup"><span data-stu-id="b56cb-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="b56cb-137">La prise en charge des opérations au niveau du plan de récupération sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="b56cb-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="b56cb-138">Pour le moment, vous ne pouvez effectuer de basculement qu’au niveau de granularité « machine virtuelle protégée » et non au niveau du plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="b56cb-138">For now, you are limited to performing fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="b56cb-139">Configuration requise pour VMM</span><span class="sxs-lookup"><span data-stu-id="b56cb-139">VMM prerequisites</span></span>
* <span data-ttu-id="b56cb-140">Vous aurez besoin d'un serveur VMM exécuté sur System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="b56cb-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="b56cb-141">Tout serveur VMM contenant des machines virtuelles à protéger doit exécuter le fournisseur Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b56cb-141">Any VMM server containing virtual machines you want to protect must be running the Azure Site Recovery Provider.</span></span> <span data-ttu-id="b56cb-142">Celui-ci est installé lors du déploiement d'Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b56cb-142">This is installed during the Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="b56cb-143">Vous aurez besoin d'au moins un cloud sur le serveur VMM que vous souhaitez protéger.</span><span class="sxs-lookup"><span data-stu-id="b56cb-143">You'll need at least one cloud on the VMM server you want to protect.</span></span> <span data-ttu-id="b56cb-144">Le coud doit contenir :</span><span class="sxs-lookup"><span data-stu-id="b56cb-144">The cloud should contain:</span></span>
  * <span data-ttu-id="b56cb-145">un ou plusieurs groupes hôtes VMM ;</span><span class="sxs-lookup"><span data-stu-id="b56cb-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="b56cb-146">un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte.</span><span class="sxs-lookup"><span data-stu-id="b56cb-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="b56cb-147">une ou plusieurs machines virtuelles sur le serveur Hyper-V source.</span><span class="sxs-lookup"><span data-stu-id="b56cb-147">One or more virtual machines on the source Hyper-V server.</span></span>
* <span data-ttu-id="b56cb-148">Pour en savoir plus sur la configuration des clouds VMM :</span><span class="sxs-lookup"><span data-stu-id="b56cb-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="b56cb-149">Lisez la documentation sur les clouds privés VMM dans les sections [Nouveautés sur le cloud privé dans System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) et [VMM 2012 et les clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="b56cb-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and the clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="b56cb-150">En savoir plus sur la [Configuration de l'infrastructure de cloud VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="b56cb-150">Learn about [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="b56cb-151">Une fois vos éléments d’infrastructure cloud en place, apprenez à créer des clouds privés dans [Création d’un cloud privé dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) et [Procédure pas à pas : Création de clouds privés avec System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="b56cb-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="b56cb-152">Conditions préalables liées à Hyper-V</span><span class="sxs-lookup"><span data-stu-id="b56cb-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="b56cb-153">Les serveurs hôtes Hyper-V doivent exécuter au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et les dernières mises à jour doivent être installées.</span><span class="sxs-lookup"><span data-stu-id="b56cb-153">The host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have the latest updates installed.</span></span>
* <span data-ttu-id="b56cb-154">Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="b56cb-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="b56cb-155">Vous devez configurer manuellement le service Broker du cluster.</span><span class="sxs-lookup"><span data-stu-id="b56cb-155">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="b56cb-156">Concernant l'option</span><span class="sxs-lookup"><span data-stu-id="b56cb-156">For</span></span>
* <span data-ttu-id="b56cb-157">Pour obtenir des instructions, consultez [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx)(Configuration du service Broker de réplication Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="b56cb-157">For instructions see [How to Configure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="b56cb-158">Tout cluster ou serveur hôte Hyper-V pour lequel vous souhaitez gérer la protection doit être inclus dans un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="b56cb-158">Any Hyper-V host server or cluster for which you want to manage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="b56cb-159">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="b56cb-159">Network mapping prerequisites</span></span>
<span data-ttu-id="b56cb-160">Quand vous protégez des machines virtuelles dans Azure, le mappage réseau relie les réseaux de machines virtuelles sur le serveur VMM source et les réseaux Azure cibles pour permettre ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b56cb-160">When you protect virtual machines in Azure, the network mapping  maps the virtual machine networks on the source VMM server and target Azure networks to enable the following:</span></span>

* <span data-ttu-id="b56cb-161">Toutes les machines qui basculent sur le même réseau peuvent se connecter les unes aux autres, quel que soit le plan de récupération auquel elles appartiennent.</span><span class="sxs-lookup"><span data-stu-id="b56cb-161">All machines which fail over on the same network can connect to each other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="b56cb-162">Si une passerelle réseau est configurée sur le réseau Azure cible, les machines virtuelles peuvent se connecter à d'autres machines virtuelles locales.</span><span class="sxs-lookup"><span data-stu-id="b56cb-162">If a network gateway is setup on the target Azure network, virtual machines can connect to other on-premises virtual machines.</span></span>
* <span data-ttu-id="b56cb-163">Si vous ne configurez pas le mappage réseau, seules les machines virtuelles qui basculent dans le même plan de récupération peuvent se connecter les unes aux autres après le basculement vers Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-163">If you don’t configure network mapping, only the virtual machines that fail over in the same recovery plan will be able to connect to each other after fail-over to Azure.</span></span>

<span data-ttu-id="b56cb-164">Si vous souhaitez déployer le mappage réseau, les conditions suivantes doivent être remplies :</span><span class="sxs-lookup"><span data-stu-id="b56cb-164">If you want to deploy network mapping you'll need the following:</span></span>

* <span data-ttu-id="b56cb-165">Les machines virtuelles que vous souhaitez protéger sur le serveur VMM source doivent être connectées à un réseau de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b56cb-165">The virtual machines you want to protect on the source VMM server should be connected to a VM network.</span></span> <span data-ttu-id="b56cb-166">Ce réseau doit être lié à un réseau logique lui-même associé au cloud.</span><span class="sxs-lookup"><span data-stu-id="b56cb-166">That network should be linked to a logical network that is associated with the cloud.</span></span>
* <span data-ttu-id="b56cb-167">Un réseau Azure auquel les machines virtuelles répliquées peuvent se connecter après le basculement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-167">An Azure network to which replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="b56cb-168">Vous sélectionnez ce réseau au moment du basculement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-168">You'll select this network at the time of fail-over.</span></span> <span data-ttu-id="b56cb-169">Le réseau doit être dans la même région que votre abonnement Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b56cb-169">The network should be in the same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="b56cb-170">Pour en savoir plus sur le mappage réseau, consultez :</span><span class="sxs-lookup"><span data-stu-id="b56cb-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="b56cb-171">Vue d’ensemble de la configuration de la mise en réseau logique dans VMM</span><span class="sxs-lookup"><span data-stu-id="b56cb-171">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="b56cb-172">Configuration de réseaux de machines virtuelles et de passerelles dans VMM</span><span class="sxs-lookup"><span data-stu-id="b56cb-172">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="b56cb-173">How to configure and monitor virtual networks in Azure (Configuration et analyse des réseaux virtuels dans Azure)</span><span class="sxs-lookup"><span data-stu-id="b56cb-173">How to configure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="b56cb-174">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="b56cb-174">PowerShell prerequisites</span></span>
<span data-ttu-id="b56cb-175">Assurez-vous qu’Azure PowerShell est prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="b56cb-175">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="b56cb-176">Si vous utilisez déjà PowerShell, vous devrez passer à la version 0.8.10 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-176">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="b56cb-177">Pour plus d’informations sur la configuration de PowerShell, consultez [Guide d’installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b56cb-177">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="b56cb-178">Une fois PowerShell configuré, vous pouvez afficher toutes les applets de commande disponibles pour le service [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b56cb-178">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="b56cb-179">Pour obtenir des conseils sur l’utilisation des applets de commande, par exemple, comment les valeurs de paramètres, les entrées et les sorties sont gérées dans Azure PowerShell, consultez le [Guide de prise en main des applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="b56cb-179">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="b56cb-180">Étape 1 : Définition de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="b56cb-180">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="b56cb-181">Dans Azure PowerShell, connectez-vous à votre compte Azure à l’aide des applets de commande suivantes</span><span class="sxs-lookup"><span data-stu-id="b56cb-181">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="b56cb-182">Obtenez la liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="b56cb-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="b56cb-183">Cette opération affiche également la liste des ID de chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-183">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="b56cb-184">Notez l’ID de l’abonnement dans lequel vous voulez créer le coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b56cb-184">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="b56cb-185">Définissez l’abonnement dans lequel le coffre Recovery Services doit être créé en mentionnant l’ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="b56cb-185">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="b56cb-186">Étape 2 : Création du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b56cb-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="b56cb-187">Création d’un groupe de ressources dans Azure Resource Manager, si ce n’est déjà fait</span><span class="sxs-lookup"><span data-stu-id="b56cb-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="b56cb-188">Créez un coffre Recovery Services et stockez l’objet de coffre ASR créé dans une variable (qui sera utilisée plus tard).</span><span class="sxs-lookup"><span data-stu-id="b56cb-188">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="b56cb-189">Vous pouvez également récupérer l’objet de coffre ASR après la création à l’aide de l’applet de commande Get-AzureRMRecoveryServicesVault :-</span><span class="sxs-lookup"><span data-stu-id="b56cb-189">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="b56cb-190">Étape 3 : Définition du contexte du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b56cb-190">Step 3: Set the Recovery Services Vault context</span></span>

<span data-ttu-id="b56cb-191">Définissez le contexte du coffre en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="b56cb-191">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="b56cb-192">Étape 4 : Installation du fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b56cb-192">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="b56cb-193">Sur la machine VMM, créez un répertoire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-193">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="b56cb-194">Extrayez les fichiers à l'aide du fournisseur téléchargé en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="b56cb-194">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="b56cb-195">Installez le fournisseur à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-195">Install the provider using the following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="b56cb-196">Attendez que l'installation se termine.</span><span class="sxs-lookup"><span data-stu-id="b56cb-196">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="b56cb-197">Inscrivez le serveur dans le coffre à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-197">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="b56cb-198">Étape 5 : Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="b56cb-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="b56cb-199">Si vous n’avez pas de compte de stockage Azure, créez un compte avec activation de la géo-réplication en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-199">If you don't have an Azure storage account, create a geo-replication enabled account in the same geo as the vault by running the following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="b56cb-200">Le compte de stockage doit se trouver dans la même région que le service Azure Site Recovery et être associé au même abonnement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-200">Note that the storage account must be in the same region as the Azure Site Recovery service, and be associated with the same subscription.</span></span>

## <a name="step-6-install-the-azure-recovery-services-agent"></a><span data-ttu-id="b56cb-201">Étape 6 : Installation de l'agent Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="b56cb-201">Step 6: Install the Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="b56cb-202">Téléchargez l’agent Azure Recovery Services à partir de [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) et installez-le sur chaque serveur hôte Hyper-V situé dans les clouds VMM que vous voulez protéger.</span><span class="sxs-lookup"><span data-stu-id="b56cb-202">Download the Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in the VMM clouds you want to protect.</span></span>
2. <span data-ttu-id="b56cb-203">Exécutez la commande suivante sur l’ensemble des hôtes VMM :</span><span class="sxs-lookup"><span data-stu-id="b56cb-203">Run the following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="b56cb-204">Étape 7 : Configuration des paramètres de protection de cloud</span><span class="sxs-lookup"><span data-stu-id="b56cb-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="b56cb-205">Créez un profil de protection dans Azure en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-205">Create a replication policy to Azure by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify the number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="b56cb-206">Récupérez un conteneur de protection en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b56cb-206">Get a protection container by running the following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="b56cb-207">Enregistrez les détails de la stratégie dans une variable à l’aide de la tâche qui a été créée et en mentionnant le nom convivial de la stratégie :</span><span class="sxs-lookup"><span data-stu-id="b56cb-207">Get the policy details to a variable using the job that was created and mentioning the friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="b56cb-208">Lancez l’association du conteneur de protection avec la stratégie de réplication :</span><span class="sxs-lookup"><span data-stu-id="b56cb-208">Start the association of the protection container with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="b56cb-209">Une fois la tâche terminée, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-209">After the job has finished, run the following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="b56cb-210">Une fois la tâche terminée, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-210">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="b56cb-211">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b56cb-211">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="b56cb-212">Étape 8 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="b56cb-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="b56cb-213">Avant de commencer le mappage réseau, vérifiez que les machines virtuelles sur le serveur VMM source sont connectées à un réseau de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b56cb-213">Before you begin network mapping verify that virtual machines on the source VMM server are connected to a VM network.</span></span> <span data-ttu-id="b56cb-214">En outre, vous devez créer un ou plusieurs réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="b56cb-215">Pour en savoir plus sur la création d’un réseau virtuel à l’aide d’Azure Resource Manager et de PowerShell, consultez [Création d’un réseau virtuel avec une connexion de site à site VPN à l’aide d’Azure Resource Manager et de PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b56cb-215">Learn more about how to create a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="b56cb-216">Notez que plusieurs réseaux de machines virtuelles peuvent être mappés à un seul réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-216">Note that multiple Virtual Machine networks can be mapped to a single Azure network.</span></span> <span data-ttu-id="b56cb-217">Si le réseau cible est associé à plusieurs sous-réseaux et que l’un d’eux porte le même nom que celui du sous-réseau dans lequel se trouve la machine virtuelle source, la machine virtuelle de réplication est connectée à ce sous-réseau cible après le basculement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-217">If the target network has multiple subnets and one of those subnets has the same name as subnet on which the source virtual machine is located, then the replica virtual machine will be connected to that target subnet after fail-over.</span></span> <span data-ttu-id="b56cb-218">S’il n’existe aucun sous-réseau cible avec un nom correspondant, la machine virtuelle est connectée au premier sous-réseau du réseau.</span><span class="sxs-lookup"><span data-stu-id="b56cb-218">If there is no target subnet with a matching name, the virtual machine will be connected to the first subnet in the network.</span></span>

1. <span data-ttu-id="b56cb-219">La première commande récupère les serveurs pour le coffre Azure Site Recovery actuel.</span><span class="sxs-lookup"><span data-stu-id="b56cb-219">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="b56cb-220">La commande stocke les serveurs Microsoft Azure Site Recovery dans la variable tableau $Servers.</span><span class="sxs-lookup"><span data-stu-id="b56cb-220">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="b56cb-221">La deuxième commande récupère le réseau Site Recovery pour le premier serveur du tableau $Servers.</span><span class="sxs-lookup"><span data-stu-id="b56cb-221">The second command gets the site recovery network for the first server in the $Servers array.</span></span> <span data-ttu-id="b56cb-222">La commande stocke les réseaux dans la variable $Networks.</span><span class="sxs-lookup"><span data-stu-id="b56cb-222">The command stores the networks in the $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="b56cb-223">La troisième commande obtient les réseaux virtuels Azure et stocke cette valeur dans la variable $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="b56cb-223">The third command gets Azure virtual networks, and then that value in the $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="b56cb-224">L'applet de commande finale crée un mappage entre le réseau principal et le réseau de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-224">The final cmdlet creates a mapping between the primary network and the Azure virtual machine network.</span></span> <span data-ttu-id="b56cb-225">L'applet de commande fixe le réseau principal comme premier élément de $Networks.</span><span class="sxs-lookup"><span data-stu-id="b56cb-225">The cmdlet specifies the primary network as the first element of $Networks.</span></span> <span data-ttu-id="b56cb-226">L’applet de commande spécifie un réseau de machines virtuelles comme premier élément de $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="b56cb-226">The cmdlet specifies a virtual machine network as the first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="b56cb-227">Étape 9 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="b56cb-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="b56cb-228">Une fois que les serveurs, les clouds et les réseaux ont été configurés correctement, vous pouvez activer la protection pour les machines virtuelles du cloud.</span><span class="sxs-lookup"><span data-stu-id="b56cb-228">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

 <span data-ttu-id="b56cb-229">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b56cb-229">Note the following:</span></span>

* <span data-ttu-id="b56cb-230">Les machines virtuelles doivent répondre aux exigences liées à Azure.</span><span class="sxs-lookup"><span data-stu-id="b56cb-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="b56cb-231">Pour en savoir plus sur ces dernières, consultez [Configuration requise et prise en charge](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) dans le guide de planification.</span><span class="sxs-lookup"><span data-stu-id="b56cb-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in the planning guide.</span></span>
* <span data-ttu-id="b56cb-232">Pour activer la protection, vous devez définir les propriétés du système d’exploitation et du disque du système d’exploitation pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b56cb-232">To enable protection, the operating system and operating system disk properties must be set for the virtual machine.</span></span> <span data-ttu-id="b56cb-233">Lorsque vous créez une machine virtuelle dans VMM à l'aide d'un modèle de machine virtuelle, vous pouvez définir la propriété.</span><span class="sxs-lookup"><span data-stu-id="b56cb-233">When you create a virtual machine in VMM using a virtual machine template you can set the property.</span></span> <span data-ttu-id="b56cb-234">Vous pouvez également définir ces propriétés pour des machines virtuelles existantes sous les onglets **Général** et **Configuration matérielle** des propriétés de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b56cb-234">You can also set these properties for existing virtual machines on the **General** and **Hardware Configuration** tabs of the virtual machine properties.</span></span> <span data-ttu-id="b56cb-235">Si vous ne définissez pas ces propriétés dans VMM, vous pourrez les configurer dans le portail Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b56cb-235">If you don't set these properties in VMM you'll be able to configure them in the Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="b56cb-236">Afin d’activer la protection, exécutez la commande suivante pour récupérer le conteneur de protection :</span><span class="sxs-lookup"><span data-stu-id="b56cb-236">To enable protection, run the following command to get the protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="b56cb-237">Récupérez l’entité de protection (machine virtuelle) en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b56cb-237">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="b56cb-238">Activez la récupération d’urgence de la machine virtuelle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-238">Enable the DR for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="b56cb-239">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="b56cb-239">Test your deployment</span></span>
<span data-ttu-id="b56cb-240">Pour tester votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération comportant plusieurs machines virtuelles et y exécuter un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-240">To test your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for the plan.</span></span> <span data-ttu-id="b56cb-241">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="b56cb-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="b56cb-242">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="b56cb-242">Note that:</span></span>

* <span data-ttu-id="b56cb-243">Si vous voulez vous connecter à la machine virtuelle dans Azure avec le Bureau à distance après le basculement, activez Connexion Bureau à distance sur la machine virtuelle avant d’exécuter le test de basculement.</span><span class="sxs-lookup"><span data-stu-id="b56cb-243">If you want to connect to the virtual machine in Azure using Remote Desktop after the fail-over, enable Remote Desktop Connection on the virtual machine before you run the test failover.</span></span>
* <span data-ttu-id="b56cb-244">Après le basculement, vous utilisez une adresse IP publique pour vous connecter à la machine virtuelle dans Azure avec le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="b56cb-244">After fail-over, you'll use a public IP address to connect to the virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="b56cb-245">Dans ce cas, assurez-vous qu'aucune de vos stratégies de domaine ne vous empêche de vous connecter à une machine virtuelle avec une adresse publique.</span><span class="sxs-lookup"><span data-stu-id="b56cb-245">If you want to do this, ensure you don't have any domain policies that prevent you from connecting to a virtual machine using a public address.</span></span>

<span data-ttu-id="b56cb-246">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="b56cb-246">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="b56cb-247">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="b56cb-247">Run a test failover</span></span>
- <span data-ttu-id="b56cb-248">Lancez le test de basculement en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-248">Start the test failover by running the following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="b56cb-249">Exécuter un basculement planifié</span><span class="sxs-lookup"><span data-stu-id="b56cb-249">Run a planned failover</span></span>
- <span data-ttu-id="b56cb-250">Lancez le basculement planifié en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-250">Start the planned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="b56cb-251">Exécuter un basculement non planifié</span><span class="sxs-lookup"><span data-stu-id="b56cb-251">Run an unplanned failover</span></span>
- <span data-ttu-id="b56cb-252">Lancez le basculement non planifié en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b56cb-252">Start the unplanned failover by running the following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="b56cb-253"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="b56cb-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="b56cb-254">Utilisez les commandes suivantes pour suivre l’activité.</span><span class="sxs-lookup"><span data-stu-id="b56cb-254">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="b56cb-255">Vous devez attendre la fin du traitement entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="b56cb-255">Note that you have to wait in between jobs for the processing to finish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="b56cb-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b56cb-256">Next steps</span></span>
<span data-ttu-id="b56cb-257">[En savoir plus](/powershell/module/azurerm.recoveryservices.backup/#recovery) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b56cb-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
