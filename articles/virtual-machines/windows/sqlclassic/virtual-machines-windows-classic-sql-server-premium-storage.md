---
title: "Utilisation de Stockage Premium Azure avec SQL Server | Microsoft Docs"
description: "Cet article utilise des ressources créées avec le modèle de déploiement classique et fournit des conseils sur l'utilisation du stockage d’Azure Premium Storage avec SQL Server s'exécutant sur des machines virtuelles Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 6790db207fc7ec8a4b1546ef07c97ef30abe9513
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="7f347-103">Utilisation du stockage Premium Azure avec SQL Server sur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="7f347-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="7f347-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7f347-104">Overview</span></span>
<span data-ttu-id="7f347-105">[stockage Premium Azure](../../../storage/common/storage-premium-storage.md) est la nouvelle génération de stockage qui offre une faible latence et un débit d'E/S élevé.</span><span class="sxs-lookup"><span data-stu-id="7f347-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is the next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="7f347-106">Il est particulièrement adapté aux principales charges de travail E/S intensives telles que SQL Server sur [des machines virtuelles](https://azure.microsoft.com/services/virtual-machines/)IaaS.</span><span class="sxs-lookup"><span data-stu-id="7f347-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f347-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7f347-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7f347-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="7f347-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7f347-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7f347-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="7f347-110">Cet article fournit une planification et des conseils pour la migration d'une machine virtuelle exécutant SQL Server afin d'utiliser le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server to use Premium Storage.</span></span> <span data-ttu-id="7f347-111">Cela inclut l'infrastructure Azure (mise en réseau, stockage) et les étapes de la machine virtuelle Windows hôte.</span><span class="sxs-lookup"><span data-stu-id="7f347-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="7f347-112">L’exemple de l’ [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) montre une migration complète de bout en bout de machines virtuelles plus importantes afin de tirer parti du stockage SSD local amélioré avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f347-112">The example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end to end migration of how to move larger VMs to take advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="7f347-113">Il est important de comprendre le processus complet d'utilisation du stockage Premium Azure avec SQL Server sur des machines virtuelles IAAS,</span><span class="sxs-lookup"><span data-stu-id="7f347-113">It is important to understand the end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="7f347-114">notamment :</span><span class="sxs-lookup"><span data-stu-id="7f347-114">This includes:</span></span>

* <span data-ttu-id="7f347-115">Identification de la configuration requise pour utiliser le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-115">Identification of the prerequisites to use Premium Storage.</span></span>
* <span data-ttu-id="7f347-116">Exemples de déploiement de SQL Server sur IaaS vers un stockage Premium pour les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="7f347-116">Examples of deploying SQL Server on IaaS to Premium Storage for new deployments.</span></span>
* <span data-ttu-id="7f347-117">Exemples de migration de déploiements existants, à la fois de serveurs autonomes et de déploiements à l’aide de groupes de disponibilité SQL Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="7f347-118">Approches de migration possibles.</span><span class="sxs-lookup"><span data-stu-id="7f347-118">Possible migration approaches.</span></span>
* <span data-ttu-id="7f347-119">Exemple complet présentant les étapes Azure, Windows et SQL Server pour la migration d’une implémentation Always On existante.</span><span class="sxs-lookup"><span data-stu-id="7f347-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for the migration of an existing Always On implementation.</span></span>

