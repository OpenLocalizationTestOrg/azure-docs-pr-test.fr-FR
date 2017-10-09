---
title: "aaaCreate une machine virtuelle Azure avec réseau d’accélérée | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec l’accélération de mise en réseau."
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
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a><span data-ttu-id="3ecfa-103">Créer une machine virtuelle avec mise en réseau accélérée</span><span class="sxs-lookup"><span data-stu-id="3ecfa-103">Create a virtual machine with Accelerated Networking</span></span>

<span data-ttu-id="3ecfa-104">Dans ce didacticiel, vous apprendrez comment toocreate une Machine virtuelle Azure (VM) avec l’accélération de réseau.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-104">In this tutorial, you learn how toocreate an Azure Virtual Machine (VM) with Accelerated Networking.</span></span> <span data-ttu-id="3ecfa-105">La mise en réseau accélérée a été mise à disposition générale pour Windows et est proposée en préversion publique pour certaines distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-105">Accelerated Networking is GA for Windows and in a Public Preview for specific Linux distributions.</span></span> <span data-ttu-id="3ecfa-106">Mise en réseau d’accélérée permet tooa de virtualisation (SR-IOV) d’e/s de racine unique machine virtuelle, ce qui améliore considérablement les performances de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-106">Accelerated networking enables single root I/O virtualization (SR-IOV) tooa VM, greatly improving its networking performance.</span></span> <span data-ttu-id="3ecfa-107">Ce chemin d’accès de hautes performances ignore hôte hello à partir du chemin de données hello en réduisant la latence, l’instabilité et l’utilisation du processeur, pour une utilisation avec les plus exigeantes charges de travail réseau hello sur les types de machine virtuelle pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-107">This high-performance path bypasses hello host from hello datapath reducing latency, jitter, and CPU utilization, for use with hello most demanding network workloads on supported VM types.</span></span> <span data-ttu-id="3ecfa-108">Hello suivant image montre communication entre les deux machines virtuelles (VM) avec et sans mise en réseau d’accélérée :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-108">hello following picture shows communication between two virtual machines (VM) with and without accelerated networking:</span></span>

![Opérateurs de comparaison](./media/virtual-network-create-vm-accelerated-networking/image1.png)

