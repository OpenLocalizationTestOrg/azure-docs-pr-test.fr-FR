---
title: "machines virtuelles d’aaaReplicate Hyper-V dans les clouds VMM à l’aide d’Azure Site Recovery et PowerShell (Resource Manager) | Documents Microsoft"
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
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="c37b8-103">Réplication d’ordinateurs virtuels Hyper-V dans VMM tooAzure de nuages à l’aide de PowerShell et le Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c37b8-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="c37b8-105">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c37b8-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="c37b8-106">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="c37b8-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="c37b8-107">PowerShell - Classique</span><span class="sxs-lookup"><span data-stu-id="c37b8-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="c37b8-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c37b8-108">Overview</span></span>
<span data-ttu-id="c37b8-109">Azure Site Recovery contribue stratégie récupération tooyour commerciale la continuité des activités et d’urgence en coordonnant la réplication, le basculement et récupération des machines virtuelles dans un nombre de scénarios de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c37b8-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="c37b8-110">Pour obtenir la liste complète de déploiement de scénarios consultez hello [vue d’ensemble d’Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c37b8-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="c37b8-111">Cet article explique comment les tâches courantes toouse PowerShell tooautomate vous devez tooperform lorsque vous configurez Azure Site Recovery tooreplicate Hyper-V virtual machines dans le stockage de System Center VMM clouds tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="c37b8-112">article de Hello inclut les conditions préalables requises pour le scénario de hello et vous montre</span><span class="sxs-lookup"><span data-stu-id="c37b8-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="c37b8-113">Comment tooset d’un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="c37b8-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="c37b8-114">Installer hello fournisseur Azure Site Recovery sur le serveur VMM de hello source</span><span class="sxs-lookup"><span data-stu-id="c37b8-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="c37b8-115">Inscrire le serveur de hello dans le coffre de hello, ajoutez un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="c37b8-116">Installer l’agent de hello Azure Recovery Services sur les serveurs hôtes Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c37b8-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="c37b8-117">Configurer les paramètres de protection pour les clouds VMM, qui seront appliqués tooall protégé par les ordinateurs virtuels</span><span class="sxs-lookup"><span data-stu-id="c37b8-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="c37b8-118">Activation de la protection de ces machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c37b8-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="c37b8-119">Test hello toomake de basculement que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="c37b8-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="c37b8-120">Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c37b8-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="c37b8-121">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c37b8-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c37b8-122">Cet article décrit à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="c37b8-123">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c37b8-123">Before you start</span></span>
<span data-ttu-id="c37b8-124">Assurez-vous que les conditions préalables sont remplies :</span><span class="sxs-lookup"><span data-stu-id="c37b8-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="c37b8-125">Conditions préalables pour Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-125">Azure prerequisites</span></span>
* <span data-ttu-id="c37b8-126">Vous aurez besoin d’un compte [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="c37b8-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="c37b8-127">Si vous n’en avez pas, commencez avec un [compte gratuit](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="c37b8-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="c37b8-128">En outre, vous pouvez lire sur hello [tarification d’Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="c37b8-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="c37b8-129">Vous devez un abonnement du fournisseur de services cryptographiques si vous essayez du scénario abonnement CSP hello réplication tooa.</span><span class="sxs-lookup"><span data-stu-id="c37b8-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="c37b8-130">En savoir plus sur le programme du fournisseur de services cryptographiques hello dans [comment tooenroll dans le programme du fournisseur de services cryptographiques hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b8-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="c37b8-131">Vous aurez besoin d’un tooAzure données répliquées toostore de compte de stockage (Resource Manager) v2 Azure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="c37b8-132">compte de Hello doit géo-réplication activée.</span><span class="sxs-lookup"><span data-stu-id="c37b8-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="c37b8-133">Il doit être en hello même région que hello service Azure Site Recovery et être associé à hello même abonnement ou hello CSP.</span><span class="sxs-lookup"><span data-stu-id="c37b8-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="c37b8-134">toolearn en savoir plus sur la configuration de stockage Azure, consultez hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) pour référence.</span><span class="sxs-lookup"><span data-stu-id="c37b8-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="c37b8-135">Vous devez toomake que que machines virtuelles tooprotect conformes hello [conditions préalables de machine virtuelle Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="c37b8-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="c37b8-136">Actuellement, seules les opérations au niveau de la machine virtuelle sont possibles par le biais de Powershell.</span><span class="sxs-lookup"><span data-stu-id="c37b8-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="c37b8-137">La prise en charge des opérations au niveau du plan de récupération sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="c37b8-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="c37b8-138">Pour l’instant, vous êtes limité tooperforming basculements seulement à un niveau de granularité 'protected VM' et pas à un niveau d’un Plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="c37b8-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="c37b8-139">Configuration requise pour VMM</span><span class="sxs-lookup"><span data-stu-id="c37b8-139">VMM prerequisites</span></span>
* <span data-ttu-id="c37b8-140">Vous aurez besoin d'un serveur VMM exécuté sur System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="c37b8-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="c37b8-141">N’importe quel serveur VMM contenant des machines virtuelles que vous souhaitiez tooprotect doit être en cours d’exécution hello fournisseur Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c37b8-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="c37b8-142">Il est installé pendant hello déploiement d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c37b8-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="c37b8-143">Vous devez au moins un cloud sur hello serveur VMM que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="c37b8-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="c37b8-144">cloud de Hello doit contenir :</span><span class="sxs-lookup"><span data-stu-id="c37b8-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="c37b8-145">un ou plusieurs groupes hôtes VMM ;</span><span class="sxs-lookup"><span data-stu-id="c37b8-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="c37b8-146">un ou plusieurs serveurs hôtes Hyper-V ou clusters dans chaque groupe hôte.</span><span class="sxs-lookup"><span data-stu-id="c37b8-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="c37b8-147">Un ou plusieurs ordinateurs virtuels sur le serveur d’Hyper-V source hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="c37b8-148">Pour en savoir plus sur la configuration des clouds VMM :</span><span class="sxs-lookup"><span data-stu-id="c37b8-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="c37b8-149">En savoir plus sur des clouds privés VMM dans [Nouveautés dans le Cloud privé avec System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) et dans [clouds VMM 2012 et hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="c37b8-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="c37b8-150">En savoir plus sur [configuration hello VMM de l’infrastructure cloud](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="c37b8-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="c37b8-151">Une fois vos éléments d’infrastructure cloud en place, apprenez à créer des clouds privés dans [Création d’un cloud privé dans VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) et [Procédure pas à pas : Création de clouds privés avec System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="c37b8-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="c37b8-152">Conditions préalables liées à Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c37b8-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="c37b8-153">Hello serveurs hôtes Hyper-V doivent être en cours d’exécution au moins **Windows Server 2012** avec le rôle Hyper-V ou **Microsoft Hyper-V Server 2012** et avez hello les dernières mises à jour installées.</span><span class="sxs-lookup"><span data-stu-id="c37b8-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="c37b8-154">Si vous utilisez Hyper-V dans un cluster, notez que le service Broker du cluster n'est pas créé automatiquement si vous avez un cluster basé sur des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="c37b8-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="c37b8-155">Vous devez manuellement service broker de cluster tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="c37b8-156">Concernant l'option</span><span class="sxs-lookup"><span data-stu-id="c37b8-156">For</span></span>
* <span data-ttu-id="c37b8-157">Pour obtenir des instructions, consultez [comment tooConfigure Service Broker de réplication Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="c37b8-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="c37b8-158">N’importe quel serveur hôte Hyper-V ou le cluster dont vous voulez toomanage protection doit être inclus dans un cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="c37b8-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="c37b8-159">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="c37b8-159">Network mapping prerequisites</span></span>
<span data-ttu-id="c37b8-160">Lorsque vous protégez des machines virtuelles dans Azure, le mappage réseau hello mappe les réseaux d’ordinateurs virtuels hello sur serveur VMM de source hello et suivant de hello de tooenable de réseaux Azure cible :</span><span class="sxs-lookup"><span data-stu-id="c37b8-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="c37b8-161">Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans.</span><span class="sxs-lookup"><span data-stu-id="c37b8-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="c37b8-162">Si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter tooother locaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="c37b8-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="c37b8-163">Si vous ne configurez pas le mappage réseau, uniquement hello des machines virtuelles qui basculent Bonjour même plan de récupération sera en mesure de tooconnect tooeach autres après basculement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="c37b8-164">Si vous souhaitez que le mappage réseau toodeploy, vous devez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="c37b8-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="c37b8-165">Hello machines virtuelles tooprotect sur le serveur VMM de hello source doit être connecté tooa réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c37b8-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="c37b8-166">Ce réseau doit être lié tooa réseau logique associé au cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="c37b8-167">Un réseau de Azure toowhich répliquée d’ordinateurs virtuels peuvent se connecter après le basculement.</span><span class="sxs-lookup"><span data-stu-id="c37b8-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="c37b8-168">Vous devez sélectionner ce réseau au moment de hello de basculement.</span><span class="sxs-lookup"><span data-stu-id="c37b8-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="c37b8-169">réseau de Hello doivent se trouver dans hello même région que votre abonnement Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c37b8-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="c37b8-170">Pour en savoir plus sur le mappage réseau, consultez :</span><span class="sxs-lookup"><span data-stu-id="c37b8-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="c37b8-171">Comment tooconfigure les réseaux logiques dans VMM</span><span class="sxs-lookup"><span data-stu-id="c37b8-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="c37b8-172">Comment tooconfigure VM réseaux et passerelles dans VMM</span><span class="sxs-lookup"><span data-stu-id="c37b8-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="c37b8-173">Comment tooconfigure et analyse des réseaux virtuels dans Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="c37b8-174">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="c37b8-174">PowerShell prerequisites</span></span>
<span data-ttu-id="c37b8-175">Assurez-vous que vous avez toogo prêt d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c37b8-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="c37b8-176">Si vous utilisez déjà PowerShell, vous devez tooupgrade tooversion 0.8.10 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="c37b8-177">Pour plus d’informations sur la configuration de PowerShell, consultez hello [Guide tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="c37b8-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="c37b8-178">Après avoir configuré et configuré de PowerShell, vous pouvez afficher toutes les hello des applets de commande disponibles pour le service de hello [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c37b8-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="c37b8-179">toolearn sur les conseils qui peuvent vous aider à utiliser des applets de commande hello, telles que la façon dont les valeurs de paramètre, les entrées et sorties sont généralement gérées dans Azure PowerShell, consultez hello [Guide tooget démarré avec les applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="c37b8-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="c37b8-180">Étape 1 : Définir l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="c37b8-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="c37b8-181">À partir de Azure powershell, connexion tooyour compte Azure : à l’aide de hello suivant d’applets de commande</span><span class="sxs-lookup"><span data-stu-id="c37b8-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="c37b8-182">Obtenez la liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="c37b8-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="c37b8-183">Cela affiche également la liste hello abonnement pour chacun des abonnements de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="c37b8-184">Notez le subscriptionID hello d’abonnement hello dans lesquels vous souhaitez toocreate hello coffre recovery services</span><span class="sxs-lookup"><span data-stu-id="c37b8-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="c37b8-185">Définir l’abonnement hello dans le hello coffre recovery services est toobe créé en mentionnant l’ID d’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="c37b8-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="c37b8-186">Étape 2 : Création du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="c37b8-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="c37b8-187">Création d’un groupe de ressources dans Azure Resource Manager, si ce n’est déjà fait</span><span class="sxs-lookup"><span data-stu-id="c37b8-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="c37b8-188">Créer un coffre Recovery Services et enregistrer hello créé l’objet de coffre de récupération automatique du système dans une variable (sera utilisée ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="c37b8-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="c37b8-189">Vous pouvez également récupérer hello ASR coffre après la création d’objets à l’aide d’applet de commande Get-AzureRMRecoveryServicesVault de hello :-</span><span class="sxs-lookup"><span data-stu-id="c37b8-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="c37b8-190">Étape 3 : Définir le contexte du coffre Recovery Services hello</span><span class="sxs-lookup"><span data-stu-id="c37b8-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="c37b8-191">Définir le contexte de coffre de hello en exécutant hello commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c37b8-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="c37b8-192">Étape 4 : Installer hello fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c37b8-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="c37b8-193">Sur l’ordinateur VMM hello, créez un répertoire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="c37b8-194">Extrayez les fichiers hello à l’aide de fournisseur de hello téléchargé en exécutant hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="c37b8-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="c37b8-195">Installez le fournisseur hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="c37b8-195">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="c37b8-196">Attendez que hello installation toofinish.</span><span class="sxs-lookup"><span data-stu-id="c37b8-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="c37b8-197">Inscrire un serveur hello dans le coffre de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="c37b8-198">Étape 5 : Création d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c37b8-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="c37b8-199">Si vous n’avez pas un compte de stockage Azure, créez un compte de géo-réplication activée Bonjour même emplacement que le hello coffre en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="c37b8-200">Notez que le compte de stockage hello doit être en hello même région que le service d’Azure Site Recovery hello et être associé à hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="c37b8-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="c37b8-201">Étape 6 : Installer hello Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="c37b8-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="c37b8-202">Télécharger l’agent Azure Recovery Services hello [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) et installer sur chaque serveur hôte de Hyper-V situé dans hello VMM clouds que vous souhaitez tooprotect.</span><span class="sxs-lookup"><span data-stu-id="c37b8-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="c37b8-203">Exécutez hello commande suivante sur tous les hôtes VMM :</span><span class="sxs-lookup"><span data-stu-id="c37b8-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="c37b8-204">Étape 7 : Configuration des paramètres de protection de cloud</span><span class="sxs-lookup"><span data-stu-id="c37b8-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="c37b8-205">Créer un tooAzure de stratégie de réplication en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="c37b8-206">Pour obtenir un conteneur de protection, hello suivant les commandes en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="c37b8-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="c37b8-207">Obtenir la variable tooa détails hello de stratégie à l’aide de la tâche hello qui a été créé et mentionner le nom de la stratégie convivial hello :</span><span class="sxs-lookup"><span data-stu-id="c37b8-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="c37b8-208">Démarrer l’association hello du conteneur de protection hello avec la stratégie de réplication hello :</span><span class="sxs-lookup"><span data-stu-id="c37b8-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="c37b8-209">Une fois le travail de hello terminée, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="c37b8-210">Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="c37b8-211">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c37b8-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="c37b8-212">Étape 8 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="c37b8-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="c37b8-213">Avant de commencer le mappage réseau Vérifiez que les ordinateurs virtuels sur le serveur VMM de hello source sont connectés tooa réseau d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c37b8-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="c37b8-214">En outre, vous devez créer un ou plusieurs réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="c37b8-215">En savoir plus sur toocreate un virtuel réseau à l’aide d’Azure Resource Manager et PowerShell dans [créer un réseau virtuel avec une connexion VPN de site à site à l’aide du Gestionnaire de ressources Azure et PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c37b8-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="c37b8-216">Notez que plusieurs réseaux d’ordinateurs virtuels peuvent être mappés tooa réseau Azure unique.</span><span class="sxs-lookup"><span data-stu-id="c37b8-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="c37b8-217">Si le réseau cible de hello possède plusieurs sous-réseaux et d’un de ces sous-réseaux a hello trouve du même nom que le sous-réseau sur lequel hello source virtual machine, puis hello ordinateur virtuel sera connecté toothat cible sous-réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="c37b8-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="c37b8-218">S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello sera connecté toohello premier sous-réseau de réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="c37b8-219">Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="c37b8-220">commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="c37b8-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="c37b8-221">commande deuxième Hello obtient réseau de récupération de site hello pour le premier serveur de hello hello $Servers tableau.</span><span class="sxs-lookup"><span data-stu-id="c37b8-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="c37b8-222">commande Hello stocke des réseaux de hello dans la variable de hello $Networks.</span><span class="sxs-lookup"><span data-stu-id="c37b8-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="c37b8-223">Hello troisième commande récupère les réseaux virtuels Azure et ensuite cette valeur dans la variable de hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="c37b8-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="c37b8-224">applet de commande finale Hello crée un mappage entre le réseau principal de hello et réseau de machine virtuelle Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="c37b8-225">applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello de $Networks.</span><span class="sxs-lookup"><span data-stu-id="c37b8-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="c37b8-226">applet de commande Hello spécifie un réseau d’ordinateurs virtuels en tant que premier élément de hello de $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="c37b8-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="c37b8-227">Étape 9 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c37b8-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="c37b8-228">Une fois que les réseaux, les clouds et les serveurs de hello sont correctement configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="c37b8-229">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c37b8-229">Note hello following:</span></span>

* <span data-ttu-id="c37b8-230">Les machines virtuelles doivent répondre aux exigences liées à Azure.</span><span class="sxs-lookup"><span data-stu-id="c37b8-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="c37b8-231">Archiver ces [prise en charge et les conditions préalables](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) dans le guide de planification hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="c37b8-232">protection de tooenable, système d’exploitation de hello et propriétés de disque de système d’exploitation doivent être définies pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="c37b8-233">Lorsque vous créez un ordinateur virtuel dans VMM à l’aide d’un modèle d’ordinateur virtuel, vous pouvez définir la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="c37b8-234">Vous pouvez également définir ces propriétés pour les ordinateurs virtuels existants sur hello **général** et **Configuration matérielle** onglets des propriétés d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="c37b8-235">Si vous ne définissez pas ces propriétés dans VMM, vous serez en mesure de tooconfigure dans le portail Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="c37b8-236">protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :</span><span class="sxs-lookup"><span data-stu-id="c37b8-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="c37b8-237">Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="c37b8-238">Activer hello récupération d’urgence pour hello machine virtuelle en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="c37b8-239">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="c37b8-239">Test your deployment</span></span>
<span data-ttu-id="c37b8-240">tootest votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs machines virtuelles et exécuter un basculement test pour un plan de hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="c37b8-241">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="c37b8-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="c37b8-242">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="c37b8-242">Note that:</span></span>

* <span data-ttu-id="c37b8-243">Si vous souhaitez tooconnect toohello machine virtuelle Azure à l’aide du Bureau à distance après le basculement hello, activer la connexion Bureau à distance sur l’ordinateur virtuel de hello avant d’exécuter le test de basculement hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="c37b8-244">Après le basculement, vous allez utiliser un ordinateur virtuel toohello de publique IP adresse tooconnect dans Azure à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="c37b8-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="c37b8-245">Si vous voulez toodo, assurez-vous que vous n’avez pas les stratégies de domaine qui vous empêchent de connexion tooa machine virtuelle une adresse publique.</span><span class="sxs-lookup"><span data-stu-id="c37b8-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="c37b8-246">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="c37b8-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="c37b8-247">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="c37b8-247">Run a test failover</span></span>
- <span data-ttu-id="c37b8-248">Démarrez hello test de basculement en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="c37b8-249">Exécuter un basculement planifié</span><span class="sxs-lookup"><span data-stu-id="c37b8-249">Run a planned failover</span></span>
- <span data-ttu-id="c37b8-250">Hello de démarrer le basculement planifié en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="c37b8-251">Exécuter un basculement non planifié</span><span class="sxs-lookup"><span data-stu-id="c37b8-251">Run an unplanned failover</span></span>
- <span data-ttu-id="c37b8-252">Démarrer hello basculement non planifié en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c37b8-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="c37b8-253"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="c37b8-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="c37b8-254">Utilisez hello suivant l’activité de commandes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="c37b8-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="c37b8-255">Notez que vous avez toowait entre les travaux pour hello traitement toofinish.</span><span class="sxs-lookup"><span data-stu-id="c37b8-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="c37b8-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c37b8-256">Next steps</span></span>
<span data-ttu-id="c37b8-257">[En savoir plus](/powershell/module/azurerm.recoveryservices.backup/#recovery) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c37b8-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
