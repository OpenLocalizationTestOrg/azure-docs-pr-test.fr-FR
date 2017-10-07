---
title: aaaUse le stockage Azure Premium avec SQL Server | Documents Microsoft
description: "Cet article utilise les ressources créées avec le modèle de déploiement classique hello et fournit des conseils sur l’utilisation de stockage Azure Premium avec SQL Server s’exécutant sur des Machines virtuelles Azure."
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
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="fbc10-103">Utilisation du stockage Premium Azure avec SQL Server sur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="fbc10-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="fbc10-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fbc10-104">Overview</span></span>
<span data-ttu-id="fbc10-105">[Stockage Azure Premium](../../../storage/common/storage-premium-storage.md) est hello nouvelle génération de stockage qui fournit une latence faible et haut débit d’e/s.</span><span class="sxs-lookup"><span data-stu-id="fbc10-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="fbc10-106">Il est particulièrement adapté aux principales charges de travail E/S intensives telles que SQL Server sur [des machines virtuelles](https://azure.microsoft.com/services/virtual-machines/)IaaS.</span><span class="sxs-lookup"><span data-stu-id="fbc10-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbc10-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fbc10-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fbc10-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fbc10-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="fbc10-110">Cet article fournit des conseils pour migrer un ordinateur virtuel en cours d’exécution SQL Server toouse stockage Premium et planification.</span><span class="sxs-lookup"><span data-stu-id="fbc10-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="fbc10-111">Cela inclut l'infrastructure Azure (mise en réseau, stockage) et les étapes de la machine virtuelle Windows hôte.</span><span class="sxs-lookup"><span data-stu-id="fbc10-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="fbc10-112">exemple Hello Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) montre une migration de tooend complètes de fin de l’amélioration des toomove supérieure machines virtuelles tootake parti de local stockage SSD avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbc10-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="fbc10-113">Elle consiste toounderstand important hello bout en bout utilisant le stockage Azure Premium avec SQL Server sur des machines virtuelles IAAS.</span><span class="sxs-lookup"><span data-stu-id="fbc10-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="fbc10-114">notamment :</span><span class="sxs-lookup"><span data-stu-id="fbc10-114">This includes:</span></span>

* <span data-ttu-id="fbc10-115">Identification des conditions préalables de hello toouse stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="fbc10-116">Exemples de déploiement de SQL Server sur IaaS tooPremium stockage pour les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="fbc10-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="fbc10-117">Exemples de migration de déploiements existants, à la fois de serveurs autonomes et de déploiements à l’aide de groupes de disponibilité SQL Always On.</span><span class="sxs-lookup"><span data-stu-id="fbc10-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="fbc10-118">Approches de migration possibles.</span><span class="sxs-lookup"><span data-stu-id="fbc10-118">Possible migration approaches.</span></span>
* <span data-ttu-id="fbc10-119">Exemple de bout en bout complète les étapes de Azure, Windows et SQL Server pour la migration de hello d’une implémentation existante Always On.</span><span class="sxs-lookup"><span data-stu-id="fbc10-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="fbc10-120">Pour plus de détails sur l’utilisation de SQL Server dans les machines virtuelles Azure, consultez la rubrique [SQL Server dans les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fbc10-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="fbc10-121">**Auteur :** Daniel Sol **Réviseurs techniques :** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span><span class="sxs-lookup"><span data-stu-id="fbc10-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="fbc10-122">Configuration requise pour le stockage Premium</span><span class="sxs-lookup"><span data-stu-id="fbc10-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="fbc10-123">Il existe plusieurs conditions préalables à l'utilisation du stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="fbc10-124">Taille de la machine</span><span class="sxs-lookup"><span data-stu-id="fbc10-124">Machine size</span></span>
<span data-ttu-id="fbc10-125">Pour l’utilisation de stockage Premium, vous devrez toouse DS série Machines virtuelles (VM).</span><span class="sxs-lookup"><span data-stu-id="fbc10-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="fbc10-126">Si vous n’avez pas utilisé les ordinateurs de la série DS dans votre service cloud avant, vous devez supprimer hello existante de machine virtuelle, conserver les disques hello attaché et ensuite créer un nouveau service cloud avant de recréer hello machine virtuelle en tant que DS * taille de rôle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="fbc10-127">Pour plus d’informations sur l’utilisation des tailles des machines virtuelles, consultez la rubrique [Tailles des machines virtuelles et des services cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbc10-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="fbc10-128">Services cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-128">Cloud services</span></span>
<span data-ttu-id="fbc10-129">Vous pouvez uniquement utiliser des machines virtuelles DS* avec un stockage Premium si elles ont été créées dans un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="fbc10-130">Si vous utilisez SQL Server Always On dans Azure, hello toujours écouteur fait référence toohello Azure interne ou externe charge équilibrage de l’adresse IP qui est associé à un service cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="fbc10-131">Cet article se concentre sur la façon de toomigrate tout en conservant la disponibilité dans ce scénario.</span><span class="sxs-lookup"><span data-stu-id="fbc10-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-132">Doit être une série DS * hello première machine virtuelle qui est déployé toohello nouveau Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="fbc10-133">Réseaux virtuels régionaux</span><span class="sxs-lookup"><span data-stu-id="fbc10-133">Regional VNETS</span></span>
<span data-ttu-id="fbc10-134">Pour les machines virtuelles DS * vous devez configurer hello réseau virtuel (VNET) qui héberge votre toobe de machines virtuelles régional.</span><span class="sxs-lookup"><span data-stu-id="fbc10-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="fbc10-135">Cette hello « s’étend » le réseau virtuel est tooallow toobe de machines virtuelles plus grande hello configuré dans d’autres clusters et autoriser la communication entre eux.</span><span class="sxs-lookup"><span data-stu-id="fbc10-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="fbc10-136">Bonjour suivant capture d’écran, hello emplacement en surbrillance montre les réseaux virtuels régionaux, tandis que le premier résultat de hello montre un réseau virtuel « étroit ».</span><span class="sxs-lookup"><span data-stu-id="fbc10-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="fbc10-138">Vous pouvez déclencher un tooa de toomigrate de ticket de support Microsoft réseau virtuel régional, Microsoft fera une modification, puis toocomplete hello migration tooregional réseaux virtuels, attribuez à la propriété de hello AffinityGroup dans la configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="fbc10-139">Tout d’abord exporter hello Configuration réseau dans PowerShell, puis remplacez hello **AffinityGroup** propriété Bonjour **VirtualNetworkSite** élément avec un **emplacement** propriété.</span><span class="sxs-lookup"><span data-stu-id="fbc10-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="fbc10-140">Spécifiez `Location = XXXX` où `XXXX` est une région Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc10-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="fbc10-141">Importez ensuite la nouvelle configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-141">Then import hello new configuration.</span></span>