<span data-ttu-id="3ecfa-110">Sans mise en réseau d’accélérée, le trafic réseau vers et depuis hello machine virtuelle doit parcourir hôte de hello et du commutateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-110">Without accelerated networking, all networking traffic in and out of hello VM must traverse hello host and hello virtual switch.</span></span> <span data-ttu-id="3ecfa-111">commutateur virtuel de Hello fournit toutes les stratégies, telles que réseau des groupes de sécurité, accéder à des listes de contrôle, d’isolement et le trafic réseau virtualisé services toonetwork.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-111">hello virtual switch provides all policy enforcement, such as network security groups, access control lists, isolation, and other network virtualized services toonetwork traffic.</span></span> <span data-ttu-id="3ecfa-112">toolearn plus d’informations sur les commutateurs virtuels, lire hello [virtualisation de réseau Hyper-V et le commutateur virtuel](https://technet.microsoft.com/library/jj945275.aspx) l’article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-112">toolearn more about virtual switches, read hello [Hyper-V network virtualization and virtual switch](https://technet.microsoft.com/library/jj945275.aspx) article.</span></span>

<span data-ttu-id="3ecfa-113">Avec un réseau d’accélérée, le trafic réseau arrive sur l’interface réseau de la machine virtuelle hello (NIC) et est ensuite transféré toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-113">With accelerated networking, network traffic arrives at hello VM's network interface (NIC), and is then forwarded toohello VM.</span></span> <span data-ttu-id="3ecfa-114">Toutes les stratégies de réseau qui hello commutateur virtuel applique sans mise en réseau d’accélérée sont déchargées et appliquées sur le matériel.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-114">All network policies that hello virtual switch applies without accelerated networking are offloaded and applied in hardware.</span></span> <span data-ttu-id="3ecfa-115">Application de la stratégie dans le matériel permet hello NIC tooforward trafic réseau directement toohello machine virtuelle, en ignorant les hôte hello et du commutateur virtuel de hello, tout en conservant toutes les stratégies de hello elle appliquée dans l’hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-115">Applying policy in hardware enables hello NIC tooforward network traffic directly toohello VM, bypassing hello host and hello virtual switch, while maintaining all hello policy it applied in hello host.</span></span>

<span data-ttu-id="3ecfa-116">Hello avantages d’un réseau d’accélérée s’appliquent uniquement toohello ordinateur virtuel sur lequel il est activé sur.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-116">hello benefits of accelerated networking only apply toohello VM that it is enabled on.</span></span> <span data-ttu-id="3ecfa-117">Pour de meilleurs résultats de hello, elle est idéale tooenable cette fonctionnalité au moins deux machines virtuelles connectées toohello même réseau virtuel Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-117">For hello best results, it is ideal tooenable this feature on at least two VMs connected toohello same Azure Virtual Network (VNet).</span></span> <span data-ttu-id="3ecfa-118">Lors de la communication entre les réseaux virtuels ou de la connexion locale, cette fonctionnalité a une latence toooverall un impact minimal.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-118">When communicating across VNets or connecting on-premises, this feature has minimal impact toooverall latency.</span></span>

> [!WARNING]
> <span data-ttu-id="3ecfa-119">Cette Linux version préliminaire publique ne peut pas avoir de hello même niveau de disponibilité et la fiabilité en tant que fonctionnalités qui sont en général version en disponibilité.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-119">This Linux Public Preview may not have hello same level of availability and reliability as features that are in general availability release.</span></span> <span data-ttu-id="3ecfa-120">fonctionnalité de Hello n’est pas pris en charge peut-être avoir limitées des fonctionnalités et ne peut-être pas être disponible dans tous les emplacements Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-120">hello feature is not supported, may have constrained capabilities, and may not be available in all Azure locations.</span></span> <span data-ttu-id="3ecfa-121">Hello plus récentes des notifications sur disponibilité et l’état de cette fonctionnalité, vérifiez la page mises à jour de réseau virtuel Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-121">For hello most up-to-date notifications on availability and status of this feature, check hello Azure Virtual Network updates page.</span></span>

## <a name="benefits"></a><span data-ttu-id="3ecfa-122">Avantages</span><span class="sxs-lookup"><span data-stu-id="3ecfa-122">Benefits</span></span>
* <span data-ttu-id="3ecfa-123">**Latence inférieure / plus élevé de paquets par seconde (pps) :** suppression hello commutateur à partir du chemin de données hello supprime hello temps paquets dans hôte hello pour le traitement de la stratégie et d’augmente hello le nombre de paquets qui peuvent être traitées à l’intérieur de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-123">**Lower Latency / Higher packets per second (pps):** Removing hello virtual switch from hello datapath removes hello time packets spend in hello host for policy processing and increases hello number of packets that can be processed inside hello VM.</span></span>
* <span data-ttu-id="3ecfa-124">**Réduit l’instabilité :** commutateur virtuel traitement dépend de hello de stratégie qui a besoin de toobe appliquée et hello charge de travail de hello CPU qui effectue le traitement de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-124">**Reduced jitter:** Virtual switch processing depends on hello amount of policy that needs toobe applied and hello workload of hello CPU that is doing hello processing.</span></span> <span data-ttu-id="3ecfa-125">Hello stratégie mise en œuvre toohello matériel de déchargement supprime cette variabilité remettre des paquets directement toohello machine virtuelle, la suppression de communication de tooVM hôte hello et toutes les interruptions de logiciel et contexte bascule.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-125">Offloading hello policy enforcement toohello hardware removes that variability by delivering packets directly toohello VM, removing hello host tooVM communication and all software interrupts and context switches.</span></span>
* <span data-ttu-id="3ecfa-126">**Réduit l’utilisation du processeur :** commutateur virtuel de contournement hello dans l’hôte de hello entraîne l’utilisation du processeur accessible sans pour traiter le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-126">**Decreased CPU utilization:** Bypassing hello virtual switch in hello host leads tooless CPU utilization for processing network traffic.</span></span>

## <span data-ttu-id="3ecfa-127"><a name="Limitations"></a>Limitations</span><span class="sxs-lookup"><span data-stu-id="3ecfa-127"><a name="Limitations"></a>Limitations</span></span>
<span data-ttu-id="3ecfa-128">Hello limites suivantes existe lors de l’utilisation de cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-128">hello following limitations exist when using this capability:</span></span>

* <span data-ttu-id="3ecfa-129">**Création d’interface réseau :** la mise en réseau accélérée ne peut être activée que pour une nouvelle carte réseau.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-129">**Network interface creation:** Accelerated networking can only be enabled for a new NIC.</span></span> <span data-ttu-id="3ecfa-130">Elle ne peut pas être activée pour une carte réseau existante.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-130">It cannot be enabled for an existing NIC.</span></span>
* <span data-ttu-id="3ecfa-131">**Création d’ordinateurs virtuels :** une carte d’interface réseau avec un réseau d’accélérée activée peut uniquement être attachée tooa VM lorsque hello la machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-131">**VM creation:** A NIC with accelerated networking enabled can only be attached tooa VM when hello VM is created.</span></span> <span data-ttu-id="3ecfa-132">Hello carte réseau ne peut pas être attaché tooan existant de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-132">hello NIC cannot be attached tooan existing VM.</span></span>
* <span data-ttu-id="3ecfa-133">**Régions :** des machines virtuelles Windows avec mise en réseau accélérée sont proposées dans la plupart des régions Azure.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-133">**Regions:** Windows VMs with accelerated networking are offered in most Azure regions.</span></span> <span data-ttu-id="3ecfa-134">Des machines virtuelles Linux avec mise en réseau accélérée sont proposées dans plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-134">Linux VMs with accelerated networking are offered in multiple regions.</span></span> <span data-ttu-id="3ecfa-135">Cette fonctionnalité est disponible dans des régions Hello se développe.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-135">hello regions this capability is available in is expanding.</span></span> <span data-ttu-id="3ecfa-136">Consultez hello Azure virtuel réseau blog mises à jour ci-dessous pour les informations les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-136">Please see hello Azure Virtual Networking Updates blog below for hello latest information.</span></span>   
* <span data-ttu-id="3ecfa-137">**Systèmes d’exploitation pris en charge :** Windows : Microsoft Windows Server 2012 R2 Datacenter et Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-137">**Supported operating systems:** Windows: Microsoft Windows Server 2012 R2 Datacenter and Windows Server 2016.</span></span> <span data-ttu-id="3ecfa-138">Linux : Ubuntu Server 16.04 LTS avec noyau 4.4.0-77 ou supérieur, SLES 12 SP2, RHEL 7.3 et CentOS 7.3 (publié par « Rogue Wave Software »).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-138">Linux: Ubuntu Server 16.04 LTS with kernel 4.4.0-77 or higher, SLES 12 SP2, RHEL 7.3 and CentOS 7.3 (Published by “Rogue Wave Software”).</span></span>
* <span data-ttu-id="3ecfa-139">**Taille de machine virtuelle :** tailles d’instance à usage général et de calcul optimisé avec au moins huit cœurs.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-139">**VM Size:** General purpose and compute-optimized instance sizes with eight or more cores.</span></span> <span data-ttu-id="3ecfa-140">Pour plus d’informations, consultez hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles des tailles de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-140">For more information, see hello [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM sizes articles.</span></span> <span data-ttu-id="3ecfa-141">Hello des tailles prises en charge instance développera Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-141">hello set of supported VM instance sizes will expand in hello future.</span></span>
* <span data-ttu-id="3ecfa-142">**Déploiement via Azure Resource Manager (ARM) uniquement :** la mise en réseau accélérée n’est pas disponible pour le déploiement via ASM/RDFE.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-142">**Deployment through Azure Resource Manager (ARM) only:** Accelerated Networking is not available for deployment through ASM/RDFE.</span></span>

<span data-ttu-id="3ecfa-143">Modifications toothese limitations sont annoncées via hello [le réseau virtuel Azure met à jour](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-143">Changes toothese limitations are announced through hello [Azure Virtual Networking updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) page.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="3ecfa-144">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="3ecfa-144">Create a Windows VM</span></span>
<span data-ttu-id="3ecfa-145">Vous pouvez utiliser hello portail Azure ou Azure [PowerShell](#windows-powershell) toocreate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-145">You can use hello Azure portal or Azure [PowerShell](#windows-powershell) toocreate hello VM.</span></span>

### <span data-ttu-id="3ecfa-146"><a name="windows-portal"></a>Portail</span><span class="sxs-lookup"><span data-stu-id="3ecfa-146"><a name="windows-portal"></a>Portal</span></span>

1. <span data-ttu-id="3ecfa-147">À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-147">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="3ecfa-148">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-148">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="3ecfa-149">Dans le portail de hello, cliquez sur **+ nouveau** > **de calcul** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-149">In hello portal, click **+ New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
3. <span data-ttu-id="3ecfa-150">Bonjour **Datacenter de Windows Server 2016** panneau qui s’affiche, laissez le champ *le Gestionnaire de ressources* sélectionné sous **sélectionner un modèle de déploiement**, puis cliquez sur **créer** .</span><span class="sxs-lookup"><span data-stu-id="3ecfa-150">In hello **Windows Server 2016 Datacenter** blade that appears, leave *Resource Manager* selected under **Select a deployment model**, and click **Create**.</span></span>
4. <span data-ttu-id="3ecfa-151">Bonjour **notions de base** panneau qui s’affiche, entrez hello valeurs suivantes, laissez hello restant des options par défaut ou sélectionnez ou entrez vos propres valeurs, puis cliquez sur hello **OK** bouton :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-151">In hello **Basics** blade that appears, enter hello following values, leave hello remaining default options or select or enter your own values, and click hello **OK** button:</span></span>

    |<span data-ttu-id="3ecfa-152">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3ecfa-152">Setting</span></span>|<span data-ttu-id="3ecfa-153">Valeur</span><span class="sxs-lookup"><span data-stu-id="3ecfa-153">Value</span></span>|
    |---|---|
    |<span data-ttu-id="3ecfa-154">Nom</span><span class="sxs-lookup"><span data-stu-id="3ecfa-154">Name</span></span>|<span data-ttu-id="3ecfa-155">MyVm</span><span class="sxs-lookup"><span data-stu-id="3ecfa-155">MyVm</span></span>|
    |<span data-ttu-id="3ecfa-156">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3ecfa-156">Resource group</span></span>|<span data-ttu-id="3ecfa-157">Laissez l’option **Créer un nouveau** activée et entrez *MyResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="3ecfa-157">Leave **Create new** selected and enter *MyResourceGroup*</span></span>|
    |<span data-ttu-id="3ecfa-158">Lieu</span><span class="sxs-lookup"><span data-stu-id="3ecfa-158">Location</span></span>|<span data-ttu-id="3ecfa-159">Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="3ecfa-159">West US 2</span></span>|

    <span data-ttu-id="3ecfa-160">Si vous êtes tooAzure nouvelle, en savoir plus sur [groupes de ressources](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnements](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), et [emplacements](https://azure.microsoft.com/regions) (également appelée le tooas régions).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-160">If you're new tooAzure, learn more about [Resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (which are also referred tooas regions).</span></span>
5. <span data-ttu-id="3ecfa-161">Bonjour **choisir une taille** panneau qui s’affiche, entrez *8* Bonjour **nombre Minimum de cœurs** zone, puis cliquez sur **afficher toutes les**.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-161">In hello **Choose a size** blade that appears, enter *8* in hello **Minimum cores** box, then click **View all**.</span></span>
6. <span data-ttu-id="3ecfa-162">Cliquez sur **DS4_V2 Standard**, ou tout pris en charge d’ordinateur virtuel, puis cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-162">Click **DS4_V2 Standard**, or any supported VM, then click hello **Select** button.</span></span>
7. <span data-ttu-id="3ecfa-163">Bonjour **paramètres** panneau qui s’affiche, conservez tous les paramètres en tant que-est, à l’exception de clic **activé** sous **Accelerated réseau**, puis cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-163">In hello **Settings** blade that appears, leave all settings as-is, except click **Enabled** under **Accelerated networking**, then click hello **OK** button.</span></span> <span data-ttu-id="3ecfa-164">**Remarque :** si, dans les étapes précédentes, vous avez sélectionné pour la taille de machine virtuelle, système d’exploitation ou emplacement, les valeurs qui ne sont pas répertoriées dans hello [Limitations](#Limitations) section de cet article, **Accelerated réseau**n’est pas visible.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-164">**Note:** If, in previous steps, you selected values for VM size, operating system, or location that aren't listed in hello [Limitations](#Limitations) section of this article, **Accelerated networking** isn't visible.</span></span>
8. <span data-ttu-id="3ecfa-165">Bonjour **Résumé** panneau qui s’affiche, cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-165">In hello **Summary** blade that appears, click hello **OK** button.</span></span> <span data-ttu-id="3ecfa-166">Azure démarre la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-166">Azure starts creating hello VM.</span></span> <span data-ttu-id="3ecfa-167">La création de la machine virtuelle prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-167">VM creation takes a few minutes.</span></span>
9. <span data-ttu-id="3ecfa-168">tooinstall hello accelerated pilote réseau pour Windows, hello terminé les étapes Bonjour [configurer Windows](#configure-windows) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-168">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="3ecfa-169"><a name="windows-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ecfa-169"><a name="windows-powershell"></a>PowerShell</span></span>
1. <span data-ttu-id="3ecfa-170">Installez hello dernière version de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-170">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="3ecfa-171">Si vous êtes nouveau tooAzure PowerShell, lisez hello [vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-171">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="3ecfa-172">Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows hello, en tapant **powershell**, puis en cliquant sur **PowerShell** hello résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-172">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="3ecfa-173">Dans la fenêtre PowerShell, entrez hello `login-azurermaccount` toosign de commande avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-173">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="3ecfa-174">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-174">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="3ecfa-175">Dans votre navigateur, copiez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-175">In your browser, copy hello following script:</span></span>
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

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. <span data-ttu-id="3ecfa-176">Dans la fenêtre PowerShell, avec le bouton droit de script de hello toopaste et démarrer son exécution.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-176">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="3ecfa-177">Vous êtes invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-177">You are prompted for a username and password.</span></span> <span data-ttu-id="3ecfa-178">Utilisez ces informations d’identification toolog dans toohello machine virtuelle lors de la connexion tooit à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-178">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="3ecfa-179">Si le script de hello échoue et que vous avez modifié les valeurs dans le script de hello avant son exécution, vérifiez les valeurs hello utilisées pour la taille de machine virtuelle, système d’exploitation, et qu’emplacement sont répertoriés dans hello [Limitations](#Limitations) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-179">If hello script fails, and you changed values in hello script before executing it, confirm hello values you used for VM size, operating system, and location are listed in hello [Limitations](#Limitations) section of this article.</span></span>
6. <span data-ttu-id="3ecfa-180">tooinstall hello accelerated pilote réseau pour Windows, hello terminé les étapes Bonjour [configurer Windows](#configure-windows) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-180">tooinstall hello accelerated networking driver for Windows, complete hello steps in hello [Configure Windows](#configure-windows) section of this article.</span></span>

### <span data-ttu-id="3ecfa-181"><a name="configure-windows"></a>Configurer Windows</span><span class="sxs-lookup"><span data-stu-id="3ecfa-181"><a name="configure-windows"></a>Configure Windows</span></span>
<span data-ttu-id="3ecfa-182">Une fois que vous créez hello machine virtuelle dans Azure, vous devez installer le pilote de réseau d’accélérée hello pour Windows.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-182">Once you create hello VM in Azure, you must install hello accelerated networking driver for Windows.</span></span> <span data-ttu-id="3ecfa-183">Avant d’exécuter hello comme suit, vous devez avoir créé une machine virtuelle Windows avec un réseau d’accélérée à l’aide soit hello [portal](#windows-portal) ou [PowerShell](#windows-powershell) les étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-183">Before completing hello following steps, you must have created a Windows VM with accelerated networking using either hello [portal](#windows-portal) or [PowerShell](#windows-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="3ecfa-184">À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-184">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="3ecfa-185">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-185">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="3ecfa-186">Dans la zone hello qui contient le texte hello *recherche les ressources* haut hello de hello portail Azure, tapez *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-186">In hello box that contains hello text *Search resources* at hello top of hello Azure portal, type *MyVm*.</span></span> <span data-ttu-id="3ecfa-187">Lorsque **MyVm** s’affiche dans les résultats de recherche hello, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-187">When **MyVm** appears in hello search results, click it.</span></span>
3. <span data-ttu-id="3ecfa-188">Bonjour **MyVm** panneau qui s’affiche, cliquez sur hello **Connect** bouton hello en haut à gauche du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-188">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="3ecfa-189">**Remarque :** si **création** est visible sous hello **Connect** bouton, Azure n’est pas encore terminée création hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-189">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="3ecfa-190">Cliquez sur **Connect** uniquement une fois que vous ne voyez plus **création** sous hello **Connect** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-190">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
4. <span data-ttu-id="3ecfa-191">Autoriser votre hello toodownload de navigateur **MyVm.rdp** fichier.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-191">Allow your browser toodownload hello **MyVm.rdp** file.</span></span>  <span data-ttu-id="3ecfa-192">Une fois téléchargé, cliquez sur hello fichier tooopen il.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-192">Once downloaded, click hello file tooopen it.</span></span> 
5. <span data-ttu-id="3ecfa-193">Cliquez sur hello **Connect** bouton Bonjour **connexion Bureau à distance** zone qui s’affiche vous informant que hello éditeur de connexion à distance de hello ne peut pas être identifié.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-193">Click hello **Connect** button in hello **Remote Desktop Connection** box that appears, notifying you that hello publisher of hello remote connection can't be identified.</span></span>
6. <span data-ttu-id="3ecfa-194">Bonjour **sécurité Windows** zone qui s’affiche, cliquez sur **plus de choix**, puis cliquez sur **utiliser un autre compte**.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-194">In hello **Windows Security** box that appears, click **More choices**, then click **Use a different account**.</span></span> <span data-ttu-id="3ecfa-195">Entrez le nom d’utilisateur hello et le mot de passe entré à l’étape 4, puis cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-195">Enter hello username and password you entered in step 4, then click hello **OK** button.</span></span>
7. <span data-ttu-id="3ecfa-196">Cliquez sur hello **Oui** bouton de boîte de connexion Bureau à distance hello qui s’affiche, indiquant que l’identité hello de l’ordinateur distant de hello ne peut pas être vérifiée.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-196">Click hello **Yes** button in hello Remote Desktop Connection box that appears, notifying you that hello identity of hello remote computer cannot be verified.</span></span>
8. <span data-ttu-id="3ecfa-197">Cliquez sur le bouton de démarrage de Windows hello, sur **le Gestionnaire de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-197">Right-click hello Windows Start button and click **Device Manager**.</span></span> <span data-ttu-id="3ecfa-198">Développez hello **cartes réseau** nœud.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-198">Expand hello **Network adapters** node.</span></span> <span data-ttu-id="3ecfa-199">Vérifiez que hello **Mellanox ConnectX-3 virtuel fonction Ethernet adaptateur** s’affiche, comme indiqué dans hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-199">Confirm that hello **Mellanox ConnectX-3 Virtual Function Ethernet Adapter** appears, as shown in hello following picture:</span></span>
   
    ![Gestionnaire de périphériques](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. <span data-ttu-id="3ecfa-201">La mise en réseau accélérée est maintenant activée pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-201">Accelerated Networking is now enabled for your VM.</span></span>

## <a name="create-a-linux-vm"></a><span data-ttu-id="3ecfa-202">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="3ecfa-202">Create a Linux VM</span></span>
<span data-ttu-id="3ecfa-203">Vous pouvez utiliser hello portail Azure ou Azure [PowerShell](#linux-powershell) toocreate un Ubuntu ou le SLES VM.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-203">You can use hello Azure portal or Azure [PowerShell](#linux-powershell) toocreate an Ubuntu or SLES VM.</span></span> <span data-ttu-id="3ecfa-204">Le flux de travail est différent pour les machines virtuelles RHEL et CentOS.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-204">For RHEL and CentOS VMs there is a different workflow.</span></span>  <span data-ttu-id="3ecfa-205">Consultez les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-205">Please see hello instructions below.</span></span>

### <span data-ttu-id="3ecfa-206"><a name="linux-portal"></a>Portail</span><span class="sxs-lookup"><span data-stu-id="3ecfa-206"><a name="linux-portal"></a>Portal</span></span>
1. <span data-ttu-id="3ecfa-207">S’inscrire à hello accéléré mise en réseau pour l’aperçu de Linux en effectuant les étapes 1 à 5 de hello [créer un VM Linux - PowerShell](#linux-powershell) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-207">Register for hello accelerated networking for Linux preview by completing steps 1-5 of hello [Create a Linux VM - PowerShell](#linux-powershell) section of this article.</span></span>  <span data-ttu-id="3ecfa-208">Impossible d’inscrire pour l’aperçu hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-208">You cannot register for hello preview in hello portal.</span></span>
2. <span data-ttu-id="3ecfa-209">Complète les étapes 1-8 les hello en [créer une machine virtuelle Windows - portail](#windows-portal) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-209">Complete steps 1-8 in hello [Create a Windows VM - portal](#windows-portal) section of this article.</span></span> <span data-ttu-id="3ecfa-210">À l’étape 2, cliquez sur **Ubuntu Server 16.04 LTS** au lieu de **Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-210">In step 2, click **Ubuntu Server 16.04 LTS** instead of **Windows Server 2016 Datacenter**.</span></span> <span data-ttu-id="3ecfa-211">Pour ce didacticiel, choisissez toouse un mot de passe, plutôt que d’une clé SSH, bien que pour les déploiements de production, vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-211">For this tutorial, choose toouse a password, rather than an SSH key, though for production deployments, you can use either.</span></span> <span data-ttu-id="3ecfa-212">Si **Accelerated réseau** n’apparaît pas lorsque vous terminez l’étape 7 de hello [créer une machine virtuelle Windows - portail](#windows-portal) section de cet article, il est probablement pour l’une des hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-212">If **Accelerated networking** does not appear when you complete step 7 of hello [Create a Windows VM - portal](#windows-portal) section of this article, it's likely for one of hello following reasons:</span></span>
    - <span data-ttu-id="3ecfa-213">Vous n’êtes pas encore inscrit pour l’aperçu de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-213">You are not yet registered for hello preview.</span></span> <span data-ttu-id="3ecfa-214">Vérifiez que votre état de l’enregistrement est **inscrit**, comme expliqué à l’étape 4 de hello [créer un VM Linux - Powershell](#linux-powershell) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-214">Confirm that your registration state is **Registered**, as explained in step 4 of hello [Create a Linux VM - Powershell](#linux-powershell) section of this article.</span></span> <span data-ttu-id="3ecfa-215">**Remarque :** si vous avez participé hello Accelerated mise en réseau pour l’aperçu de machines virtuelles Windows (son aucun toouse tooregister nécessaire plu ne Accelerated mise en réseau pour les machines virtuelles Windows), vous n'êtes pas automatiquement enregistré pour hello Accelerated mise en réseau pour Afficher un aperçu des machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-215">**Note:** If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="3ecfa-216">Vous devez vous inscrire pour hello Accelerated mise en réseau pour afficher un aperçu des machines virtuelles Linux tooparticipate qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-216">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
    - <span data-ttu-id="3ecfa-217">Vous n’avez pas sélectionné une taille de machine virtuelle, système d’exploitation ou emplacement répertorié dans hello [Limitations](#limitations) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-217">You have not selected a VM size, operating system, or location listed in hello [Limitations](#limitations) section of this article.</span></span>
3. <span data-ttu-id="3ecfa-218">tooinstall hello accelerated pilote réseau pour Linux, hello terminé les étapes Bonjour [configurer de Linux](#configure-linux) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-218">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="3ecfa-219"><a name="linux-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ecfa-219"><a name="linux-powershell"></a>PowerShell</span></span>

>[!WARNING]
><span data-ttu-id="3ecfa-220">Si vous créez les machines virtuelles Linux avec un réseau d’accélérée dans un abonnement et que vous tentez ensuite toocreate une machine virtuelle de Windows avec un réseau d’accélérée Bonjour même abonnement, hello la création de la machine virtuelle Windows risque d’échouer.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-220">If you create Linux VMs with accelerated networking in a subscription, and then attempt toocreate a Windows VM with accelerated networking in hello same subscription, hello Windows VM creation may fail.</span></span> <span data-ttu-id="3ecfa-221">Dans cette version préliminaire, il est recommandé de tester les machines virtuelles Linux et Windows avec une mise en réseau accélérée dans des abonnements distincts.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-221">During this preview, it's recommended that you test Linux and Windows VMs with accelerated networking in separate subscriptions.</span></span>
>

1. <span data-ttu-id="3ecfa-222">Installez hello dernière version de hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-222">Install hello latest version of hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="3ecfa-223">Si vous êtes nouveau tooAzure PowerShell, lisez hello [vue d’ensemble d’Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-223">If you're new tooAzure PowerShell, read hello [Azure PowerShell overview](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) article.</span></span>
2. <span data-ttu-id="3ecfa-224">Démarrez une session PowerShell en cliquant sur le bouton Démarrer de Windows hello, en tapant **powershell**, puis en cliquant sur **PowerShell** hello résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-224">Start a PowerShell session by clicking hello Windows Start button, typing **powershell**, then clicking **PowerShell** from hello search results.</span></span>
3. <span data-ttu-id="3ecfa-225">Dans la fenêtre PowerShell, entrez hello `login-azurermaccount` toosign de commande avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-225">In your PowerShell window, enter hello `login-azurermaccount` command toosign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="3ecfa-226">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-226">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="3ecfa-227">S’inscrire à hello accéléré mise en réseau pour Azure preview en complétant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-227">Register for hello accelerated networking for Azure preview by completing hello following steps:</span></span>
    - <span data-ttu-id="3ecfa-228">Envoyer un courrier électronique trop[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) avec votre ID d’abonnement Azure et l’utilisation prévue.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-228">Send an email too[axnpreview@microsoft.com](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) with your Azure subscription ID and intended use.</span></span> <span data-ttu-id="3ecfa-229">Veuillez attendre un e-mail de confirmation de la part de Microsoft concernant l’activation de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-229">Please wait for an email confirmation from Microsoft about your subscription being enabled.</span></span>
    - <span data-ttu-id="3ecfa-230">Entrez hello suivant tooconfirm de commande que vous êtes inscrit pour l’aperçu de hello :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-230">Enter hello following command tooconfirm you are registered for hello preview:</span></span>
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        <span data-ttu-id="3ecfa-231">Ne poursuivez pas à l’étape 5 jusqu'à ce que **inscrit** apparaît dans hello de sortie après avoir entré la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-231">Do not continue with step 5 until **Registered** appears in hello output after you enter hello previous command.</span></span> <span data-ttu-id="3ecfa-232">Votre sortie doit ressembler à la suivante hello de sortie avant de continuer :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-232">Your output must look like hello following output before continuing:</span></span>
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      ><span data-ttu-id="3ecfa-233">Si vous avez participé hello Accelerated mise en réseau pour l’aperçu de machines virtuelles Windows (son aucun toouse tooregister nécessaire plu ne Accelerated mise en réseau pour les machines virtuelles Windows), vous n'êtes pas automatiquement enregistré pour hello Accelerated mise en réseau pour les machines virtuelles Linux preview.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-233">If you participated in hello Accelerated networking for Windows VMs preview (it's no longer necessary tooregister toouse Accelerated networking for Windows VMs), you are not automatically registered for hello Accelerated networking for Linux VMs preview.</span></span> <span data-ttu-id="3ecfa-234">Vous devez vous inscrire pour hello Accelerated mise en réseau pour afficher un aperçu des machines virtuelles Linux tooparticipate qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-234">You must register for hello Accelerated networking for Linux VMs preview tooparticipate in it.</span></span>
      >
5. <span data-ttu-id="3ecfa-235">Dans votre navigateur, copiez hello suivant le script en remplaçant Ubuntu ou SLES comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-235">In your browser, copy hello following script substituting Ubuntu or SLES as desired.</span></span>  <span data-ttu-id="3ecfa-236">Ici encore, Redhat et CentOS ont un flux de travail différent, décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-236">Again, Redhat and CentOS have a different workflow outlined below:</span></span>

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

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. <span data-ttu-id="3ecfa-237">Dans la fenêtre PowerShell, avec le bouton droit de script de hello toopaste et démarrer son exécution.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-237">In your PowerShell window, right-click toopaste hello script and start executing it.</span></span> <span data-ttu-id="3ecfa-238">Vous êtes invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-238">You are prompted for a username and password.</span></span> <span data-ttu-id="3ecfa-239">Utilisez ces informations d’identification toolog dans toohello machine virtuelle lors de la connexion tooit à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-239">Use these credentials toolog in toohello VM when connecting tooit in hello next step.</span></span> <span data-ttu-id="3ecfa-240">Si le script de hello échoue, vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-240">If hello script fails, confirm that:</span></span>
    - <span data-ttu-id="3ecfa-241">Vous êtes inscrit pour l’aperçu de hello, comme expliqué à l’étape 4</span><span class="sxs-lookup"><span data-stu-id="3ecfa-241">You are registered for hello preview, as explained in step 4</span></span>
    - <span data-ttu-id="3ecfa-242">Si vous avez modifié taille d’ordinateur virtuel, type de système d’exploitation ou les valeurs d’emplacement dans le script de hello avant son exécution, que les valeurs hello sont répertoriés dans hello [Limitations](#Limitations) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-242">If you changed VM size, operating system type, or location values in hello script before executing it, that hello values are listed in hello [Limitations](#Limitations) section of this article.</span></span>
7. <span data-ttu-id="3ecfa-243">tooinstall hello accelerated pilote réseau pour Linux, hello terminé les étapes Bonjour [configurer de Linux](#configure-linux) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-243">tooinstall hello accelerated networking driver for Linux, complete hello steps in hello [Configure Linux](#configure-linux) section of this article.</span></span>

### <span data-ttu-id="3ecfa-244"><a name="configure-linux"></a>Configurer Linux</span><span class="sxs-lookup"><span data-stu-id="3ecfa-244"><a name="configure-linux"></a>Configure Linux</span></span>

<span data-ttu-id="3ecfa-245">Une fois que vous créez hello machine virtuelle dans Azure, vous devez installer le pilote de réseau d’accélérée hello pour Linux.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-245">Once you create hello VM in Azure, you must install hello accelerated networking driver for Linux.</span></span> <span data-ttu-id="3ecfa-246">Avant d’exécuter hello comme suit, vous devez avoir créé un VM Linux avec un réseau d’accélérée à l’aide soit hello [portal](#linux-portal) ou [PowerShell](#linux-powershell) les étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-246">Before completing hello following steps, you must have created a Linux VM with accelerated networking using either hello [portal](#linux-portal) or [PowerShell](#linux-powershell) steps in this article.</span></span> 

1. <span data-ttu-id="3ecfa-247">À partir d’un navigateur Internet, ouvrez hello Azure [portal](https://portal.azure.com) et connectez-vous avec votre Azure [compte](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-247">From an Internet browser, open hello Azure [portal](https://portal.azure.com) and sign in with your Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="3ecfa-248">Si vous n’avez pas de compte, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/offers/ms-azr-0044p).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-248">If you don't already have an account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="3ecfa-249">Haut hello hello portail, toohello droite de hello *recherche les ressources* barre, cliquez sur hello **> _** icône toostart un shell de cloud d’un interpréteur de commandes (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="3ecfa-249">At hello top of hello portal, toohello right of hello *Search resources* bar, click hello **>_** icon toostart a Bash cloud shell (Preview).</span></span> <span data-ttu-id="3ecfa-250">Hello Bash cloud shell volet s’affiche en bas de hello du portail de hello et après quelques secondes, présente une  **username@Azure:~ $** invite.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-250">hello Bash cloud shell pane appears at hello bottom of hello portal and after a few seconds, presents a **username@Azure:~$** prompt.</span></span> <span data-ttu-id="3ecfa-251">Si vous pouvez SSH toohello machine virtuelle à partir de votre ordinateur, plutôt que de shell du cloud hello, instructions hello dans ce didacticiel supposent à l’aide de shell du cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-251">Though you can SSH toohello VM from your computer, rather than hello cloud shell, hello instructions in this tutorial assume you're using hello cloud shell.</span></span>
3. <span data-ttu-id="3ecfa-252">Haut hello du portail de hello, dans la zone de hello contient texte hello *recherche les ressources*, type *MyVm*.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-252">At hello top of hello portal, in hello box that contains hello text *Search resources*, type *MyVm*.</span></span> <span data-ttu-id="3ecfa-253">Lorsque **MyVm** s’affiche dans les résultats de recherche hello, cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-253">When **MyVm** appears in hello search results, click it.</span></span>
4. <span data-ttu-id="3ecfa-254">Bonjour **MyVm** panneau qui s’affiche, cliquez sur hello **Connect** bouton hello en haut à gauche du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-254">In hello **MyVm** blade that appears, click hello **Connect** button in hello top left corner of hello blade.</span></span> <span data-ttu-id="3ecfa-255">**Remarque :** si **création** est visible sous hello **Connect** bouton, Azure n’est pas encore terminée création hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-255">**Note:** If **Creating** is visible under hello **Connect** button, Azure has not yet finished creating hello VM.</span></span> <span data-ttu-id="3ecfa-256">Cliquez sur **Connect** uniquement une fois que vous ne voyez plus **création** sous hello **Connect** bouton.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-256">Click **Connect** only after you no longer see **Creating** under hello **Connect** button.</span></span>
5. <span data-ttu-id="3ecfa-257">Azure ouvre un message vous en informant tooenter hello `ssh adminuser@<ipaddress>`.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-257">Azure opens a box telling you tooenter hello `ssh adminuser@<ipaddress>`.</span></span> <span data-ttu-id="3ecfa-258">Entrez cette commande dans hello cloud shell (ou la copie à partir de la zone hello apparues dans l’étape 4 et le coller dans le shell toohello cloud), puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-258">Enter this command in hello cloud shell (or copy it from hello box that appeared in step 4 and paste it in toohello cloud shell), then press Enter.</span></span>
6. <span data-ttu-id="3ecfa-259">Entrée **Oui** question toohello demandant vous si vous souhaitez que toocontinue vous vous connectez, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-259">Enter **yes** toohello question asking you if you want toocontinue connecting, then press Enter.</span></span>
7. <span data-ttu-id="3ecfa-260">Mot de passe hello que vous avez entré lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-260">Enter hello password you entered when creating hello VM.</span></span> <span data-ttu-id="3ecfa-261">Une fois connecté avec succès toohello machine virtuelle, vous voyez un adminuser@MyVm:~ invite$.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-261">Once successfully logged in toohello VM, you see an adminuser@MyVm:~$ prompt.</span></span> <span data-ttu-id="3ecfa-262">Vous êtes désormais connecté toohello machine virtuelle via une session cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-262">You are now logged in toohello VM through hello cloud shell session.</span></span> <span data-ttu-id="3ecfa-263">**Remarque :** les sessions de Cloud Shell expirent après 10 minutes d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-263">**Note:** Cloud shell sessions time out after 10 minutes of inactivity.</span></span>

<span data-ttu-id="3ecfa-264">À ce stade, les instructions de hello varient en fonction distribution hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-264">At this point, hello instructions vary based on hello distribution you are using.</span></span> 

#### <a name="ubuntusles"></a><span data-ttu-id="3ecfa-265">Ubuntu/SLES</span><span class="sxs-lookup"><span data-stu-id="3ecfa-265">Ubuntu/SLES</span></span>

1. <span data-ttu-id="3ecfa-266">À l’invite de hello, entrez `uname -r` et vérifiez la version de hello pour :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-266">At hello prompt, enter `uname -r` and confirm hello version for:</span></span>

    * <span data-ttu-id="3ecfa-267">Ubuntu « 4.4.0-77-generic », ou supérieur</span><span class="sxs-lookup"><span data-stu-id="3ecfa-267">Ubuntu is "4.4.0-77-generic," or greater</span></span>
    * <span data-ttu-id="3ecfa-268">SLES « 4.4.59-92.20-default » ou supérieur</span><span class="sxs-lookup"><span data-stu-id="3ecfa-268">SLES is "4.4.59-92.20-default" or greater</span></span>

2. <span data-ttu-id="3ecfa-269">Créer une liaison entre la carte de mise en réseau standard hello et hello accéléré la carte réseau virtuelle mise en réseau par les commandes hello en cours d’exécution qui suivent.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-269">Create a bond between hello standard networking vNIC and hello accelerated networking vNIC by running hello commands that follow.</span></span> <span data-ttu-id="3ecfa-270">Le trafic réseau utilise hello plu performants d’accélérée vNIC mise en réseau, alors que l’obligation de hello garantit que le trafic réseau n’est pas interrompu sur certaines modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-270">Network traffic uses hello higher performing accelerated networking vNIC, while hello bond ensures that networking traffic is not interrupted across certain configuration changes.</span></span>
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. <span data-ttu-id="3ecfa-271">Après l’exécution du script hello, hello machine virtuelle redémarre après une seconde 60 suspendre.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-271">After running hello script, hello VM will restart after a 60 second pause.</span></span>
4. <span data-ttu-id="3ecfa-272">Une fois hello machine virtuelle est redémarrée, reconnectez tooit en effectuant les étapes 5 à 7 à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-272">Once hello VM is restarted, reconnect tooit by completing steps 5-7 again.</span></span>
5. <span data-ttu-id="3ecfa-273">Exécutez hello `ifconfig` commande et confirmer que bond0 n’a rien et interface de hello est affiché comme étant en service.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-273">Run hello `ifconfig` command and confirm that bond0 has come up and hello interface is showing as UP.</span></span> 
 
 >[!NOTE]
      ><span data-ttu-id="3ecfa-274">Applications à l’aide de la mise en réseau d’accélérée doivent communiquer sur hello *bond0* interface non *eth0*.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-274">Applications using accelerated networking must communicate over hello *bond0* interface, not *eth0*.</span></span>  <span data-ttu-id="3ecfa-275">nom de l’interface Hello peut changer avant la mise en réseau d’accélérée rendue publique.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-275">hello interface name may change before accelerated networking reaches general availability.</span></span>

#### <a name="rhelcentos"></a><span data-ttu-id="3ecfa-276">RHEL/CentOS</span><span class="sxs-lookup"><span data-stu-id="3ecfa-276">RHEL/CentOS</span></span>

<span data-ttu-id="3ecfa-277">Création d’un Red Hat Enterprise Linux ou la machine virtuelle de CentOS 7.3 requiert certains extra étapes tooload hello pilotes les plus récents nécessaires pour SR-IOV et hello virtuel fonction aucun pilote de carte réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-277">Creating a Red Hat Enterprise Linux or CentOS 7.3 VM requires some extra steps tooload hello latest drivers needed for SR-IOV and hello Virtual Function (VF) driver for hello network card.</span></span> <span data-ttu-id="3ecfa-278">Hello première phase d’instructions de hello prépare une image qui peut être utilisé toomake un ou plusieurs ordinateurs virtuels qui ont des pilotes hello préchargés.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-278">hello first phase of hello instructions prepares an image that can be used toomake one or more virtual machines that have hello drivers pre-loaded.</span></span>

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a><span data-ttu-id="3ecfa-279">Phase 1 : préparer une image de base Red Hat Enterprise Linux ou CentOS 7.3.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-279">Phase one: prepare a Red Hat Enterprise Linux or CentOS 7.3 base image.</span></span> 

1.  <span data-ttu-id="3ecfa-280">Approvisionner une machine virtuelle non-SRIOV CentOS 7.3 sur Azure</span><span class="sxs-lookup"><span data-stu-id="3ecfa-280">Provision a non-SRIOV CentOS 7.3 VM on Azure</span></span>

2.  <span data-ttu-id="3ecfa-281">Installer LIS 4.2.2 :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-281">Install LIS 4.2.2:</span></span>
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  <span data-ttu-id="3ecfa-282">Télécharger les fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="3ecfa-282">Download config files</span></span>
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  <span data-ttu-id="3ecfa-283">Annuler l’approvisionnement de cette machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3ecfa-283">Deprovision this VM</span></span>

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  <span data-ttu-id="3ecfa-284">À partir du portail Azure, arrêter cet ordinateur virtuel ; et accédez « Disques » de tooVM, capture URI de hello OSDisk VHD.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-284">From Azure portal, stop this VM; and go tooVM’s "Disks", capture hello OSDisk’s VHD URI.</span></span> <span data-ttu-id="3ecfa-285">Cet URI contient le nom de disque dur virtuel de l’image de base hello et son compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-285">This URI contains hello base image’s VHD name and its storage account.</span></span> 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a><span data-ttu-id="3ecfa-286">Phase 2 : approvisionner de nouvelles machines virtuelles sur Azure</span><span class="sxs-lookup"><span data-stu-id="3ecfa-286">Phase two: Provision new VMs on Azure</span></span>

1.  <span data-ttu-id="3ecfa-287">Configurer de nouveaux ordinateurs virtuels en fonction avec New-AzureRMVMConfig à l’aide de hello base image VHD capturé dans la première phase, avec AcceleratedNetworking activé sur une carte réseau virtuelle hello :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-287">Provision new VMs based with New-AzureRMVMConfig using hello base image VHD captured in phase one, with AcceleratedNetworking enabled on hello vNIC:</span></span>

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
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
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
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  <span data-ttu-id="3ecfa-288">Après l’heure de démarrage des machines virtuelles, appareil de fonction virtuelle hello par « lspci » et vérifiez l’entrée de Mellanox hello.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-288">After VMs boot up, check hello VF device by "lspci" and check hello Mellanox entry.</span></span> <span data-ttu-id="3ecfa-289">Par exemple, nous devrions voir cet élément dans la sortie de lspci hello :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-289">For example, we should see this item in hello lspci output:</span></span>
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  <span data-ttu-id="3ecfa-290">Exécutez le script de liaison hello par :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-290">Run hello bonding script by:</span></span>

    ```bash
    sudo bondvf.sh
    ```

4.  <span data-ttu-id="3ecfa-291">Redémarrez hello nouvelles machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="3ecfa-291">Reboot hello new VMs:</span></span>

    ```bash
    sudo reboot
    ```

<span data-ttu-id="3ecfa-292">Hello machine virtuelle doit commencer par bond0 configuré et hello chemin Accelerated réseau activé.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-292">hello VM should start with bond0 configured and hello Accelerated Networking path enabled.</span></span>  <span data-ttu-id="3ecfa-293">Exécutez `ifconfig` tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="3ecfa-293">Run `ifconfig` tooconfirm.</span></span>
