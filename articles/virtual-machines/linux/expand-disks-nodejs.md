---
title: "Développer le disque du système d’exploitation sur une machine virtuelle Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Cet article explique comment développer le disque virtuel du système d’exploitation sur une machine virtuelle Linux à l’aide de l’interface Azure CLI 1.0 et du modèle de déploiement Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="fe289-103">Développer le disque de système d’exploitation sur une machine virtuelle Linux à l’aide de l’interface Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fe289-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="fe289-104">La taille par défaut de disque virtuel pour le système d’exploitation est généralement de 30 Go sur une machine virtuelle Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fe289-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="fe289-105">Vous pouvez [ajouter des disques de données](add-disk.md) afin d’offrir un espace de stockage supplémentaire, mais vous pouvez également développer le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fe289-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="fe289-106">Cet article vous explique comment développer le disque du système d’exploitation sur une machine virtuelle Linux à l’aide de disques non managés avec l’interface Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="fe289-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="fe289-107">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="fe289-107">CLI versions to complete the task</span></span>
<span data-ttu-id="fe289-108">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="fe289-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="fe289-109">[Azure CLI 1.0](#prerequisites) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="fe289-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fe289-110">[Azure CLI 2.0](expand-disks.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe289-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe289-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fe289-111">Prerequisites</span></span>
<span data-ttu-id="fe289-112">La [dernière version de l’interface Azure CLI 1.0](../../cli-install-nodejs.md) doit être installée et connectée à un [compte Azure](https://azure.microsoft.com/pricing/free-trial/) à l’aide du mode Resource Manager comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe289-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="fe289-113">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="fe289-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fe289-114">Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fe289-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="fe289-115">Développer le disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="fe289-115">Expand OS disk</span></span>

1. <span data-ttu-id="fe289-116">Il est impossible d’exécuter les opérations sur les disques durs virtuels avec la machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fe289-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="fe289-117">L’exemple suivant arrête et redéploie la machine virtuelle nommée *myVM* dans le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="fe289-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="fe289-118">`azure vm stop` ne publie pas les ressources de calcul.</span><span class="sxs-lookup"><span data-stu-id="fe289-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="fe289-119">Pour publier les ressources de calcul, utilisez `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="fe289-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="fe289-120">La machine virtuelle doit être libérée pour développer le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="fe289-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="fe289-121">Modifiez la taille du disque non géré du système d’exploitation à l’aide de la commande `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="fe289-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="fe289-122">L’exemple suivant met à jour la machine virtuelle nommée *myVM* dans le groupe de ressources nommé *myResourceGroup* sur la valeur de *50* Go :</span><span class="sxs-lookup"><span data-stu-id="fe289-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="fe289-123">Démarrez votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="fe289-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="fe289-124">Établissez une connexion SSH à votre machine virtuelle à l’aide des informations d’identification appropriées.</span><span class="sxs-lookup"><span data-stu-id="fe289-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="fe289-125">Pour vérifier que le disque du système d’exploitation a été redimensionné, utilisez `df -h`.</span><span class="sxs-lookup"><span data-stu-id="fe289-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="fe289-126">La sortie de l’exemple suivant indique que la partition primaire (*/dev/sda1*) est désormais de 50 Go :</span><span class="sxs-lookup"><span data-stu-id="fe289-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="fe289-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe289-127">Next steps</span></span>
<span data-ttu-id="fe289-128">Si vous avez besoin de stockage supplémentaire, vous pouvez également [ajouter des disques de données à une machine virtuelle Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fe289-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="fe289-129">Pour plus d’informations sur le chiffrement de disque, consultez la section [Chiffrer des disques sur une machine virtuelle Linux à l’aide de l’interface de ligne de commande Azure (CLI)](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="fe289-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
