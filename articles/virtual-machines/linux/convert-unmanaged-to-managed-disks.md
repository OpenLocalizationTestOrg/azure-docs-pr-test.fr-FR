---
title: "Convertir les disques non gérés d’une machine virtuelle Linux dans Azure en disques gérés - Azure Managed Disks | Microsoft Docs"
description: "Conversion des disques non gérés d’une machine virtuelle Linux en disques gérés à l’aide d’Azure CLI 2.0 dans le modèle de déploiement Resource Manager"
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
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a><span data-ttu-id="d3634-103">Convertir les disques non gérés d’une machine virtuelle Linux en disques gérés</span><span class="sxs-lookup"><span data-stu-id="d3634-103">Convert a Linux virtual machine from unmanaged disks to managed disks</span></span>

<span data-ttu-id="d3634-104">Si vos machines virtuelles Linux existantes utilisent des disques non gérés, vous pouvez les convertir pour qu’elles utilisent des disques gérés par le biais du service [Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3634-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert the VMs to use managed disks through the [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="d3634-105">Ce processus convertit le disque du système d’exploitation ainsi que tous les autres disques de données attachés.</span><span class="sxs-lookup"><span data-stu-id="d3634-105">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="d3634-106">Cet article explique comment convertir des machines virtuelles avec Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d3634-106">This article shows you how to convert VMs by using the Azure CLI.</span></span> <span data-ttu-id="d3634-107">Si vous devez installer ou mettre à niveau l’interface, consultez [Installation d’Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d3634-107">If you need to install or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="d3634-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d3634-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="d3634-109">Convertir des machines virtuelles à instance unique</span><span class="sxs-lookup"><span data-stu-id="d3634-109">Convert single-instance VMs</span></span>
<span data-ttu-id="d3634-110">Cette section explique comment convertir vos machines virtuelles Azure à instance unique à partir de disques non gérés vers des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="d3634-110">This section covers how to convert single-instance Azure VMs from unmanaged disks to managed disks.</span></span> <span data-ttu-id="d3634-111">(Si vos machines virtuelles sont dans un groupe à haute disponibilité, voir la section suivante.) Vous pouvez utiliser ce processus pour convertir les machines virtuelles qui utilisent des disques non gérés premium (SSD) afin qu’elles utilisent des disques gérés premium, ou qui utilisent des disques non gérés standard (HDD) afin qu’elles utilisent des disques gérés standard.</span><span class="sxs-lookup"><span data-stu-id="d3634-111">(If your VMs are in an availability set, see the next section.) You can use this process to convert the VMs from premium (SSD) unmanaged disks to premium managed disks, or from standard (HDD) unmanaged disks to standard managed disks.</span></span>

1. <span data-ttu-id="d3634-112">Libérez la machine virtuelle à l’aide de [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="d3634-112">Deallocate the VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="d3634-113">L’exemple suivant libère la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="d3634-113">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="d3634-114">Convertissez la machine virtuelle afin qu’elle utilise des disques gérés à l’aide de la commande [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="d3634-114">Convert the VM to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="d3634-115">Le processus suivant convertit la machine virtuelle nommée `myVM`, y compris le disque du système d’exploitation et tous les disques de données :</span><span class="sxs-lookup"><span data-stu-id="d3634-115">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="d3634-116">Démarrez la machine virtuelle une fois la conversion vers les disques gérés effectuée à l’aide de la commande [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="d3634-116">Start the VM after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="d3634-117">L’exemple suivant démarre la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="d3634-117">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="d3634-118">Convertir des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="d3634-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="d3634-119">Si les machines virtuelles que vous souhaitez convertir pour utiliser des disques gérés se trouvent dans un groupe à haute disponibilité, vous devez tout d’abord convertir ce dernier en groupe à haute disponibilité géré.</span><span class="sxs-lookup"><span data-stu-id="d3634-119">If the VMs that you want to convert to managed disks are in an availability set, you first need to convert the availability set to a managed availability set.</span></span>

<span data-ttu-id="d3634-120">Toutes les machines virtuelles dans le groupe à haute disponibilité doivent être libérées avant de convertir le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d3634-120">All VMs in the availability set must be deallocated before you convert the availability set.</span></span> <span data-ttu-id="d3634-121">Prévoyez de convertir toutes les machines virtuelles vers des disques gérés une fois que le groupe à haute disponibilité a lui-même été converti en groupe à haute disponibilité géré.</span><span class="sxs-lookup"><span data-stu-id="d3634-121">Plan to convert all VMs to managed disks after the availability set itself has been converted to a managed availability set.</span></span> <span data-ttu-id="d3634-122">Vous pouvez ensuite démarrer toutes les machines virtuelles et poursuivre un fonctionnement normal.</span><span class="sxs-lookup"><span data-stu-id="d3634-122">Then, start all the VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="d3634-123">Répertoriez toutes les machines virtuelles contenues dans un groupe à haute disponibilité à l’aide de la commande [az vm availability-set list](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="d3634-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="d3634-124">L’exemple suivant répertorie toutes les machines virtuelles dans le groupe à haute disponibilité nommé `myAvailabilitySet` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="d3634-124">The following example lists all VMs in the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="d3634-125">Libérez toutes les machines virtuelles à l’aide de la commande [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="d3634-125">Deallocate all the VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="d3634-126">L’exemple suivant libère la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="d3634-126">The following example deallocates the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="d3634-127">Convertissez le groupe à haute disponibilité à l’aide de la commande [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="d3634-127">Convert the availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="d3634-128">L’exemple suivant convertit le groupe à haute disponibilité nommé `myAvailabilitySet` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="d3634-128">The following example converts the availability set named `myAvailabilitySet` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="d3634-129">Convertissez toutes les machines virtuelles vers des disques gérés à l’aide de la commande [az vm convert](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="d3634-129">Convert all the VMs to managed disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="d3634-130">Le processus suivant convertit la machine virtuelle nommée `myVM`, y compris le disque du système d’exploitation et tous les disques de données :</span><span class="sxs-lookup"><span data-stu-id="d3634-130">The following process converts the VM named `myVM`, including the OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="d3634-131">Démarrez toutes les machines virtuelles une fois la conversion vers des disques gérés effectuée à l’aide de la commande [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="d3634-131">Start all the VMs after the conversion to managed disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="d3634-132">L’exemple suivant démarre la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="d3634-132">The following example starts the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="d3634-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3634-133">Next steps</span></span>
<span data-ttu-id="d3634-134">Pour plus d’informations sur les options de stockage, voir la page [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3634-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
