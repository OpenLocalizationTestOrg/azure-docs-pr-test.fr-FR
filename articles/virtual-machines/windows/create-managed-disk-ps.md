---
title: "aaaCreate un disque géré à partir d’un disque dur virtuel dans Azure | Documents Microsoft"
description: "Créer un disque géré à partir d’un disque dur virtuel est en cours d’un compte de stockage Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="fd06c-103">Créer des disques gérés à partir de disques non gérés dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="fd06c-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="fd06c-104">Un disque géré peut être créé à partir d’un disque de données ou d’un disque du système d’exploitation existant hébergé dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fd06c-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="fd06c-105">Vous pouvez également créer un disque vide utilisable comme nouveau disque de données pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fd06c-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fd06c-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fd06c-106">Before you begin</span></span>
<span data-ttu-id="fd06c-107">Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="fd06c-107">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="fd06c-108">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="fd06c-108">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="fd06c-109">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd06c-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="fd06c-110">Créer un disque géré à partir d’un disque dur virtuel dans un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="fd06c-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="fd06c-111">Dans l’exemple hello nous créer un disque à partir d’un disque dur virtuel en tant que disque géré et affectez-le toohello paramètre **$disque1** toouse plus tard.</span><span class="sxs-lookup"><span data-stu-id="fd06c-111">In hello example we create a disk from a VHD as managed disk and assign it toohello parameter **$disk1** toouse later.</span></span> 

<span data-ttu-id="fd06c-112">Hello disque géré sera créé dans hello **ouest des États-Unis** emplacement, dans un groupe de ressources nommé **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd06c-112">hello managed disk will be created in hello **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="fd06c-113">disque de Hello sera nommé **myDisk** et il sera créé à partir d’un fichier de disque dur virtuel nommé **myDisk.vhd** nous téléchargé précédemment tooa compte de stockage nommé **mystorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="fd06c-113">hello disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded tooa storage account named **mystorageaccount**.</span></span> <span data-ttu-id="fd06c-114">disque géré de Hello sera créé dans le stockage de premium localement redondant (LRS).</span><span class="sxs-lookup"><span data-stu-id="fd06c-114">hello managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="fd06c-115">StandardLRS et PremiumLRS sont hello uniquement **- AccountType** options disponibles pour des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="fd06c-115">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="fd06c-116">Définir les paramètres requis</span><span class="sxs-lookup"><span data-stu-id="fd06c-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="fd06c-117">Créer un disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="fd06c-117">Create hello data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="fd06c-118">Créez un disque de données vide comme disque géré</span><span class="sxs-lookup"><span data-stu-id="fd06c-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="fd06c-119">Dans l’exemple hello nous créer un disque de données vide en tant que disque géré et affectez-le toohello paramètre **dataDisk2 $** toouse plus tard.</span><span class="sxs-lookup"><span data-stu-id="fd06c-119">In hello example we create an empty data disk as managed disk and assign it toohello parameter **$dataDisk2** toouse later.</span></span> <span data-ttu-id="fd06c-120">Un disque de données vide devez toobe initialisé la connexion toohello machine virtuelle et à l’aide de diskmgmt.msc ou [à distance via WinRM et un script](attach-disk-ps.md#initialize-the-disk), une fois qu’il est attaché tooa machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fd06c-120">An empty data disk will need toobe initialized logging in toohello VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached tooa running VM.</span></span>

<span data-ttu-id="fd06c-121">disque de données vide Hello sera créé dans hello **ouest des États-Unis** emplacement, dans un groupe de ressources nommé **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="fd06c-121">hello empty data disk will be created in hello **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="fd06c-122">disque de Hello sera nommé **myEmptyDataDisk**.</span><span class="sxs-lookup"><span data-stu-id="fd06c-122">hello disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="fd06c-123">un disque vide Hello sera créé dans le stockage de premium localement redondant (LRS).</span><span class="sxs-lookup"><span data-stu-id="fd06c-123">hello empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="fd06c-124">StandardLRS et PremiumLRS sont hello uniquement **- AccountType** options disponibles pour des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="fd06c-124">StandardLRS and PremiumLRS are hello only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="fd06c-125">taille du disque Hello dans cet exemple est de 128 Go, mais vous devez choisir une taille qui répond aux besoins de hello de toutes les applications en cours d’exécution sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fd06c-125">hello disk size in this example is 128GB, but you should choose a size that meets hello needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="fd06c-126">Définir les paramètres requis</span><span class="sxs-lookup"><span data-stu-id="fd06c-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="fd06c-127">Créer un disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="fd06c-127">Create hello data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="fd06c-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fd06c-128">Next Steps</span></span>   
- <span data-ttu-id="fd06c-129">Si vous disposez déjà d’une machine virtuelle, vous pouvez y [attacher un disque de données](attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fd06c-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
