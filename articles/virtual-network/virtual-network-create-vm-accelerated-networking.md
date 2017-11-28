---
title: "Créer une machine virtuelle Azure avec mise en réseau accélérée| Documents Microsoft"
description: "Apprenez à créer une machine virtuelle avec mise en réseau accélérée."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 449425189a3b42dcb2c31316c1c8e38fac69d761
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="19b44-103">Créer une machine virtuelle avec mise en réseau accélérée</span><span class="sxs-lookup"><span data-stu-id="19b44-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="19b44-104">Ce didacticiel explique comment créer une machine virtuelle Azure (VM) avec mise en réseau accélérée.</span><span class="sxs-lookup"><span data-stu-id="19b44-104">In this tutorial, you learn how to create an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="19b44-105">La mise en réseau accélérée a été mise à disposition générale pour Windows et est proposée en préversion publique pour certaines distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="19b44-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="19b44-106">Une mise en réseau accélérée permet d’opérer une virtualisation d’E/S d’une racine unique (SR-IOV) sur une machine virtuelle, ce qui améliore considérablement les performances de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="19b44-106">Accelerated networking enables single root I/O virtualization (SR-IOV) to a VM, greatly improving its networking performance.</span></span> <span data-ttu-id="19b44-107">Cette voie hautement performante court-circuite l’hôte du chemin d’accès aux données, réduisant ainsi la latence, l’instabilité et l’utilisation du processeur pour servir les charges de travail réseau les plus exigeantes sur les types de machines virtuelles pris en charge.</span><span class="sxs-lookup"><span data-stu-id="19b44-107">This high-performance path bypasses the host from the datapath reducing latency, jitter, and CPU utilization, for use with the most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="19b44-108">L’illustration suivante montre la communication entre deux machines virtuelles avec ou sans mise en réseau accélérée :</span><span class="sxs-lookup"><span data-stu-id="19b44-108">The following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Opérateurs de comparaison](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="19b44-110">Sans mise en réseau accélérée, tout le trafic réseau en direction et en provenance de la machine virtuelle doit transiter par l’hôte et le commutateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="19b44-110">Without accelerated networking, all networking traffic in and out of the VM must traverse the host and the virtual switch.</span></span> <span data-ttu-id="19b44-111">Le commutateur virtuel fournit au trafic réseau toutes les stratégies, telles que les groupes de sécurité réseau, les listes de contrôle d’accès, l’isolation et d’autres services de réseau virtualisé.</span><span class="sxs-lookup"><span data-stu-id="19b44-111">The virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services to network traffic.</span></span> <span data-ttu-id="19b44-112">Pour plus d’informations sur les commutateurs virtuels, voir [Vue d’ensemble de la virtualisation de réseau Hyper-V](https://technet.microsoft.com/library/jj945275.aspx).</span><span class="sxs-lookup"><span data-stu-id="19b44-112">To learn more about virtual switches, read the [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="19b44-113">Dans le cas d’une mise en réseau accélérée, le trafic réseau parvient à la carte réseau de la machine virtuelle avant d’être transféré vers celle-ci.</span><span class="sxs-lookup"><span data-stu-id="19b44-113">With accelerated networking, network traffic arrives at the VM's network interface (NIC), and is then forwarded to the VM.</span></span> <span data-ttu-id="19b44-114">Toutes les stratégies réseau que le commutateur virtuel applique sans mise en réseau accélérée sont déchargées et appliquées dans le matériel.</span><span class="sxs-lookup"><span data-stu-id="19b44-114">All network policies that the virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="19b44-115">L’application de la stratégie au niveau du matériel permet à la carte réseau de transférer le trafic directement à la machine virtuelle, en ignorant l’hôte et le commutateur virtuel, tout en conservant toutes les stratégies qu’il a appliquées dans l’hôte.</span><span class="sxs-lookup"><span data-stu-id="19b44-115">Applying policy in hardware enables the NIC to forward network traffic directly to the VM, bypassing the host and the virtual switch, while maintaining all the policy it applied in the host.</span></span>

<span data-ttu-id="19b44-116">Les avantages d’une mise en réseau accélérée s’appliquent uniquement à la machine virtuelle activée.</span><span class="sxs-lookup"><span data-stu-id="19b44-116">The benefits of accelerated networking only apply to the VM that it is enabled on.</span></span> <span data-ttu-id="19b44-117">Pour des résultats optimaux, il convient d’activer cette fonctionnalité sur au moins deux machines virtuelles connectées au même réseau virtuel Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="19b44-117">For the best results, it is ideal to enable this feature on at least two VMs connected to the same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="19b44-118">Lors de la communication entre réseaux virtuels ou d’une connexion locale, cette fonctionnalité a une incidence minimale sur la latence globale.</span><span class="sxs-lookup"><span data-stu-id="19b44-118">When communicating across VNets or connecting on-premises, this feature has minimal impact to overall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="19b44-119">La préversion publique de Linux n’offre peut-être pas les mêmes niveaux de disponibilité et de fiabilité que les fonctions de la version mise à la disposition générale.</span><span class="sxs-lookup"><span data-stu-id="19b44-119">This Linux Public Preview may not have the same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="19b44-120">Cette fonctionnalité n’est pas prise en charge, est susceptible de disposer de possibilités limitées et peut ne pas être disponible à certains emplacements Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-120">The feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="19b44-121">Pour les notifications les plus récentes sur la disponibilité et l’état de cette fonctionnalité, consultez la page relative aux mises à jour du réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-121">For the most up-to-date notifications on availability and status of this feature, check the Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="19b44-122">Avantages</span><span class="sxs-lookup"><span data-stu-id="19b44-122">Benefits</span></span>
* <span data-ttu-id="19b44-123">**Latence plus faible/Nombre supérieur de paquets par seconde (pps) :** la suppression du commutateur virtuel du chemin de données évite que les paquets liés au traitement des stratégies séjournent sur l’hôte, ce qui augmente le nombre de paquets pouvant être traités dans la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-123">**Lower Latency / Higher packets per second (pps):** Removing the virtual switch from the datapath removes the time packets spend in the host for policy processing and increases the number of packets that can be processed inside the VM.</span></span>
* <span data-ttu-id="19b44-124">**Instabilité réduite :** le traitement du commutateur virtuel dépend de la quantité de stratégie qui doit être appliquée et de la charge de travail du processeur qui effectue le traitement.</span><span class="sxs-lookup"><span data-stu-id="19b44-124">**Reduced jitter:** Virtual switch processing depends on the amount of policy that needs to be applied and the workload of the CPU that is doing the processing.</span></span> <span data-ttu-id="19b44-125">Le déchargement des stratégies sur le matériel supprime cette variabilité en fournissant des paquets directement à la machine virtuelle, en supprimant l’hôte dans la communication de la machine virtuelle et toutes les interruptions de logiciel et les changements de contexte.</span><span class="sxs-lookup"><span data-stu-id="19b44-125">Offloading the policy enforcement to the hardware removes that variability by delivering packets directly to the VM, removing the host to VM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="19b44-126">**Utilisation réduite du processeur :** ignorer le commutateur virtuel dans l’hôte réduit l’utilisation du processeur pour le traitement du trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="19b44-126">**Decreased CPU utilization:** Bypassing the virtual switch in the host leads to less CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="19b44-127"><a name="Limitations"></a>Limitations</span><span class="sxs-lookup"><span data-stu-id="19b44-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="19b44-128">Les limitations suivantes existent lors de l’utilisation de cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="19b44-128">The following limitations exist when using this capability:</span></span>

* <span data-ttu-id="19b44-129">**Création d’interface réseau :** la mise en réseau accélérée ne peut être activée que pour une nouvelle carte réseau.</span><span class="sxs-lookup"><span data-stu-id="19b44-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="19b44-130">Elle ne peut pas être activée pour une carte réseau existante.</span><span class="sxs-lookup"><span data-stu-id="19b44-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="19b44-131">**Création de machine virtuelle :** une carte réseau avec mise en réseau accélérée activée ne peut être attachée à une machine virtuelle que lors de la création de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="19b44-131">**VM creation:** A NIC with accelerated networking enabled can only be attached to a VM when the VM is created.</span></span> <span data-ttu-id="19b44-132">Une carte réseau ne peut pas être attachée à une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="19b44-132">The NIC cannot be attached to an existing VM.</span></span>
* <span data-ttu-id="19b44-133">**Régions :** des machines virtuelles Windows avec mise en réseau accélérée sont proposées dans la plupart des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="19b44-134">Des machines virtuelles Linux avec mise en réseau accélérée sont proposées dans plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="19b44-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="19b44-135">La liste des régions où cette fonctionnalité est disponible ne cesse de s’allonger.</span><span class="sxs-lookup"><span data-stu-id="19b44-135">The regions this capability is available in is expanding.</span></span> <span data-ttu-id="19b44-136">Consultez le blog consacré aux mises à jour du réseau virtuel Azure ci-dessous pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="19b44-136">Please see the Azure Virtual Networking Updates blog below for the latest information.</span></span>   
* <span data-ttu-id="19b44-137">**Systèmes d’exploitation pris en charge :** Windows : Microsoft Windows Server 2012 R2 Datacenter et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="19b44-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="19b44-138">Linux : Ubuntu Server 16.04 LTS avec noyau 4.4.0-77 ou supérieur, SLES 12 SP2, RHEL 7.3 et CentOS 7.3 (publié par « Rogue Wave Software »).</span><span class="sxs-lookup"><span data-stu-id="19b44-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="19b44-139">**Taille de machine virtuelle :** tailles d’instance à usage général et de calcul optimisé avec au moins huit cœurs.</span><span class="sxs-lookup"><span data-stu-id="19b44-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="19b44-140">Pour plus d’informations, voir les articles sur les tailles de machine virtuelle [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19b44-140">For more information, see the [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="19b44-141">Le nombre de tailles d’instance de machine virtuelle augmentera dans le futur.</span><span class="sxs-lookup"><span data-stu-id="19b44-141">The set of supported VM instance sizes will expand in the future.</span></span>
* <span data-ttu-id="19b44-142">**Déploiement via Azure Resource Manager (ARM) uniquement :** la mise en réseau accélérée n’est pas disponible pour le déploiement via ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="19b44-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="19b44-143">Les modifications de ces limites seront annoncées via la page [Mises à jour concernant la mise en réseau virtuel Azure](https://azure.microsoft.com/updates/accelerated-networking-in-preview).</span><span class="sxs-lookup"><span data-stu-id="19b44-143">Changes to these limitations are announced through the [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="19b44-144">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="19b44-144">Create a Windows VM</span></span>
<span data-ttu-id="19b44-145">Pour créer la machine virtuelle, vous pouvez utiliser le Portail Azure ou Azure [PowerShell](#windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="19b44-145">You can use the Azure portal or Azure [PowerShell](#windows-powershell) to create the VM.</span></span>

### <span data-ttu-id="19b44-146"><a name="windows-portal"></a>Portail</span><span class="sxs-lookup"><span data-stu-id="19b44-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="19b44-147">Dans un navigateur Internet, ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous avec votre [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-147">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="19b44-148">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="19b44-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="19b44-149">Dans le portail, cliquez sur **+ Nouveau** > **Calcul** > **Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="19b44-149">In the portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="19b44-150">Dans le panneau **Windows Server Datacenter 2016** qui s’affiche, laissez l’option *Resource Manager* activée sous **Sélectionnez un modèle de déploiement** et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="19b44-150">In the **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="19b44-151">Dans le panneau **De base** qui s’affiche, entrez les valeurs suivantes, conservez les autres options par défaut ou sélectionnez ou entrez vos propres valeurs, puis cliquez sur le bouton **OK**:</span><span class="sxs-lookup"><span data-stu-id="19b44-151">In the **Basics** blade that appears, enter the following values, leave the remaining default options or select or enter your own values, and click the **OK** button:</span></span>

    |<span data-ttu-id="19b44-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="19b44-152">Setting</span></span>|<span data-ttu-id="19b44-153">Valeur</span><span class="sxs-lookup"><span data-stu-id="19b44-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="19b44-154">Nom</span><span class="sxs-lookup"><span data-stu-id="19b44-154">Name</span></span>|<span data-ttu-id="19b44-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="19b44-155">MyVm</span></span>|
    |<span data-ttu-id="19b44-156">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="19b44-156">Resource group</span></span>|<span data-ttu-id="19b44-157">Laissez l’option **Créer un nouveau** activée et entrez *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="19b44-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="19b44-158">Lieu</span><span class="sxs-lookup"><span data-stu-id="19b44-158">Location</span></span>|<span data-ttu-id="19b44-159">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="19b44-159">West US 2</span></span>|

    <span data-ttu-id="19b44-160">Si vous débutez avec Azure, apprenez-en davantage sur les [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), les [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) et les [emplacements](https://azure.microsoft.com/regions) (également appelés régions).</span><span class="sxs-lookup"><span data-stu-id="19b44-160">If you're new to Azure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred to as regions).</span></span>
5. <span data-ttu-id="19b44-161">Dans le panneau **Choisir une taille** qui s’affiche, dans la zonr **Nombre minimum de cœurs**, entrez *8*, puis cliquez sur **Afficher tout**.</span><span class="sxs-lookup"><span data-stu-id="19b44-161">In the **Choose a size** blade that appears, enter *8* in the **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="19b44-162">Cliquez sur **DS4_V2 Standard** ou sur toute autre machine virtuelle prise en charge, puis sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="19b44-162">Click **DS4_V2 Standard**, or any supported VM, then click the **Select** button.</span></span>
7. <span data-ttu-id="19b44-163">Dans le panneau **Paramètres** qui s’affiche, ne modifiez aucun paramètres, sauf l’option **Activée** sous **Mise en réseau accélérée**, puis cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="19b44-163">In the **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click the **OK** button.</span></span> <span data-ttu-id="19b44-164">**Remarque :** si, dans les étapes précédentes, vous avez sélectionné des valeurs pour la taille de machine virtuelle, le système d’exploitation ou l’emplacement qui ne figurent pas dans la section [Limitations](#Limitations) de cet article, la boîte de dialogue **Mise en réseau accélérée** n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="19b44-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in the [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="19b44-165">Dans le panneau **Résumé** qui s’affiche, cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="19b44-165">In the **Summary** blade that appears, click the **OK** button.</span></span> <span data-ttu-id="19b44-166">Azure commence à créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-166">Azure starts creating the VM.</span></span> <span data-ttu-id="19b44-167">La création de la machine virtuelle prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="19b44-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="19b44-168">Pour installer le pilote de mise en réseau accélérée pour Windows, procédez de la manière décrite dans la section [Configurer Windows](#configure-windows) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-168">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="19b44-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="19b44-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="19b44-170">Installez la dernière version du module Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/).</span><span class="sxs-lookup"><span data-stu-id="19b44-170">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="19b44-171">Si vous débutez dans l’utilisation d’Azure PowerShell, voir [Vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19b44-171">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="19b44-172">Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows, en tapant **powershell**, puis en cliquant sur **PowerShell** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="19b44-172">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="19b44-173">Dans la fenêtre PowerShell, entrez la commande `login-azurermaccount` pour vous connecter avec votre [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-173">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="19b44-174">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="19b44-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="19b44-175">Dans votre navigateur, copiez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="19b44-175">In your browser, copy the following script:</span></span>
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="19b44-176">Dans la fenêtre PowerShell, cliquez avec le bouton droit pour coller le script et commencer à l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="19b44-176">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="19b44-177">Vous êtes invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b44-177">You are prompted for a username and password.</span></span> <span data-ttu-id="19b44-178">Utilisez ces informations d’identification pour vous ouvrir une session sur la machine virtuelle lors de la connexion à celle-ci à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="19b44-178">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="19b44-179">Si le script échoue et que vous avez modifié des valeurs dans celui-ci avant de l’exécuter, vérifiez que les valeurs que vous avez utilisées pour la taille de machine virtuelle, le système d’exploitation et l’emplacement figurent dans la section [Limitations](#Limitations) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-179">If the script fails, and you changed values in the script before executing it, confirm the values you used for VM size, operating system, and location are listed in the [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="19b44-180">Pour installer le pilote de mise en réseau accélérée pour Windows, procédez de la manière décrite dans la section [Configurer Windows](#configure-windows) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-180">To install the accelerated networking driver for Windows, complete the steps in the [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="19b44-181"><a name="configure-windows"></a>Configurer Windows</span><span class="sxs-lookup"><span data-stu-id="19b44-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="19b44-182">Après avoir créé la machine virtuelle dans Azure, vous devez installer le pilote de mise en réseau accélérée pour Windows.</span><span class="sxs-lookup"><span data-stu-id="19b44-182">Once you create the VM in Azure, you must install the accelerated networking driver for Windows.</span></span> <span data-ttu-id="19b44-183">Avant de passer aux étapes suivantes, vous devez avoir créé une machine virtuelle Windows avec une mise en réseau accélérée en suivant l’une des étapes [portail](#windows-portal) ou [PowerShell](#windows-powershell) décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-183">Before completing the following steps, you must have created a Windows VM with accelerated networking using either the [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="19b44-184">Dans un navigateur Internet, ouvrez le [portail](https://portal.azure.com) Azure et connectez-vous avec votre [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-184">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="19b44-185">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="19b44-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="19b44-186">Dans la boîte de dialogue contenant le texte *Rechercher des ressources* en haut du portail Azure, tapez *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="19b44-186">In the box that contains the text *Search resources* at the top of the Azure portal, type *MyVm*.</span></span> <span data-ttu-id="19b44-187">Lorsque **MyVm** apparaît dans les résultats de recherche, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="19b44-187">When **MyVm** appears in the search results, click it.</span></span>
3. <span data-ttu-id="19b44-188">Dans le panneau **MyVm** qui s’affiche, cliquez sur le bouton **Connexion** dans l’angle supérieur gauche du panneau.</span><span class="sxs-lookup"><span data-stu-id="19b44-188">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="19b44-189">**Remarque :** si **Création** est visible sous le bouton **Connexion**, cela signifie qu’Azure n’a pas encore fini de créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-189">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="19b44-190">Ne cliquez sur **Connexion** que lorsque la mention **Création** disparaît sous le bouton **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="19b44-190">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
4. <span data-ttu-id="19b44-191">Autorisez votre navigateur à télécharger le fichier **MyVm.rdp**.</span><span class="sxs-lookup"><span data-stu-id="19b44-191">Allow your browser to download the **MyVm.rdp** file.</span></span>  <span data-ttu-id="19b44-192">Une fois le fichier téléchargé, cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="19b44-192">Once downloaded, click the file to open it.</span></span> 
5. <span data-ttu-id="19b44-193">Dans la boîte de dialogue **Connexion Bureau à distance** qui s’affiche, indiquant que le serveur de publication de la connexion à distance ne peut pas être identifié, cliquez sur le bouton **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="19b44-193">Click the **Connect** button in the **Remote Desktop Connection** box that appears, notifying you that the publisher of the remote connection can't be identified.</span></span>
6. <span data-ttu-id="19b44-194">Dans la boîte de dialogue **Sécurité Windows** qui s’affiche, cliquez sur **Autres choix**, puis sur **Utiliser un autre compte**.</span><span class="sxs-lookup"><span data-stu-id="19b44-194">In the **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="19b44-195">Entrez le nom d’utilisateur et le mot de passe que vous avez entrés à l’étape 4, puis cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="19b44-195">Enter the username and password you entered in step 4, then click the **OK** button.</span></span>
7. <span data-ttu-id="19b44-196">Dans la boîte de dialogue Connexion Bureau à distance qui s’affiche, vous informant que l’identité de l’ordinateur distant ne peut pas être vérifiée, cliquez sur le bouton **Oui**.</span><span class="sxs-lookup"><span data-stu-id="19b44-196">Click the **Yes** button in the Remote Desktop Connection box that appears, notifying you that the identity of the remote computer cannot be verified.</span></span>
8. <span data-ttu-id="19b44-197">Cliquez avec le bouton droit sur le bouton Démarrer de Windows, puis cliquez sur **Gestionnaire de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="19b44-197">Right-click the Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="19b44-198">Développez le nœud **Cartes réseau**.</span><span class="sxs-lookup"><span data-stu-id="19b44-198">Expand the **Network adapters** node.</span></span> <span data-ttu-id="19b44-199">Vérifiez que la mention **Carte Ethernet Mellanox ConnectX-3 fonction virtuelle** s’affiche comme dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="19b44-199">Confirm that the **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in the following picture:</span></span>
   
    ![Gestionnaire de périphériques](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="19b44-201">La mise en réseau accélérée est maintenant activée pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="19b44-202">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="19b44-202">Create a Linux VM</span></span>
<span data-ttu-id="19b44-203">Vous pouvez utiliser le portail Azure ou Azure [PowerShell](#linux-powershell) pour créer une machine virtuelle Ubuntu ou SLES.</span><span class="sxs-lookup"><span data-stu-id="19b44-203">You can use the Azure portal or Azure [PowerShell](#linux-powershell) to create an Ubuntu or SLES VM.</span></span> <span data-ttu-id="19b44-204">Le flux de travail est différent pour les machines virtuelles RHEL et CentOS.</span><span class="sxs-lookup"><span data-stu-id="19b44-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="19b44-205">Consultez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="19b44-205">Please see the instructions below.</span></span>

### <span data-ttu-id="19b44-206"><a name="linux-portal"></a>Portail</span><span class="sxs-lookup"><span data-stu-id="19b44-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="19b44-207">Inscrivez-vous à la mise en réseau accélérée pour Linux en version préliminaire en procédant de la manière décrite dans les étapes 1 à 5 de la section [Créer une machine virtuelle Linux - PowerShell](#linux-powershell) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-207">Register for the accelerated networking for Linux preview by completing steps 1-5 of the [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="19b44-208">Vous ne pouvez pas vous inscrire à la version préliminaire via le portail.</span><span class="sxs-lookup"><span data-stu-id="19b44-208">You cannot register for the preview in the portal.</span></span>
2. <span data-ttu-id="19b44-209">Procédez de la manière décrite dans les étapes 1 à 8 dans la section [Créer une machine virtuelle Windows - Portail](#windows-portal) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-209">Complete steps 1-8 in the [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="19b44-210">À l’étape 2, cliquez sur **Ubuntu Server 16.04 LTS** au lieu de **Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="19b44-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="19b44-211">Dans le cadre de ce didacticiel, choisissez d’utiliser un mot de passe plutôt qu’une clé SSH. Cependant, pour des déploiements de production, vous pouvez utiliser celle-ci.</span><span class="sxs-lookup"><span data-stu-id="19b44-211">For this tutorial, choose to use a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="19b44-212">Si la mention **Mise en réseau accélérée** n’apparaît pas lorsque vous procédez de la manière décrite à l’étape 7 dans la section [Créer une machine virtuelle Windows - Portail](#windows-portal) de cet article, c’est probablement pour l’une des raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="19b44-212">If **Accelerated networking** does not appear when you complete step 7 of the [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of the following reasons:</span></span>
    - <span data-ttu-id="19b44-213">Vous n’êtes pas encore inscrit pour la version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="19b44-213">You are not yet registered for the preview.</span></span> <span data-ttu-id="19b44-214">Vérifiez que votre état d’enregistrement est **Inscrit**, comme décrit à l’étape 4 dans la section [Créer une machine virtuelle Linux - PowerShell](#linux-powershell) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-214">Confirm that your registration state is **Registered**, as explained in step 4 of the [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="19b44-215">**Remarque :** si vous avez participé à la mise en réseau accélérée pour la version préliminaire de machines virtuelles Windows (il n’est plus nécessaire de vous inscrire pour la mise en réseau accélérée pour les machines virtuelles), vous n’êtes pas automatiquement inscrit pour la mise en réseau accélérée pour machines virtuelles Linux en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="19b44-215">**Note:** If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="19b44-216">Pour y participer, vous devez vous inscrire à la mise en réseau accélérée pour machines virtuelles Linux en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="19b44-216">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
    - <span data-ttu-id="19b44-217">Vous n’avez pas sélectionné de taille de machine virtuelle, de système d’exploitation ou d’emplacement répertorié dans la section [Limitations](#limitations) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-217">You have not selected a VM size, operating system, or location listed in the [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="19b44-218">Pour installer le pilote de mise en réseau accélérée pour Linux, procédez de la manière décrite dans la section [Configurer Linux](#configure-linux) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-218">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="19b44-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="19b44-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="19b44-220">Si vous créez des machines virtuelles Linux avec mise en réseau accélérée, puis tentez de créer une machine virtuelle Windows avec mise en réseau accélérée dans le même abonnement, la création de la machine virtuelle Windows peut échouer.</span><span class="sxs-lookup"><span data-stu-id="19b44-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt to create a Windows VM with accelerated networking in the same subscription, the Windows VM creation may fail.</span></span> <span data-ttu-id="19b44-221">Dans cette version préliminaire, il est recommandé de tester les machines virtuelles Linux et Windows avec une mise en réseau accélérée dans des abonnements distincts.</span><span class="sxs-lookup"><span data-stu-id="19b44-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="19b44-222">Installez la dernière version du module Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/).</span><span class="sxs-lookup"><span data-stu-id="19b44-222">Install the latest version of the Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="19b44-223">Si vous débutez dans l’utilisation d’Azure PowerShell, voir [Vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19b44-223">If you're new to Azure PowerShell, read the [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="19b44-224">Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows, en tapant **powershell**, puis en cliquant sur **PowerShell** dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="19b44-224">Start a PowerShell session by clicking the Windows Start button, typing **powershell**, then clicking **PowerShell** from the search results.</span></span>
3. <span data-ttu-id="19b44-225">Dans la fenêtre PowerShell, entrez la commande `login-azurermaccount` pour vous connecter avec votre [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-225">In your PowerShell window, enter the `login-azurermaccount` command to sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="19b44-226">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="19b44-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="19b44-227">Inscrivez-vous à la mise en réseau accélérée pour Azure en version préliminaire en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="19b44-227">Register for the accelerated networking for Azure preview by completing the following steps:</span></span>
    - <span data-ttu-id="19b44-228">Envoyez un e-mail à [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) en indiquant votre ID d’abonnement Azure et l’utilisation prévue.</span><span class="sxs-lookup"><span data-stu-id="19b44-228">Send an email to [axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="19b44-229">Veuillez attendre un e-mail de confirmation de la part de Microsoft concernant l’activation de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="19b44-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="19b44-230">Entrez la commande suivante pour confirmer que vous êtes inscrit à la version préliminaire :</span><span class="sxs-lookup"><span data-stu-id="19b44-230">Enter the following command to confirm you are registered for the preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="19b44-231">Ne passez pas à l’étape 5 tant que la mention **Inscrit** n’apparaît pas dans la sortie après que vous avez entré la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="19b44-231">Do not continue with step 5 until **Registered** appears in the output after you enter the previous command.</span></span> <span data-ttu-id="19b44-232">Pour que vous puissiez continuer, la sortie doit ressembler ceci :</span><span class="sxs-lookup"><span data-stu-id="19b44-232">Your output must look like the following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="19b44-233">Si vous avez participé à la mise en réseau accélérée pour la version préliminaire de machines virtuelles Windows (il n’est plus nécessaire de vous inscrire pour la mise en réseau accélérée pour les machines virtuelles), vous n’êtes pas automatiquement inscrit pour la mise en réseau accélérée pour machines virtuelles Linux en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="19b44-233">If you participated in the Accelerated networking for Windows VMs preview (it's no longer necessary to register to use Accelerated networking for Windows VMs), you are not automatically registered for the Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="19b44-234">Pour y participer, vous devez vous inscrire à la mise en réseau accélérée pour machines virtuelles Linux en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="19b44-234">You must register for the Accelerated networking for Linux VMs preview to participate in it.</span></span>
      >
5. <span data-ttu-id="19b44-235">Dans votre navigateur, copiez le script suivant en remplaçant Ubuntu ou SLES selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="19b44-235">In your browser, copy the following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="19b44-236">Ici encore, Redhat et CentOS ont un flux de travail différent, décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="19b44-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define the new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create the virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="19b44-237">Dans la fenêtre PowerShell, cliquez avec le bouton droit pour coller le script et commencer à l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="19b44-237">In your PowerShell window, right-click to paste the script and start executing it.</span></span> <span data-ttu-id="19b44-238">Vous êtes invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b44-238">You are prompted for a username and password.</span></span> <span data-ttu-id="19b44-239">Utilisez ces informations d’identification pour vous ouvrir une session sur la machine virtuelle lors de la connexion à celle-ci à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="19b44-239">Use these credentials to log in to the VM when connecting to it in the next step.</span></span> <span data-ttu-id="19b44-240">Si le script échoue, vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="19b44-240">If the script fails, confirm that:</span></span>
    - <span data-ttu-id="19b44-241">Vous êtes inscrit pour la version préliminaire, comme expliqué à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="19b44-241">You are registered for the preview, as explained in step 4</span></span>
    - <span data-ttu-id="19b44-242">Si vous avez modifié la taille de machine virtuelle, le type de système d’exploitation ou les valeurs d’emplacement dans le script avant l’exécution de celui-ci, les valeurs sont bien celles mentionnées dans la section [Limitations](#Limitations) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-242">If you changed VM size, operating system type, or location values in the script before executing it, that the values are listed in the [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="19b44-243">Pour installer le pilote de mise en réseau accélérée pour Linux, procédez de la manière décrite dans la section [Configurer Linux](#configure-linux) de cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-243">To install the accelerated networking driver for Linux, complete the steps in the [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="19b44-244"><a name="configure-linux"></a>Configurer Linux</span><span class="sxs-lookup"><span data-stu-id="19b44-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="19b44-245">Une fois la machine virtuelle crée dans Azure, vous devez installer le pilote de mise en réseau accélérée pour Linux.</span><span class="sxs-lookup"><span data-stu-id="19b44-245">Once you create the VM in Azure, you must install the accelerated networking driver for Linux.</span></span> <span data-ttu-id="19b44-246">Avant de passer aux étapes suivantes, vous devez avoir créé une machine virtuelle Linux avec une mise en réseau accélérée en suivant l’une des étapes [portail](#linux-portal) ou [PowerShell](#linux-powershell) décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="19b44-246">Before completing the following steps, you must have created a Linux VM with accelerated networking using either the [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="19b44-247">Dans un navigateur Internet, ouvrez le [portail](https://portal.azure.com) Azure et connectez-vous avec votre [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) Azure.</span><span class="sxs-lookup"><span data-stu-id="19b44-247">From an Internet browser, open the Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="19b44-248">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="19b44-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="19b44-249">En haut du portail, à droite de la barre *Rechercher des ressources*, cliquez sur l’icône **>_** pour démarrer un Cloud Shell Bash (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="19b44-249">At the top of the portal, to the right of the *Search resources* bar, click the **>_** icon to start a Bash cloud shell (Preview).</span></span> <span data-ttu-id="19b44-250">Le volet Cloud Shell Bash apparaît au bas du portail et, après quelques secondes, présente une invite  **username@Azure:~$**.</span><span class="sxs-lookup"><span data-stu-id="19b44-250">The Bash cloud shell pane appears at the bottom of the portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="19b44-251">Bien que vous puissiez utiliser une clé SSH plutôt que le Cloud Shell pour vous connecter à la machine virtuelle à partir de votre ordinateur, les instructions de ce didacticiel supposent que vous utilisez le Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="19b44-251">Though you can SSH to the VM from your computer, rather than the cloud shell, the instructions in this tutorial assume you're using the cloud shell.</span></span>
3. <span data-ttu-id="19b44-252">En haut du portail, dans la boîte de dialogue contenant le texte *Rechercher des ressources*, tapez *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="19b44-252">At the top of the portal, in the box that contains the text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="19b44-253">Lorsque **MyVm** apparaît dans les résultats de recherche, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="19b44-253">When **MyVm** appears in the search results, click it.</span></span>
4. <span data-ttu-id="19b44-254">Dans le panneau **MyVm** qui s’affiche, cliquez sur le bouton **Connexion** dans l’angle supérieur gauche du panneau.</span><span class="sxs-lookup"><span data-stu-id="19b44-254">In the **MyVm** blade that appears, click the **Connect** button in the top left corner of the blade.</span></span> <span data-ttu-id="19b44-255">**Remarque :** si **Création** est visible sous le bouton **Connexion**, cela signifie qu’Azure n’a pas encore fini de créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-255">**Note:** If **Creating** is visible under the **Connect** button, Azure has not yet finished creating the VM.</span></span> <span data-ttu-id="19b44-256">Ne cliquez sur **Connexion** que lorsque la mention **Création** disparaît sous le bouton **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="19b44-256">Click **Connect** only after you no longer see **Creating** under the **Connect** button.</span></span>
5. <span data-ttu-id="19b44-257">Azure ouvre une boîte de dialogue invitant à entrer l’`ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="19b44-257">Azure opens a box telling you to enter the `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="19b44-258">Entrez la commande suivante dans le Cloud Shell (ou copier-la à partir de la boîte de dialogue qui s’est affichée à l’étape 4 et collez-la dans le Cloud Shell), puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="19b44-258">Enter this command in the cloud shell (or copy it from the box that appeared in step 4 and paste it in to the cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="19b44-259">Tapez **Oui** en réponse à la question vous demandant si vous souhaitez poursuivre l’opération de connexion, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="19b44-259">Enter **yes** to the question asking you if you want to continue connecting, then press Enter.</span></span>
7. <span data-ttu-id="19b44-260">Tapez le mot de passe que vous avez entré lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="19b44-260">Enter the password you entered when creating the VM.</span></span> <span data-ttu-id="19b44-261">Une fois connecté à la machine virtuelle, vous voyez s’afficher l’invite adminuser@MyVm:~$.</span><span class="sxs-lookup"><span data-stu-id="19b44-261">Once successfully logged in to the VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="19b44-262">Vous êtes à présent connecté à la machine virtuelle via la session de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="19b44-262">You are now logged in to the VM through the cloud shell session.</span></span> <span data-ttu-id="19b44-263">**Remarque :** les sessions de Cloud Shell expirent après 10 minutes d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="19b44-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="19b44-264">À ce stade, les instructions varient en fonction de la distribution que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="19b44-264">At this point, the instructions vary based on the distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="19b44-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="19b44-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="19b44-266">À l’invite, entrez `uname -r` et confirmez que la version pour :</span><span class="sxs-lookup"><span data-stu-id="19b44-266">At the prompt, enter `uname -r` and confirm the version for:</span></span>

    * <span data-ttu-id="19b44-267">Ubuntu « 4.4.0-77-generic », ou supérieur</span><span class="sxs-lookup"><span data-stu-id="19b44-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="19b44-268">SLES « 4.4.59-92.20-default » ou supérieur</span><span class="sxs-lookup"><span data-stu-id="19b44-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="19b44-269">Créez une liaison entre la carte réseau virtuelle de mise en réseau standard et la carte réseau virtuelle de mise en réseau accélérée en exécutant les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="19b44-269">Create a bond between the standard networking vNIC and the accelerated networking vNIC by running the commands that follow.</span></span> <span data-ttu-id="19b44-270">Le trafic réseau utilise la carte réseau virtuelle de mise en réseau accélérée la plus performante, tandis que la liaison garantit que le trafic réseau ne soit pas interrompu lors de certains changements de configuration.</span><span class="sxs-lookup"><span data-stu-id="19b44-270">Network traffic uses the higher performing accelerated networking vNIC, while the bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="19b44-271">Après avoir exécuté le script, la machine virtuelle redémarre après une pause de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="19b44-271">After running the script, the VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="19b44-272">Une fois que la machine virtuelle a redémarré, reconnectez-vous à celle-ci en procédant de la manière décrite aux étapes 5 à 7.</span><span class="sxs-lookup"><span data-stu-id="19b44-272">Once the VM is restarted, reconnect to it by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="19b44-273">Exécutez la commande `ifconfig`, en vérifiant que bond0 apparaît et que l’interface s’affiche comme étant en service.</span><span class="sxs-lookup"><span data-stu-id="19b44-273">Run the `ifconfig` command and confirm that bond0 has come up and the interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="19b44-274">Les applications utilisant une mise en réseau accélérée doivent communiquer via l’interface *bond0*, et non *eth0*.</span><span class="sxs-lookup"><span data-stu-id="19b44-274">Applications using accelerated networking must communicate over the *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="19b44-275">Le nom de l’interface peut changer avant que la mise en réseau accélérée soit en disponibilité générale.</span><span class="sxs-lookup"><span data-stu-id="19b44-275">The interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="19b44-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="19b44-276">RHEL/CentOS</span></span>

<span data-ttu-id="19b44-277">La création d’une machine virtuelle Red Hat Enterprise Linux ou CentOS 7.3 nécessite quelques étapes supplémentaires pour charger les derniers pilotes requis pour SR-IOV ainsi que le pilote Virtual Fonction (VF) pour la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="19b44-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps to load the latest drivers needed for SR-IOV and the Virtual Function (VF) driver for the network card.</span></span> <span data-ttu-id="19b44-278">La première phase des instructions prépare une image qui peut être utilisée pour créer une ou plusieurs machines virtuelles sur lesquelles les pilotes sont préchargés.</span><span class="sxs-lookup"><span data-stu-id="19b44-278">The first phase of the instructions prepares an image that can be used to make one or more virtual machines that have the drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="19b44-279">Phase 1 : préparer une image de base Red Hat Enterprise Linux ou CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="19b44-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="19b44-280">Approvisionner une machine virtuelle non-SRIOV CentOS 7.3 sur Azure</span><span class="sxs-lookup"><span data-stu-id="19b44-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="19b44-281">Installer LIS 4.2.2 :</span><span class="sxs-lookup"><span data-stu-id="19b44-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="19b44-282">Télécharger les fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="19b44-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="19b44-283">Annuler l’approvisionnement de cette machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="19b44-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="19b44-284">Depuis le portail Azure, arrêtez cette machine virtuelle, accédez aux « disques » de la machine virtuelle puis capturez l’URI du disque dur virtuel OSDisk.</span><span class="sxs-lookup"><span data-stu-id="19b44-284">From Azure portal, stop this VM; and go to VM’s "Disks", capture the OSDisk’s VHD URI.</span></span> <span data-ttu-id="19b44-285">Cet URI contient le nom du disque dur virtuel de l’image de base et son compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="19b44-285">This URI contains the base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="19b44-286">Phase 2 : approvisionner de nouvelles machines virtuelles sur Azure</span><span class="sxs-lookup"><span data-stu-id="19b44-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="19b44-287">Approvisionnez de nouvelles machines virtuelles basées sur New-AzureRMVMConfig à l’aide de l’image de base VHD capturée lors de la première phase, avec AcceleratedNetworking activé sur la carte réseau virtuelle :</span><span class="sxs-lookup"><span data-stu-id="19b44-287">Provision new VMs based with New-AzureRMVMConfig using the base image VHD captured in phase one, with AcceleratedNetworking enabled on the vNIC:</span></span>

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate the public IP address to it
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify the base image's VHD URI (from phase one step 5). 
    # Note: The storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need to replace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for the location from which the new image binary large object (BLOB) is copied to start the virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for the VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create the virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="19b44-288">Une fois les machines virtuelles démarrées, vérifiez le périphérique VF à l’aide de « lspci » et vérifiez l’entrée Mellanox.</span><span class="sxs-lookup"><span data-stu-id="19b44-288">After VMs boot up, check the VF device by "lspci" and check the Mellanox entry.</span></span> <span data-ttu-id="19b44-289">Par exemple, nous devrions voir cet élément dans la sortie lspci :</span><span class="sxs-lookup"><span data-stu-id="19b44-289">For example, we should see this item in the lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="19b44-290">Exécutez le script de liaison par :</span><span class="sxs-lookup"><span data-stu-id="19b44-290">Run the bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="19b44-291">Redémarrez les nouvelles machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="19b44-291">Reboot the new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="19b44-292">La machine virtuelle devrait commencer par bond0 configuré, avec activation du chemin de mise réseau accélérée.</span><span class="sxs-lookup"><span data-stu-id="19b44-292">The VM should start with bond0 configured and the Accelerated Networking path enabled.</span></span>  <span data-ttu-id="19b44-293">Exécutez `ifconfig` pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="19b44-293">Run `ifconfig` to confirm.</span></span>
