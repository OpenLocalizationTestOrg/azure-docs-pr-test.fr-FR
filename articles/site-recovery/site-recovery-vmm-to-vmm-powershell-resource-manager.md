---
title: aaaReplicate site secondaire de VMM tooa machines virtuelles Hyper-V avec PowerShell (Azure Resource Manager) | Documents Microsoft
description: "Décrit comment la réplication tooorchestrate toodeploy Azure Site Recovery, le basculement et récupération des ordinateurs virtuels Hyper-V dans VMM nuages tooa site VMM secondaire à l’aide de PowerShell (Resource Manager)."
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="bee1a-103">Réplication d’ordinateurs virtuels Hyper-V dans VMM clouds tooa secondaire de site VMM à l’aide de PowerShell (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="bee1a-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bee1a-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="bee1a-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="bee1a-105">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="bee1a-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="bee1a-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bee1a-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="bee1a-107">Récupération de Site de tooAzure Bienvenue !</span><span class="sxs-lookup"><span data-stu-id="bee1a-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="bee1a-108">Utilisez cet article si vous souhaitez tooreplicate virtuels Hyper-V gérés dans le site secondaire de System Center Virtual Machine Manager (VMM) clouds tooa sur site.</span><span class="sxs-lookup"><span data-stu-id="bee1a-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="bee1a-109">Cet article explique comment les tâches courantes toouse PowerShell tooautomate vous devez tooperform lorsque vous configurez des ordinateurs virtuels de Azure Site Recovery tooreplicate Hyper-V dans les clouds de System Center VMM clouds tooSystem Center VMM dans le site secondaire.</span><span class="sxs-lookup"><span data-stu-id="bee1a-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="bee1a-110">article de Hello inclut les conditions préalables requises pour le scénario de hello et vous montre</span><span class="sxs-lookup"><span data-stu-id="bee1a-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="bee1a-111">Comment tooset d’un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="bee1a-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="bee1a-112">Installer hello fournisseur Azure Site Recovery sur le serveur VMM de hello source et de serveur VMM de hello cible</span><span class="sxs-lookup"><span data-stu-id="bee1a-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="bee1a-113">Enregistrer l’ou les serveurs VMM hello dans le coffre de hello</span><span class="sxs-lookup"><span data-stu-id="bee1a-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="bee1a-114">Configurer la stratégie de réplication pour hello Cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="bee1a-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="bee1a-115">les paramètres de réplication Hello dans la stratégie de hello sera appliqué tooall protégé par les ordinateurs virtuels</span><span class="sxs-lookup"><span data-stu-id="bee1a-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="bee1a-116">Activer la protection des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="bee1a-117">Test de basculement des machines virtuelles hello individuellement ou dans le cadre d’une récupération de plan toomake que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="bee1a-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="bee1a-118">Effectuer planifié ou un basculement non planifié d’ordinateurs virtuels, individuellement ou dans le cadre d’un toomake de plan de récupération que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="bee1a-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="bee1a-119">Si vous rencontrez des problèmes de configuration de ce scénario, publiez vos questions sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bee1a-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="bee1a-120">Azure dispose de deux [modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) différents pour créer et utiliser des ressources : le déploiement Azure Resource Manager et le déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="bee1a-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="bee1a-121">Azure a également deux portails : hello portail classique Azure qui prend en charge le modèle de déploiement classique hello et hello portail Azure avec prise en charge pour les deux modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="bee1a-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="bee1a-122">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="bee1a-123">Conditions préalables locales</span><span class="sxs-lookup"><span data-stu-id="bee1a-123">On-premises prerequisites</span></span>
<span data-ttu-id="bee1a-124">Voici ce que vous aurez besoin dans hello principal et secondaire local sites toodeploy ce scénario :</span><span class="sxs-lookup"><span data-stu-id="bee1a-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="bee1a-125">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="bee1a-125">**Prerequisites**</span></span> | <span data-ttu-id="bee1a-126">**Détails**</span><span class="sxs-lookup"><span data-stu-id="bee1a-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="bee1a-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="bee1a-127">**VMM**</span></span> |<span data-ttu-id="bee1a-128">Nous vous recommandons de que déployer un serveur VMM dans le site principal de hello et un serveur VMM dans le site secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="bee1a-129">Vous pouvez également effectuer la [réplication entre des clouds sur un seul serveur VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="bee1a-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="bee1a-130">toodo cela, vous devez au moins deux clouds configurés sur le serveur VMM de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="bee1a-131">Serveurs VMM doivent exécuter au moins System Center 2012 SP1 avec les dernières mises à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="bee1a-132">Chaque serveur VMM doit avoir à un ou plusieurs clouds configurés et tous les clouds doivent avoir le profil de capacité de Hyper-V hello définie.</span><span class="sxs-lookup"><span data-stu-id="bee1a-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="bee1a-133">Les clouds doivent contenir un ou plusieurs groupes hôtes VMM.</span><span class="sxs-lookup"><span data-stu-id="bee1a-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="bee1a-134">En savoir plus sur la configuration des clouds VMM dans [l’infrastructure de cloud computing configuration hello VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), et [procédure pas à pas : création de clouds privés avec System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="bee1a-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="bee1a-135">Les serveurs VMM doivent avoir accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="bee1a-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="bee1a-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="bee1a-136">**Hyper-V**</span></span> |<span data-ttu-id="bee1a-137">Serveurs Hyper-V doivent être en cours d’exécution au moins Windows Server 2012 avec un rôle de hello Hyper-V et avez hello les dernières mises à jour installées.</span><span class="sxs-lookup"><span data-stu-id="bee1a-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="bee1a-138">Un serveur Hyper-V doit contenir au moins une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bee1a-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="bee1a-139">Les serveurs hôte Hyper-V doivent se trouver dans des groupes hôtes dans des clouds VMM principaux et secondaires hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="bee1a-140">Si vous exécutez Hyper-V dans un cluster Windows Server 2012 R2, vous devez installer la [mise à jour 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="bee1a-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="bee1a-141">Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster avec adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="bee1a-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="bee1a-142">Vous devez manuellement service broker de cluster tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="bee1a-143">[En savoir plus](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="bee1a-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="bee1a-144">**Fournisseur**</span><span class="sxs-lookup"><span data-stu-id="bee1a-144">**Provider**</span></span> |<span data-ttu-id="bee1a-145">Au cours du déploiement de Site Recovery vous installez hello fournisseur Azure Site Recovery sur les serveurs VMM.</span><span class="sxs-lookup"><span data-stu-id="bee1a-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="bee1a-146">Hello fournisseur communique avec Site Recovery via HTTPS 443 tooorchestrate réplication.</span><span class="sxs-lookup"><span data-stu-id="bee1a-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="bee1a-147">Réplication de données se produit entre des serveurs de Hyper-V des principaux et secondaires hello sur hello LAN ou une connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="bee1a-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="bee1a-148">Hello fournisseur qui s’exécute sur le serveur VMM de hello doit accéder aux URL de toothese : *. hypervrecoverymanager.windowsazure.com ; *. accesscontrol.windows.net ; *. backup.windowsazure.com ; *. blob.core.windows.net ; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="bee1a-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="bee1a-149">En outre autoriser la communication de pare-feu de hello VMM serveurs toohello [plages d’adresses IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et autoriser le protocole HTTPS (443) de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="bee1a-150">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="bee1a-150">Network mapping prerequisites</span></span>
<span data-ttu-id="bee1a-151">Mappages de mappage réseau entre réseaux VM de VMM sur les serveurs VMM des principaux et secondaires hello pour :</span><span class="sxs-lookup"><span data-stu-id="bee1a-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="bee1a-152">Optimiser le positionnement des machines virtuelles de réplication sur les hôtes Hyper-V secondaires après le basculement.</span><span class="sxs-lookup"><span data-stu-id="bee1a-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="bee1a-153">Connecter des réseaux d’ordinateurs virtuels tooappropriate réplica machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bee1a-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="bee1a-154">Si vous ne configurez pas réseau mappage réplica machines virtuelles ne seront connecté tooany réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="bee1a-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="bee1a-155">Si vous souhaitez tooset réseau mappage lors de la récupération de Site déploiement ici est que vous devez :</span><span class="sxs-lookup"><span data-stu-id="bee1a-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="bee1a-156">Assurez-vous que les ordinateurs virtuels sur la source de hello serveur hôte Hyper-V sont connecté tooa réseau de VMM VM.</span><span class="sxs-lookup"><span data-stu-id="bee1a-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="bee1a-157">Ce réseau doit être lié tooa réseau logique associé au cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="bee1a-158">Vérifiez qu’un réseau de machines virtuelles correspondant configuré cloud hello secondaire que vous allez utiliser pour la récupération.</span><span class="sxs-lookup"><span data-stu-id="bee1a-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="bee1a-159">Ce réseau d’ordinateurs virtuels doit être lié tooa réseau logique associé avec le cloud secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="bee1a-160">En savoir plus sur la configuration des réseaux VMM Bonjour articles suivants</span><span class="sxs-lookup"><span data-stu-id="bee1a-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="bee1a-161">Comment tooconfigure les réseaux logiques dans VMM</span><span class="sxs-lookup"><span data-stu-id="bee1a-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="bee1a-162">Comment tooconfigure VM réseaux et passerelles dans VMM</span><span class="sxs-lookup"><span data-stu-id="bee1a-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="bee1a-163">[Découvrez plus d’informations](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sur le fonctionnement du mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="bee1a-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="bee1a-164">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="bee1a-164">PowerShell prerequisites</span></span>
<span data-ttu-id="bee1a-165">Assurez-vous que vous avez toogo prêt d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bee1a-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="bee1a-166">Si vous utilisez déjà PowerShell, vous devez tooupgrade tooversion 0.8.10 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bee1a-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="bee1a-167">Pour plus d’informations sur la configuration de PowerShell, consultez hello [Guide tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="bee1a-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="bee1a-168">Après avoir configuré et configuré de PowerShell, vous pouvez afficher toutes les hello des applets de commande disponibles pour le service de hello [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bee1a-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="bee1a-169">toolearn sur les conseils qui peuvent vous aider à utiliser des applets de commande hello, telles que la façon dont les valeurs de paramètre, les entrées et sorties sont généralement gérées dans Azure PowerShell, consultez hello [Guide tooget démarré avec les applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="bee1a-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="bee1a-170">Étape 1 : Définir l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="bee1a-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="bee1a-171">À partir de Azure powershell, connexion tooyour compte Azure : à l’aide de hello suivant d’applets de commande</span><span class="sxs-lookup"><span data-stu-id="bee1a-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="bee1a-172">Obtenez la liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="bee1a-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="bee1a-173">Cela affiche également la liste hello abonnement pour chacun des abonnements de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="bee1a-174">Notez le subscriptionID hello d’abonnement hello dans lesquels vous souhaitez toocreate hello coffre recovery services</span><span class="sxs-lookup"><span data-stu-id="bee1a-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="bee1a-175">Définir l’abonnement hello dans le hello coffre recovery services est toobe créé en mentionnant l’ID d’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="bee1a-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="bee1a-176">Étape 2 : Création du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="bee1a-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="bee1a-177">Création d’un groupe de ressources Azure Resource Manager, si ce n’est déjà fait</span><span class="sxs-lookup"><span data-stu-id="bee1a-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="bee1a-178">Créer un coffre Recovery Services et enregistrer hello créé l’objet de coffre de récupération automatique du système dans une variable (sera utilisée ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="bee1a-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="bee1a-179">Vous pouvez également récupérer hello ASR coffre après la création d’objets à l’aide d’applet de commande Get-AzureRMRecoveryServicesVault de hello :-</span><span class="sxs-lookup"><span data-stu-id="bee1a-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="bee1a-180">Étape 3 : Définir le contexte du coffre Recovery Services hello</span><span class="sxs-lookup"><span data-stu-id="bee1a-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="bee1a-181">Si vous avez déjà créé un coffre de sauvegarde, exécutez hello ci-dessous coffre de commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="bee1a-182">Définir le contexte de coffre de hello en exécutant hello commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bee1a-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="bee1a-183">Étape 4 : Installer hello fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="bee1a-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="bee1a-184">Sur l’ordinateur VMM hello, créez un répertoire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="bee1a-185">Extrayez les fichiers hello à l’aide de fournisseur de hello téléchargé en exécutant hello commande suivante</span><span class="sxs-lookup"><span data-stu-id="bee1a-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="bee1a-186">Installez le fournisseur hello hello suivant les commandes à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="bee1a-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="bee1a-187">Attendez que hello installation toofinish.</span><span class="sxs-lookup"><span data-stu-id="bee1a-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="bee1a-188">Inscrire un serveur hello dans le coffre de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="bee1a-189">Étape 5 : Créer et associer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="bee1a-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="bee1a-190">Créer une stratégie de réplication Hyper-V 2012 R2 en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="bee1a-191">Hello cloud VMM peut contenir des hôtes Hyper-V qui exécutent différentes versions de Windows Server (comme indiqué dans les conditions préalables de hello Hyper-V), mais la stratégie de réplication hello est spécifique à la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bee1a-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="bee1a-192">Si vos hôtes exécutent des versions de système d’exploitation différentes, créez des stratégies de réplication spécifiques à chaque version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bee1a-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="bee1a-193">Par exemple : si vous avez cinq hôtes exécutant Windows Servers 2012 et trois hôtes exécutant Windows Server 2012 R2, créez deux stratégies de réplication : une pour chaque version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="bee1a-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="bee1a-194">Obtenir le conteneur de protection principale hello (Cloud VMM principal) et le conteneur de protection de récupération (recovery Cloud VMM) en exécutant hello suivant les commandes :</span><span class="sxs-lookup"><span data-stu-id="bee1a-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="bee1a-195">Récupérer la stratégie hello créé à l’étape 1 à l’aide de nom convivial de hello de stratégie de hello</span><span class="sxs-lookup"><span data-stu-id="bee1a-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="bee1a-196">Démarrer l’association hello du conteneur de protection hello (Cloud VMM) avec la stratégie de réplication hello :</span><span class="sxs-lookup"><span data-stu-id="bee1a-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="bee1a-197">Attendez que hello stratégie association tâche toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bee1a-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="bee1a-198">Vous pouvez vérifier si hello est terminée à l’aide de hello suivant extrait de code PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bee1a-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="bee1a-199">Une fois le travail de hello a terminé le traitement, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="bee1a-200">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bee1a-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="bee1a-201">Étape 6 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="bee1a-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="bee1a-202">Hello première commande Obtient les serveurs pour le coffre Azure Site Recovery en cours hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="bee1a-203">commande Hello stocke les serveurs Microsoft Azure Site Recovery hello dans la variable de tableau hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="bee1a-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="bee1a-204">Hello ci-dessous commandes obtenir réseau de récupération de site hello pour les serveurs VMM de source hello et hello cible VMM.</span><span class="sxs-lookup"><span data-stu-id="bee1a-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="bee1a-205">serveur VMM de Hello source peut être hello premier ou un tableau de serveurs hello deuxième hello en un seul.</span><span class="sxs-lookup"><span data-stu-id="bee1a-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="bee1a-206">Vérifier les noms hello hello de serveurs de VMM et obtenir des réseaux de hello correctement</span><span class="sxs-lookup"><span data-stu-id="bee1a-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="bee1a-207">applet de commande finale Hello crée un mappage entre le réseau principal de hello et récupération hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="bee1a-208">applet de commande Hello Spécifie le réseau principal de hello en tant que premier élément de hello du réseau de récupération $PrimaryNetworks et hello en tant que premier élément de hello de $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="bee1a-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="bee1a-209">Étape 7 : Configuration du mappage de stockage</span><span class="sxs-lookup"><span data-stu-id="bee1a-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="bee1a-210">Hello commande ci-dessous obtient la liste hello des classifications de stockage dans $storageclassifications variable.</span><span class="sxs-lookup"><span data-stu-id="bee1a-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="bee1a-211">Hello ci-dessous commandes obtenir la classification de source de hello dans $SourceClassificaion variable et classification cible dans $TargetClassification variable.</span><span class="sxs-lookup"><span data-stu-id="bee1a-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="bee1a-212">les classifications source et cible Hello peuvent être n’importe quel élément dans le tableau de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="bee1a-213">Consultez la sortie toohello Hello ci-dessous index hello toofigure des commandes de classifications source et cible dans le tableau de $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="bee1a-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="bee1a-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="bee1a-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="bee1a-215">Hello ci-dessous l’applet de commande crée un mappage entre la classification de source de hello et classification de cible hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="bee1a-216">Étape 8 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bee1a-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="bee1a-217">Une fois que les réseaux, les clouds et les serveurs de hello sont correctement configurés, vous pouvez activer la protection des machines virtuelles dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="bee1a-218">protection de tooenable, exécutez hello suivant du conteneur de protection de commande tooget hello :</span><span class="sxs-lookup"><span data-stu-id="bee1a-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="bee1a-219">Obtenir l’entité de protection hello (VM) en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="bee1a-220">Activer la réplication pour hello machine virtuelle en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="bee1a-221">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="bee1a-221">Test your deployment</span></span>
<span data-ttu-id="bee1a-222">planification de votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération composé de plusieurs ordinateurs virtuels et exécuter un test de basculement pour hello tootest.</span><span class="sxs-lookup"><span data-stu-id="bee1a-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="bee1a-223">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="bee1a-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="bee1a-224">Vous pouvez créer un plan de récupération pour votre application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bee1a-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="bee1a-225">achèvement de hello toocheck d’opération de hello, suivez les étapes de hello dans [surveiller l’activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="bee1a-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="bee1a-226">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="bee1a-226">Run a test failover</span></span>
1. <span data-ttu-id="bee1a-227">Exécutez hello ci-dessous applets de commande tooget hello VM réseau toowhich que vous voulez utiliser le basculement de tootest vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bee1a-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="bee1a-228">Effectuer un test de basculement d’un ordinateur virtuel de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="bee1a-229">Effectuer un test de basculement d’un plan de récupération de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="bee1a-230">Exécuter un basculement planifié</span><span class="sxs-lookup"><span data-stu-id="bee1a-230">Run a planned failover</span></span>
1. <span data-ttu-id="bee1a-231">Effectuer un basculement planifié d’un ordinateur virtuel de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="bee1a-232">Effectuer un basculement planifié d’un plan de récupération de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="bee1a-233">Exécuter un basculement non planifié</span><span class="sxs-lookup"><span data-stu-id="bee1a-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="bee1a-234">Effectuer un basculement non planifié d’un ordinateur virtuel de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="bee1a-235">2. effectuez un basculement non planifié d’un plan de récupération de manière hello suivante :</span><span class="sxs-lookup"><span data-stu-id="bee1a-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="bee1a-236"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="bee1a-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="bee1a-237">Utilisez hello suivant l’activité de commandes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="bee1a-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="bee1a-238">Notez que vous avez toowait entre les travaux pour hello traitement toofinish.</span><span class="sxs-lookup"><span data-stu-id="bee1a-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="bee1a-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bee1a-239">Next steps</span></span>
<span data-ttu-id="bee1a-240">[En savoir plus](/powershell/module/azurerm.recoveryservices.backup/#recovery) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bee1a-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
