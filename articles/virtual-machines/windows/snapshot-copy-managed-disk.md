---
title: "aaaCreate une copie d’un disque géré de Azure pour sauvegarder | Documents Microsoft"
description: "Découvrez comment toocreate émet une copie d’un toouse des disques gérés Azure précédent ou de résolution des problèmes de disque."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="81316-103">Créer une copie d’un disque dur virtuel stocké en tant que disque Azure géré à l’aide de captures instantanées gérées</span><span class="sxs-lookup"><span data-stu-id="81316-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="81316-104">Prendre un instantané d’un disque géré pour la sauvegarde ou créer un disque gérés à partir de la capture instantanée de hello et attachez-le tootroubleshoot de machine virtuelle de test tooa.</span><span class="sxs-lookup"><span data-stu-id="81316-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="81316-105">Une capture instantanée gérée est une copie complète d’un disque géré de machine virtuelle à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="81316-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="81316-106">Elle crée une copie en lecture seule de votre disque dur virtuel et, par défaut, le stocke sous la forme d’un disque géré Standard.</span><span class="sxs-lookup"><span data-stu-id="81316-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="81316-107">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="81316-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="81316-108">Pour plus d’informations sur la tarification, consultez la page [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="81316-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="81316-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="81316-109">Before you begin</span></span>
<span data-ttu-id="81316-110">Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="81316-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="81316-111">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="81316-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="81316-112">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="81316-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="81316-113">Copiez hello disque dur virtuel avec un instantané</span><span class="sxs-lookup"><span data-stu-id="81316-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="81316-114">Utiliser PowerShell tootake un instantané de hello géré disque ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="81316-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="81316-115">Utilisez tootake portail Azure un instantané</span><span class="sxs-lookup"><span data-stu-id="81316-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="81316-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81316-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81316-117">Désormais, dans le coin supérieur gauche de hello, cliquez sur **nouveau** et recherchez **instantané**.</span><span class="sxs-lookup"><span data-stu-id="81316-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="81316-118">Dans le panneau de la capture instantanée hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="81316-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="81316-119">Entrez un **nom** pour la capture instantanée de hello.</span><span class="sxs-lookup"><span data-stu-id="81316-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="81316-120">Sélectionnez un existant [groupe de ressources](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau.</span><span class="sxs-lookup"><span data-stu-id="81316-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="81316-121">Sélectionnez un emplacement de centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="81316-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="81316-122">Pour **disque Source**, sélectionnez hello toosnapshot de disques gérés.</span><span class="sxs-lookup"><span data-stu-id="81316-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="81316-123">Sélectionnez hello **type de compte** instantané d’hello toouse toostore.</span><span class="sxs-lookup"><span data-stu-id="81316-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="81316-124">Nous vous recommandons d’utiliser le type **Standard_LRS**, sauf si vous avez besoin de la stocker sur un disque hautes performances.</span><span class="sxs-lookup"><span data-stu-id="81316-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="81316-125">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="81316-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="81316-126">Utilisez PowerShell tootake un instantané</span><span class="sxs-lookup"><span data-stu-id="81316-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="81316-127">Hello suit afficher vous tooget hello disque dur virtuel de disque toobe copié, créer des configurations de capture instantanée hello et prenez un instantané du disque de hello en utilisant l’applet de commande New-AzureRmSnapshot de hello<!--Add link toocmdlet when available-->.</span><span class="sxs-lookup"><span data-stu-id="81316-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="81316-128">Définissez certains paramètres.</span><span class="sxs-lookup"><span data-stu-id="81316-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="81316-129">Remplacez les valeurs de paramètre hello :</span><span class="sxs-lookup"><span data-stu-id="81316-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="81316-130">« myResourceGroup » avec le groupe de ressources de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="81316-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="81316-131">« southeastasia » avec hello zone géographique où vous souhaitez votre instantané gérés stockées.</span><span class="sxs-lookup"><span data-stu-id="81316-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="81316-132">« ContosoMD_datadisk1 » avec le nom de hello du disque du disque dur virtuel hello que vous souhaitez toocopy.</span><span class="sxs-lookup"><span data-stu-id="81316-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="81316-133">« ContosoMD_datadisk1_snapshot1 » avec hello nom que vous souhaitez toouse du nouvel instantané hello.</span><span class="sxs-lookup"><span data-stu-id="81316-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="81316-134">Obtenir toobe de disque hello disque dur virtuel copié.</span><span class="sxs-lookup"><span data-stu-id="81316-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="81316-135">Créer des configurations de capture instantanée hello.</span><span class="sxs-lookup"><span data-stu-id="81316-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="81316-136">Prendre un instantané hello.</span><span class="sxs-lookup"><span data-stu-id="81316-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="81316-137">Toouse hello instantané toocreate un disque géré et d’attacher une machine virtuelle qui doit effectuer haute toobe, utilisez le paramètre hello `-AccountType Premium_LRS` avec la commande hello AzureRmSnapshot de nouveau.</span><span class="sxs-lookup"><span data-stu-id="81316-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="81316-138">paramètre Hello crée l’instantané d’hello afin qu’il est stocké comme disque Premium gérés.</span><span class="sxs-lookup"><span data-stu-id="81316-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="81316-139">Les disques gérés Premium sont plus chers que les disques gérés Standard.</span><span class="sxs-lookup"><span data-stu-id="81316-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="81316-140">Vérifiez qu’il vous faut vraiment le niveau Premium avant d’utiliser ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="81316-140">So be sure you really need Premium before using that parameter.</span></span>