<span data-ttu-id="7f347-120">Pour plus de détails sur l’utilisation de SQL Server dans les machines virtuelles Azure, consultez la rubrique [SQL Server dans les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f347-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="7f347-121">**Auteur :** Daniel Sol **Réviseurs techniques :** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="7f347-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="7f347-122">Configuration requise pour le stockage Premium</span><span class="sxs-lookup"><span data-stu-id="7f347-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="7f347-123">Il existe plusieurs conditions préalables à l'utilisation du stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="7f347-124">Taille de la machine</span><span class="sxs-lookup"><span data-stu-id="7f347-124">Machine size</span></span>
<span data-ttu-id="7f347-125">Pour utiliser le stockage Premium, vous devrez utiliser des machines virtuelles (VM) de série DS.</span><span class="sxs-lookup"><span data-stu-id="7f347-125">For using Premium Storage you will need to use DS series Virtual Machines (VM).</span></span> <span data-ttu-id="7f347-126">Si vous n'avez jamais utilisé de machines de série DS dans votre service cloud, vous devez supprimer la machine virtuelle existante, conserver les disques connectés, puis créer un nouveau service cloud avant de recréer la machine virtuelle avec une taille de rôle DS*.</span><span class="sxs-lookup"><span data-stu-id="7f347-126">If you have not used DS Series machines in your cloud service before, you must delete the existing VM, keep the attached disks, and then create a new cloud service before recreating the VM as DS* role size.</span></span> <span data-ttu-id="7f347-127">Pour plus d’informations sur l’utilisation des tailles des machines virtuelles, consultez la rubrique [Tailles des machines virtuelles et des services cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f347-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="7f347-128">Services cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-128">Cloud services</span></span>
<span data-ttu-id="7f347-129">Vous pouvez uniquement utiliser des machines virtuelles DS* avec un stockage Premium si elles ont été créées dans un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="7f347-130">Si vous utilisez SQL Server Always On dans Azure, l’écouteur Always On fera référence à l’adresse IP de l’équilibreur de charge interne (ILB) ou de l’équilibreur de charge externe (ELB) Azure associée à un service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-130">If you are using SQL Server Always On in Azure, the Always On Listener will refer to the Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="7f347-131">Cet article explique comment effectuer la migration tout en conservant la disponibilité dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="7f347-131">This article focuses on how to migrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-132">Une série DS* doit être la première machine virtuelle déployée sur le nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-132">A DS* Series must be the first VM that is deployed to the new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="7f347-133">Réseaux virtuels régionaux</span><span class="sxs-lookup"><span data-stu-id="7f347-133">Regional VNETS</span></span>
<span data-ttu-id="7f347-134">Pour les machines virtuelles DS*, le réseau virtuel (VNET) qui héberge vos machines virtuelles doit être régional.</span><span class="sxs-lookup"><span data-stu-id="7f347-134">For DS* VMs you must configure the Virtual Network (VNET) hosting your VMs to be regional.</span></span> <span data-ttu-id="7f347-135">Cela « étend » le réseau virtuel pour permettre de configurer des machines virtuelles plus importantes dans d'autres clusters et établir la communication entre elles.</span><span class="sxs-lookup"><span data-stu-id="7f347-135">This “widens” the VNET is to allow the larger VMs to be provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="7f347-136">Dans la capture d'écran suivante, l'emplacement mis en surbrillance montre les réseaux virtuels régionaux, tandis que le premier résultat montre un réseau virtuel « étroit ».</span><span class="sxs-lookup"><span data-stu-id="7f347-136">In the following screenshot, the highlighted Location shows regional VNETs, whereas the first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="7f347-138">Vous pouvez soumettre un ticket de support Microsoft pour migrer vers un réseau virtuel régional ; Microsoft apportera une modification, finalisera la migration vers les réseaux virtuels régionaux, puis modifiera la propriété AffinityGroup dans la configuration du réseau.</span><span class="sxs-lookup"><span data-stu-id="7f347-138">You can raise a Microsoft support ticket to migrate to a regional VNET, Microsoft will make a change, then to complete the migration to regional VNETs, change the property AffinityGroup in the network configuration.</span></span> <span data-ttu-id="7f347-139">Exportez d’abord la configuration du réseau dans PowerShell, puis remplacez la propriété **AffinityGroup** de l’élément **VirtualNetworkSite** par une propriété **Location**.</span><span class="sxs-lookup"><span data-stu-id="7f347-139">First export the Network Configuration in PowerShell, and then replace the **AffinityGroup** property in the **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="7f347-140">Spécifiez `Location = XXXX` où `XXXX` est une région Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="7f347-141">Puis importez la nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="7f347-141">Then import the new configuration.</span></span>

<span data-ttu-id="7f347-142">Par exemple, si l'on considère la configuration de réseau virtuel suivante :</span><span class="sxs-lookup"><span data-stu-id="7f347-142">For example, considering the following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="7f347-143">Pour convertir cette configuration en un réseau virtuel régional en Europe de l'Ouest, modifiez la configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f347-143">To move this to a regional VNET in West Europe, change the configuration to the following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="7f347-144">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="7f347-144">Storage accounts</span></span>
<span data-ttu-id="7f347-145">Vous devrez créer un nouveau compte de stockage configuré pour le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-145">You will need to create a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="7f347-146">Notez que l'utilisation du stockage Premium est définie au niveau du compte de stockage et non des disques durs virtuels individuels ; mais lorsque vous utilisez une machine virtuelle de série DS*, vous pouvez connecter des disques durs virtuels à partir de comptes de stockage Premium et Standard.</span><span class="sxs-lookup"><span data-stu-id="7f347-146">Note that the use of Premium Storage is set at the storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="7f347-147">Cette méthode est recommandée si vous ne souhaitez pas placer le disque dur virtuel du système d'exploitation sur le compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-147">You may consider this if you do not want to place the OS VHD on to the Premium Storage account.</span></span>

<span data-ttu-id="7f347-148">La commande **New-AzureStorageAccountPowerShell** suivante avec le **Type** « Premium_LRS » crée un compte de stockage Premium :</span><span class="sxs-lookup"><span data-stu-id="7f347-148">The following **New-AzureStorageAccountPowerShell** command with the "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="7f347-149">Paramètres de cache des disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="7f347-149">VHDs Cache Settings</span></span>
<span data-ttu-id="7f347-150">La principale différence avec la création de disques faisant partie d'un compte de stockage Premium est le paramètre de cache des disques.</span><span class="sxs-lookup"><span data-stu-id="7f347-150">The main difference between creating disks that are part of a Premium Storage account is the disk cache setting.</span></span> <span data-ttu-id="7f347-151">Pour les disques de volume de données SQL Server, il est recommandé d’utiliser le paramètre de cache de lecture**Read Caching**.</span><span class="sxs-lookup"><span data-stu-id="7f347-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="7f347-152">Pour les volumes de journaux de transactions, le paramètre de cache des disques doit être défini sur**None**.</span><span class="sxs-lookup"><span data-stu-id="7f347-152">For Transaction log volumes, the disk cache setting should be set to ‘**None**’.</span></span> <span data-ttu-id="7f347-153">Il s'agit d'une différence par rapport aux recommandations pour les comptes de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="7f347-153">This is different from the recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="7f347-154">Une fois les disques durs virtuels connectés, le paramètre de cache ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="7f347-154">Once the VHDs have been attached, the cache setting cannot be altered.</span></span> <span data-ttu-id="7f347-155">Vous devez déconnecter puis reconnecter le disque dur virtuel avec un paramètre de cache mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7f347-155">You would need to detach and reattach the VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="7f347-156">Espaces de stockage Windows</span><span class="sxs-lookup"><span data-stu-id="7f347-156">Windows storage spaces</span></span>
<span data-ttu-id="7f347-157">Vous pouvez utiliser les [espaces de stockage Windows](https://technet.microsoft.com/library/hh831739.aspx) comme vous l'avez fait avec le système de stockage Standard précédent pour migrer une machine virtuelle qui utilise déjà des espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="7f347-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you to migrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="7f347-158">L'exemple de l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (étape 9 et suivantes) montre le code Powershell pour extraire et importer une machine virtuelle comportant plusieurs disques durs virtuels connectés.</span><span class="sxs-lookup"><span data-stu-id="7f347-158">The example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates the Powershell code to extract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="7f347-159">Des pools de stockage avaient été utilisés avec un compte de stockage Azure Standard pour améliorer le débit et de réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="7f347-159">Storage Pools were used with Standard Azure storage account to enhance throughput and reduce latency.</span></span> <span data-ttu-id="7f347-160">Vous trouverez peut-être utile de tester des pools de stockage avec un stockage Premium pour les nouveaux déploiements, mais notez que ces tests compliquent la configuration du stockage.</span><span class="sxs-lookup"><span data-stu-id="7f347-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-to-find-which-azure-virtual-disks-map-to-storage-pools"></a><span data-ttu-id="7f347-161">Identification des disques virtuels Azure à mapper aux pools de stockage</span><span class="sxs-lookup"><span data-stu-id="7f347-161">How to find which Azure Virtual Disks map to storage pools</span></span>
<span data-ttu-id="7f347-162">Comme il existe différents paramètres de cache pour les disques durs virtuels connectés, vous pouvez décider de copier les disques durs virtuels sur un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-162">As there are different cache setting recommendations for attached VHDs, you might decide to copy the VHDs to a Premium Storage account.</span></span> <span data-ttu-id="7f347-163">Toutefois, lorsque vous les reconnectez à la nouvelle machine virtuelle de série DS, vous devrez peut-être modifier les paramètres du cache.</span><span class="sxs-lookup"><span data-stu-id="7f347-163">However, when you reattach them to the new DS series VM, you might need to alter the cache settings.</span></span> <span data-ttu-id="7f347-164">Il est plus simple d'appliquer les paramètres de cache du stockage Premium recommandés si vous utilisez des disques durs virtuels distincts pour les fichiers de données SQL et les fichiers journaux (plutôt qu'un seul disque dur virtuel regroupant le tout).</span><span class="sxs-lookup"><span data-stu-id="7f347-164">It is simpler to apply the Premium Storage recommended cache settings when you have separate VHDs for the SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-165">Si vous avez des fichiers de données SQL Server et des fichiers journaux sur le même volume, l'option de mise en cache que vous choisissez dépend des modèles d'accès E/S pour vos charges de travail de base de données.</span><span class="sxs-lookup"><span data-stu-id="7f347-165">If you have SQL Server data and log files on the same volume, the caching option you choose depends on the IO access patterns for your database workloads.</span></span> <span data-ttu-id="7f347-166">Seuls des tests permettent d'identifier l'option de mise en cache la mieux adaptée à ce scénario.</span><span class="sxs-lookup"><span data-stu-id="7f347-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="7f347-167">Toutefois, si vous utilisez des espaces de stockage Windows composé de plusieurs disques durs virtuels, vous devrez examiner vos scripts d’origine pour identifier quels disques durs virtuels figurent dans un pool spécifique afin de définir ensuite les paramètres du cache pour chaque disque.</span><span class="sxs-lookup"><span data-stu-id="7f347-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need to look at your original scripts to identify which attached VHDs are in what specific pool, so you can then set the cache settings accordingly for each disk.</span></span>

<span data-ttu-id="7f347-168">Si vous n'avez pas de script d'origine disponible pour afficher les disques durs virtuels mappés au pool de stockage, vous pouvez utiliser les étapes suivantes pour déterminer le mappage de pool de stockage/disque.</span><span class="sxs-lookup"><span data-stu-id="7f347-168">If you do not have original script available to show you which VHDs map to the storage pool, you can use the following steps to determine the disk/storage pool mapping.</span></span>

<span data-ttu-id="7f347-169">Pour chaque disque, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f347-169">For each disk, use the following steps:</span></span>

1. <span data-ttu-id="7f347-170">Affichez la liste des disques connectés à la machine virtuelle à l'aide de la commande **Get-AzureVM** :</span><span class="sxs-lookup"><span data-stu-id="7f347-170">Get list of disks attached to VM with the **Get-AzureVM** command:</span></span>

    <span data-ttu-id="7f347-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="7f347-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="7f347-172">Notez le nom du disque et le LUN.</span><span class="sxs-lookup"><span data-stu-id="7f347-172">Note the Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="7f347-174">Bureau à distance dans la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-174">Remote desktop into the VM.</span></span> <span data-ttu-id="7f347-175">Accédez ensuite à **Gestion de l’ordinateur** | **Gestionnaire de périphériques** | **Lecteurs de disque**.</span><span class="sxs-lookup"><span data-stu-id="7f347-175">Then go to **Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="7f347-176">Examinez les propriétés de chacun  des « disques virtuels Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="7f347-176">Look at the properties of each of the ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="7f347-178">Ici, le numéro LUN désigne le numéro LUN que vous spécifiez lors de la connexion du disque dur virtuel à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-178">The LUN number here is a reference to the LUN number you specify when attaching the VHD to the VM.</span></span>
5. <span data-ttu-id="7f347-179">Pour le « disque virtuel Microsoft », accédez à l’onglet **Détails**, puis dans la liste **Propriété**, accédez à **Clé pilote**.</span><span class="sxs-lookup"><span data-stu-id="7f347-179">For the ‘Microsoft Virtual Disk’ go to the **Details** tab, then in the **Property** list, go to **Driver Key**.</span></span> <span data-ttu-id="7f347-180">Dans la zone **Valeur**, notez le **décalage**, c’est-à-dire 0002 dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="7f347-180">In the **Value**, note the **Offset**, which is 0002 in the following screenshot.</span></span> <span data-ttu-id="7f347-181">La valeur 0002 indique l'élément PhysicalDisk2 auquel le pool de stockage fait référence.</span><span class="sxs-lookup"><span data-stu-id="7f347-181">The 0002 denotes the PhysicalDisk2 that the storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="7f347-183">Pour chaque pool de stockage, videz les disques associés :</span><span class="sxs-lookup"><span data-stu-id="7f347-183">For each storage pool, dump out the associated disks:</span></span>

    <span data-ttu-id="7f347-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="7f347-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="7f347-186">Vous pouvez désormais utiliser ces informations pour associer des disques durs virtuels connectés aux disques physiques dans les pools de stockage.</span><span class="sxs-lookup"><span data-stu-id="7f347-186">Now you can use this information to associate attached VHDs to Physical Disks in Storage Pools.</span></span>

<span data-ttu-id="7f347-187">Une fois que vous avez mappé les disques durs virtuels aux disques physiques dans les pools de stockage, vous pouvez les déconnecter et les copier vers un compte de stockage Premium, puis les connecter en utilisant le paramètre de cache approprié.</span><span class="sxs-lookup"><span data-stu-id="7f347-187">Once you have mapped VHDs to Physical Disks in Storage Pools you can then detach and copy them over to a Premium Storage account, then attach them with the correct cache setting.</span></span> <span data-ttu-id="7f347-188">Consultez les étapes 8 à 12 de l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-188">Please see the example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="7f347-189">Ces étapes indiquent comment extraire dans un fichier CSV une configuration de disque de disque dur virtuel connecté à une machine virtuelle, copier les disques durs virtuels, modifier les paramètres de cache de la configuration de disque, puis redéployer la machine virtuelle comme machine virtuelle de série DS avec tous les disques connectés.</span><span class="sxs-lookup"><span data-stu-id="7f347-189">These steps show how to extract a VM-attached VHD disk configuration to a CSV file, copy the VHDs, alter the disk configuration cache settings, and finally redeploy the VM as a DS series VM with all the attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="7f347-190">Bande passante de stockage de la machine virtuelle et débit de stockage du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="7f347-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="7f347-191">Les performances de stockage dépendent de la taille de la machine virtuelle DS* spécifiée et des tailles des disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="7f347-191">The amount of storage performance depends on the DS* VM size specified and the VHD sizes.</span></span> <span data-ttu-id="7f347-192">Les machines virtuelles offrent différentes tolérances pour le nombre de disques durs virtuels peuvent être connectés et la bande passante maximale prise en charge (Mo/s).</span><span class="sxs-lookup"><span data-stu-id="7f347-192">The VMs have different allowances for the number of VHDs that can be attached and the maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="7f347-193">Pour connaître les numéros de bande passante spécifiques, consultez la rubrique [Tailles des machines virtuelles et des services cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f347-193">For the specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7f347-194">Les disques de plus grande taille augmentent le nombre d'opérations d'E/S par seconde.</span><span class="sxs-lookup"><span data-stu-id="7f347-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="7f347-195">Vous devez en tenir compte lorsque vous étudiez votre chemin de migration.</span><span class="sxs-lookup"><span data-stu-id="7f347-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="7f347-196">Pour plus d’informations, [consultez le tableau des opérations d’E/S et des types de disque](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="7f347-196">For details, [see the table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="7f347-197">Enfin, notez que les machines virtuelles prennent en charge différentes bandes passantes maximales pour tous les disques connectés.</span><span class="sxs-lookup"><span data-stu-id="7f347-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="7f347-198">Sous une charge élevée, vous risquez de saturer la bande passante de disque maximale disponible pour cette taille de rôle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-198">Under high load, you could saturate the maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="7f347-199">Par exemple un disque Standard_DS14 prendra en charge jusqu'à 512 Mo/s ; par conséquent, avec trois disques P30, vous pourriez saturer la bande passante de disque de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-199">For example a Standard_DS14 will support up to 512MB/s; therefore, with three P30 disks you could saturate the disk bandwidth of the VM.</span></span> <span data-ttu-id="7f347-200">Mais dans cet exemple, la limite de débit peut être dépassée selon la combinaison d'opérations d'E/S en lecture et écriture.</span><span class="sxs-lookup"><span data-stu-id="7f347-200">But in this example, the throughput limit could be exceeded depending on the mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="7f347-201">Nouveaux déploiements</span><span class="sxs-lookup"><span data-stu-id="7f347-201">New deployments</span></span>
<span data-ttu-id="7f347-202">Les deux sections suivantes montrent comment déployer des machines virtuelles SQL Server dans un stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-202">The next two sections demonstrate how you can deploy SQL Server VMs to Premium Storage.</span></span> <span data-ttu-id="7f347-203">Comme mentionné précédemment, il est inutile de placer le disque du système d'exploitation sur un stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-203">As mentioned before, you do not necessarily need to place the OS disk onto Premium storage.</span></span> <span data-ttu-id="7f347-204">Vous pouvez choisir de le faire si vous avez l'intention de placer des charges de travail d'E/S intensives sur le disque dur virtuel du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="7f347-204">You might choose to do this if you are intending to place any intensive IO workloads on the OS VHD.</span></span>

<span data-ttu-id="7f347-205">Le premier exemple montre l'utilisation d'images de galerie Azure existantes.</span><span class="sxs-lookup"><span data-stu-id="7f347-205">The first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="7f347-206">Le deuxième exemple montre l'utilisation d'une image de machine virtuelle personnalisée stockée dans un compte de stockage Standard existant.</span><span class="sxs-lookup"><span data-stu-id="7f347-206">The second example shows how to use a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-207">Ces exemples supposent que vous avez déjà créé un réseau virtuel régional.</span><span class="sxs-lookup"><span data-stu-id="7f347-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="7f347-208">Création d'une nouvelle machine virtuelle avec un stockage Premium et une image de galerie</span><span class="sxs-lookup"><span data-stu-id="7f347-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="7f347-209">L'exemple suivant montre comment placer le disque dur virtuel du système d'exploitation sur un stockage Premium et comment connecter les disques durs virtuels de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-209">The example below shows how to place the OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="7f347-210">Toutefois, vous pouvez également placer le disque du système d'exploitation sur un compte de stockage Standard puis connecter les disques durs virtuels qui résident sur un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-210">However, you can also place the OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="7f347-211">Ces deux scénarios sont présentés.</span><span class="sxs-lookup"><span data-stu-id="7f347-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="7f347-212">Étape 1 : création d'un compte de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="7f347-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="7f347-213">Étape 2 : création d'un nouveau service cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="7f347-214">Étape 3 : réservation d'une adresse IP virtuelle de service cloud (facultatif)</span><span class="sxs-lookup"><span data-stu-id="7f347-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="7f347-215">Étape 4 : création d'un conteneur de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="7f347-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="7f347-216">Étape 5 : placement du disque dur virtuel du système d'exploitation sur Standard ou Premium stockage</span><span class="sxs-lookup"><span data-stu-id="7f347-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used to place the OS VHD in

    #If you want to place the OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted to place the OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="7f347-217">Étape 6 : création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7f347-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from the Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember to change to DS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks to VM Config
    #Note the size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising the Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-to-use-premium-storage-with-a-custom-image"></a><span data-ttu-id="7f347-218">Création d’une machine virtuelle pour utiliser Premium Storage avec une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="7f347-218">Create a new VM to use Premium Storage with a custom image</span></span>
<span data-ttu-id="7f347-219">Ce scénario vous montre où sont placées les images personnalisées existantes qui résident sur un compte de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="7f347-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="7f347-220">Comme mentionné, si vous souhaitez placer le disque dur virtuel du système d'exploitation sur un stockage Premium, vous devez copier l'image existante sur le compte de stockage Standard et la transférer vers un stockage Premium pour pouvoir l'utiliser.</span><span class="sxs-lookup"><span data-stu-id="7f347-220">As mentioned if you want to place the OS VHD on Premium Storage you will need to copy the image that exists in the Standard Storage account and transfer them to a Premium Storage before it can be used.</span></span> <span data-ttu-id="7f347-221">Si vous disposez d’une image locale, vous pouvez également utiliser cette méthode pour la copier directement sur le compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-221">If you have an image on-premises, you can also use this method to copy that directly to the Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="7f347-222">Étape 1 : création d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="7f347-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="7f347-223">Étape 2 : création d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="7f347-224">Étape 3 : utilisation d’une image existante</span><span class="sxs-lookup"><span data-stu-id="7f347-224">Step 3: Use existing image</span></span>
<span data-ttu-id="7f347-225">Vous pouvez utiliser une image existante.</span><span class="sxs-lookup"><span data-stu-id="7f347-225">You can use an existing image.</span></span> <span data-ttu-id="7f347-226">Vous pouvez [prendre l’image d’une machine existante](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f347-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="7f347-227">Notez que cette machine n’a pas besoin d’être une machine DS\*.</span><span class="sxs-lookup"><span data-stu-id="7f347-227">Note the machine you image does not have to be DS* machine.</span></span> <span data-ttu-id="7f347-228">Une fois l’image créée, appliquez les étapes suivantes, qui montrent comment la copier dans le compte Stockage Premium à l’aide de l’applet de commande PowerShell **Start-AzureStorageBlobCopy**.</span><span class="sxs-lookup"><span data-stu-id="7f347-228">Once you have the image, the following steps show how to copy it to the Premium Storage account with the **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for the storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="7f347-229">Étape 4: copie d'objets Blob entre des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="7f347-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="7f347-230">Étape 5 : vérification régulière de l'état de la copie :</span><span class="sxs-lookup"><span data-stu-id="7f347-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-to-azure-disk-repository-in-subscription"></a><span data-ttu-id="7f347-231">Étape 6 : ajout d’un disque d’image au référentiel de disque Azure dans l’abonnement</span><span class="sxs-lookup"><span data-stu-id="7f347-231">Step 6: Add Image disk to Azure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="7f347-232">Il est possible que même si l'état indique que l'opération a réussi, une erreur de bail de disque s'affiche.</span><span class="sxs-lookup"><span data-stu-id="7f347-232">You may find that even though the status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="7f347-233">Dans ce cas, attendez 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="7f347-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-the-vm"></a><span data-ttu-id="7f347-234">Étape 7 : création de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7f347-234">Step 7:  Build the VM</span></span>
<span data-ttu-id="7f347-235">Ici, vous créez la machine virtuelle à partir de votre image et connectez deux disques durs virtuels de stockage Premium :</span><span class="sxs-lookup"><span data-stu-id="7f347-235">Here you are building the VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need to be a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use to DS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="7f347-236">Déploiements existants qui n’utilisent pas les groupes de disponibilité Always On</span><span class="sxs-lookup"><span data-stu-id="7f347-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="7f347-237">Pour des déploiements existants, voir tout d’abord la section [Conditions préalables](#prerequisites-for-premium-storage) de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="7f347-237">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="7f347-238">Il existe différents points à prendre en compte concernant les déploiements SQL Server qui utilisent ou non des groupes de disponibilité Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="7f347-239">Si vous n’utilisez pas Always On et que vous disposez d’un serveur SQL Server autonome, vous pouvez effectuer une mise à niveau vers Premium Storage à l’aide d’un nouveau service cloud et d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7f347-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade to Premium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="7f347-240">Examinez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7f347-240">Consider the following options:</span></span>

* <span data-ttu-id="7f347-241">**Créez une nouvelle machine virtuelle SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7f347-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="7f347-242">Vous pouvez créer une nouvelle machine virtuelle SQL qui utilise un compte de stockage Premium comme décrit dans les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="7f347-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="7f347-243">Ensuite, sauvegardez et restaurez votre configuration SQL Server et vos bases de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7f347-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="7f347-244">L'application devra être mise à jour pour référencer la nouvelle configuration SQL Server si elle accessible de façon interne ou externe.</span><span class="sxs-lookup"><span data-stu-id="7f347-244">The application will need to be updated to reference the new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="7f347-245">Vous devez copier tous les objets 'out of db' comme si vous effectuiez une migration SQL Server de type Side by Side (SxS).</span><span class="sxs-lookup"><span data-stu-id="7f347-245">You would need to copy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="7f347-246">Cela inclut des objets tels que les connexions, les certificats et les serveurs liés.</span><span class="sxs-lookup"><span data-stu-id="7f347-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="7f347-247">**Migrez une machine virtuelle SQL Server existante**.</span><span class="sxs-lookup"><span data-stu-id="7f347-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="7f347-248">Cette opération exige la déconnexion de la machine virtuelle SQL Server, puis son transfert vers un nouveau service cloud, y compris la copie de tous ses disques durs virtuels connectés au compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-248">This will require taking the SQL Server VM offline, then transferring it to a new cloud service, which includes copying all of its attached VHDs to the Premium Storage account.</span></span> <span data-ttu-id="7f347-249">Lorsque la machine virtuelle est mise en ligne, l'application référencera le nom d'hôte du serveur comme avant.</span><span class="sxs-lookup"><span data-stu-id="7f347-249">When the VM comes online, the application will reference the server host name as before.</span></span> <span data-ttu-id="7f347-250">N'oubliez pas que la taille du disque existant affectera les performances.</span><span class="sxs-lookup"><span data-stu-id="7f347-250">Be aware that the size of the existing disk will affect the performance characteristics.</span></span> <span data-ttu-id="7f347-251">Par exemple, un disque de 400 Go correspond à un disque P20.</span><span class="sxs-lookup"><span data-stu-id="7f347-251">For example, a 400 GB disk gets rounded up to a P20.</span></span> <span data-ttu-id="7f347-252">Si vous savez que vous n'avez pas besoin de telles performances, vous pouvez recréer la machine virtuelle comme une machine virtuelle de série DS et connecter des disques durs virtuels de stockage Premium offrant la taille ou les performances requises.</span><span class="sxs-lookup"><span data-stu-id="7f347-252">If you know that you do not require that disk performance, then you could recreate the VM as a DS Series VM, and attach Premium Storage VHDs of the size/performance specification you require.</span></span> <span data-ttu-id="7f347-253">Vous pouvez ensuite déconnecter puis reconnecter les fichiers de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7f347-253">Then you could detach and reattach the SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-254">Lors de la copie de disques durs virtuels, tenez compte de la taille car ce paramètre détermine le type de disque de stockage Premium correspondant, et donc les performances du disque.</span><span class="sxs-lookup"><span data-stu-id="7f347-254">When copying the VHD disks you should be aware of the size, depending on the size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="7f347-255">Comme Azure utilisera le disque le plus proche, si vous avez un disque de 400 Go, ce sera un disque de type P20.</span><span class="sxs-lookup"><span data-stu-id="7f347-255">Azure will round up to the nearest disk size, so if you have a 400GB disk, this will be rounded up to a P20.</span></span> <span data-ttu-id="7f347-256">Selon les besoins d'E/S existants du disque dur virtuel du système d'exploitation, vous n'aurez peut-être pas besoin de migrer vers un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-256">Depending on your existing IO requirements of the OS VHD, you might not need to migrate this to a Premium Storage account.</span></span>
>
>

<span data-ttu-id="7f347-257">Si votre serveur SQL Server est accessible en externe, l'adresse IP virtuelle du service cloud changera.</span><span class="sxs-lookup"><span data-stu-id="7f347-257">If your SQL Server is accessed externally, then the cloud service VIP will change.</span></span> <span data-ttu-id="7f347-258">Vous devez également mettre à jour les points de terminaison, les listes de contrôle d’accès (ACL) et les paramètres DNS.</span><span class="sxs-lookup"><span data-stu-id="7f347-258">You will also have to update end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="7f347-259">Déploiements existants qui utilisent les groupes de disponibilité Always On</span><span class="sxs-lookup"><span data-stu-id="7f347-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="7f347-260">Pour des déploiements existants, voir tout d’abord la section [Conditions préalables](#prerequisites-for-premium-storage) de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="7f347-260">For existing deployments, first see the [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="7f347-261">Dans cette section, nous examinons la façon dont le groupe de disponibilité Always On interagit avec la mise en réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="7f347-262">Nous décomposerons ensuite les migrations en deux scénarios : les migrations où une interruption de service est tolérée, et celles où vous devez limiter au maximum les temps d'arrêt.</span><span class="sxs-lookup"><span data-stu-id="7f347-262">We will then break down migrations in to two scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="7f347-263">Les groupes locaux de disponibilité Always On SQL Server utilisent un écouteur local qui inscrit un nom DNS virtuel ainsi qu’une adresse IP partagée entre un ou plusieurs serveurs SQL.</span><span class="sxs-lookup"><span data-stu-id="7f347-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="7f347-264">Lorsque les clients se connectent, ils sont dirigés via l'IP de l'écouteur vers le serveur SQL principal.</span><span class="sxs-lookup"><span data-stu-id="7f347-264">When clients connect they are routed through the listener IP to the Primary SQL Server.</span></span> <span data-ttu-id="7f347-265">À ce stade, il s’agit du serveur qui possède la ressource IP Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-265">This is the server that owns the Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="7f347-267">Dans Microsoft Azure, vous ne pouvez attribuer qu'une seule adresse IP à une carte réseau sur la machine virtuelle ; par conséquent, pour atteindre la même couche d'abstraction qu'en local, Azure utilise l'adresse IP attribuée aux équilibreurs de charge internes/externes (ILB/ELB).</span><span class="sxs-lookup"><span data-stu-id="7f347-267">In Microsoft Azure you can have only one IP address assigned to a NIC on the VM, so in order to achieve the same layer of abstraction as on-premises, Azure utilizes the IP address that is assigned to the Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="7f347-268">La ressource IP partagée entre les serveurs est définie sur la même adresse IP que l'ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="7f347-268">The IP resource that is shared between the servers is set to the same IP as the ILB/ELB.</span></span> <span data-ttu-id="7f347-269">Il est publié dans le DNS, et le trafic client est transmis via l'ILB/ELB au réplica SQL Server principal.</span><span class="sxs-lookup"><span data-stu-id="7f347-269">This is published in the DNS, and client traffic is passed through the ILB/ELB to the Primary SQL Server replica.</span></span> <span data-ttu-id="7f347-270">L’ILB/ELB sait identifier le serveur SQL principal, puisqu’il utilise des sondes pour détecter la ressource IP Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-270">The ILB/ELB knows which SQL Server is primary since it uses probes to probe the Always On IP resource.</span></span> <span data-ttu-id="7f347-271">Dans l'exemple précédent, il teste chaque nœud comportant un point de terminaison référencé par l'ELB/ILB, et celui qui répond est le serveur SQL principal.</span><span class="sxs-lookup"><span data-stu-id="7f347-271">In the previous example, it probes each node that has an endpoint referenced by the ELB/ILB, whichever responds is the Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-272">L'ILB et l'ELB sont affectés à un service cloud Azure particulier et par conséquent, toute migration de cloud dans Azure impliquera probablement le changement de l'adresse IP de l'équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="7f347-272">The ILB and ELB are both assigned to a particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that the Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="7f347-273">Migration de déploiements Always On autorisant des temps d’arrêt</span><span class="sxs-lookup"><span data-stu-id="7f347-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="7f347-274">Il existe deux stratégies de migration de déploiements Always On qui autorisent des temps d’arrêt :</span><span class="sxs-lookup"><span data-stu-id="7f347-274">There are two strategies to migrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="7f347-275">**Ajouter plusieurs réplicas secondaires à un cluster Always On existant**</span><span class="sxs-lookup"><span data-stu-id="7f347-275">**Add more secondary replicas to an existing Always On Cluster**</span></span>
2. <span data-ttu-id="7f347-276">**Effectuer la migration vers un nouveau cluster Always On**</span><span class="sxs-lookup"><span data-stu-id="7f347-276">**Migrate to a new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-to-an-existing-always-on-cluster"></a><span data-ttu-id="7f347-277">1. Ajouter plusieurs réplicas secondaires à un cluster Always On existant</span><span class="sxs-lookup"><span data-stu-id="7f347-277">1. Add more Secondary Replicas to an Existing Always On Cluster</span></span>
<span data-ttu-id="7f347-278">Une stratégie consiste à ajouter plusieurs serveurs secondaires au groupe de disponibilité Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-278">One strategy is to add more secondaries to the Always On Availability Group.</span></span> <span data-ttu-id="7f347-279">Vous devez ajouter ces réplicas à un nouveau service cloud et mettre à jour l'écouteur avec la nouvelle adresse IP de l'équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="7f347-279">You need to add these into a new cloud service and update the listener with the new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="7f347-280">Points d’arrêt :</span><span class="sxs-lookup"><span data-stu-id="7f347-280">Points of downtime:</span></span>
* <span data-ttu-id="7f347-281">Validation de cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-281">Cluster Validation.</span></span>
* <span data-ttu-id="7f347-282">Test des basculements Always On de nouveaux réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="7f347-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="7f347-283">Si vous utilisez des pools de stockage Windows au sein de la machine virtuelle pour augmenter le débit d'E/S, ces pools seront mis hors ligne pendant une validation complète de cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-283">If you are using Windows Storage Pools within the VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="7f347-284">Le test de validation est requis lorsque vous ajoutez des nœuds au cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-284">The validation test is required when you add nodes to the cluster.</span></span> <span data-ttu-id="7f347-285">Le temps nécessaire à l'exécution du test peut varier ; vous devez donc tester le cluster dans votre environnement de test représentatif pour obtenir une durée approximative de la durée de cette opération.</span><span class="sxs-lookup"><span data-stu-id="7f347-285">The time it takes to run the test can vary, so you should test this in your representative test environment to get an approximate time of how long this will take.</span></span>

<span data-ttu-id="7f347-286">Vous devez prévoir suffisamment de temps pour effectuer un basculement manuel et un test CHAOS sur les nœuds récemment ajoutés pour vérifier que la haute disponibilité Always On fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="7f347-286">You should provision time where you can perform manual failover and chaos testing on the newly added nodes to ensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="7f347-288">Avant d’effectuer la validation, vous devez arrêter toutes les instances de SQL Server qui utilisent les pools de stockage.</span><span class="sxs-lookup"><span data-stu-id="7f347-288">You should stop all instances of SQL Server where the Storage Pools are used before the Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="7f347-289">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="7f347-289">High-level steps</span></span>
>

1. <span data-ttu-id="7f347-290">Créez deux serveurs SQL dans le nouveau service cloud avec une connexion au stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="7f347-291">Copiez les sauvegardes complètes et effectuez une restauration avec **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="7f347-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="7f347-292">Copiez les objets dépendants 'out of user DB', notamment que les connexions.</span><span class="sxs-lookup"><span data-stu-id="7f347-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="7f347-293">Créez un nouvel équilibreur de charge interne (ILB) ou utilisez un équilibreur de charge externe (ELB), puis configurez ensuite les points de terminaison d'équilibrage de charge sur les deux nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="7f347-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7f347-294">Vérifiez que la configuration du point de terminaison est correcte pour tous les nœuds avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="7f347-294">Check all Nodes have the correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="7f347-295">Arrêtez l'accès de l'utilisateur/application à SQL Server (si vous utilisez des pools de stockage).</span><span class="sxs-lookup"><span data-stu-id="7f347-295">Stop User/Application Access to the SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="7f347-296">Arrêtez les services du moteur SQL Server sur tous les nœuds (si vous utilisez des pools de stockage).</span><span class="sxs-lookup"><span data-stu-id="7f347-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="7f347-297">Ajoutez de nouveaux nœuds de cluster et effectuez la validation complète.</span><span class="sxs-lookup"><span data-stu-id="7f347-297">Add new Nodes to cluster and run full validation.</span></span>
8. <span data-ttu-id="7f347-298">Une fois la validation réussie, démarrez tous les services SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7f347-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="7f347-299">Sauvegardez les journaux des transactions et restaurez les bases de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7f347-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="7f347-300">Ajoutez de nouveaux nœuds au groupe de disponibilité Always On et définissez la réplication sur **Synchrone**.</span><span class="sxs-lookup"><span data-stu-id="7f347-300">Add new nodes into the Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="7f347-301">Ajoutez la ressource d’adresse IP de l’ILB/ELB du nouveau service cloud par le biais de PowerShell pour Always On en fonction de l’exemple multisite de [l’annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-301">Add the IP address resource of the new Cloud Service ILB/ELB through PowerShell for Always On based on the Multi-site example in the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="7f347-302">Dans le clustering Windows, définissez les **propriétaires possibles** de la ressource d’**adresse IP** sur les nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="7f347-302">In Windows clustering, set the **Possible owners** of the **IP Address** resource to the new nodes old.</span></span> <span data-ttu-id="7f347-303">Consultez la section « Ajout d'une ressource d'adresse IP sur le même sous-réseau » de l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-303">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="7f347-304">Basculement vers un des nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="7f347-304">Failover to one of the new nodes.</span></span>
13. <span data-ttu-id="7f347-305">Configurez les nouveaux nœuds en tant que partenaires de basculement automatique puis testez les basculements.</span><span class="sxs-lookup"><span data-stu-id="7f347-305">Make the new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="7f347-306">Supprimez les nœuds d'origine du groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="7f347-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="7f347-307">Avantages</span><span class="sxs-lookup"><span data-stu-id="7f347-307">Advantages</span></span>
* <span data-ttu-id="7f347-308">Les nouveaux serveurs SQL peuvent être testés (SQL Server et application) avant d’être ajoutés à Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-308">New SQL Servers can be tested (SQL Server and Application) before they are added to Always On.</span></span>
* <span data-ttu-id="7f347-309">Vous pouvez modifier la taille de la machine virtuelle et personnaliser le stockage exactement selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7f347-309">You can change the VM size and customize the storage to your exact requirements.</span></span> <span data-ttu-id="7f347-310">Mais il serait préférable de conserver tous les chemins vers les fichiers SQL.</span><span class="sxs-lookup"><span data-stu-id="7f347-310">However, it would be beneficial to keep all the SQL file paths the same.</span></span>
* <span data-ttu-id="7f347-311">Vous pouvez contrôler le démarrage du transfert des sauvegardes de base de données pour les réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="7f347-311">You can control when the transfer of the DB backups to the Secondary Replicas are started.</span></span> <span data-ttu-id="7f347-312">Cela diffère de l'utilisation de l'applet de commande Azure **Start-AzureStorageBlobCopy** pour copier des disques durs virtuels car il s'agit d'une copie asynchrone.</span><span class="sxs-lookup"><span data-stu-id="7f347-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet to copy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="7f347-313">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="7f347-313">Disadvantages</span></span>
* <span data-ttu-id="7f347-314">Lorsque vous utilisez des pools de stockage Windows, un temps d'arrêt se produit au niveau du cluster lors de la validation complète du cluster pour les nouveaux nœuds supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="7f347-314">When using Windows Storage Pools, there is Cluster downtime during the Full Cluster Validation for the new additional nodes.</span></span>
* <span data-ttu-id="7f347-315">En fonction de la version SQL Server et du nombre de réplicas secondaires existants, vous ne pourrez peut-être pas ajouter plusieurs réplicas secondaires sans supprimer des réplicas secondaires existants.</span><span class="sxs-lookup"><span data-stu-id="7f347-315">Depending on the SQL Server Version and the existing number of secondary replicas, you might not be able to add more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="7f347-316">Le transfert des données SQL peut prendre du temps lors de la configuration des réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="7f347-316">There could be long SQL data transfer time while setting up the secondaries.</span></span>
* <span data-ttu-id="7f347-317">Pendant la migration, l’exécution de nouvelles machines en parallèle entraîne un coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="7f347-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-to-a-new-always-on-cluster"></a><span data-ttu-id="7f347-318">2. Effectuer la migration vers un nouveau cluster Always On</span><span class="sxs-lookup"><span data-stu-id="7f347-318">2. Migrate to a new Always On Cluster</span></span>
<span data-ttu-id="7f347-319">Une autre stratégie consiste à créer un tout nouveau cluster Always On avec de nouveaux nœuds dans le nouveau service cloud en incitant les clients à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="7f347-319">Another strategy is to create a brand new Always On Cluster with brand new nodes in new cloud service and then redirect the clients to use it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="7f347-320">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="7f347-320">Points of downtime</span></span>
<span data-ttu-id="7f347-321">Un temps d’arrêt se produit lorsque vous transférez des applications et des utilisateurs vers le nouvel écouteur Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-321">There is downtime when you transfer applications and users to the new Always On listener.</span></span> <span data-ttu-id="7f347-322">Ce temps d'arrêt dépend des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7f347-322">The downtime depends on:</span></span>

* <span data-ttu-id="7f347-323">Le temps nécessaire pour restaurer les sauvegardes du journal des transactions final aux bases de données sur les nouveaux serveurs.</span><span class="sxs-lookup"><span data-stu-id="7f347-323">The time taken to restore final transaction log backups to databases on new servers.</span></span>
* <span data-ttu-id="7f347-324">Le temps nécessaire pour mettre à jour les applications clientes afin d’utiliser le nouvel écouteur Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-324">The time taken to update client applications to use new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="7f347-325">Avantages</span><span class="sxs-lookup"><span data-stu-id="7f347-325">Advantages</span></span>
* <span data-ttu-id="7f347-326">Vous pouvez tester l'environnement de production réel, SQL Server, et les modifications apportées à la build du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="7f347-326">You can test the actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="7f347-327">Vous avez la possibilité de personnaliser le stockage et de réduire la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7f347-327">You have the option to customize the storage and to potentially reduce size of VM.</span></span> <span data-ttu-id="7f347-328">Cela pourrait entraîner une réduction des coûts.</span><span class="sxs-lookup"><span data-stu-id="7f347-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="7f347-329">Vous pouvez mettre à jour votre build ou version SQL Server pendant ce processus.</span><span class="sxs-lookup"><span data-stu-id="7f347-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="7f347-330">Vous pouvez également mettre à niveau le système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="7f347-330">You can also upgrade the Operating System.</span></span>
* <span data-ttu-id="7f347-331">Le cluster Always On précédent peut servir de cible de restauration solide.</span><span class="sxs-lookup"><span data-stu-id="7f347-331">The previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="7f347-332">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="7f347-332">Disadvantages</span></span>
* <span data-ttu-id="7f347-333">Vous devez modifier le nom DNS de l’écouteur si vous souhaitez exécuter les deux clusters Always On simultanément.</span><span class="sxs-lookup"><span data-stu-id="7f347-333">You need to change the DNS name of the listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="7f347-334">Cela ajoute une surcharge administrative lors de la migration car les chaînes de l'application cliente doivent refléter le nouveau nom de l'écouteur.</span><span class="sxs-lookup"><span data-stu-id="7f347-334">This adds administration overhead during the migration as client application strings must reflect the new Listener name.</span></span>
* <span data-ttu-id="7f347-335">Vous devez mettre en œuvre un mécanisme de synchronisation entre les deux environnements afin de les garder aussi proches que possible et réduire ainsi les exigences de synchronisation finale avant la migration.</span><span class="sxs-lookup"><span data-stu-id="7f347-335">You must implement a synchronization mechanism between the two environments to keep them as close as possible to minimize the final synchronization requirements before migration.</span></span>
* <span data-ttu-id="7f347-336">Pendant la migration, le nouvel environnement est exécuté, ce qui entraîne un coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="7f347-336">There is added cost during migration while you have the new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="7f347-337">Migration de déploiements Always On avec un temps d’arrêt minimal</span><span class="sxs-lookup"><span data-stu-id="7f347-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="7f347-338">Il existe deux stratégies pour effectuer la migration de déploiements Always On avec un temps d’arrêt minimal :</span><span class="sxs-lookup"><span data-stu-id="7f347-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="7f347-339">**Utiliser un service secondaire existant : site unique**</span><span class="sxs-lookup"><span data-stu-id="7f347-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="7f347-340">**Utiliser des réplicas secondaires existants : multi-sites**</span><span class="sxs-lookup"><span data-stu-id="7f347-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="7f347-341">1. Utilisation d’un service secondaire existant : site unique</span><span class="sxs-lookup"><span data-stu-id="7f347-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="7f347-342">Une stratégie limitant les temps d'arrêt consiste à prendre un service cloud existant secondaire et à supprimer le service cloud actuel.</span><span class="sxs-lookup"><span data-stu-id="7f347-342">One strategy for minimal downtime is to take an existing cloud secondary and remove it from the current cloud service.</span></span> <span data-ttu-id="7f347-343">Copiez les disques durs virtuels vers le nouveau compte de stockage Premium et créez la machine virtuelle dans le nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-343">Then copy the VHDs to the new Premium Storage account, and create the VM in the new cloud service.</span></span> <span data-ttu-id="7f347-344">Puis mettez à jour l'écouteur dans le clustering et effectuez le basculement.</span><span class="sxs-lookup"><span data-stu-id="7f347-344">Then update the listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="7f347-345">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="7f347-345">Points of downtime</span></span>
* <span data-ttu-id="7f347-346">Un temps d’arrêt se produit lorsque vous mettez à jour le nœud final avec le point de terminaison d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="7f347-346">There is downtime when you update the final node with the Load Balanced endpoint.</span></span>
* <span data-ttu-id="7f347-347">La reconnexion de votre client peut être retardée en fonction de votre configuration client/DNS.</span><span class="sxs-lookup"><span data-stu-id="7f347-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="7f347-348">Un temps d’arrêt supplémentaire survient si vous choisissez de mettre hors ligne le groupe Cluster Always On afin de permuter les adresses IP.</span><span class="sxs-lookup"><span data-stu-id="7f347-348">There is additional downtime if you choose to take the Always On Cluster group offline to swap out the IP addresses.</span></span> <span data-ttu-id="7f347-349">Vous pouvez éviter cela en utilisant une dépendance OR et en choisissant les propriétaires possibles pour la ressource d’adresse IP ajoutée.</span><span class="sxs-lookup"><span data-stu-id="7f347-349">You can avoid this by using an OR dependency and Possible Owners for the added IP Address resource.</span></span> <span data-ttu-id="7f347-350">Consultez la section « Ajout d'une ressource d'adresse IP sur le même sous-réseau » de l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-350">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="7f347-351">Lorsque vous souhaitez que le nœud ajouté joue le rôle de partenaire de basculement Always On, vous devez ajouter un point de terminaison Azure avec une référence au jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="7f347-351">When you want the added node to partake in as an Always On Failover Partner, you need to add an Azure Endpoint with a reference to the Load Balanced Set.</span></span> <span data-ttu-id="7f347-352">Lorsque vous exécutez la commande **Add-AzureEndpoint** pour cette opération, les connexions actuelles restent ouvertes, mais les nouvelles connexions à l'écouteur ne pourront pas être établies tant que l'équilibreur de charge n'a pas été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7f347-352">When you run the **Add-AzureEndpoint** command to do this, current connections to remain open, but new connections to the listener will not be able to be established until the load balancer has updated.</span></span> <span data-ttu-id="7f347-353">Dans ce test, l'opération dure de 90 à 120 secondes (à vérifier).</span><span class="sxs-lookup"><span data-stu-id="7f347-353">In testing this was seen to last 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="7f347-354">Avantages</span><span class="sxs-lookup"><span data-stu-id="7f347-354">Advantages</span></span>
* <span data-ttu-id="7f347-355">Aucun coût supplémentaire pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="7f347-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="7f347-356">Une migration un à un.</span><span class="sxs-lookup"><span data-stu-id="7f347-356">A one-to-one migration.</span></span>
* <span data-ttu-id="7f347-357">Moins de complexité.</span><span class="sxs-lookup"><span data-stu-id="7f347-357">Reduced complexity.</span></span>
* <span data-ttu-id="7f347-358">Permet d'augmenter le nombre d'opérations d'E/S à partir des SKU de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="7f347-359">Lorsque les disques sont déconnectés de la machine virtuelle et copiés vers le nouveau service cloud, un outil tiers peut être utilisé pour augmenter la taille du disque dur virtuel et fournir des débits plus importants.</span><span class="sxs-lookup"><span data-stu-id="7f347-359">When the disks are detached from the VM and copied to the new cloud service, a 3rd party tool can be used to increase the VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="7f347-360">Pour augmenter la taille du disque dur virtuel, consultez ce [forum de discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="7f347-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="7f347-361">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="7f347-361">Disadvantages</span></span>
* <span data-ttu-id="7f347-362">Il existe une perte temporaire de haute disponibilité et de récupération d'urgence pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="7f347-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="7f347-363">Comme il s'agit d'une migration 1:1, vous devez utiliser une taille minimale de machine virtuelle qui prendra en charge le nombre de disques durs virtuels, et vous risquez donc de ne plus pouvoir réduire vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="7f347-363">As this is a 1:1 migration, you will have to use a minimum VM size that will support your number of VHDs, so you might not be able to downsize your VMs.</span></span>
* <span data-ttu-id="7f347-364">Pour ce scénario, utilisez l'applet de commande Azure **Start-AzureStorageBlobCopy** , qui est asynchrone.</span><span class="sxs-lookup"><span data-stu-id="7f347-364">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="7f347-365">Il n'existe aucun contrat SLA à la fin de la copie.</span><span class="sxs-lookup"><span data-stu-id="7f347-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="7f347-366">Le temps de copie varie selon la durée d'attente dans la file et de la quantité de données à transférer.</span><span class="sxs-lookup"><span data-stu-id="7f347-366">The time of the copies varies, while this depends on wait in queue it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="7f347-367">Le temps de copie augmente si le transfert est destiné à un autre centre de données Azure prenant en charge le stockage Premium dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="7f347-367">The copy time increases if the transfer is going to another Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="7f347-368">Si vous avez seulement 2 nœuds, prévoyez une atténuation au cas où la copie prend plus de temps que lors du test.</span><span class="sxs-lookup"><span data-stu-id="7f347-368">If you just have 2 nodes, consider a possible mitigation in case the copy takes longer than in testing.</span></span> <span data-ttu-id="7f347-369">Dans ce cas, suivez ces conseils.</span><span class="sxs-lookup"><span data-stu-id="7f347-369">This could include the following ideas.</span></span>
  * <span data-ttu-id="7f347-370">Ajoutez un 3e nœud SQL Server temporaire pour la haute disponibilité avant la migration, avec un temps d'arrêt convenu.</span><span class="sxs-lookup"><span data-stu-id="7f347-370">Add a temporary 3rd SQL Server node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="7f347-371">Exécutez la migration en dehors de la maintenance Azure planifiée.</span><span class="sxs-lookup"><span data-stu-id="7f347-371">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="7f347-372">Vérifiez que vous avez correctement configuré votre quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="7f347-373">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="7f347-373">High-level steps</span></span>
<span data-ttu-id="7f347-374">Ce document ne présente pas un exemple complet de bout en bout, toutefois, l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fournit des informations qui peuvent être exploitées pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="7f347-374">This document does not demonstrate a complete end to end example, however the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged to perform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="7f347-376">Collectez la configuration des disques et supprimez le nœud (ne supprimez pas les disques durs virtuels connectés).</span><span class="sxs-lookup"><span data-stu-id="7f347-376">Gather disk configuration, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="7f347-377">Création d'un compte de stockage Premium et copie des disques durs virtuels à partir du compte de stockage Standard</span><span class="sxs-lookup"><span data-stu-id="7f347-377">Create a Premium Storage account and copy VHDs from the Standard Storage account</span></span>
* <span data-ttu-id="7f347-378">Créez un service cloud et redéployez la machine virtuelle SQL2 dans ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-378">Create new cloud service and redeploy the SQL2 VM in that cloud service.</span></span> <span data-ttu-id="7f347-379">Créez la machine virtuelle à l'aide du disque dur virtuel d'origine du système d'exploitation copié et connectez les disques durs virtuels copiés.</span><span class="sxs-lookup"><span data-stu-id="7f347-379">Create the VM using the copied original OS VHD and attaching the copied VHDs.</span></span>
* <span data-ttu-id="7f347-380">Configurez l'ILB/ELB et ajoutez des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7f347-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="7f347-381">Mettez à jour l'écouteur en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f347-381">Update Listener by either:</span></span>
  * <span data-ttu-id="7f347-382">Mettez hors ligne le groupe Always On et mettez à jour l’écouteur Always On avec la nouvelle adresse IP de l’ILB/ELB.</span><span class="sxs-lookup"><span data-stu-id="7f347-382">Taking the Always On Group offline and updating the Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="7f347-383">Ou ajoutez la ressource d’adresse IP de l’ILB/ELB du nouveau service cloud via PowerShell dans le clustering Windows.</span><span class="sxs-lookup"><span data-stu-id="7f347-383">Or adding the IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="7f347-384">Puis affectez les propriétaires possibles de la ressource d'adresse IP au nœud migré, SQL2, définissez ce paramètre comme dépendance OR dans le nom de réseau.</span><span class="sxs-lookup"><span data-stu-id="7f347-384">Then set the Possible owners of the IP Address resource to the migrated node, SQL2, and set this as OR dependency in the Network Name.</span></span> <span data-ttu-id="7f347-385">Consultez la section « Ajout d'une ressource d'adresse IP sur le même sous-réseau » de l' [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-385">See the ‘Adding IP Address Resource on Same Subnet’ section of the [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="7f347-386">Vérifiez la configuration/propagation DNS vers les clients.</span><span class="sxs-lookup"><span data-stu-id="7f347-386">Check DNS configuration/propogation to the clients.</span></span>
* <span data-ttu-id="7f347-387">Migrez la machine virtuelle SQL1 et suivez les étapes 2 à 4.</span><span class="sxs-lookup"><span data-stu-id="7f347-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="7f347-388">Si vous utilisez les étapes 5ii, ajoutez SQL1 comme propriétaire possible pour la ressource d'adresse IP ajoutée</span><span class="sxs-lookup"><span data-stu-id="7f347-388">If using steps 5ii, then add SQL1 as a Possible Owner for the added IP Address Resource</span></span>
* <span data-ttu-id="7f347-389">Testez les basculements.</span><span class="sxs-lookup"><span data-stu-id="7f347-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="7f347-390">2. Utilisation de réplicas secondaires existants : multi-sites</span><span class="sxs-lookup"><span data-stu-id="7f347-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="7f347-391">Si vous disposez de nœuds dans plusieurs centres de données Azure ou que vous évoluez dans un environnement hybride, vous pouvez utiliser une configuration Always On dans cet environnement pour réduire les temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="7f347-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment to minimize downtime.</span></span>

<span data-ttu-id="7f347-392">L’approche consiste à définir la synchronisation Always On sur Synchrone pour le centre de données Azure local ou secondaire, puis à basculer sur ce serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="7f347-392">The approach is to change the Always On synchronization to Synchronous for the on-premises or secondary Azure DC, and then failover over to that SQL Server.</span></span> <span data-ttu-id="7f347-393">Copiez les disques durs virtuels vers un compte de stockage Premium, puis redéployez la machine dans un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-393">Then copy the VHDs to a Premium Storage account, and redeploy the machine into a new cloud service.</span></span> <span data-ttu-id="7f347-394">Mettez à jour l'écouteur, puis restaurez-le.</span><span class="sxs-lookup"><span data-stu-id="7f347-394">Update the listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="7f347-395">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="7f347-395">Points of downtime</span></span>
<span data-ttu-id="7f347-396">Le temps d'arrêt inclut le délai de basculement vers l'autre centre de données et inversement.</span><span class="sxs-lookup"><span data-stu-id="7f347-396">The downtime consists of the time to failover to the alternative DC and back.</span></span> <span data-ttu-id="7f347-397">Il dépend de votre configuration client/DNS et la reconnexion du client peut être retardée.</span><span class="sxs-lookup"><span data-stu-id="7f347-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="7f347-398">Considérons l’exemple ci-après d’une configuration Always On hybride :</span><span class="sxs-lookup"><span data-stu-id="7f347-398">Consider the following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="7f347-400">Avantages</span><span class="sxs-lookup"><span data-stu-id="7f347-400">Advantages</span></span>
* <span data-ttu-id="7f347-401">Vous pouvez utiliser l'infrastructure existante.</span><span class="sxs-lookup"><span data-stu-id="7f347-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="7f347-402">Vous avez la possibilité d'effectuer d'abord une pré-mise à niveau du stockage Azure sur le centre de données de récupération d'urgence Azure.</span><span class="sxs-lookup"><span data-stu-id="7f347-402">You have the option to pre-upgrade the Azure storage on the DR Azure DC first.</span></span>
* <span data-ttu-id="7f347-403">Le stockage du centre de données de récupération d'urgence Azure peut être reconfiguré.</span><span class="sxs-lookup"><span data-stu-id="7f347-403">The DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="7f347-404">Il existe un minimum de deux basculements pendant la migration, à l'exclusion des basculements de test.</span><span class="sxs-lookup"><span data-stu-id="7f347-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="7f347-405">Vous n'avez pas besoin déplacer des données SQL Server avec la sauvegarde et la restauration.</span><span class="sxs-lookup"><span data-stu-id="7f347-405">You do not need to move SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="7f347-406">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="7f347-406">Disadvantages</span></span>
* <span data-ttu-id="7f347-407">En fonction de l'accès client à SQL Server, il peut y avoir une latence plus élevée lorsque SQL Server est en cours d'exécution dans un autre centre de données que l'application.</span><span class="sxs-lookup"><span data-stu-id="7f347-407">Depending on client access to SQL Server, there might be increased latency when SQL Server is running in an alternative DC to the application.</span></span>
* <span data-ttu-id="7f347-408">Le temps de copie des disques durs virtuels vers un stockage Premium peut être long.</span><span class="sxs-lookup"><span data-stu-id="7f347-408">The copy time of VHDs to Premium storage could be long.</span></span> <span data-ttu-id="7f347-409">Cela peut affecter votre décision de conserver ou non le nœud du groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="7f347-409">This might affect your decision on whether to keep the node in the Availability Group.</span></span> <span data-ttu-id="7f347-410">Considérez cela si la journalisation des charges de travail intensives est nécessaire pendant la migration, car le nœud principal doit conserver les transactions non répliquées dans son journal des transactions.</span><span class="sxs-lookup"><span data-stu-id="7f347-410">Consider this for when log intensive work loads are running during the migration is required, since the Primary node will have to keep the unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="7f347-411">Par conséquent, cela peut augmenter considérablement.</span><span class="sxs-lookup"><span data-stu-id="7f347-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="7f347-412">Pour ce scénario, utilisez l'applet de commande Azure **Start-AzureStorageBlobCopy** , qui est asynchrone.</span><span class="sxs-lookup"><span data-stu-id="7f347-412">This scenario would use the Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="7f347-413">Il n'existe aucun contrat SLA à la fin.</span><span class="sxs-lookup"><span data-stu-id="7f347-413">There is no SLA on completion.</span></span> <span data-ttu-id="7f347-414">Le temps des copies varie selon la durée d'attente dans la file et de la quantité de données à transférer.</span><span class="sxs-lookup"><span data-stu-id="7f347-414">The time of the copies varies, while this depends on wait in queue, it will also depend on the amount of data to transfer.</span></span> <span data-ttu-id="7f347-415">Vous n'avez donc qu'un seul nœud dans votre deuxième centre de données, et vous devez effectuer les opérations d'atténuation au cas où la copie prend plus de temps que lors des tests.</span><span class="sxs-lookup"><span data-stu-id="7f347-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case the copy takes longer than in testing.</span></span> <span data-ttu-id="7f347-416">Dans ce cas, suivez ces conseils.</span><span class="sxs-lookup"><span data-stu-id="7f347-416">This could include the following ideas.</span></span>
  * <span data-ttu-id="7f347-417">Ajoutez un 2e nœud SQL Server temporaire pour la haute disponibilité avant la migration, avec un temps d'arrêt convenu.</span><span class="sxs-lookup"><span data-stu-id="7f347-417">Add a temporary 2nd SQL node for HA before the migration with agreed downtime.</span></span>
  * <span data-ttu-id="7f347-418">Exécutez la migration en dehors de la maintenance Azure planifiée.</span><span class="sxs-lookup"><span data-stu-id="7f347-418">Run the migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="7f347-419">Vérifiez que vous avez correctement configuré votre quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="7f347-420">Ce scénario suppose que vous avez documenté votre installation et savez comment le stockage est mappé pour apporter des modifications aux paramètres de mise en cache optimale des disques.</span><span class="sxs-lookup"><span data-stu-id="7f347-420">This scenario assumes that you have documented your install and know how the storage is mapped in order to make changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="7f347-421">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="7f347-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="7f347-423">Définissez le centre de données Azure local/alternatif comme SQL Server principal et partenaire de basculement automatique (AFP).</span><span class="sxs-lookup"><span data-stu-id="7f347-423">Make the on-premises / alternate Azure DC the SQL Server Primary, and make it the other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="7f347-424">Collectez les informations de configuration des disques de SQL2 et supprimez le nœud (ne supprimez pas les disques durs virtuels connectés).</span><span class="sxs-lookup"><span data-stu-id="7f347-424">Gather disk configuration information from SQL2, and remove the node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="7f347-425">Créez un compte de stockage Premium et copiez les disques durs virtuels à partir du compte de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="7f347-425">Create a Premium Storage account and copy VHDs from the Standard Storage account.</span></span>
* <span data-ttu-id="7f347-426">Créez un nouveau service cloud et créez la machine virtuelle SQL2 avec ses disques de stockage Premium connectés.</span><span class="sxs-lookup"><span data-stu-id="7f347-426">Create a new cloud service and create the SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="7f347-427">Configurez l'ILB/ELB et ajoutez des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="7f347-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="7f347-428">Mettez à jour l’écouteur Always On avec la nouvelle adresse IP de l’ILB/ELB, puis testez le basculement.</span><span class="sxs-lookup"><span data-stu-id="7f347-428">Update the Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="7f347-429">Vérifiez la configuration DNS.</span><span class="sxs-lookup"><span data-stu-id="7f347-429">Check the DNS configuration.</span></span>
* <span data-ttu-id="7f347-430">Définissez l'AFP sur SQL2, migrez SQL1 puis suivez les étapes 2 à 5.</span><span class="sxs-lookup"><span data-stu-id="7f347-430">Change the AFP to SQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="7f347-431">Testez les basculements.</span><span class="sxs-lookup"><span data-stu-id="7f347-431">Test failovers.</span></span>
* <span data-ttu-id="7f347-432">Repositionnez l'AFP sur SQL1 et SQL2</span><span class="sxs-lookup"><span data-stu-id="7f347-432">Switch the AFP back to SQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-to-premium-storage"></a><span data-ttu-id="7f347-433">Annexe : migration d’un cluster Always On multisite vers Premium Storage</span><span class="sxs-lookup"><span data-stu-id="7f347-433">Appendix: Migrating a Multisite Always On Cluster to Premium Storage</span></span>
<span data-ttu-id="7f347-434">Le reste de cette rubrique décrit un exemple détaillé de conversion d’un cluster Always On multisite en stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="7f347-434">The remainder of this topic provides a detailed example of converting a multi-site Always On cluster to Premium storage.</span></span> <span data-ttu-id="7f347-435">L'exemple décrit également la conversion de l'écouteur d'un équilibreur de charge externe (ELB) à un équilibrage de charge interne (ILB).</span><span class="sxs-lookup"><span data-stu-id="7f347-435">It also converts the Listener from using an external load balancer (ELB) to an internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="7f347-436">Environnement</span><span class="sxs-lookup"><span data-stu-id="7f347-436">Environment</span></span>
* <span data-ttu-id="7f347-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="7f347-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="7f347-438">1 base de données de fichiers sur SP</span><span class="sxs-lookup"><span data-stu-id="7f347-438">1 DB Files on SP</span></span>
* <span data-ttu-id="7f347-439">2 x pools de stockage par nœud</span><span class="sxs-lookup"><span data-stu-id="7f347-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="7f347-441">MV :</span><span class="sxs-lookup"><span data-stu-id="7f347-441">VM:</span></span>
<span data-ttu-id="7f347-442">Cet exemple décrit la conversion d'un ELB en ILB.</span><span class="sxs-lookup"><span data-stu-id="7f347-442">In this example we are going to demonstrate moving from an ELB to ILB.</span></span> <span data-ttu-id="7f347-443">L'ELB étant disponible avant l'ILB, cet exemple montre comment effectuer la conversion pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="7f347-443">ELB was available before ILB, so this shows how to switch to this during the migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-to-subscription"></a><span data-ttu-id="7f347-445">Étapes préparatoires : se connecter à l’abonnement</span><span class="sxs-lookup"><span data-stu-id="7f347-445">Pre Steps: Connect to Subscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="7f347-446">Étape 1: créer les nouveaux compte de stockage et service cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where the vm to migrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-the-permitted-failures-on-resources-optional"></a><span data-ttu-id="7f347-447">Étape 2 : augmenter le niveau des échecs autorisés sur les ressources <Optional></span><span class="sxs-lookup"><span data-stu-id="7f347-447">Step 2: Increase the permitted failures on resources <Optional></span></span>
<span data-ttu-id="7f347-448">Sur certaines ressources appartenant à votre groupe de disponibilité Always On, il existe des limites concernant le nombre d’erreurs qui peuvent se produire dans une période où le service de cluster tente de redémarrer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7f347-448">On certain resources that belong to your Always On Availability Group there are limits on how many failures that can occur in a period, where the cluster service will attempt to restart the resource group.</span></span> <span data-ttu-id="7f347-449">Il est recommandé d'augmenter cette valeur au cours de cette procédure car si vous n'effectuez pas manuellement les basculements en arrêtant les machines, vous risquez de vous rapprocher de cette limite.</span><span class="sxs-lookup"><span data-stu-id="7f347-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close to this limit.</span></span>

<span data-ttu-id="7f347-450">Il est prudent de doubler la tolérance de défaillance ; pour cela, ouvrez le Gestionnaire du cluster de basculement, puis accédez aux propriétés du groupe de ressources Always On :</span><span class="sxs-lookup"><span data-stu-id="7f347-450">It would be prudent to double the failure allowance, to do this in Failover Cluster Manager, go to the Properties of the Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="7f347-452">Modifiez le nombre maximal d'échecs à 6.</span><span class="sxs-lookup"><span data-stu-id="7f347-452">Change the Maximum Failures to 6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="7f347-453">Étape 3 : ajouter une ressource d’adresse IP au groupe de clusters <Optional></span><span class="sxs-lookup"><span data-stu-id="7f347-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="7f347-454">Si vous n'avez qu'une seule adresse IP pour le groupe de clusters et qu'elle est alignée sur le sous-réseau cloud, prenez garde car si vous mettez hors ligne accidentellement tous les nœuds de cluster du cloud sur ce réseau, la ressource IP du cluster et le nom du réseau cluster ne pourront pas être mis en ligne.</span><span class="sxs-lookup"><span data-stu-id="7f347-454">If you have only one IP address for the Cluster Group and this is aligned to the cloud subnet, beware, if you accidentally take offline all cluster nodes in the cloud on that network then the Cluster IP resource and Cluster Network Name will not be able to come online.</span></span> <span data-ttu-id="7f347-455">Dans ce cas, cela empêcherait les mises à jour d'autres ressources de cluster.</span><span class="sxs-lookup"><span data-stu-id="7f347-455">In the event of this it will prevent updates to other cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="7f347-456">Étape 4 : configuration DNS</span><span class="sxs-lookup"><span data-stu-id="7f347-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="7f347-457">L’implémentation d’une transition fluide dépend du mode d’utilisation et de configuration du DNS.</span><span class="sxs-lookup"><span data-stu-id="7f347-457">To implement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="7f347-458">Lorsque la fonctionnalité Always On est installée, elle crée un groupe de ressources de cluster Windows ; si vous ouvrez le Gestionnaire du cluster de basculement, vous verrez qu’il comporte au moins trois ressources, et les deux auxquelles ce document fait référence sont :</span><span class="sxs-lookup"><span data-stu-id="7f347-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, the two that the document refers to are:</span></span>

* <span data-ttu-id="7f347-459">Nom de réseau virtuel (VNN) : il s’agit du nom DNS utilisé par le client pour se connecter aux serveurs SQL par le biais d’Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-459">Virtual Network Name (VNN) – This is the DNS name that client connect to when wanting to connect to SQL Servers via Always On.</span></span>
* <span data-ttu-id="7f347-460">Ressource d'adresse IP – il s'agit de l'adresse IP associée au VNN ; vous pouvez en utiliser plusieurs, et dans une configuration multi-sites, vous aurez une adresse IP par site/sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="7f347-460">IP Address Resource – This is the IP address that associated with the VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="7f347-461">Lors de la connexion à SQL Server, le pilote du client SQL Server extrait les enregistrements DNS associés à l’écouteur, et tente de vous connecter à chaque adresse IP Always On associée. Nous abordons ci-dessous certains facteurs pouvant influencer cette opération.</span><span class="sxs-lookup"><span data-stu-id="7f347-461">When connecting to SQL Server, the SQL Server Client driver will retrieve the DNS records associated with the listener and try to connect to each Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="7f347-462">Le nombre d’enregistrements DNS simultanés associés au nom de l’écouteur dépend non seulement du nombre d’adresses IP associées, mais également du paramètre « RegisterAllIpProviders » de clustering de basculement pour la ressource VNN Always On.</span><span class="sxs-lookup"><span data-stu-id="7f347-462">The number of concurrent DNS records that are associated with the listener name depends not only on the number of IP addresses associated, but the ‘RegisterAllIpProviders’setting in Failover Clustering for the Always ON VNN resource.</span></span>

<span data-ttu-id="7f347-463">Lorsque vous déployez Always On dans Azure, différentes étapes permettent de créer l’écouteur et les adresses IP, et vous devez définir manuellement le paramètre « RegisterAllIpProviders » sur 1, contrairement à un déploiement Always On local, où il est déjà défini sur 1.</span><span class="sxs-lookup"><span data-stu-id="7f347-463">When you deploy Always On in Azure there are different steps to create the Listener and IP Addresses, you have to manually configure the ‘RegisterAllIpProviders’ to 1, this is different to an on-premises Always On deployment where it is already set to 1.</span></span>

<span data-ttu-id="7f347-464">Si 'RegisterAllIpProviders' est défini sur 0, vous ne verrez qu'un seul enregistrement DNS dans le DNS associé à l'écouteur :</span><span class="sxs-lookup"><span data-stu-id="7f347-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with the Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="7f347-466">Si 'RegisterAllIpProviders' est 1 :</span><span class="sxs-lookup"><span data-stu-id="7f347-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="7f347-468">Le code ci-dessous vide les paramètres VNN et les définit pour vous. Notez que, pour que la modification soit appliquée, vous devez mettre le VNN hors ligne puis le remettre en ligne, et que cette déconnexion de l’écouteur entraîne une interruption de la connectivité client.</span><span class="sxs-lookup"><span data-stu-id="7f347-468">The code below will dump out the VNN settings and set it for you, please note, for the change to take effect you will need to take the VNN offline and turn it back online, this taking the Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="7f347-469">Dans une étape de migration ultérieure, vous devrez mettre à jour l’écouteur Always On avec une adresse IP mise à jour faisant référence à un équilibreur de charge, ce qui impliquera la suppression et l’ajout d’une ressource d’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="7f347-469">In a later migration step you will need to update the Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="7f347-470">Après la mise à jour de l'adresse IP, vous devez vérifier que la nouvelle adresse IP a été mise à jour dans la zone DNS et que les clients ont mis à jour leur cache DNS local.</span><span class="sxs-lookup"><span data-stu-id="7f347-470">After the IP update, you need to ensure the new IP address has been updated in DNS Zone and that the clients are updating their local DNS cache.</span></span>

<span data-ttu-id="7f347-471">Si vos clients résident dans un segment de réseau différent et référencent un autre serveur DNS, vous devez tenir compte de ce qui se passe au niveau du transfert de la zone DNS pendant la migration, car le délai de reconnexion de l’application est contraint au moins par le temps de transfert de la zone de toute nouvelle adresse IP pour l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="7f347-471">If your clients reside in a different network segment and reference a different DNS server, you need to consider what happens about DNS Zone Transfer during the migration, as the application reconnect time will be constrained by at least the Zone Transfer Time of any new IP addresses for the listener.</span></span> <span data-ttu-id="7f347-472">Si vous êtes pressé par le temps, vous devez étudier et forcer le test d'un transfert de zone incrémentiel avec vos équipes Windows, et également consigner l'enregistrement de l'hôte DNS en choisissant une durée de vie TTL (Time To Live) inférieure pour permettre aux clients de se mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="7f347-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put the DNS host record to a lower Time To Live (TTL), so the clients update.</span></span> <span data-ttu-id="7f347-473">Pour plus d’informations, consultez [Transferts de zone incrémentiels](https://technet.microsoft.com/library/cc958973.aspx) et [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f347-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="7f347-474">Par défaut, la durée de vie (TTL) d’un enregistrement DNS associé à l’écouteur Always On dans Azure est de 1 200 secondes.</span><span class="sxs-lookup"><span data-stu-id="7f347-474">By default the TTL for DNS Record that is associated with the Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="7f347-475">Vous pouvez réduire ce paramètre si vous êtes pressé par le temps pendant votre migration afin de permettre aux clients de mettre à jour leurs DNS avec l'adresse IP mise à jour pour l'écouteur.</span><span class="sxs-lookup"><span data-stu-id="7f347-475">You may wish to reduce this if you are under time constraint during your migration to ensure the clients update their DNS with the updated IP address for the listener.</span></span> <span data-ttu-id="7f347-476">Vous pouvez afficher et modifier la configuration en vidant la configuration du VNN :</span><span class="sxs-lookup"><span data-stu-id="7f347-476">You can see and modify the configuration by dumping out the configuration of the VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="7f347-477">Veuillez noter que la diminution de la valeur 'HostRecordTTL' augmente le trafic DNS.</span><span class="sxs-lookup"><span data-stu-id="7f347-477">Please note, the lower the ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="7f347-478">Paramètres de l’application cliente</span><span class="sxs-lookup"><span data-stu-id="7f347-478">Client application settings</span></span>
<span data-ttu-id="7f347-479">Si votre application cliente SQL prend en charge .Net 4.5 SQLClient, vous pouvez utiliser le mot clé « MULTISUBNETFAILOVER = TRUE » ; il est recommandé d’appliquer ce dernier, car il accélère la connexion au groupe de disponibilité SQL Always On pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="7f347-479">If your SQL client application supports the .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended to be applied as it allows for faster connection to SQL Always On Availability Group during failover.</span></span> <span data-ttu-id="7f347-480">Il énumère toutes les adresses IP associées à l’écouteur Always On en parallèle et effectue une tentative de reconnexion TCP plus rapide lors d’un basculement.</span><span class="sxs-lookup"><span data-stu-id="7f347-480">It enumerates through all IP addresses associated with the Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="7f347-481">Pour plus d'informations sur les paramètres ci-dessus, consultez la rubrique [Mot clé MultiSubnetFailover et fonctionnalités associées](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="7f347-481">For more information regarding the settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="7f347-482">Consultez également [Prise en charge SqlClient pour la haute disponibilité et récupération d’urgence](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="7f347-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="7f347-483">Étape 5 : paramètres de quorum de cluster</span><span class="sxs-lookup"><span data-stu-id="7f347-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="7f347-484">Comme vous allez arrêter au moins un serveur SQL à la fois, vous devez modifier le paramètre de quorum du cluster. Si vous utilisez le système File Share Witness (FSW) avec deux nœuds, vous devez définir le quorum pour prendre en compte une majorité de nœuds et utiliser le vote dynamique afin qu’un seul nœud reste actif.</span><span class="sxs-lookup"><span data-stu-id="7f347-484">As you are going to be taking out at least one SQL Server down at a time, you should modify the cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set the quorum to allow node majority and utilize dynamic voting, and this is to allow for a single node to remain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="7f347-485">Pour plus d'informations sur la gestion et la configuration du quorum de cluster, consultez la rubrique [Configurer et gérer le quorum dans un cluster de basculement Windows Server 2012](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f347-485">For more information on managing and configuring the cluster quorum, please see [Configure and Manage the Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="7f347-486">Étape 6 : extraction des points de terminaison et des ACL existants</span><span class="sxs-lookup"><span data-stu-id="7f347-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for the Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="7f347-487">Enregistrez ces éléments dans un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="7f347-487">Save these to a text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="7f347-488">Étape 7 : modification les partenaires de basculement et des modes de réplication</span><span class="sxs-lookup"><span data-stu-id="7f347-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="7f347-489">Si vous avez plus de 2 serveurs SQL, vous devez définir sur 'Synchrone' le basculement d’un autre serveur secondaire d’un centre de données ou en local et le configurer comme partenaire de basculement automatique (AFP) ; cela garantit une haute disponibilité lorsque vous apportez des modifications.</span><span class="sxs-lookup"><span data-stu-id="7f347-489">If you have more than 2 SQL Servers, you should change the failover of another secondary in another DC or on-premises to ‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="7f347-490">Vous pouvez le faire via TSQL ou via SSMS :</span><span class="sxs-lookup"><span data-stu-id="7f347-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="7f347-492">Étape 8 : Suppression de la machine virtuelle secondaire du service cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="7f347-493">Vous devez prévoir de migrer d'abord un nœud de cloud secondaire ; s'il s'agit du nœud principal, vous devez effectuer un basculement manuel.</span><span class="sxs-lookup"><span data-stu-id="7f347-493">You should be planning to migrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns the disks associated with the VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="7f347-494">Étape 9 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement</span><span class="sxs-lookup"><span data-stu-id="7f347-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="7f347-495">Pour les volumes de données, ces paramètres doivent être définis sur READONLY.</span><span class="sxs-lookup"><span data-stu-id="7f347-495">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="7f347-496">Pour les volumes TLOG, ils doivent être définis sur NONE.</span><span class="sxs-lookup"><span data-stu-id="7f347-496">For TLOG volumes these should be set to NONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="7f347-498">Étape 10 : copie de disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="7f347-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="7f347-499">Vous pouvez vérifier l'état de la copie des disques durs virtuels pour le compte de stockage Premium :</span><span class="sxs-lookup"><span data-stu-id="7f347-499">You can check the copy status of the VHDs to the Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="7f347-501">Attendez que toutes ces opérations soient correctement terminées.</span><span class="sxs-lookup"><span data-stu-id="7f347-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="7f347-502">Pour plus d'informations pour les objets BLOB individuels :</span><span class="sxs-lookup"><span data-stu-id="7f347-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="7f347-503">Étape 11 : inscription du disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="7f347-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="7f347-504">Étape 12 : importation d’un serveur secondaire dans un nouveau service cloud</span><span class="sxs-lookup"><span data-stu-id="7f347-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="7f347-505">Le code ci-dessous utilise également l'option ajoutée ici pour importer la machine et utiliser l'adresse IP virtuelle conservable.</span><span class="sxs-lookup"><span data-stu-id="7f347-505">The code below also uses the added option here you can import the machine and use the retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember to change to XIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks to a VM during a deploy to a new cloud service and new storage account is different from just attaching VHDs to just a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="7f347-506">Étape 13 : création d'un ILB sur le nouveau service cloud, ajout de points terminaux d'équilibrage de charge et d'ACL</span><span class="sxs-lookup"><span data-stu-id="7f347-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="7f347-507">Étape 14 : mise à jour d’Always On</span><span class="sxs-lookup"><span data-stu-id="7f347-507">Step 14: Update Always On</span></span>
    #Code to be executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # the azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency to Listener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="7f347-509">Supprimez maintenant l'ancienne adresse IP du service cloud.</span><span class="sxs-lookup"><span data-stu-id="7f347-509">Now remove the old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="7f347-511">Étape 15 : vérification de la mise à jour DNS</span><span class="sxs-lookup"><span data-stu-id="7f347-511">Step 15: DNS update check</span></span>
<span data-ttu-id="7f347-512">Vous devriez maintenant vérifier les serveurs DNS sur les réseaux du client SQL Server et vous assurer que le clustering a ajouté l'enregistrement hôte supplémentaire pour l'adresse IP ajoutée.</span><span class="sxs-lookup"><span data-stu-id="7f347-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added the extra host record for the added IP address.</span></span> <span data-ttu-id="7f347-513">Si ces serveurs DNS n’ont pas été mis à jour, essayez de forcer un transfert de la zone DNS et vérifiez que les clients sur le sous-réseau peuvent résoudre les deux adresses IP Always On, ce qui évite d’attendre la réplication DNS automatique.</span><span class="sxs-lookup"><span data-stu-id="7f347-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that the clients in there subnet are able to resolve to both Always On IP Addresses, this is so you do not need to wait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="7f347-514">Étape 16 : reconfiguration d’Always On</span><span class="sxs-lookup"><span data-stu-id="7f347-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="7f347-515">À ce stade, attendez que le nœud secondaire qui a été migré soit totalement resynchronisé avec le nœud local, puis basculez vers un nœud de réplication synchrone pour en faire l’AFP.</span><span class="sxs-lookup"><span data-stu-id="7f347-515">At this point you wait for the secondary that node that was migrated to fully resynchronize with the on-premises node and switch to synchronous replication node and make it the AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="7f347-516">Étape 17 : migration du deuxième nœud</span><span class="sxs-lookup"><span data-stu-id="7f347-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild to new cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="7f347-517">Étape 18 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement</span><span class="sxs-lookup"><span data-stu-id="7f347-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="7f347-518">Pour les volumes de données, ces paramètres doivent être définis sur READONLY.</span><span class="sxs-lookup"><span data-stu-id="7f347-518">For data volumes these should be set to READONLY.</span></span>

<span data-ttu-id="7f347-519">Pour les volumes TLOG, ils doivent être définis sur NONE.</span><span class="sxs-lookup"><span data-stu-id="7f347-519">For TLOG volumes these should be set to NONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="7f347-521">Étape 19 : création d'un nouveau compte de stockage indépendant pour le nœud secondaire</span><span class="sxs-lookup"><span data-stu-id="7f347-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset the storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="7f347-522">Étape 20 : copie de disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="7f347-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created the container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy to Premium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="7f347-523">Vous pouvez vérifier l'état de copie de tous les disques durs virtuels : ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span><span class="sxs-lookup"><span data-stu-id="7f347-523">You can check the VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="7f347-525">Attendez que toutes ces opérations soient correctement terminées.</span><span class="sxs-lookup"><span data-stu-id="7f347-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="7f347-526">Pour plus d'informations pour les objets BLOB individuels :</span><span class="sxs-lookup"><span data-stu-id="7f347-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="7f347-527">Étape 21 : inscription du disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="7f347-527">Step 21: Register OS disk</span></span>
    #change storage account to the new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join to existing Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different to just a straight cloud service change
    #note if you do not have a disk label the command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="7f347-528">Étape 22 : ajout de points de terminaison et de ACL avec équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="7f347-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in the Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="7f347-529">Étape 23 : test du basculement</span><span class="sxs-lookup"><span data-stu-id="7f347-529">Step 23: Test failover</span></span>
<span data-ttu-id="7f347-530">Vous devriez maintenant laisser le nœud migré se synchroniser avec le nœud Always On local, le placer en mode de réplication synchrone et attendre qu’il soit synchronisé.</span><span class="sxs-lookup"><span data-stu-id="7f347-530">You should now let the migrated node synchronize with the on-premises Always On node, place it in to synchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="7f347-531">Effectuez ensuite un basculement du nœud local vers le premier nœud migré, c'est-à-dire l'AFP.</span><span class="sxs-lookup"><span data-stu-id="7f347-531">Then failover from on-prem to the first node migrated, which is the AFP.</span></span> <span data-ttu-id="7f347-532">Une fois l'opération réussie, changez le dernier nœud migré en AFP.</span><span class="sxs-lookup"><span data-stu-id="7f347-532">Once that has worked, change the last migrated node to the AFP.</span></span>

<span data-ttu-id="7f347-533">Vous devez tester les basculements entre tous les nœuds de test et effectuer des tests CHAOS pour vous assurer que les basculements se sont déroulés comme prévu et en temps opportun.</span><span class="sxs-lookup"><span data-stu-id="7f347-533">You should test failovers between all nodes and run though chaos tests to ensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="7f347-534">Étape 24 : réinitialisation des paramètres du quorum de cluster / TTL DNS / Partenaires de basculement / Paramètres de synchronisation</span><span class="sxs-lookup"><span data-stu-id="7f347-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="7f347-535">Ajout de ressource d'adresse IP sur le même sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7f347-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="7f347-536">Si vous disposez seulement de 2 serveurs SQL et que vous souhaitez en effectuer la migration vers un nouveau service cloud tout en les conservant sur le même sous-réseau, vous pouvez éviter de mettre hors ligne l’écouteur pour supprimer l’adresse IP Always On d’origine afin d’ajouter la nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="7f347-536">If you have only 2 SQL Servers and want to migrate them to a new cloud service, but want to keep them on the same subnet, you can avoid taking the listener offline to delete the original Always On IP Address and add the New IP Address.</span></span> <span data-ttu-id="7f347-537">Si vous migrez les machines virtuelles vers un autre sous-réseau, inutile d'effectuer cette opération car un autre réseau de cluster référencera ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="7f347-537">If you are migrating the VMs to another subnet you will not need to do this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="7f347-538">Une fois que vous avez sélectionné le serveur secondaire migré et ajouté la nouvelle ressource d'adresse IP pour le nouveau service cloud avant d'effectuer le basculement du serveur principal, vous devez suivre ces étapes dans le gestionnaire de basculement du cluster :</span><span class="sxs-lookup"><span data-stu-id="7f347-538">Once you have brought up the migrated secondary and added in the new IP Address resource for the new cloud service before failover the existing Primary, you should take these steps within the Cluster Failover Manager:</span></span>

<span data-ttu-id="7f347-539">Pour ajouter l'adresse IP, consultez l'étape 14 de l' [annexe](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="7f347-539">To add in IP Address, see the [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="7f347-540">Pour la ressource d’adresse IP actuelle, changez le propriétaire possible en « Serveur SQL principal existant », « dansqlams4 » dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7f347-540">For the current IP Address resource, change the possible owner to ‘Existing Primary SQL Server’, in the example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="7f347-542">Pour la nouvelle ressource d’adresse IP, changez le propriétaire possible en « Serveur SQL secondaire migré », « dansqlams5 » dans l’exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7f347-542">For the new IP Address resource, change the possible owner to ‘Migrated secondary SQL Server’, in the example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="7f347-544">Une fois ces opérations terminées, vous pouvez effectuer le basculement, et lorsque le dernier nœud est migré, les propriétaires possibles doivent être modifiés pour ajouter ce nœud comme propriétaire possible :</span><span class="sxs-lookup"><span data-stu-id="7f347-544">Once this is set you can failover, and when the last node is migrated the Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="7f347-546">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7f347-546">Additional resources</span></span>
* [<span data-ttu-id="7f347-547">Stockage Premium Azure</span><span class="sxs-lookup"><span data-stu-id="7f347-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="7f347-548">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="7f347-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="7f347-549">SQL Server dans des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="7f347-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
