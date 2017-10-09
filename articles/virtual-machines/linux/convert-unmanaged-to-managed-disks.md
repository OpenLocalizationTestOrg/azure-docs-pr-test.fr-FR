---
title: "aaaConvert une machine virtuelle de Linux dans Azure du code non disques toomanaged disques - Azure géré | Documents Microsoft"
description: "Comment tooconvert un VM Linux à partir de disques non managé toomanaged disques à l’aide d’Azure CLI 2.0 dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="370c1-103">Convertir une machine virtuelle Linux à partir de disques toomanaged de disques non managé</span><span class="sxs-lookup"><span data-stu-id="370c1-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="370c1-104">Si vous avez existant Linux virtual machines virtuelles qui utilisent des disques non managés, vous pouvez convertir les disques de toouse géré de machines virtuelles de hello via hello [disques gérés d’Azure](../windows/managed-disks-overview.md) service.</span><span class="sxs-lookup"><span data-stu-id="370c1-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="370c1-105">Ce processus convertit le disque de hello du système d’exploitation et les disques de données attaché.</span><span class="sxs-lookup"><span data-stu-id="370c1-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="370c1-106">Cet article vous explique comment tooconvert machines virtuelles à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="370c1-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="370c1-107">Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="370c1-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="370c1-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="370c1-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="370c1-109">Convertir des machines virtuelles à instance unique</span><span class="sxs-lookup"><span data-stu-id="370c1-109">Convert single-instance VMs</span></span>
<span data-ttu-id="370c1-110">Cette section explique comment des machines virtuelles Azure à partir de non managé à instance unique de tooconvert disques toomanaged disques.</span><span class="sxs-lookup"><span data-stu-id="370c1-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="370c1-111">(Si vos machines virtuelles sont dans un ensemble de disponibilité, voir section suivante de hello). Vous pouvez utiliser cette disques toostandard géré de disques de machines virtuelles à partir de disques de toopremium géré disques premium (SSD) non managée, ou à partir de la norme (HDD) non managées processus tooconvert hello.</span><span class="sxs-lookup"><span data-stu-id="370c1-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="370c1-112">Désallouer hello machine virtuelle à l’aide de [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="370c1-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="370c1-113">exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="370c1-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="370c1-114">Convertir les disques de toomanaged hello machine virtuelle à l’aide de [az vm convertir](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="370c1-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="370c1-115">Hello suivant convertit des processus hello ordinateur virtuel nommé `myVM`, y compris les disques hello du système d’exploitation et les disques de données :</span><span class="sxs-lookup"><span data-stu-id="370c1-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="370c1-116">Démarrer hello machine virtuelle une fois les disques toomanaged hello conversion à l’aide de [début de machine virtuelle az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="370c1-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="370c1-117">Hello après le démarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="370c1-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="370c1-118">Convertir des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="370c1-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="370c1-119">Si hello machines virtuelles que vous souhaitez tooconvert toomanaged disques se trouvent dans un ensemble de disponibilité, vous devez commencer tooconvert hello disponibilité ensemble tooa géré à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="370c1-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="370c1-120">Tous les ordinateurs virtuels dans le groupe à haute disponibilité hello doivent être libérées avant de convertir hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="370c1-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="370c1-121">Tooconvert plan tous les disques toomanaged de machines virtuelles après la disponibilité de hello définir elle-même a été converti tooa géré à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="370c1-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="370c1-122">Ensuite, démarrez tous les ordinateurs virtuels de hello et continue à fonctionner normalement.</span><span class="sxs-lookup"><span data-stu-id="370c1-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="370c1-123">Répertoriez toutes les machines virtuelles contenues dans un groupe à haute disponibilité à l’aide de la commande [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="370c1-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="370c1-124">Hello exemple suivant répertorie toutes les machines virtuelles hello groupe à haute disponibilité nommée `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="370c1-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="370c1-125">Libérer toutes les machines virtuelles de hello à l’aide de [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="370c1-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="370c1-126">exemple Hello désalloue hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="370c1-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="370c1-127">Convertir hello groupe à haute disponibilité à l’aide de [convert de haute-disponibilité az vm](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="370c1-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="370c1-128">Hello suivant convertit hello groupe à haute disponibilité nommée `myAvailabilitySet` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="370c1-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="370c1-129">Convertir tous les disques de toomanaged hello machines virtuelles à l’aide de [az vm convertir](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="370c1-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="370c1-130">Hello suivant convertit des processus hello ordinateur virtuel nommé `myVM`, y compris les disques hello du système d’exploitation et les disques de données :</span><span class="sxs-lookup"><span data-stu-id="370c1-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="370c1-131">Démarrer tous les ordinateurs virtuels de hello après les disques toomanaged hello conversion à l’aide de [début de machine virtuelle az](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="370c1-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="370c1-132">Hello après le démarrage de l’exemple hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="370c1-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="370c1-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="370c1-133">Next steps</span></span>
<span data-ttu-id="370c1-134">Pour plus d’informations sur les options de stockage, voir la page [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="370c1-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
