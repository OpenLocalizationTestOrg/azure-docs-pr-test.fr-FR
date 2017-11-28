---
title: "aaaDetach un disque de données à partir d’une machine virtuelle Windows - Azure | Documents Microsoft"
description: "En savoir plus toodetach un disque de données à partir d’une machine virtuelle dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a><span data-ttu-id="293cc-103">Toodetach données de disque à partir d’une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="293cc-103">How toodetach a data disk from a Windows virtual machine</span></span>
<span data-ttu-id="293cc-104">Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher.</span><span class="sxs-lookup"><span data-stu-id="293cc-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="293cc-105">Cela supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne le supprime pas de stockage.</span><span class="sxs-lookup"><span data-stu-id="293cc-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span>

> [!WARNING]
> <span data-ttu-id="293cc-106">Si vous détachez un disque, il n’est pas supprimé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="293cc-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="293cc-107">Si vous êtes abonné tooPremium stockage, vous continuerez tooincur des frais de stockage pour le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="293cc-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="293cc-108">Pour plus d’informations, consultez trop[tarification et facturation lors de l’utilisation du stockage Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="293cc-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span>
>
>

<span data-ttu-id="293cc-109">Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.</span><span class="sxs-lookup"><span data-stu-id="293cc-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>

## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="293cc-110">Détacher un disque de données à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="293cc-110">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="293cc-111">Dans le concentrateur de portail hello, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="293cc-111">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="293cc-112">Sélectionnez la machine virtuelle hello qui possède le disque de données hello toodetach et cliquez sur **arrêter** toodeallocate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="293cc-112">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="293cc-113">Dans le panneau de la machine virtuelle hello, sélectionnez **disques**.</span><span class="sxs-lookup"><span data-stu-id="293cc-113">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="293cc-114">En haut de hello Hello **disques** panneau, sélectionnez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="293cc-114">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="293cc-115">Bonjour **disques** panneau, toohello plus à droite hello du disque de données que vous aimeriez toodetach, cliquez sur hello ![détacher l’image du bouton](./media/detach-disk/detach.png) bouton détacher.</span><span class="sxs-lookup"><span data-stu-id="293cc-115">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="293cc-116">Après la suppression de disque de hello, cliquez sur Enregistrer en haut de hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="293cc-116">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="293cc-117">Dans le panneau de la machine virtuelle hello, cliquez sur **vue d’ensemble** puis cliquez sur hello **Démarrer** bouton haut hello hello toorestart de panneau hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="293cc-117">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>



<span data-ttu-id="293cc-118">disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="293cc-118">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>

## <a name="detach-a-data-disk-using-powershell"></a><span data-ttu-id="293cc-119">Détacher un disque de données avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="293cc-119">Detach a data disk using PowerShell</span></span>
<span data-ttu-id="293cc-120">Dans cet exemple, hello la première commande obtient hello ordinateur virtuel nommé **MyVM07** Bonjour **RG11** groupe de ressources à l’aide d’applet de commande Get-AzureRmVM de hello.</span><span class="sxs-lookup"><span data-stu-id="293cc-120">In this example, hello first command gets hello virtual machine named **MyVM07** in hello **RG11** resource group using hello Get-AzureRmVM cmdlet.</span></span> <span data-ttu-id="293cc-121">Hello commande magasins hello machine virtuelle dans hello **$VirtualMachine** variable.</span><span class="sxs-lookup"><span data-stu-id="293cc-121">hello command stores hello virtual machine in hello **$VirtualMachine** variable.</span></span>

<span data-ttu-id="293cc-122">commande deuxième Hello supprime le disque de données hello nommé DataDisk3 à partir de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="293cc-122">hello second command removes hello data disk named DataDisk3 from hello virtual machine.</span></span>

<span data-ttu-id="293cc-123">commande finale Hello met à jour l’état hello du processus de hello toocomplete hello machine virtuelle de la suppression de disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="293cc-123">hello final command updates hello state of hello virtual machine toocomplete hello process of removing hello data disk.</span></span>

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

<span data-ttu-id="293cc-124">Pour plus d’informations, consultez [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="293cc-124">For more information, see [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).</span></span>

## <a name="next-steps"></a><span data-ttu-id="293cc-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="293cc-125">Next steps</span></span>
<span data-ttu-id="293cc-126">Si vous souhaitez que le disque de données hello tooreuse, vous pouvez juste [attachez-le tooanother machine virtuelle](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="293cc-126">If you want tooreuse hello data disk, you can just [attach it tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

