---
title: "Répliquer des machines virtuelles Hyper-V dans VMM sur un site secondaire avec PowerShell (Azure Resource Manager) | Microsoft Docs"
description: "Explique comment déployer Azure Site Recovery pour orchestrer la réplication, le basculement et la récupération des machines virtuelles Hyper-V dans des clouds VMM vers un site VMM secondaire avec PowerShell (Resource Manager)"
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="1d280-103">Répliquer des machines virtuelles Hyper-V dans des clouds VMM sur un site VMM secondaire avec PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="1d280-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d280-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1d280-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="1d280-105">Portail Classic</span><span class="sxs-lookup"><span data-stu-id="1d280-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="1d280-106">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d280-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="1d280-107">Bienvenue dans Azure Site Recovery !</span><span class="sxs-lookup"><span data-stu-id="1d280-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="1d280-108">Cet article vous permet de répliquer des machines virtuelles Hyper-V locales gérées sur les clouds System Center Virtual Machine Manager (VMM) dans un site secondaire.</span><span class="sxs-lookup"><span data-stu-id="1d280-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="1d280-109">Cet article vous montre comment utiliser PowerShell pour automatiser les tâches courantes à effectuer lorsque vous configurez Azure Site Recovery pour répliquer des machines virtuelles Hyper-V dans des clouds System Center VMM vers des clouds VMMM System Center sur un site secondaire.</span><span class="sxs-lookup"><span data-stu-id="1d280-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="1d280-110">L’article inclut la configuration requise pour le scénario et décrit les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d280-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="1d280-111">Configuration d’un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="1d280-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="1d280-112">Installation du fournisseur Azure Site Recovery sur les serveurs VMM source et cible</span><span class="sxs-lookup"><span data-stu-id="1d280-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="1d280-113">Inscription des serveurs VMM auprès du coffre</span><span class="sxs-lookup"><span data-stu-id="1d280-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="1d280-114">Configurez la stratégie de réplication pour le cloud VMM.</span><span class="sxs-lookup"><span data-stu-id="1d280-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="1d280-115">Les paramètres de réplication de la stratégie s’appliqueront à toutes les machines virtuelles protégées</span><span class="sxs-lookup"><span data-stu-id="1d280-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="1d280-116">Activez la protection des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1d280-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="1d280-117">Testez le basculement des machines virtuelles, individuellement ou dans le cadre d’un plan de récupération, pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="1d280-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="1d280-118">Effectuez un basculement planifié ou non planifié de machines virtuelles, individuellement ou dans le cadre d’un plan de récupération, pour vous assurer que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="1d280-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="1d280-119">Si vous rencontrez des problèmes pour mettre en œuvre ce scénario, posez vos questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1d280-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="1d280-120">Azure dispose de deux [modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) différents pour créer et utiliser des ressources : le déploiement Azure Resource Manager et le déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="1d280-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1d280-121">De plus, Azure propose deux portails : le portail Azure Classic, qui prend en charge le modèle de déploiement classique, et le portail Azure, qui gère les deux modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1d280-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="1d280-122">Cet article traite du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d280-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="1d280-123">Conditions préalables locales</span><span class="sxs-lookup"><span data-stu-id="1d280-123">On-premises prerequisites</span></span>
<span data-ttu-id="1d280-124">Voici ce que dont aurez besoin sur les sites locaux principaux et secondaires pour déployer ce scénario :</span><span class="sxs-lookup"><span data-stu-id="1d280-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="1d280-125">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1d280-125">**Prerequisites**</span></span> | <span data-ttu-id="1d280-126">**Détails**</span><span class="sxs-lookup"><span data-stu-id="1d280-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="1d280-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="1d280-127">**VMM**</span></span> |<span data-ttu-id="1d280-128">Nous vous recommandons de déployer un serveur VMM dans le site principal et un autre dans le site secondaire.</span><span class="sxs-lookup"><span data-stu-id="1d280-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="1d280-129">Vous pouvez également effectuer la [réplication entre des clouds sur un seul serveur VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="1d280-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="1d280-130">Pour ce faire, vous avez besoin d’au moins deux clouds configurés sur le serveur VMM.</span><span class="sxs-lookup"><span data-stu-id="1d280-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="1d280-131">Les serveurs VMM doivent exécuter au moins System Center 2012 SP1 avec les dernières mises à jour.</span><span class="sxs-lookup"><span data-stu-id="1d280-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="1d280-132">Chaque serveur VMM doit disposer d’un ou plusieurs clouds configurés et tous les clouds doivent avoir le profil de capacité Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="1d280-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="1d280-133">Les clouds doivent contenir un ou plusieurs groupes hôtes VMM.</span><span class="sxs-lookup"><span data-stu-id="1d280-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="1d280-134">Pour plus d’informations sur la configuration des clouds VMM, consultez [Configuration de la structure des clouds VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric) et [Procédure pas à pas : création de clouds privés avec System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d280-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="1d280-135">Les serveurs VMM doivent avoir accès à Internet.</span><span class="sxs-lookup"><span data-stu-id="1d280-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="1d280-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="1d280-136">**Hyper-V**</span></span> |<span data-ttu-id="1d280-137">Les serveurs Hyper-V doivent exécuter au moins Windows Server 2012 avec le rôle Hyper-V et les dernières mises à jour doivent être installées.</span><span class="sxs-lookup"><span data-stu-id="1d280-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="1d280-138">Un serveur Hyper-V doit contenir au moins une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d280-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="1d280-139">Les serveurs hôtes Hyper-V doivent être situés dans des groupes hôtes dans les clouds VMM principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="1d280-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="1d280-140">Si vous exécutez Hyper-V dans un cluster Windows Server 2012 R2, vous devez installer la [mise à jour 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="1d280-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="1d280-141">Si vous exécutez Hyper-V dans un cluster sous Windows Server 2012, notez que le répartiteur de clusters n’est pas créé automatiquement si vous avez un cluster avec adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="1d280-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="1d280-142">Vous devez configurer manuellement le service Broker du cluster.</span><span class="sxs-lookup"><span data-stu-id="1d280-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="1d280-143">[En savoir plus](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d280-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="1d280-144">**Fournisseur**</span><span class="sxs-lookup"><span data-stu-id="1d280-144">**Provider**</span></span> |<span data-ttu-id="1d280-145">Pendant un déploiement de Site Recovery, le fournisseur Azure Site Recovery est installé sur les serveurs VMM.</span><span class="sxs-lookup"><span data-stu-id="1d280-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="1d280-146">Le fournisseur communique avec Site Recovery sur le port HTTPS 443 pour orchestrer la réplication.</span><span class="sxs-lookup"><span data-stu-id="1d280-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="1d280-147">La réplication des données a lieu entre les serveurs Hyper-V principaux et secondaires via le réseau local ou une connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="1d280-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="1d280-148">Le fournisseur qui s’exécute sur le serveur VMM a besoin d’accéder à ces URL : *.hypervrecoverymanager.windowsazure.com ; *.accesscontrol.windows.net ; *.backup.windowsazure.com ; *.blob.core.windows.net ; *.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="1d280-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="1d280-149">Autorisez également la communication de pare-feu des serveurs VMM vers les [plages IP de centre de données Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) et autorisez le protocole HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="1d280-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="1d280-150">Conditions préalables liées au mappage réseau</span><span class="sxs-lookup"><span data-stu-id="1d280-150">Network mapping prerequisites</span></span>
<span data-ttu-id="1d280-151">Le mappage réseau effectue un mappage entre les réseaux de machines virtuelles VMM sur les serveurs VMM principaux et secondaires pour :</span><span class="sxs-lookup"><span data-stu-id="1d280-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="1d280-152">Optimiser le positionnement des machines virtuelles de réplication sur les hôtes Hyper-V secondaires après le basculement.</span><span class="sxs-lookup"><span data-stu-id="1d280-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="1d280-153">Connecter les machines virtuelles de réplication aux réseaux de machines virtuelles appropriés.</span><span class="sxs-lookup"><span data-stu-id="1d280-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="1d280-154">Si vous ne configurez pas le mappage réseau, les machines virtuelles de réplication ne seront connectées à aucun réseau après le basculement.</span><span class="sxs-lookup"><span data-stu-id="1d280-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="1d280-155">Si vous voulez configurer le mappage réseau lors du déploiement Site Recovery, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1d280-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="1d280-156">Assurez-vous que l’ensemble des machines virtuelles du serveur hôte Hyper-V source sont connectées à un réseau de machines virtuelles VMM.</span><span class="sxs-lookup"><span data-stu-id="1d280-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="1d280-157">Ce réseau doit être lié à un réseau logique lui-même associé au cloud.</span><span class="sxs-lookup"><span data-stu-id="1d280-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="1d280-158">Vérifiez que le cloud secondaire que vous allez utiliser pour la récupération est configuré avec un réseau de machines virtuelles correspondant.</span><span class="sxs-lookup"><span data-stu-id="1d280-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="1d280-159">Ce réseau de machines virtuelles doit être lié à un réseau logique lui-même associé au cloud secondaire.</span><span class="sxs-lookup"><span data-stu-id="1d280-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="1d280-160">Pour en savoir plus sur la configuration des réseaux VMM, consultez les articles ci-dessous</span><span class="sxs-lookup"><span data-stu-id="1d280-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="1d280-161">Vue d’ensemble de la configuration de la mise en réseau logique dans VMM</span><span class="sxs-lookup"><span data-stu-id="1d280-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="1d280-162">Configuration de réseaux de machines virtuelles et de passerelles dans VMM</span><span class="sxs-lookup"><span data-stu-id="1d280-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="1d280-163">[En savoir plus](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) sur le fonctionnement du mappage réseau.</span><span class="sxs-lookup"><span data-stu-id="1d280-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="1d280-164">Conditions préalables pour PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d280-164">PowerShell prerequisites</span></span>
<span data-ttu-id="1d280-165">Assurez-vous qu’Azure PowerShell est prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="1d280-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="1d280-166">Si vous utilisez déjà PowerShell, vous devrez passer à la version 0.8.10 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1d280-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="1d280-167">Pour plus d’informations sur la configuration de PowerShell, consultez [Guide d’installation et de configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="1d280-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="1d280-168">Une fois PowerShell configuré, vous pouvez afficher toutes les applets de commande disponibles pour le service [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d280-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="1d280-169">Pour obtenir des conseils sur l’utilisation des applets de commande, par exemple, comment les valeurs de paramètres, les entrées et les sorties sont gérées dans Azure PowerShell, consultez le [Guide de prise en main des applets de commande Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="1d280-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="1d280-170">Étape 1 : Définition de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="1d280-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="1d280-171">Dans Azure PowerShell, connectez-vous à votre compte Azure à l’aide des applets de commande suivantes</span><span class="sxs-lookup"><span data-stu-id="1d280-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="1d280-172">Obtenez la liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="1d280-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="1d280-173">Cette opération affiche également la liste des ID de chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="1d280-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="1d280-174">Notez l’ID de l’abonnement dans lequel vous voulez créer le coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="1d280-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="1d280-175">Définissez l’abonnement dans lequel le coffre Recovery Services doit être créé en mentionnant l’ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="1d280-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="1d280-176">Étape 2 : Création du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="1d280-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="1d280-177">Création d’un groupe de ressources Azure Resource Manager, si ce n’est déjà fait</span><span class="sxs-lookup"><span data-stu-id="1d280-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="1d280-178">Créez un coffre Recovery Services et stockez l’objet de coffre ASR créé dans une variable (qui sera utilisée plus tard).</span><span class="sxs-lookup"><span data-stu-id="1d280-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="1d280-179">Vous pouvez également récupérer l’objet de coffre ASR après la création à l’aide de l’applet de commande Get-AzureRMRecoveryServicesVault :-</span><span class="sxs-lookup"><span data-stu-id="1d280-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="1d280-180">Étape 3 : Définition du contexte du coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="1d280-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="1d280-181">Si vous avez déjà créé un coffre, exécutez la commande ci-dessous pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="1d280-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="1d280-182">Définissez le contexte du coffre en exécutant la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="1d280-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="1d280-183">Étape 4 : Installation du fournisseur Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="1d280-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="1d280-184">Sur la machine VMM, créez un répertoire en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="1d280-185">Extrayez les fichiers à l'aide du fournisseur téléchargé en exécutant la commande suivante</span><span class="sxs-lookup"><span data-stu-id="1d280-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="1d280-186">Installez le fournisseur à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="1d280-187">Attendez que l'installation se termine.</span><span class="sxs-lookup"><span data-stu-id="1d280-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="1d280-188">Inscrivez le serveur dans le coffre à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="1d280-189">Étape 5 : Créer et associer une stratégie de réplication</span><span class="sxs-lookup"><span data-stu-id="1d280-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="1d280-190">Créez une stratégie de réplication Hyper-V 2012 R2 en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="1d280-191">Le cloud VMM peut contenir des hôtes Hyper-V exécutant différentes versions de Windows Server (comme indiqué dans les conditions requises pour Hyper-V), mais la stratégie de réplication est spécifique à la version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1d280-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="1d280-192">Si vos hôtes exécutent des versions de système d’exploitation différentes, créez des stratégies de réplication spécifiques à chaque version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1d280-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="1d280-193">Par exemple : si vous avez cinq hôtes exécutant Windows Servers 2012 et trois hôtes exécutant Windows Server 2012 R2, créez deux stratégies de réplication : une pour chaque version du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1d280-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="1d280-194">Obtenez le conteneur de protection principal (cloud VMM principal) et le conteneur de protection de récupération (cloud VMM de récupération) en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d280-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="1d280-195">Récupérer la stratégie que vous avez créé à l’étape 1 en utilisant le nom convivial de la stratégie</span><span class="sxs-lookup"><span data-stu-id="1d280-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="1d280-196">Lancez l’association du conteneur de protection (cloud VMM) avec la stratégie de réplication :</span><span class="sxs-lookup"><span data-stu-id="1d280-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="1d280-197">Attendez que la tâche d’association de la stratégie se termine.</span><span class="sxs-lookup"><span data-stu-id="1d280-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="1d280-198">Vous pouvez vérifier si la tâche est terminée à l’aide de l’extrait de code PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="1d280-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="1d280-199">Une fois la tâche terminée, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="1d280-200">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="1d280-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="1d280-201">Étape 6 : Configuration du mappage réseau</span><span class="sxs-lookup"><span data-stu-id="1d280-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="1d280-202">La première commande récupère les serveurs pour le coffre Azure Site Recovery actuel.</span><span class="sxs-lookup"><span data-stu-id="1d280-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="1d280-203">La commande stocke les serveurs Microsoft Azure Site Recovery dans la variable tableau $Servers.</span><span class="sxs-lookup"><span data-stu-id="1d280-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="1d280-204">Les commandes ci-dessous permettent d’obtenir le réseau de Site Recovery pour les serveurs VMM source et cible.</span><span class="sxs-lookup"><span data-stu-id="1d280-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="1d280-205">Le serveur VMM source peut être le premier ou le second serveur dans le groupe de serveurs.</span><span class="sxs-lookup"><span data-stu-id="1d280-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="1d280-206">Vérifier les noms des serveurs VMM et obtenir correctement les réseaux</span><span class="sxs-lookup"><span data-stu-id="1d280-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="1d280-207">L'applet de commande finale crée un mappage entre le réseau principal et le réseau de récupération.</span><span class="sxs-lookup"><span data-stu-id="1d280-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="1d280-208">L’applet de commande spécifie le réseau principal en tant que premier élément de $PrimaryNetworks, et le réseau de récupération en tant que premier élément de $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="1d280-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="1d280-209">Étape 7 : Configuration du mappage de stockage</span><span class="sxs-lookup"><span data-stu-id="1d280-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="1d280-210">La commande ci-dessous récupère la liste des classifications de stockage dans la variable $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="1d280-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="1d280-211">Les commandes suivantes récupèrent la classification source dans la variable $SourceClassification, et la classification cible dans la variable $SourceClassificaion.</span><span class="sxs-lookup"><span data-stu-id="1d280-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="1d280-212">Les classifications source et cible peuvent être n’importe quel élément du tableau.</span><span class="sxs-lookup"><span data-stu-id="1d280-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="1d280-213">Reportez-vous à la sortie de la commande suivante pour déterminer l’index des classifications source et cible dans le tableau $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="1d280-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="1d280-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="1d280-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="1d280-215">L’applet de commande ci-dessous crée un mappage entre la classification source et la classification cible.</span><span class="sxs-lookup"><span data-stu-id="1d280-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="1d280-216">Étape 8 : Activation de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1d280-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="1d280-217">Une fois que les serveurs, les clouds et les réseaux ont été configurés correctement, vous pouvez activer la protection pour les machines virtuelles du cloud.</span><span class="sxs-lookup"><span data-stu-id="1d280-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="1d280-218">Afin d’activer la protection, exécutez la commande suivante pour récupérer le conteneur de protection :</span><span class="sxs-lookup"><span data-stu-id="1d280-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="1d280-219">Récupérez l’entité de protection (machine virtuelle) en exécutant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1d280-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="1d280-220">Activez la réplication de la machine virtuelle en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1d280-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="1d280-221">Tester votre déploiement</span><span class="sxs-lookup"><span data-stu-id="1d280-221">Test your deployment</span></span>
<span data-ttu-id="1d280-222">Pour tester votre déploiement, vous pouvez exécuter un test de basculement pour une seule machine virtuelle, ou créer un plan de récupération comportant plusieurs machines virtuelles et exécuter sur lui un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="1d280-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="1d280-223">Il simule votre mécanisme de basculement et de récupération dans un réseau isolé.</span><span class="sxs-lookup"><span data-stu-id="1d280-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="1d280-224">Vous pouvez créer un plan de récupération pour votre application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1d280-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="1d280-225">Pour vérifier que l'opération est terminée, suivez les étapes décrites dans la section [Suivi de l'activité](#monitor).</span><span class="sxs-lookup"><span data-stu-id="1d280-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="1d280-226">Exécution d’un test de basculement</span><span class="sxs-lookup"><span data-stu-id="1d280-226">Run a test failover</span></span>
1. <span data-ttu-id="1d280-227">Exécutez les applets de commande ci-dessous pour obtenir le réseau de machines virtuelles sur lesquels vous souhaitez tester le basculement de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1d280-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="1d280-228">Effectuez un test de basculement d’une machine virtuelle en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="1d280-229">Effectuez un test de basculement d’un plan de récupération en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="1d280-230">Exécuter un basculement planifié</span><span class="sxs-lookup"><span data-stu-id="1d280-230">Run a planned failover</span></span>
1. <span data-ttu-id="1d280-231">Effectuez un basculement planifié d’une machine virtuelle en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="1d280-232">Effectuez un basculement planifié d’un plan de récupération en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="1d280-233">Exécuter un basculement non planifié</span><span class="sxs-lookup"><span data-stu-id="1d280-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="1d280-234">Effectuez un basculement non planifié d’une machine virtuelle en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="1d280-235">2. Effectuez un basculement non planifié d’un plan de récupération en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="1d280-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="1d280-236"><a name=monitor></a> Suivi de l'activité</span><span class="sxs-lookup"><span data-stu-id="1d280-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="1d280-237">Utilisez les commandes suivantes pour suivre l’activité.</span><span class="sxs-lookup"><span data-stu-id="1d280-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="1d280-238">Vous devez attendre la fin du traitement entre les tâches.</span><span class="sxs-lookup"><span data-stu-id="1d280-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="1d280-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d280-239">Next steps</span></span>
<span data-ttu-id="1d280-240">[En savoir plus](/powershell/module/azurerm.recoveryservices.backup/#recovery) sur Azure Site Recovery avec les applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d280-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
