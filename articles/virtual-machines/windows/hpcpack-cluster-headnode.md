---
title: "aaaCreate un nœud principal HPC Pack dans une machine virtuelle Azure | Documents Microsoft"
description: "Découvrez comment toouse hello déploiement de gestionnaire de ressources Azure portal et hello modèle toocreate un nœud principal de Microsoft HPC Pack 2012 R2 dans une machine virtuelle Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a><span data-ttu-id="6c411-103">Créer un nœud principal de hello d’un cluster HPC Pack dans une machine virtuelle de Azure avec une image de Marketplace</span><span class="sxs-lookup"><span data-stu-id="6c411-103">Create hello head node of an HPC Pack cluster in an Azure VM with a Marketplace image</span></span>
<span data-ttu-id="6c411-104">Utilisez un [image de machine virtuelle Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketplace et hello toocreate portail Azure hello nœud principal d’un cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="6c411-104">Use a [Microsoft HPC Pack 2012 R2 virtual machine image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) from hello Azure Marketplace and hello Azure portal toocreate hello head node of an HPC cluster.</span></span> <span data-ttu-id="6c411-105">Cette image de machine virtuelle HPC Pack est basée sur Windows Server 2012 R2 Datacenter avec HPC Pack 2012 R2 Update 3 préinstallé.</span><span class="sxs-lookup"><span data-stu-id="6c411-105">This HPC Pack VM image is based on Windows Server 2012 R2 Datacenter with HPC Pack 2012 R2 Update 3 pre-installed.</span></span> <span data-ttu-id="6c411-106">Utilisez ce nœud principal pour un déploiement preuve de concept de HPC Pack dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6c411-106">Use this head node for a proof of concept deployment of HPC Pack in Azure.</span></span> <span data-ttu-id="6c411-107">Vous pouvez ensuite ajouter calcul nœuds toohello cluster toorun HPC les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="6c411-107">You can then add compute nodes toohello cluster toorun HPC workloads.</span></span>

> [!TIP]
> <span data-ttu-id="6c411-108">toodeploy un cluster HPC Pack 2012 R2 complète dans Azure qui inclut le nœud principal de hello et les nœuds de calcul, nous vous recommandons d’utiliser une méthode automatisée.</span><span class="sxs-lookup"><span data-stu-id="6c411-108">toodeploy a complete HPC Pack 2012 R2 cluster in Azure that includes hello head node and compute nodes, we recommend that you use an automated method.</span></span> <span data-ttu-id="6c411-109">Les options sont hello [script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) et les modèles de gestionnaire de ressources tels que hello [cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/).</span><span class="sxs-lookup"><span data-stu-id="6c411-109">Options include hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and Resource Manager templates such as hello [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/).</span></span> <span data-ttu-id="6c411-110">Des modèles Resource Manager sont également disponibles pour les [clusters Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates).</span><span class="sxs-lookup"><span data-stu-id="6c411-110">Resource Manager templates are also available for [Microsoft HPC Pack 2016 clusters](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates).</span></span> 
> 
> 

## <a name="planning-considerations"></a><span data-ttu-id="6c411-111">Considérations en matière de planification</span><span class="sxs-lookup"><span data-stu-id="6c411-111">Planning considerations</span></span>
<span data-ttu-id="6c411-112">Comme indiqué dans la figure suivante de hello, vous déployez le nœud principal de HPC Pack hello dans un domaine Active Directory dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="6c411-112">As shown in hello following figure, you deploy hello HPC Pack head node in an Active Directory domain in an Azure virtual network.</span></span>

![Nœud principal HPC Pack][headnode]

* <span data-ttu-id="6c411-114">**Domaine Active Directory**: hello HPC Pack 2012 R2 nœud principal doit être joints à un domaine Active Directory de tooan dans Azure avant de démarrer les services HPC hello sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c411-114">**Active Directory domain**: hello HPC Pack 2012 R2 head node must be joined tooan Active Directory domain in Azure before you start hello HPC services on hello VM.</span></span> <span data-ttu-id="6c411-115">Comme indiqué dans cet article, pour un déploiement de preuve de concept, vous pouvez promouvoir hello machine virtuelle que vous créez pour le nœud principal de hello comme contrôleur de domaine avant de démarrer les services HPC hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-115">As shown in this article, for a proof of concept deployment, you can promote hello VM you create for hello head node as a domain controller before starting hello HPC services.</span></span> <span data-ttu-id="6c411-116">Une autre option consiste à toodeploy un contrôleur de domaine distincts et de forêt dans Azure toowhich vous joignez hello machine virtuelle du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="6c411-116">Another option is toodeploy a separate domain controller and forest in Azure toowhich you join hello head node VM.</span></span>

* <span data-ttu-id="6c411-117">**Modèle de déploiement**: la plupart des déploiements de nouveau, Microsoft recommande d’utiliser le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-117">**Deployment model**: For most new deployments, Microsoft recommends that you use hello Resource Manager deployment model.</span></span> <span data-ttu-id="6c411-118">Cet article suppose que vous utilisez ce modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="6c411-118">This article assumes that you use this deployment model.</span></span>

* <span data-ttu-id="6c411-119">**Réseau virtuel Azure**: lorsque vous utilisez hello Gestionnaire de ressources du déploiement modèle toodeploy hello nœud principal, vous spécifiez ou créez un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="6c411-119">**Azure virtual network**: When you use hello Resource Manager deployment model toodeploy hello head node, you specify or create an Azure virtual network.</span></span> <span data-ttu-id="6c411-120">Vous utilisez les réseaux virtuels hello si vous avez besoin de tooan-domaine d’Active Directory existant toojoin hello du nœud principal.</span><span class="sxs-lookup"><span data-stu-id="6c411-120">You use hello virtual network if you need toojoin hello head node tooan existing Active Directory domain.</span></span> <span data-ttu-id="6c411-121">Vous besoin également ultérieure tooadd de nœud de calcul cluster toohello de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6c411-121">You also need it later tooadd compute node VMs toohello cluster.</span></span>

## <a name="steps-toocreate-hello-head-node"></a><span data-ttu-id="6c411-122">Nœud de tête hello toocreate étapes</span><span class="sxs-lookup"><span data-stu-id="6c411-122">Steps toocreate hello head node</span></span>
<span data-ttu-id="6c411-123">Voici les principales étapes à suivre toouse hello toocreate portail Azure une machine virtuelle de Azure pour le nœud principal HPC Pack de hello à l’aide du modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-123">Following are high-level steps toouse hello Azure portal toocreate an Azure VM for hello HPC Pack head node by using hello Resource Manager deployment model.</span></span> 

1. <span data-ttu-id="6c411-124">Si vous souhaitez toocreate une nouvelle forêt Active Directory dans Azure avec des machines virtuelles de contrôleur de domaine séparé, une option consiste à toouse un [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc).</span><span class="sxs-lookup"><span data-stu-id="6c411-124">If you want toocreate a new Active Directory forest in Azure with separate domain controller VMs, one option is toouse a [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc).</span></span> <span data-ttu-id="6c411-125">Pour une simple déploiement de preuve de concept, il a fine tooomit cette étape et configurer la machine virtuelle elle-même d’un nœud principal hello comme contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="6c411-125">For a simple proof of concept deployment, it's fine tooomit this step and configure hello head node VM itself as a domain controller.</span></span> <span data-ttu-id="6c411-126">Cette option est décrites plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6c411-126">This option is described later in this article.</span></span>
2. <span data-ttu-id="6c411-127">Sur hello [HPC Pack 2012 R2 sur Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) Bonjour Azure Marketplace, cliquez sur **créer un ordinateur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="6c411-127">On hello [HPC Pack 2012 R2 on Windows Server 2012 R2 page](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) in hello Azure Marketplace, click **Create Virtual Machine**.</span></span> 
3. <span data-ttu-id="6c411-128">Dans le portail hello, sur hello **HPC Pack 2012 R2 sur Windows Server 2012 R2** page, sélectionnez hello **le Gestionnaire de ressources** modèle de déploiement, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="6c411-128">In hello portal, on hello **HPC Pack 2012 R2 on Windows Server 2012 R2** page, select hello **Resource Manager** deployment model and then click **Create**.</span></span>
   
    ![Image HPC Pack][marketplace]
4. <span data-ttu-id="6c411-130">Utiliser les paramètres de hello tooconfigure portail hello et créer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c411-130">Use hello portal tooconfigure hello settings and create hello VM.</span></span> <span data-ttu-id="6c411-131">Si vous êtes de nouveau tooAzure, suivez le didacticiel de hello [créer une machine virtuelle Windows Bonjour Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c411-131">If you're new tooAzure, follow hello tutorial [Create a Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="6c411-132">Pour un déploiement de preuve de concept, vous pouvez généralement acceptez hello par défaut ou les paramètres recommandés.</span><span class="sxs-lookup"><span data-stu-id="6c411-132">For a proof of concept deployment, you can usually accept hello default or recommended settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6c411-133">Si vous souhaitez toojoin hello du nœud principal tooan existant de domaine Active Directory dans Azure, assurez-vous que vous spécifiez le réseau virtuel de hello pour ce domaine lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c411-133">If you want toojoin hello head node tooan existing Active Directory domain in Azure, make sure you specify hello virtual network for that domain when creating hello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="6c411-134">Une fois que vous créez hello machine virtuelle et hello machine virtuelle est en cours d’exécution, [connecter toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="6c411-134">After you create hello VM and hello VM is running, [connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) by Remote Desktop.</span></span> 
6. <span data-ttu-id="6c411-135">Joignez la forêt de domaines Active Directory hello VM tooan en choisissant une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="6c411-135">Join hello VM tooan Active Directory domain forest by choosing one of hello following options:</span></span>
   
   * <span data-ttu-id="6c411-136">Si vous avez créé hello machine virtuelle dans un réseau virtuel Azure avec une forêt de domaines existante, joindre la forêt de toohello hello machine virtuelle à l’aide d’outils standard du Gestionnaire de serveur ou Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6c411-136">If you created hello VM in an Azure virtual network with an existing domain forest, join hello VM toohello forest by using standard Server Manager or Windows PowerShell tools.</span></span> <span data-ttu-id="6c411-137">Ensuite, redémarrez.</span><span class="sxs-lookup"><span data-stu-id="6c411-137">Then restart.</span></span>
   * <span data-ttu-id="6c411-138">Si vous avez créé hello machine virtuelle dans un réseau virtuel (sans une forêt de domaines), puis promouvoir hello machine virtuelle comme contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="6c411-138">If you created hello VM in a new virtual network (without an existing domain forest), then promote hello VM as a domain controller.</span></span> <span data-ttu-id="6c411-139">Utilisez les étapes standard tooinstall et configurer le rôle des Services de domaine Active Directory hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-139">Use standard steps tooinstall and configure hello Active Directory Domain Services role on hello head node.</span></span> <span data-ttu-id="6c411-140">Pour obtenir la procédure détaillée, consultez [Installer une nouvelle forêt Active Directory Windows Server 2012](https://technet.microsoft.com/library/jj574166.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c411-140">For detailed steps, see [Install a New Windows Server 2012 Active Directory Forest](https://technet.microsoft.com/library/jj574166.aspx).</span></span>
7. <span data-ttu-id="6c411-141">Après avoir hello machine virtuelle est en cours d’exécution et est joint à un tooan forêt Active Directory, démarrez les services HPC Pack hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c411-141">After hello VM is running and is joined tooan Active Directory forest, start hello HPC Pack services as follows:</span></span>
   
    <span data-ttu-id="6c411-142">a.</span><span class="sxs-lookup"><span data-stu-id="6c411-142">a.</span></span> <span data-ttu-id="6c411-143">Se connecter toohello nœud principal à l’aide d’un compte de domaine qui est membre du groupe Administrateurs local de hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-143">Connect toohello head node VM using a domain account that is a member of hello local Administrators group.</span></span> <span data-ttu-id="6c411-144">Par exemple, utiliser le compte d’administrateur hello configuré lorsque vous avez créé la machine virtuelle du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-144">For example, use hello administrator account you set up when you created hello head node VM.</span></span>
   
    <span data-ttu-id="6c411-145">b.</span><span class="sxs-lookup"><span data-stu-id="6c411-145">b.</span></span> <span data-ttu-id="6c411-146">Pour une configuration de nœud principal par défaut, démarrez Windows PowerShell en tant qu’administrateur et tapez Bonjour suivant :</span><span class="sxs-lookup"><span data-stu-id="6c411-146">For a default head node configuration, start Windows PowerShell as an administrator and type hello following:</span></span>
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    <span data-ttu-id="6c411-147">Il peut prendre plusieurs minutes pour hello HPC Pack services toostart.</span><span class="sxs-lookup"><span data-stu-id="6c411-147">It can take several minutes for hello HPC Pack services toostart.</span></span>
   
    <span data-ttu-id="6c411-148">Pour d’autres options de configuration du nœud principal, tapez `get-help HPCHNPrepare.ps1`.</span><span class="sxs-lookup"><span data-stu-id="6c411-148">For additional head node configuration options, type `get-help HPCHNPrepare.ps1`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c411-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c411-149">Next steps</span></span>
* <span data-ttu-id="6c411-150">Vous pouvez désormais travailler avec le nœud principal de hello de votre cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6c411-150">You can now work with hello head node of your HPC Pack cluster.</span></span> <span data-ttu-id="6c411-151">Par exemple, démarrez HPC Cluster Manager et hello complète [liste des tâches de déploiement](https://technet.microsoft.com/library/jj884141.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c411-151">For example, start HPC Cluster Manager, and complete hello [Deployment To-do List](https://technet.microsoft.com/library/jj884141.aspx).</span></span>
* <span data-ttu-id="6c411-152">Si vous souhaitez tooincrease hello cluster calcul capacité à la demande, ajoutez [nœuds de croissance Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="6c411-152">If you want tooincrease hello cluster compute capacity on-demand, add [Azure burst nodes](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in a cloud service.</span></span> 
* <span data-ttu-id="6c411-153">Essayez d’exécuter un test de charge sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6c411-153">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="6c411-154">Pour obtenir un exemple, consultez hello HPC Pack [mise en route](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="6c411-154">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png