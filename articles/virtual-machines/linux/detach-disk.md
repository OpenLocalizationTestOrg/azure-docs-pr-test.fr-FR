---
title: "aaaDetach un disque de données à partir d’un VM Linux - Azure | Documents Microsoft"
description: "En savoir plus toodetach un disque de données à partir d’une machine virtuelle dans Azure à l’aide de CLI 2.0 ou hello portail Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="74d9e-103">Toodetach données de disque à partir d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="74d9e-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="74d9e-104">Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher.</span><span class="sxs-lookup"><span data-stu-id="74d9e-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="74d9e-105">Cela supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne le supprime pas de stockage.</span><span class="sxs-lookup"><span data-stu-id="74d9e-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="74d9e-106">Si vous détachez un disque, il n’est pas supprimé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="74d9e-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="74d9e-107">Si vous êtes abonné tooPremium stockage, vous continuerez tooincur des frais de stockage pour le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="74d9e-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="74d9e-108">Pour plus d’informations, consultez trop[tarification et facturation lors de l’utilisation du stockage Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="74d9e-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="74d9e-109">Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.</span><span class="sxs-lookup"><span data-stu-id="74d9e-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="74d9e-110">Détacher un disque de données à l’aide de CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="74d9e-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="74d9e-111">disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="74d9e-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="74d9e-112">Détacher un disque de données à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="74d9e-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="74d9e-113">Dans le concentrateur de portail hello, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="74d9e-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="74d9e-114">Sélectionnez la machine virtuelle hello qui possède le disque de données hello toodetach et cliquez sur **arrêter** toodeallocate hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="74d9e-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="74d9e-115">Dans le panneau de la machine virtuelle hello, sélectionnez **disques**.</span><span class="sxs-lookup"><span data-stu-id="74d9e-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="74d9e-116">En haut de hello Hello **disques** panneau, sélectionnez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="74d9e-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="74d9e-117">Bonjour **disques** panneau, toohello plus à droite hello du disque de données que vous aimeriez toodetach, cliquez sur hello ![détacher l’image du bouton](./media/detach-disk/detach.png) bouton détacher.</span><span class="sxs-lookup"><span data-stu-id="74d9e-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="74d9e-118">Après la suppression de disque de hello, cliquez sur Enregistrer en haut de hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="74d9e-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="74d9e-119">Dans le panneau de la machine virtuelle hello, cliquez sur **vue d’ensemble** puis cliquez sur hello **Démarrer** bouton haut hello hello toorestart de panneau hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="74d9e-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="74d9e-120">disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="74d9e-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="74d9e-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="74d9e-121">Next steps</span></span>
<span data-ttu-id="74d9e-122">Si vous souhaitez que le disque de données hello tooreuse, vous pouvez juste [attachez-le tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="74d9e-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