<span data-ttu-id="fbc10-142">Prenons l’exemple hello suivant la configuration du réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="fbc10-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="fbc10-143">toomove cette tooa réseau virtuel régional en Europe de l’ouest, modifiez hello toohello de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="fbc10-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="fbc10-144">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="fbc10-144">Storage accounts</span></span>
<span data-ttu-id="fbc10-145">Vous devez toocreate un compte de stockage qui est configuré pour le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="fbc10-146">Notez que l’utilisation hello du stockage Premium est définie à partir du compte de stockage hello, pas sur les disques durs virtuels individuels, toutefois, lors de l’utilisation d’une machine virtuelle DS * série vous pouvez attacher des disques durs virtuels à partir de comptes Premium et Standard de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="fbc10-147">Vous pouvez envisager cette option si vous ne souhaitez pas tooplace hello disque dur virtuel du système d’exploitation sur toohello compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="fbc10-148">suivant de Hello **New-AzureStorageAccountPowerShell** avec hello « Premium_LRS » **Type** crée un compte de stockage Premium :</span><span class="sxs-lookup"><span data-stu-id="fbc10-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="fbc10-149">Paramètres de cache des disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="fbc10-149">VHDs Cache Settings</span></span>
<span data-ttu-id="fbc10-150">Hello principale différence entre la création de disques qui font partie d’un compte de stockage Premium est un paramètre de cache du disque hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="fbc10-151">Pour les disques de volume de données SQL Server, il est recommandé d’utiliser le paramètre de cache de lecture**Read Caching**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="fbc10-152">Pour les volumes de journal de Transaction, le paramètre de cache de disque hello doit être défini trop '**aucun**'.</span><span class="sxs-lookup"><span data-stu-id="fbc10-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="fbc10-153">Cela est différent des recommandations hello pour les comptes de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="fbc10-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="fbc10-154">Une fois que les disques durs virtuels hello ont été attachées, paramètre de cache hello ne peut pas être modifiée.</span><span class="sxs-lookup"><span data-stu-id="fbc10-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="fbc10-155">Vous devez toodetach et rattachez hello disque dur virtuel avec un paramètre de cache mis à jour.</span><span class="sxs-lookup"><span data-stu-id="fbc10-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="fbc10-156">Espaces de stockage Windows</span><span class="sxs-lookup"><span data-stu-id="fbc10-156">Windows storage spaces</span></span>
<span data-ttu-id="fbc10-157">Vous pouvez utiliser [espaces de stockage Windows](https://technet.microsoft.com/library/hh831739.aspx) comme vous le faisiez avec le stockage Standard précédents, cela vous permettra de toomigrate une machine virtuelle qui utilise déjà des espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="fbc10-158">exemple Hello dans [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (étape 9 et suivantes) montre hello tooextract de code Powershell et importer une machine virtuelle avec plusieurs disques durs virtuels attachés.</span><span class="sxs-lookup"><span data-stu-id="fbc10-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="fbc10-159">Pools de stockage ont été utilisés avec un débit de tooenhance de compte de stockage Azure Standard et réduisent la latence.</span><span class="sxs-lookup"><span data-stu-id="fbc10-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="fbc10-160">Vous trouverez peut-être utile de tester des pools de stockage avec un stockage Premium pour les nouveaux déploiements, mais notez que ces tests compliquent la configuration du stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="fbc10-161">Comment toofind les disques virtuels Azure mapper les pools de toostorage</span><span class="sxs-lookup"><span data-stu-id="fbc10-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="fbc10-162">Qu’il existe des recommandations de cache différent pour les disques durs virtuels attachés, vous pouvez décider toocopy hello disques durs virtuels tooa compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="fbc10-163">Toutefois, lorsque vous les rattachez toohello la série DS nouvelle machine virtuelle, vous devrez peut-être les paramètres de cache tooalter hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="fbc10-164">Il est plus simple hello tooapply que stockage Premium recommandé de paramètres de cache lorsque vous avez des disques durs virtuels distincts pour hello de données SQL fichiers et journal des fichiers (plutôt qu’un disque dur virtuel unique qui contient à la fois).</span><span class="sxs-lookup"><span data-stu-id="fbc10-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-165">Si vous avez des fichiers journaux et de données de SQL Server sur le même volume, hello mise en cache de l’option choisie dépend des modèles d’accès aux e/s hello pour vos charges de travail de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="fbc10-166">Seuls des tests permettent d'identifier l'option de mise en cache la mieux adaptée à ce scénario.</span><span class="sxs-lookup"><span data-stu-id="fbc10-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="fbc10-167">Toutefois, si vous utilisez des espaces de stockage Windows sont composés de plusieurs disques durs virtuels vous devez toolook à votre tooidentify des scripts d’origine qui joint des disques durs virtuels sont dans un pool spécifique qui, par conséquent, vous pouvez ensuite définir les paramètres de cache hello en conséquence pour chaque disque.</span><span class="sxs-lookup"><span data-stu-id="fbc10-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="fbc10-168">Si vous n’avez pas d’origine tooshow disponible de script vous qui mappent des disques durs virtuels toohello pool de stockage, vous pouvez utiliser hello suivant le mappage de pools de stockage sur disque/étapes toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="fbc10-169">Pour chaque disque, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbc10-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="fbc10-170">Obtenez la liste des disques attachés tooVM avec hello **Get-AzureVM** commande :</span><span class="sxs-lookup"><span data-stu-id="fbc10-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="fbc10-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="fbc10-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="fbc10-172">Notez hello Diskname et numéro d’unité logique.</span><span class="sxs-lookup"><span data-stu-id="fbc10-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="fbc10-174">Bureau à distance dans hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="fbc10-175">Passez trop**gestion de l’ordinateur** | **le Gestionnaire de périphériques** | **disques**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="fbc10-176">Examiner les propriétés hello de chacune des hello « Microsoft des disques virtuels »</span><span class="sxs-lookup"><span data-stu-id="fbc10-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="fbc10-178">nombre LUN Hello ici est un nombre de numéro d’unité logique de toohello de référence que vous spécifiez lors de l’attachement hello VHD toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="fbc10-179">Pour hello 'Disque virtuel Microsoft' go toohello **détails** onglet, puis dans hello **propriété** liste, passez trop**clé pilote**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="fbc10-180">Bonjour **valeur**, hello de note **décalage**, qui est 0002 Bonjour suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="fbc10-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="fbc10-181">Hello 0002 indique hello PhysicalDisk2 hello références de pool de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="fbc10-183">Pour chaque pool de stockage, vidage out hello de disques associés :</span><span class="sxs-lookup"><span data-stu-id="fbc10-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="fbc10-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="fbc10-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="fbc10-186">Vous pouvez maintenant utiliser cette tooassociate informations attaché disques tooPhysical de disques durs virtuels dans les Pools de stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="fbc10-187">Une fois que vous avez mappé les disques tooPhysical de disques durs virtuels dans les Pools de stockage, vous pouvez détacher et copiez-les sur tooa compte de stockage Premium, puis de les joindre avec hello correct du paramètre de.</span><span class="sxs-lookup"><span data-stu-id="fbc10-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="fbc10-188">Consultez l’exemple hello Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), les étapes 8 à 12.</span><span class="sxs-lookup"><span data-stu-id="fbc10-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="fbc10-189">Ces étapes indiquent comment tooextract un fichier VHD de machine virtuelle attachée disque configuration tooa CSV, copier les disques durs virtuels hello, modifier les paramètres de cache de configuration de disque hello et enfin redéployer hello machine virtuelle comme disque attaché d’une machine virtuelle de la série DS avec hello tous les.</span><span class="sxs-lookup"><span data-stu-id="fbc10-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="fbc10-190">Bande passante de stockage de la machine virtuelle et débit de stockage du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="fbc10-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="fbc10-191">Hello des performances de stockage dépend hello taille de VM DS * spécifié et hello des tailles de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="fbc10-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="fbc10-192">machines virtuelles de Hello ont différentes allocations pour le nombre de hello de disques durs virtuels qui peuvent être attachés et hello ils prend en charge (Mo/s) de la bande passante maximale.</span><span class="sxs-lookup"><span data-stu-id="fbc10-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="fbc10-193">Pour les nombres de la bande passante spécifique hello, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbc10-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fbc10-194">Les disques de plus grande taille augmentent le nombre d'opérations d'E/S par seconde.</span><span class="sxs-lookup"><span data-stu-id="fbc10-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="fbc10-195">Vous devez en tenir compte lorsque vous étudiez votre chemin de migration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="fbc10-196">Pour plus d’informations, [consultez la table de hello pour les e/s et les Types de disques](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="fbc10-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="fbc10-197">Enfin, notez que les machines virtuelles prennent en charge différentes bandes passantes maximales pour tous les disques connectés.</span><span class="sxs-lookup"><span data-stu-id="fbc10-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="fbc10-198">Sous une charge élevée, vous pourriez saturer hello maximale disque la bande passante disponible pour cette taille de rôle de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="fbc10-199">Par exemple un Standard_DS14 prendra en charge des too512MB/s ; Par conséquent, avec trois disques P30 vous pourriez saturer la bande passante du disque de hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="fbc10-200">Mais dans cet exemple, la limite de débit hello peut être dépassée en fonction de la combinaison de hello de lecture et d’écriture e/s.</span><span class="sxs-lookup"><span data-stu-id="fbc10-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="fbc10-201">Nouveaux déploiements</span><span class="sxs-lookup"><span data-stu-id="fbc10-201">New deployments</span></span>
<span data-ttu-id="fbc10-202">Hello deux sections suivantes montrent comment vous pouvez déployer des machines virtuelles SQL Server tooPremium stockage.</span><span class="sxs-lookup"><span data-stu-id="fbc10-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="fbc10-203">Comme mentionné précédemment, vous ne devez pas nécessairement disque de système d’exploitation tooplace hello sur le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="fbc10-204">Vous pouvez choisir toodo cela si vous avez l’intention tooplace toutes les charges de travail intensives d’e/s sur le disque dur virtuel du système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="fbc10-205">Hello premier exemple illustre l’utilisation des Images de la galerie Azure existant.</span><span class="sxs-lookup"><span data-stu-id="fbc10-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="fbc10-206">Hello deuxième exemple montre comment toouse une machine virtuelle personnalisée de l’image que vous disposez d’un compte de stockage Standard existant.</span><span class="sxs-lookup"><span data-stu-id="fbc10-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-207">Ces exemples supposent que vous avez déjà créé un réseau virtuel régional.</span><span class="sxs-lookup"><span data-stu-id="fbc10-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="fbc10-208">Création d'une nouvelle machine virtuelle avec un stockage Premium et une image de galerie</span><span class="sxs-lookup"><span data-stu-id="fbc10-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="fbc10-209">exemple Hello ci-dessous montre comment les tooplace hello du disque dur virtuel du système d’exploitation sur un stockage premium et attacher des disques durs virtuels de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="fbc10-210">Toutefois, vous pouvez également placer le disque du système d’exploitation hello dans un compte de stockage Standard et puis attachez les disques durs virtuels qui résident dans un compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="fbc10-211">Ces deux scénarios sont présentés.</span><span class="sxs-lookup"><span data-stu-id="fbc10-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="fbc10-212">Étape 1 : création d'un compte de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="fbc10-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="fbc10-213">Étape 2 : création d'un nouveau service cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="fbc10-214">Étape 3 : réservation d'une adresse IP virtuelle de service cloud (facultatif)</span><span class="sxs-lookup"><span data-stu-id="fbc10-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="fbc10-215">Étape 4 : création d'un conteneur de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="fbc10-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="fbc10-216">Étape 5 : placement du disque dur virtuel du système d'exploitation sur Standard ou Premium stockage</span><span class="sxs-lookup"><span data-stu-id="fbc10-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="fbc10-217">Étape 6 : création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fbc10-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

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


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="fbc10-218">Créer un nouveau toouse de machine virtuelle stockage Premium avec une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="fbc10-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="fbc10-219">Ce scénario vous montre où sont placées les images personnalisées existantes qui résident sur un compte de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="fbc10-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="fbc10-220">Comme mentionné si vous voulez tooplace hello disque dur virtuel du système d’exploitation sur stockage Premium vous devez toocopy hello image qui existe dans le compte de stockage Standard de hello et les transfèrent tooa stockage Premium avant de pouvoir être utilisé.</span><span class="sxs-lookup"><span data-stu-id="fbc10-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="fbc10-221">Si vous disposez d’une image locale, vous pouvez également utiliser cette méthode toocopy directement toohello compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="fbc10-222">Étape 1 : création d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="fbc10-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="fbc10-223">Étape 2 : création d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="fbc10-224">Étape 3 : utilisation d’une image existante</span><span class="sxs-lookup"><span data-stu-id="fbc10-224">Step 3: Use existing image</span></span>
<span data-ttu-id="fbc10-225">Vous pouvez utiliser une image existante.</span><span class="sxs-lookup"><span data-stu-id="fbc10-225">You can use an existing image.</span></span> <span data-ttu-id="fbc10-226">Vous pouvez [prendre l’image d’une machine existante](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbc10-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="fbc10-227">Machine de hello Remarque vous de l’image n’a pas de toobe DS * machine.</span><span class="sxs-lookup"><span data-stu-id="fbc10-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="fbc10-228">Une fois que vous avez hello image, hello suivant les étapes indiquent comment toocopy il toohello compte de stockage Premium avec hello **AzureStorageBlobCopy de début** applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbc10-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="fbc10-229">Étape 4: copie d'objets Blob entre des comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="fbc10-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="fbc10-230">Étape 5 : vérification régulière de l'état de la copie :</span><span class="sxs-lookup"><span data-stu-id="fbc10-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="fbc10-231">Étape 6 : Ajouter l’Image tooAzure sur le disque référentiel dans l’abonnement</span><span class="sxs-lookup"><span data-stu-id="fbc10-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="fbc10-232">Vous constaterez peut-être que même si les rapports d’état sur hello comme une réussite, vous pouvez toujours obtenir une erreur de bail de disque.</span><span class="sxs-lookup"><span data-stu-id="fbc10-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="fbc10-233">Dans ce cas, attendez 10 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="fbc10-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="fbc10-234">Étape 7 : Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fbc10-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="fbc10-235">Vous créez ici hello machine virtuelle à partir de votre image et l’attachement de deux disques durs virtuels de stockage Premium :</span><span class="sxs-lookup"><span data-stu-id="fbc10-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="fbc10-236">Déploiements existants qui n’utilisent pas les groupes de disponibilité Always On</span><span class="sxs-lookup"><span data-stu-id="fbc10-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="fbc10-237">Pour les déploiements existants, tout d’abord voir hello [conditions préalables](#prerequisites-for-premium-storage) section de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="fbc10-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="fbc10-238">Il existe différents points à prendre en compte concernant les déploiements SQL Server qui utilisent ou non des groupes de disponibilité Always On.</span><span class="sxs-lookup"><span data-stu-id="fbc10-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="fbc10-239">Si vous n’utilisez pas Always On et que vous disposez d’un autonome existante de SQL Server, vous pouvez mettre à niveau tooPremium stockage à l’aide d’un nouveau compte service et le stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="fbc10-240">Tenez compte des hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbc10-240">Consider hello following options:</span></span>

* <span data-ttu-id="fbc10-241">**Créez une nouvelle machine virtuelle SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="fbc10-242">Vous pouvez créer une nouvelle machine virtuelle SQL qui utilise un compte de stockage Premium comme décrit dans les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="fbc10-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="fbc10-243">Ensuite, sauvegardez et restaurez votre configuration SQL Server et vos bases de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fbc10-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="fbc10-244">Hello application aura besoin des mises à jour de toobe tooreference hello nouveau SQL Server si elle est accessible en interne ou externe.</span><span class="sxs-lookup"><span data-stu-id="fbc10-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="fbc10-245">Vous devez toocopy tous les objets « hors db' comme si vous effectuiez une migration de (SxS) SQL Server côte à côte.</span><span class="sxs-lookup"><span data-stu-id="fbc10-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="fbc10-246">Cela inclut des objets tels que les connexions, les certificats et les serveurs liés.</span><span class="sxs-lookup"><span data-stu-id="fbc10-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="fbc10-247">**Migrez une machine virtuelle SQL Server existante**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="fbc10-248">Vous devrez déconnecter hello machine virtuelle SQL Server, puis transférer tooa nouveau service cloud, qui inclut la copie de tous ses toohello de disques durs virtuels attaché compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="fbc10-249">Lors du hello machine virtuelle est en ligne, application hello fait référence le nom d’hôte serveur hello comme avant.</span><span class="sxs-lookup"><span data-stu-id="fbc10-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="fbc10-250">N’oubliez pas que la taille hello du disque existant de hello affectera des caractéristiques de performances hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="fbc10-251">Par exemple, un disque de 400 Go obtient arrondi par excès tooa P20.</span><span class="sxs-lookup"><span data-stu-id="fbc10-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="fbc10-252">Si vous savez que vous ne requièrent pas les performances du disque, vous pourriez recréer hello machine virtuelle comme une machine virtuelle de série DS et attacher des disques durs virtuels de stockage Premium de spécification de taille et de performances hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="fbc10-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="fbc10-253">Ensuite, vous pouvez détacher et rattacher les fichiers de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-254">Lors de la copie de disques de disque dur virtuel hello vous devez être conscient de la taille de hello, selon la taille de hello signifie le type de disque de stockage Premium peuvent être regroupées en, cela détermine la spécification de performances de disque.</span><span class="sxs-lookup"><span data-stu-id="fbc10-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="fbc10-255">Taille de Azure arrondit les toohello le plus proche du disque, donc si vous avez un disque Go 400, cela sera arrondie tooa P20.</span><span class="sxs-lookup"><span data-stu-id="fbc10-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="fbc10-256">Selon vos exigences d’e/s existants de hello disque dur virtuel du système d’exploitation, vous ne devrez pas peut-être toomigrate cette tooa compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="fbc10-257">Si votre serveur SQL Server est accessible en externe, adresse IP virtuelle de service de cloud hello changera.</span><span class="sxs-lookup"><span data-stu-id="fbc10-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="fbc10-258">Vous devez également les points de terminaison tooupdate, ACL et DNS paramètres.</span><span class="sxs-lookup"><span data-stu-id="fbc10-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="fbc10-259">Déploiements existants qui utilisent les groupes de disponibilité Always On</span><span class="sxs-lookup"><span data-stu-id="fbc10-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="fbc10-260">Pour les déploiements existants, tout d’abord voir hello [conditions préalables](#prerequisites-for-premium-storage) section de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="fbc10-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="fbc10-261">Dans cette section, nous examinons la façon dont le groupe de disponibilité Always On interagit avec la mise en réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc10-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="fbc10-262">Nous sera puis décomposer les migrations dans les scénarios de tootwo : les migrations où aucun temps d’arrêt peut être tolérée et les migrations où vous devez obtenir un temps mort minimal.</span><span class="sxs-lookup"><span data-stu-id="fbc10-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="fbc10-263">Les groupes locaux de disponibilité Always On SQL Server utilisent un écouteur local qui inscrit un nom DNS virtuel ainsi qu’une adresse IP partagée entre un ou plusieurs serveurs SQL.</span><span class="sxs-lookup"><span data-stu-id="fbc10-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="fbc10-264">Lorsque les clients se connectent, ils sont routées via hello écouteur IP toohello principal SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fbc10-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="fbc10-265">Il s’agit de serveur hello propriétaire hello ressource toujours sur IP à ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="fbc10-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="fbc10-267">Dans Microsoft Azure vous pouvez avoir qu’un seul IP adresse affectée tooa NIC sur hello machine virtuelle, dans commande tooachieve hello même couche d’abstraction comme local, Azure utilise l’adresse IP hello affectée équilibreurs de charge interne/externe toohello (équilibrage de charge interne/ELB).</span><span class="sxs-lookup"><span data-stu-id="fbc10-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="fbc10-268">la ressource IP Hello qui est partagée entre les serveurs de hello est définie toohello même adresse IP en tant que hello/ELB de l’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fbc10-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="fbc10-269">Il est publié dans hello DNS, et le trafic du client est passé au réplica de serveur SQL principal toohello hello/ELB de l’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fbc10-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="fbc10-270">Hello équilibrage de charge interne/ELB sait quel serveur SQL principal, car elle utilise des ressources de sondes tooprobe hello toujours sur IP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="fbc10-271">Dans l’exemple précédent de hello, il teste chaque nœud qui possède un point de terminaison référencé par hello ELB/équilibrage de charge interne, selon celle qui répond est hello principal SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fbc10-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-272">Hello équilibrage de charge interne et ELB sont tous deux affectés service de cloud computing Azure particulier tooa, par conséquent, toute migration cloud dans Azure signifie probablement que hello que change IP d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="fbc10-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="fbc10-273">Migration de déploiements Always On autorisant des temps d’arrêt</span><span class="sxs-lookup"><span data-stu-id="fbc10-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="fbc10-274">Il existe deux stratégies toomigrate toujours sur les déploiements qui permet des temps morts :</span><span class="sxs-lookup"><span data-stu-id="fbc10-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="fbc10-275">**Ajouter plusieurs réplicas secondaires tooan existant toujours sur le Cluster**</span><span class="sxs-lookup"><span data-stu-id="fbc10-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="fbc10-276">**Migrer tooa nouveau toujours sur Cluster**</span><span class="sxs-lookup"><span data-stu-id="fbc10-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="fbc10-277">1. Ajouter plusieurs réplicas secondaires tooan toujours sur Cluster existant</span><span class="sxs-lookup"><span data-stu-id="fbc10-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="fbc10-278">Une stratégie est tooadd plusieurs bases de données secondaires toohello toujours sur le groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fbc10-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="fbc10-279">Vous devez tooadd ces éléments dans un nouveau service cloud et mettre à jour d’écouteur de hello avec hello équilibreur de charge nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fbc10-280">Points d’arrêt :</span><span class="sxs-lookup"><span data-stu-id="fbc10-280">Points of downtime:</span></span>
* <span data-ttu-id="fbc10-281">Validation de cluster.</span><span class="sxs-lookup"><span data-stu-id="fbc10-281">Cluster Validation.</span></span>
* <span data-ttu-id="fbc10-282">Test des basculements Always On de nouveaux réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="fbc10-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="fbc10-283">Si vous utilisez des Pools de stockage Windows dans hello VM pour augmenter le débit d’e/s, celles-ci sont effectuées en mode hors connexion pendant une Validation de Cluster complète.</span><span class="sxs-lookup"><span data-stu-id="fbc10-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="fbc10-284">test de validation Hello est requis lorsque vous ajoutez le cluster toohello de nœuds.</span><span class="sxs-lookup"><span data-stu-id="fbc10-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="fbc10-285">Hello temps test de hello toorun peut varier, donc vous devez tester cela dans votre tooget d’environnement de test représentatif une durée approximative de la durée de cette opération.</span><span class="sxs-lookup"><span data-stu-id="fbc10-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="fbc10-286">Vous devez configurer le moment où vous pouvez effectuer un basculement manuel et chaos test sur hello qui vient d’être ajouté des fonctions de haute disponibilité Always On tooensure nœuds comme prévu.</span><span class="sxs-lookup"><span data-stu-id="fbc10-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="fbc10-288">Vous devez arrêter toutes les instances de SQL Server où les Pools de stockage hello sont utilisées avant hello la Validation s’exécute.</span><span class="sxs-lookup"><span data-stu-id="fbc10-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="fbc10-289">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="fbc10-289">High-level steps</span></span>
>

1. <span data-ttu-id="fbc10-290">Créez deux serveurs SQL dans le nouveau service cloud avec une connexion au stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="fbc10-291">Copiez les sauvegardes complètes et effectuez une restauration avec **NORECOVERY**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="fbc10-292">Copiez les objets dépendants 'out of user DB', notamment que les connexions.</span><span class="sxs-lookup"><span data-stu-id="fbc10-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="fbc10-293">Créez un nouvel équilibreur de charge interne (ILB) ou utilisez un équilibreur de charge externe (ELB), puis configurez ensuite les points de terminaison d'équilibrage de charge sur les deux nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="fbc10-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fbc10-294">Vérifiez que tous les nœuds ont la configuration de point de terminaison hello correcte avant de continuer</span><span class="sxs-lookup"><span data-stu-id="fbc10-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="fbc10-295">Arrêter toohello d’accès de l’Application d’utilisateur SQL Server (si vous utilisez des Pools de stockage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="fbc10-296">Arrêtez les services du moteur SQL Server sur tous les nœuds (si vous utilisez des pools de stockage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="fbc10-297">Ajouter de nouveaux nœuds toocluster et exécuter la validation complète.</span><span class="sxs-lookup"><span data-stu-id="fbc10-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="fbc10-298">Une fois la validation réussie, démarrez tous les services SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fbc10-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="fbc10-299">Sauvegardez les journaux des transactions et restaurez les bases de données utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fbc10-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="fbc10-300">Ajouter de nouveaux nœuds dans le groupe de disponibilité AlwaysOn de hello et de le placer dans la réplication **synchrone**.</span><span class="sxs-lookup"><span data-stu-id="fbc10-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="fbc10-301">Ajouter hello IP ressource d’adresse de hello nouveau Cloud Service équilibrage de charge interne ELB via PowerShell pour Always On sur la base hello multisite exemple Bonjour [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="fbc10-302">Dans le clustering Windows, définissez hello **propriétaires possibles** Hello **adresse IP** ressource toohello nouveaux nœuds ancien.</span><span class="sxs-lookup"><span data-stu-id="fbc10-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="fbc10-303">Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="fbc10-304">Tooone de basculement de nouveaux nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="fbc10-305">Rendre des partenaires de basculement automatique de nouveaux nœuds hello et les tests de basculement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="fbc10-306">Supprimez les nœuds d'origine du groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fbc10-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="fbc10-307">Avantages</span><span class="sxs-lookup"><span data-stu-id="fbc10-307">Advantages</span></span>
* <span data-ttu-id="fbc10-308">Nouveaux serveurs SQL peut être testé (SQL Server et Application) avant d’être ajoutés sur tooAlways.</span><span class="sxs-lookup"><span data-stu-id="fbc10-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="fbc10-309">Vous pouvez modifier la taille de machine virtuelle hello et personnaliser des spécifications exactes de hello stockage tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbc10-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="fbc10-310">Toutefois, il serait utile tookeep tous les chemins de fichier SQL hello hello identiques.</span><span class="sxs-lookup"><span data-stu-id="fbc10-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="fbc10-311">Vous pouvez contrôler le démarrage de transfert hello de toohello de sauvegardes de base de données hello réplicas secondaires.</span><span class="sxs-lookup"><span data-stu-id="fbc10-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="fbc10-312">Cela diffère de l’utilisation d’Azure **Start-AzureStorageBlobCopy** toocopy de l’applet de commande disques durs virtuels, car il s’agit d’une copie asynchrone.</span><span class="sxs-lookup"><span data-stu-id="fbc10-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fbc10-313">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="fbc10-313">Disadvantages</span></span>
* <span data-ttu-id="fbc10-314">Lorsque vous utilisez des Pools de stockage Azure, est interruptions de service de Cluster pendant hello complète la Validation du Cluster pour les nœuds supplémentaires nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="fbc10-315">Selon hello Version de SQL Server et le nombre d’existant hello des réplicas secondaires, vous ne pouvez pas être en mesure de tooadd plusieurs réplicas secondaires sans supprimer les bases de données secondaires existantes.</span><span class="sxs-lookup"><span data-stu-id="fbc10-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="fbc10-316">Il peut être long temps de transfert de données SQL lors de la configuration des bases de données secondaires hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="fbc10-317">Pendant la migration, l’exécution de nouvelles machines en parallèle entraîne un coût supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fbc10-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="fbc10-318">2. Migrer tooa nouveau toujours sur Cluster</span><span class="sxs-lookup"><span data-stu-id="fbc10-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="fbc10-319">Une autre stratégie est toocreate un tout nouveau toujours sur Cluster avec tout nouveau nœuds dans le nouveau service cloud, puis redirection hello clients toouse il.</span><span class="sxs-lookup"><span data-stu-id="fbc10-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fbc10-320">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="fbc10-320">Points of downtime</span></span>
<span data-ttu-id="fbc10-321">Il est temps d’arrêt lorsque vous transférez des applications et les utilisateurs toohello nouveau toujours l’écouteur de.</span><span class="sxs-lookup"><span data-stu-id="fbc10-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="fbc10-322">temps d’arrêt Hello dépend :</span><span class="sxs-lookup"><span data-stu-id="fbc10-322">hello downtime depends on:</span></span>

* <span data-ttu-id="fbc10-323">Hello durée toorestore transaction finale journal sauvegardes toodatabases sur de nouveaux serveurs.</span><span class="sxs-lookup"><span data-stu-id="fbc10-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="fbc10-324">Hello durée tooupdate applications toouse nouveau Always On écouteur client.</span><span class="sxs-lookup"><span data-stu-id="fbc10-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="fbc10-325">Avantages</span><span class="sxs-lookup"><span data-stu-id="fbc10-325">Advantages</span></span>
* <span data-ttu-id="fbc10-326">Vous pouvez tester hello véritable environnement de production, SQL Server, et les modifications de génération du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fbc10-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="fbc10-327">Vous avez hello option toocustomize hello stockage et toopotentially réduire la taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fbc10-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="fbc10-328">Cela pourrait entraîner une réduction des coûts.</span><span class="sxs-lookup"><span data-stu-id="fbc10-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="fbc10-329">Vous pouvez mettre à jour votre build ou version SQL Server pendant ce processus.</span><span class="sxs-lookup"><span data-stu-id="fbc10-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="fbc10-330">Vous pouvez également mettre à niveau hello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fbc10-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="fbc10-331">Hello que précédente toujours sur Cluster peut agir comme une cible de restauration solide.</span><span class="sxs-lookup"><span data-stu-id="fbc10-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fbc10-332">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="fbc10-332">Disadvantages</span></span>
* <span data-ttu-id="fbc10-333">Vous devez le nom DNS toochange hello d’écouteur de hello si vous souhaitez que les deux clusters toujours en cours d’exécution simultanément.</span><span class="sxs-lookup"><span data-stu-id="fbc10-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="fbc10-334">Cette opération ajoute administration surcharge lors de la migration de hello comme chaînes d’application cliente doivent refléter le nouveau nom de port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="fbc10-335">Vous devez implémenter un mécanisme de synchronisation entre deux tookeep environnements hello, en tant que fermer toominimize possible hello synchronisation finale à la configuration requise avant la migration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="fbc10-336">Est ajoutée coût pendant la migration pendant que vous avez hello nouvel environnement en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fbc10-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="fbc10-337">Migration de déploiements Always On avec un temps d’arrêt minimal</span><span class="sxs-lookup"><span data-stu-id="fbc10-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="fbc10-338">Il existe deux stratégies pour effectuer la migration de déploiements Always On avec un temps d’arrêt minimal :</span><span class="sxs-lookup"><span data-stu-id="fbc10-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="fbc10-339">**Utiliser un service secondaire existant : site unique**</span><span class="sxs-lookup"><span data-stu-id="fbc10-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="fbc10-340">**Utiliser des réplicas secondaires existants : multi-sites**</span><span class="sxs-lookup"><span data-stu-id="fbc10-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="fbc10-341">1. Utilisation d’un service secondaire existant : site unique</span><span class="sxs-lookup"><span data-stu-id="fbc10-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="fbc10-342">Une stratégie pour un temps mort minimal est tootake un cloud existant secondaire et le supprimer du service de cloud actuelle hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="fbc10-343">Puis copiez hello toohello de disques durs virtuels de nouveau compte de stockage Premium et créer hello machine virtuelle dans le nouveau service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="fbc10-344">Puis mettez à jour un écouteur de hello dans la gestion de clusters et le basculement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fbc10-345">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="fbc10-345">Points of downtime</span></span>
* <span data-ttu-id="fbc10-346">Il est temps d’arrêt lorsque vous mettez à jour le nœud final de hello avec point de terminaison à charge équilibrée hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="fbc10-347">La reconnexion de votre client peut être retardée en fonction de votre configuration client/DNS.</span><span class="sxs-lookup"><span data-stu-id="fbc10-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="fbc10-348">Il est temps d’arrêt supplémentaires si vous choisissez tootake hello toujours sur le Cluster groupe hors connexion tooswap les adresses IP de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="fbc10-349">Vous pouvez éviter cela à l’aide de la dépendance OR et propriétaires possibles pour hello ajouté la ressource d’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="fbc10-350">Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="fbc10-351">Lorsque vous souhaitez hello toopartake nœud ajouté dans en tant qu’un toujours sur partenaire de basculement, vous devez tooadd un point de terminaison Azure avec un toohello de référence de charge équilibrée définie.</span><span class="sxs-lookup"><span data-stu-id="fbc10-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="fbc10-352">Lorsque vous exécutez hello **Add-AzureEndpoint** commande toodo, tooremain de connexions en cours ouvert, mais le nouvel écouteur de toohello de connexions ne seront pas en mesure de toobe établie jusqu'à ce que l’équilibrage de charge hello a mis à jour.</span><span class="sxs-lookup"><span data-stu-id="fbc10-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="fbc10-353">Dans le test, il s’agissait toolast vu 90-120 secondes, cela doit être testé.</span><span class="sxs-lookup"><span data-stu-id="fbc10-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="fbc10-354">Avantages</span><span class="sxs-lookup"><span data-stu-id="fbc10-354">Advantages</span></span>
* <span data-ttu-id="fbc10-355">Aucun coût supplémentaire pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="fbc10-356">Une migration un à un.</span><span class="sxs-lookup"><span data-stu-id="fbc10-356">A one-to-one migration.</span></span>
* <span data-ttu-id="fbc10-357">Moins de complexité.</span><span class="sxs-lookup"><span data-stu-id="fbc10-357">Reduced complexity.</span></span>
* <span data-ttu-id="fbc10-358">Permet d'augmenter le nombre d'opérations d'E/S à partir des SKU de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="fbc10-359">Lors de la partie d’un 3e hello disques sont détachés hello VM et copiés toohello de nouveau service cloud, outil peut être de taille de disque dur virtuel hello tooincrease utilisé, qui fournit des débits plus importants.</span><span class="sxs-lookup"><span data-stu-id="fbc10-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="fbc10-360">Pour augmenter la taille du disque dur virtuel, consultez ce [forum de discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span><span class="sxs-lookup"><span data-stu-id="fbc10-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fbc10-361">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="fbc10-361">Disadvantages</span></span>
* <span data-ttu-id="fbc10-362">Il existe une perte temporaire de haute disponibilité et de récupération d'urgence pendant la migration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="fbc10-363">Comme il s’agit d’une migration 1:1, vous devez toouse une taille minimale de machine virtuelle qui prend en charge le nombre de disques durs virtuels, donc vous n’êtes peut-être pas en mesure de toodownsize vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fbc10-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="fbc10-364">Ce scénario utiliseriez hello Azure **AzureStorageBlobCopy de début** applet de commande, qui est asynchrone.</span><span class="sxs-lookup"><span data-stu-id="fbc10-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="fbc10-365">Il n'existe aucun contrat SLA à la fin de la copie.</span><span class="sxs-lookup"><span data-stu-id="fbc10-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="fbc10-366">le délai de Hello de copies de hello varie, cela dépend de l’attente dans la file d’attente qu'il dépend également du montant hello de tootransfer de données.</span><span class="sxs-lookup"><span data-stu-id="fbc10-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="fbc10-367">heure Hello augmente si le transfert de hello est en train de centre de données Azure tooanother qui prend en charge le stockage Premium dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="fbc10-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="fbc10-368">Si vous avez seulement 2 nœuds, envisagez une atténuation possibles en cas de copie de hello dure plus longtemps que dans le test.</span><span class="sxs-lookup"><span data-stu-id="fbc10-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="fbc10-369">Cela peut inclure hello suivant des idées.</span><span class="sxs-lookup"><span data-stu-id="fbc10-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="fbc10-370">Ajouter un nœud SQL Server 3e temporaire pour la haute disponibilité avant la migration hello avec un temps mort convenu.</span><span class="sxs-lookup"><span data-stu-id="fbc10-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="fbc10-371">Exécutez la migration hello en dehors d’Azure maintenance planifiée.</span><span class="sxs-lookup"><span data-stu-id="fbc10-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="fbc10-372">Vérifiez que vous avez correctement configuré votre quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="fbc10-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="fbc10-373">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="fbc10-373">High-level steps</span></span>
<span data-ttu-id="fbc10-374">Ce document ne présente pas d’un exemple de tooend fin terminée, cependant hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) fournit des détails qui peuvent être optimisée tooperform cela.</span><span class="sxs-lookup"><span data-stu-id="fbc10-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="fbc10-376">Collecte la configuration de disque et supprimer un nœud hello (ne pas supprimer les disques durs virtuels attachés).</span><span class="sxs-lookup"><span data-stu-id="fbc10-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="fbc10-377">Créez un compte de stockage Premium et copier les disques durs virtuels à partir de hello compte de stockage Standard</span><span class="sxs-lookup"><span data-stu-id="fbc10-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="fbc10-378">Création du service cloud et redéployer hello SQL2 VM dans ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="fbc10-379">Créer hello machine virtuelle à l’aide de hello copié de disque dur virtuel de système d’exploitation d’origine et attachement hello copiés les disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="fbc10-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="fbc10-380">Configurez l'ILB/ELB et ajoutez des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fbc10-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="fbc10-381">Mettez à jour l'écouteur en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbc10-381">Update Listener by either:</span></span>
  * <span data-ttu-id="fbc10-382">Prendre hello groupe Always On en mode hors connexion et de mise à jour hello toujours l’écouteur d’avec équilibrage de charge interne nouveau / adresse IP de ELB.</span><span class="sxs-lookup"><span data-stu-id="fbc10-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="fbc10-383">Ou l’ajout de ressource d’adresse hello IP de nouveau Cloud Service équilibrage de charge interne/ELB via PowerShell dans le clustering Windows.</span><span class="sxs-lookup"><span data-stu-id="fbc10-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="fbc10-384">Puis ensemble hello des propriétaires possibles de toohello de ressource d’adresse IP hello migrés de nœud, SQL2 et que la dépendance OR Bonjour nom réseau.</span><span class="sxs-lookup"><span data-stu-id="fbc10-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="fbc10-385">Consultez hello 'Ajout de ressource d’adresse IP sur le même sous-réseau' section Hello [annexe](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="fbc10-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="fbc10-386">Vérifiez les clients toohello de configuration/propagation DNS.</span><span class="sxs-lookup"><span data-stu-id="fbc10-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="fbc10-387">Migrez la machine virtuelle SQL1 et suivez les étapes 2 à 4.</span><span class="sxs-lookup"><span data-stu-id="fbc10-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="fbc10-388">Si des étapes 5ii, puis ajouter SQL1 comme propriétaire Possible pour hello ajouté la ressource d’adresse IP</span><span class="sxs-lookup"><span data-stu-id="fbc10-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="fbc10-389">Testez les basculements.</span><span class="sxs-lookup"><span data-stu-id="fbc10-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="fbc10-390">2. Utilisation de réplicas secondaires existants : multi-sites</span><span class="sxs-lookup"><span data-stu-id="fbc10-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="fbc10-391">Si vous avez des nœuds dans plusieurs centres de données Azure (DC) ou si vous avez un environnement hybride, vous pouvez utiliser une configuration Always On ce temps d’arrêt toominimize environnement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="fbc10-392">approche de Hello est toochange hello Always On synchronisation tooSynchronous hello localement ou contrôleur de domaine Azure secondaire, puis basculement sur toothat SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fbc10-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="fbc10-393">Puis copier les disques durs virtuels de hello tooa compte de stockage Premium et redéployer la machine de hello dans un nouveau service cloud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="fbc10-394">Mettre à jour le port d’écoute hello et restaurez.</span><span class="sxs-lookup"><span data-stu-id="fbc10-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="fbc10-395">Points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="fbc10-395">Points of downtime</span></span>
<span data-ttu-id="fbc10-396">temps d’arrêt Hello se compose de hello temps toofailover toohello autre contrôleur de domaine et un précédent.</span><span class="sxs-lookup"><span data-stu-id="fbc10-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="fbc10-397">Il dépend de votre configuration client/DNS et la reconnexion du client peut être retardée.</span><span class="sxs-lookup"><span data-stu-id="fbc10-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="fbc10-398">Tenez compte des hello, exemple d’une configuration Always On hybride suivant :</span><span class="sxs-lookup"><span data-stu-id="fbc10-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="fbc10-400">Avantages</span><span class="sxs-lookup"><span data-stu-id="fbc10-400">Advantages</span></span>
* <span data-ttu-id="fbc10-401">Vous pouvez utiliser l'infrastructure existante.</span><span class="sxs-lookup"><span data-stu-id="fbc10-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="fbc10-402">Vous avez tout d’abord hello de mise à niveau toopre option hello stockage Azure sur hello contrôleur de domaine de récupération d’urgence Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc10-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="fbc10-403">Hello stockage de récupération d’urgence Azure le contrôleur de domaine peut être reconfiguré.</span><span class="sxs-lookup"><span data-stu-id="fbc10-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="fbc10-404">Il existe un minimum de deux basculements pendant la migration, à l'exclusion des basculements de test.</span><span class="sxs-lookup"><span data-stu-id="fbc10-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="fbc10-405">Vous ne devez toomove des données de SQL Server avec une sauvegarde et restauration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="fbc10-406">Inconvénients</span><span class="sxs-lookup"><span data-stu-id="fbc10-406">Disadvantages</span></span>
* <span data-ttu-id="fbc10-407">En fonction de tooSQL d’accès client serveur, il peut y avoir une latence accrue lorsque SQL Server est en cours d’exécution dans une autre application de toohello de contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="fbc10-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="fbc10-408">heure de disques durs virtuels tooPremium stockage Hello risque de durer longtemps.</span><span class="sxs-lookup"><span data-stu-id="fbc10-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="fbc10-409">Cela peut affecter votre décision sur si tookeep hello nœud Bonjour groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fbc10-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="fbc10-410">Là lorsque le travail nécessitant de journal charges sont en cours d’exécution pendant la migration de hello est requis, étant donné que nœud principal de hello portera tookeep hello des transactions non répliquées dans son journal des transactions.</span><span class="sxs-lookup"><span data-stu-id="fbc10-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="fbc10-411">Par conséquent, cela peut augmenter considérablement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="fbc10-412">Ce scénario utiliseriez hello Azure **AzureStorageBlobCopy de début** applet de commande, qui est asynchrone.</span><span class="sxs-lookup"><span data-stu-id="fbc10-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="fbc10-413">Il n'existe aucun contrat SLA à la fin.</span><span class="sxs-lookup"><span data-stu-id="fbc10-413">There is no SLA on completion.</span></span> <span data-ttu-id="fbc10-414">Hello le délai de copies de hello varie, cela dépend de l’attente dans la file d’attente, elle dépend également du montant hello de tootransfer de données.</span><span class="sxs-lookup"><span data-stu-id="fbc10-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="fbc10-415">Par conséquent, vous avez uniquement un seul nœud dans votre centre de données 2, vous devez prendre des mesures d’atténuation en cas de copie de hello dure plus longtemps que dans le test.</span><span class="sxs-lookup"><span data-stu-id="fbc10-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="fbc10-416">Cela peut inclure hello suivant des idées.</span><span class="sxs-lookup"><span data-stu-id="fbc10-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="fbc10-417">Ajouter un nœud SQL 2e temporaire pour la haute disponibilité avant la migration hello avec un temps mort convenu.</span><span class="sxs-lookup"><span data-stu-id="fbc10-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="fbc10-418">Exécutez la migration hello en dehors d’Azure maintenance planifiée.</span><span class="sxs-lookup"><span data-stu-id="fbc10-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="fbc10-419">Vérifiez que vous avez correctement configuré votre quorum de cluster.</span><span class="sxs-lookup"><span data-stu-id="fbc10-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="fbc10-420">Ce scénario suppose que vous avez documenté votre installation et savez comment le stockage de hello est mappé dans classer les modifications toomake pour les paramètres du cache disque optimales.</span><span class="sxs-lookup"><span data-stu-id="fbc10-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="fbc10-421">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="fbc10-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="fbc10-423">Rendre hello local / remplacement hello Azure le contrôleur de domaine principal de SQL Server et les rendre hello autres partenaires de basculement automatique (AFP).</span><span class="sxs-lookup"><span data-stu-id="fbc10-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="fbc10-424">Recueillir des informations de configuration de disque de SQL2 et supprimer un nœud hello (ne pas supprimer les disques durs virtuels attachés).</span><span class="sxs-lookup"><span data-stu-id="fbc10-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="fbc10-425">Créez un compte de stockage Premium et copier les disques durs virtuels à partir de hello compte de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="fbc10-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="fbc10-426">Créez un nouveau service cloud et hello SQL2 VM avec ses disques primes stockage attachés.</span><span class="sxs-lookup"><span data-stu-id="fbc10-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="fbc10-427">Configurez l'ILB/ELB et ajoutez des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="fbc10-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="fbc10-428">Hello de mise à jour toujours l’écouteur d’avec équilibrage de charge interne nouveau / ELB IP adresse et testez le basculement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="fbc10-429">Vérifiez la configuration de DNS hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="fbc10-430">Hello AFP tooSQL2, puis migrer SQL1 et parcourez les étapes 2 à 5.</span><span class="sxs-lookup"><span data-stu-id="fbc10-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="fbc10-431">Testez les basculements.</span><span class="sxs-lookup"><span data-stu-id="fbc10-431">Test failovers.</span></span>
* <span data-ttu-id="fbc10-432">Commutateur tooSQL1 arrière de hello AFP et SQL2</span><span class="sxs-lookup"><span data-stu-id="fbc10-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="fbc10-433">Annexe : Migration d’un stockage de tooPremium toujours sur Cluster Multisite</span><span class="sxs-lookup"><span data-stu-id="fbc10-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="fbc10-434">reste Hello de cette rubrique fournit un exemple détaillé de la conversion d’un stockage de plusieurs site Always On cluster tooPremium.</span><span class="sxs-lookup"><span data-stu-id="fbc10-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="fbc10-435">Il convertit également hello écouteur à l’aide d’un équilibreur de charge interne de tooan équilibrage de charge externe (équilibrage de charge interne).</span><span class="sxs-lookup"><span data-stu-id="fbc10-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="fbc10-436">Environnement</span><span class="sxs-lookup"><span data-stu-id="fbc10-436">Environment</span></span>
* <span data-ttu-id="fbc10-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="fbc10-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="fbc10-438">1 base de données de fichiers sur SP</span><span class="sxs-lookup"><span data-stu-id="fbc10-438">1 DB Files on SP</span></span>
* <span data-ttu-id="fbc10-439">2 x pools de stockage par nœud</span><span class="sxs-lookup"><span data-stu-id="fbc10-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="fbc10-441">MV :</span><span class="sxs-lookup"><span data-stu-id="fbc10-441">VM:</span></span>
<span data-ttu-id="fbc10-442">Dans cet exemple, nous allons toodemonstrate déplacement à partir d’un tooILB ELB.</span><span class="sxs-lookup"><span data-stu-id="fbc10-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="fbc10-443">ELB était disponible avant l’équilibrage de charge interne, cet exemple montre comment toothis tooswitch pendant hello migration.</span><span class="sxs-lookup"><span data-stu-id="fbc10-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="fbc10-445">Étapes de Pre : Se connecter tooSubscription</span><span class="sxs-lookup"><span data-stu-id="fbc10-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="fbc10-446">Étape 1: créer les nouveaux compte de stockage et service cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
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

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="fbc10-447">Étape 2 : Hello d’augmentation autorisée des défaillances sur les ressources<Optional></span><span class="sxs-lookup"><span data-stu-id="fbc10-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="fbc10-448">Sur certaines ressources qui appartiennent tooyour toujours sur le groupe de disponibilité sont les limites de nombre d’échecs qui peut se produire pendant une période où le service de cluster hello va tenter de groupe de ressources toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="fbc10-449">Il est recommandé de qu'augmenter ce tandis que vous parcourez cette procédure, étant donné que si vous n’avez pas manuellement les basculements de basculement et de déclencheur en arrêtant ordinateurs, vous peuvent obtenir toothis fermer limite.</span><span class="sxs-lookup"><span data-stu-id="fbc10-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="fbc10-450">Il serait être prudent toodouble l’allocation échec hello, toodo ce gestionnaire du Cluster de basculement, consultez des propriétés toohello hello Always On du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="fbc10-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="fbc10-452">Modifier hello too6 du nombre maximal de pannes.</span><span class="sxs-lookup"><span data-stu-id="fbc10-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="fbc10-453">Étape 3 : ajouter une ressource d’adresse IP au groupe de clusters <Optional></span><span class="sxs-lookup"><span data-stu-id="fbc10-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="fbc10-454">Si vous avez une seule adresse IP pour hello groupe du Cluster et il est aligné toohello cloud sous-réseau, soyez attentif aux, si vous accidentellement Mettez hors connexion tous les nœuds de cluster dans le cloud de hello que réseau puis de ressource d’adresse IP du Cluster hello et de nom réseau du Cluster seront pas en mesure de toocome en ligne.</span><span class="sxs-lookup"><span data-stu-id="fbc10-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="fbc10-455">Bonjour événements de ce qu’il empêchera met à jour les ressources de cluster tooother.</span><span class="sxs-lookup"><span data-stu-id="fbc10-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="fbc10-456">Étape 4 : configuration DNS</span><span class="sxs-lookup"><span data-stu-id="fbc10-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="fbc10-457">une transition en douceur dépend de la manière dont DNS est en cours de tooimplement utilisés et mis à jour.</span><span class="sxs-lookup"><span data-stu-id="fbc10-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="fbc10-458">Always On est installé, il crée un groupe de ressources de Cluster Windows, si vous ouvrez le Gestionnaire du Cluster de basculement, vous verrez qu’au minimum, il aura trois ressources, hello deux hello document fait référence à tooare :</span><span class="sxs-lookup"><span data-stu-id="fbc10-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="fbc10-459">Nom de réseau virtuel (VNN) – il s’agit hello DNS nom de ce client se connecter toowhen souhaitant tooconnect tooSQL serveurs via Always On.</span><span class="sxs-lookup"><span data-stu-id="fbc10-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="fbc10-460">Ressource d’adresse IP : il s’agit de hello d’adresses IP associées aux hello VNN, vous pouvez avoir plusieurs, et dans une configuration multisite, vous aurez une adresse IP par sous-réseau/site.</span><span class="sxs-lookup"><span data-stu-id="fbc10-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="fbc10-461">Lors de la connexion tooSQL Server, le pilote de SQL Server Client hello récupère les enregistrements DNS de hello associés au port d’écoute hello et essayez tooconnect tooeach Always On associées adresse IP, ci-dessous, nous aborderons certains facteurs pouvant influencer cela.</span><span class="sxs-lookup"><span data-stu-id="fbc10-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="fbc10-462">Hello nombre d’enregistrements DNS simultanées qui sont associés au nom de l’écouteur hello dépend non seulement de nombre hello d’adresses IP, mais hello ' RegisterAllIpProviders'setting dans le Clustering de basculement pour hello les ressources Always ON VNN.</span><span class="sxs-lookup"><span data-stu-id="fbc10-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="fbc10-463">Lorsque vous déployez Always On dans Azure il y a des étapes différentes toocreate hello écouteur et les adresses IP, toomanually configurer hello 'RegisterAllIpProviders' too1, cela est tooan autre déploiement Always On local où il est déjà défini too1.</span><span class="sxs-lookup"><span data-stu-id="fbc10-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="fbc10-464">Si 'RegisterAllIpProviders' est 0, puis vous verrez seulement un enregistrement DNS dans DNS associé hello écouteur :</span><span class="sxs-lookup"><span data-stu-id="fbc10-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="fbc10-466">Si 'RegisterAllIpProviders' est 1 :</span><span class="sxs-lookup"><span data-stu-id="fbc10-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="fbc10-468">code Hello ci-dessous vider les paramètres VNN hello et définissez-le pour vous, veuillez Remarque, Pourquoi modifier tootake effet, vous devez tootake hello VNN hors connexion et activez de nouveau en ligne, cette prise hello hors connexion à l’origine interruptions de connectivité client écouteur.</span><span class="sxs-lookup"><span data-stu-id="fbc10-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="fbc10-469">Dans une étape ultérieure de la migration, vous devez tooupdate hello Always On écouteur avec l’adresse IP mise à jour qui fera référence à un équilibrage de charge, cela implique une suppression de ressource d’adresse IP et l’addition.</span><span class="sxs-lookup"><span data-stu-id="fbc10-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="fbc10-470">Après la mise à jour de hello IP, vous devez tooensure hello nouvelle adresse IP a été mis à jour dans la Zone DNS et que les clients de hello sont à jour son cache DNS local.</span><span class="sxs-lookup"><span data-stu-id="fbc10-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="fbc10-471">Si vos clients se trouvent dans un segment de réseau et faire référence à un autre serveur DNS, vous devez tooconsider que se passe-t-il sur le transfert de Zone DNS pendant la migration de hello, reconnecter hello application heure sera contraint au moins hello temps de transfert de Zone de toutes les nouvelles adresses IP pour le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="fbc10-472">Si vous êtes sous contrainte de temps ici, vous devez discuter test forcer un transfert de zone incrémentiel avec vos équipes de Windows, et également placer hello DNS tooa enregistrement d’hôte inférieur durée tooLive (TTL), afin de mettre à jour des clients de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="fbc10-473">Pour plus d’informations, consultez [Transferts de zone incrémentiels](https://technet.microsoft.com/library/cc958973.aspx) et [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc10-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="fbc10-474">Est de 1200 secondes par hello de valeur par défaut durée de vie pour l’enregistrement DNS associé hello écouteur dans Always On dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc10-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="fbc10-475">Vous souhaiterez peut-être tooreduce cela si vous êtes sous contrainte de temps pendant votre migration tooensure hello clients mise à jour leurs DNS avec adresse IP hello mis à jour une adresse pour l’écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="fbc10-476">Vous pouvez consulter et modifier la configuration de hello en vidant configuration hello Hello VNN :</span><span class="sxs-lookup"><span data-stu-id="fbc10-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="fbc10-477">Notez hello inférieur de hello 'HostRecordTTL', un montant supérieur du trafic DNS se produit.</span><span class="sxs-lookup"><span data-stu-id="fbc10-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="fbc10-478">Paramètres de l’application cliente</span><span class="sxs-lookup"><span data-stu-id="fbc10-478">Client application settings</span></span>
<span data-ttu-id="fbc10-479">Si votre application prend en charge SQL client hello .net 4.5 SQLClient, puis vous pouvez utiliser « MULTISUBNETFAILOVER = TRUE' (mot clé), cette opération est recommandée toobe appliquée car elle permet au cours du basculement plus rapide connexion tooSQL toujours sur le groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="fbc10-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="fbc10-480">Il énumère toutes les adresses IP associés hello toujours sur l’écouteur en parallèle et effectue une vitesse de nouvelle tentative de connexion TCP plus agressive lors d’un basculement.</span><span class="sxs-lookup"><span data-stu-id="fbc10-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="fbc10-481">Pour plus d’informations sur les paramètres de hello ci-dessus, consultez [mot clé MultiSubnetFailover et fonctionnalités associées aux](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span><span class="sxs-lookup"><span data-stu-id="fbc10-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="fbc10-482">Consultez également [Prise en charge SqlClient pour la haute disponibilité et récupération d’urgence](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc10-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="fbc10-483">Étape 5 : paramètres de quorum de cluster</span><span class="sxs-lookup"><span data-stu-id="fbc10-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="fbc10-484">Comme vous vous apprêtez toobe prendre au moins un serveur SQL vers le bas à la fois, vous devez modifier la configuration de quorum du cluster hello, si avec fichier partage témoin de 2 nœuds, vous devez définir tooallow nœud majoritaire hello quorum et utiliser le vote dynamique, il s’agit de tooallow pour un permanent de tooremain nœud unique.</span><span class="sxs-lookup"><span data-stu-id="fbc10-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="fbc10-485">Pour plus d’informations sur la gestion et la configuration de quorum du cluster hello, consultez [configurer et gérer le Quorum dans un Cluster de basculement Windows Server 2012 de hello](https://technet.microsoft.com/library/jj612870.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc10-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="fbc10-486">Étape 6 : extraction des points de terminaison et des ACL existants</span><span class="sxs-lookup"><span data-stu-id="fbc10-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="fbc10-487">Enregistrer ces fichiers de texte tooa.</span><span class="sxs-lookup"><span data-stu-id="fbc10-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="fbc10-488">Étape 7 : modification les partenaires de basculement et des modes de réplication</span><span class="sxs-lookup"><span data-stu-id="fbc10-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="fbc10-489">Si vous avez plus de 2 serveurs SQL Server, vous devez modifier hello de basculement d’une autre base de données secondaire dans un autre contrôleur de domaine ou local 'too'Synchronous et que vous un partenaire de basculement automatique (AFP), il s’agit donc mettre à jour de la haute disponibilité tandis que vous apportez des modifications.</span><span class="sxs-lookup"><span data-stu-id="fbc10-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="fbc10-490">Vous pouvez le faire via TSQL ou via SSMS :</span><span class="sxs-lookup"><span data-stu-id="fbc10-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="fbc10-492">Étape 8 : Suppression de la machine virtuelle secondaire du service cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="fbc10-493">Vous devez planifier toomigrate un nœud secondaire du cloud en premier lieu, s’il s’agit actuellement principal, vous devez entreprendre un basculement manuel.</span><span class="sxs-lookup"><span data-stu-id="fbc10-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

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

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="fbc10-494">Étape 9 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement</span><span class="sxs-lookup"><span data-stu-id="fbc10-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="fbc10-495">Pour les volumes de données il doivent être définis tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="fbc10-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="fbc10-496">Pour les volumes TLOG ces doivent être définis tooNONE.</span><span class="sxs-lookup"><span data-stu-id="fbc10-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="fbc10-498">Étape 10 : copie de disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="fbc10-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
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



<span data-ttu-id="fbc10-499">Vous pouvez vérifier l’état de la copie de disques durs virtuels de hello toohello compte de stockage Premium hello :</span><span class="sxs-lookup"><span data-stu-id="fbc10-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

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

<span data-ttu-id="fbc10-501">Attendez que toutes ces opérations soient correctement terminées.</span><span class="sxs-lookup"><span data-stu-id="fbc10-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="fbc10-502">Pour plus d'informations pour les objets BLOB individuels :</span><span class="sxs-lookup"><span data-stu-id="fbc10-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="fbc10-503">Étape 11 : inscription du disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="fbc10-503">Step 11: Register OS disk</span></span>
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="fbc10-504">Étape 12 : importation d’un serveur secondaire dans un nouveau service cloud</span><span class="sxs-lookup"><span data-stu-id="fbc10-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="fbc10-505">code Hello ci-dessous utilise également les hello ajouté option ici vous pouvez importer un ordinateur hello et utiliser VIP conservables de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
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

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="fbc10-506">Étape 13 : création d'un ILB sur le nouveau service cloud, ajout de points terminaux d'équilibrage de charge et d'ACL</span><span class="sxs-lookup"><span data-stu-id="fbc10-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
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

#### <a name="step-14-update-always-on"></a><span data-ttu-id="fbc10-507">Étape 14 : mise à jour d’Always On</span><span class="sxs-lookup"><span data-stu-id="fbc10-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="fbc10-509">Supprimer le service de cloud computing ancien hello adresse IP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="fbc10-511">Étape 15 : vérification de la mise à jour DNS</span><span class="sxs-lookup"><span data-stu-id="fbc10-511">Step 15: DNS update check</span></span>
<span data-ttu-id="fbc10-512">Vous devez maintenant vérifier les serveurs DNS sur votre réseau de client SQL Server et assurez-vous que le clustering a ajouté hello enregistrement d’hôte supplémentaires pour hello ajouté l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="fbc10-513">Si ces serveurs DNS n’ont pas été mis à jour, envisagez de forcer un transfert de Zone DNS et vous assurer que les clients dans un sous-réseau il n’y a hello sont en mesure de tooresolve tooboth toujours sur des adresses IP, il s’agit donc vous n’avez pas besoin de toowait pour la réplication DNS automatique.</span><span class="sxs-lookup"><span data-stu-id="fbc10-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="fbc10-514">Étape 16 : reconfiguration d’Always On</span><span class="sxs-lookup"><span data-stu-id="fbc10-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="fbc10-515">À ce stade vous attendez hello secondaire ce nœud qui a été migré toofully se resynchroniser avec le nœud local de hello et nœud de réplication toosynchronous et rendre hello AFP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="fbc10-516">Étape 17 : migration du deuxième nœud</span><span class="sxs-lookup"><span data-stu-id="fbc10-516">Step 17: Migrate second node</span></span>
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

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="fbc10-517">Étape 18 : modification des paramètres de mise en cache du disque dans un fichier CSV et enregistrement</span><span class="sxs-lookup"><span data-stu-id="fbc10-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="fbc10-518">Pour les volumes de données il doivent être définis tooREADONLY.</span><span class="sxs-lookup"><span data-stu-id="fbc10-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="fbc10-519">Pour les volumes TLOG ces doivent être définis tooNONE.</span><span class="sxs-lookup"><span data-stu-id="fbc10-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="fbc10-521">Étape 19 : création d'un nouveau compte de stockage indépendant pour le nœud secondaire</span><span class="sxs-lookup"><span data-stu-id="fbc10-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="fbc10-522">Étape 20 : copie de disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="fbc10-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
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


<span data-ttu-id="fbc10-523">Vous pouvez vérifier l’état de copie du disque dur virtuel hello pour tous les VHD : ForEach ($disk dans $diskobjects) {$lun = $disk. Numéro d’unité logique $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Étiquette disquette $diskName = $disk. DiskName</span><span class="sxs-lookup"><span data-stu-id="fbc10-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="fbc10-525">Attendez que toutes ces opérations soient correctement terminées.</span><span class="sxs-lookup"><span data-stu-id="fbc10-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="fbc10-526">Pour plus d'informations pour les objets BLOB individuels :</span><span class="sxs-lookup"><span data-stu-id="fbc10-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="fbc10-527">Étape 21 : inscription du disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="fbc10-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
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

    #Join tooexisting Avaiability Set

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

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="fbc10-528">Étape 22 : ajout de points de terminaison et de ACL avec équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="fbc10-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="fbc10-529">Étape 23 : test du basculement</span><span class="sxs-lookup"><span data-stu-id="fbc10-529">Step 23: Test failover</span></span>
<span data-ttu-id="fbc10-530">Vous devez permettent désormais de nœud migrés de hello synchroniser avec hello local toujours sur le nœud, placez-le dans le mode de réplication toosynchronous et attendez qu’il est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="fbc10-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="fbc10-531">Basculement local toohello premier nœud migrées, c'est-à-dire hello AFP.</span><span class="sxs-lookup"><span data-stu-id="fbc10-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="fbc10-532">Une fois qu’a précédemment fonctionné, dernière modification hello migration AFP toohello de nœud.</span><span class="sxs-lookup"><span data-stu-id="fbc10-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="fbc10-533">Vous devez les tests de basculement entre tous les nœuds et exécuter que les tests chaos tooensure basculements fonctionnent comme prévu et dans un mode en temps voulu.</span><span class="sxs-lookup"><span data-stu-id="fbc10-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="fbc10-534">Étape 24 : réinitialisation des paramètres du quorum de cluster / TTL DNS / Partenaires de basculement / Paramètres de synchronisation</span><span class="sxs-lookup"><span data-stu-id="fbc10-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="fbc10-535">Ajout de ressource d'adresse IP sur le même sous-réseau</span><span class="sxs-lookup"><span data-stu-id="fbc10-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="fbc10-536">Si vous avez seulement 2 serveurs SQL Server et que vous souhaitez toomigrate les tooa nouveau service cloud, mais souhaitez tookeep sur hello même sous-réseau, vous pouvez éviter de créer de port d’écoute hello toodelete hors connexion d’origine de hello toujours sur l’adresse IP et ajouter la nouvelle adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="fbc10-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="fbc10-537">Si vous migrez un sous-réseau de tooanother de machines virtuelles hello vous en n'aurez pas besoin toodo comme il y aura un réseau de cluster supplémentaire qui fera référence à ce sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="fbc10-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="fbc10-538">Une fois que vous avez affiché hello migrer la base de données secondaire et ajouté dans la nouvelle ressource d’adresse IP hello pour le nouveau service de cloud hello avant basculement hello principal existant, vous devez effectuer ces opérations dans hello Gestionnaire du Cluster de basculement :</span><span class="sxs-lookup"><span data-stu-id="fbc10-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="fbc10-539">tooadd dans l’adresse IP, consultez hello [annexe](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), étape 14.</span><span class="sxs-lookup"><span data-stu-id="fbc10-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="fbc10-540">Pour la ressource d’adresse IP actuelle hello, modifier hello propriétaire possible too'Existing principal SQL Server », dans l’exemple hello ci-dessous, « dansqlams4 » :</span><span class="sxs-lookup"><span data-stu-id="fbc10-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="fbc10-542">Nouvelle ressource d’adresse IP hello, modifiez hello propriétaire possible too'Migrated secondaire SQL Server », dans l’exemple hello ci-dessous, « dansqlams5 » :</span><span class="sxs-lookup"><span data-stu-id="fbc10-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="fbc10-544">Une fois cette vous pouvez basculer et lors de la migration du dernier nœud hello hello des propriétaires possibles doivent être modifiés afin de ce nœud est ajouté comme propriétaire Possible :</span><span class="sxs-lookup"><span data-stu-id="fbc10-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="fbc10-546">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fbc10-546">Additional resources</span></span>
* [<span data-ttu-id="fbc10-547">Stockage Premium Azure</span><span class="sxs-lookup"><span data-stu-id="fbc10-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="fbc10-548">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="fbc10-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="fbc10-549">SQL Server dans des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="fbc10-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
