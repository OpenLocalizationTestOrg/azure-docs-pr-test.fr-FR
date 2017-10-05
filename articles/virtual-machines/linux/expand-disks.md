---
title: "Développer les disques durs virtuels sur une machine virtuelle Linux dans Azure | Microsoft Docs"
description: "Apprenez à développer des disques durs virtuels sur une machine virtuelle Linux avec Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="f5b23-103">Comment développer des disques durs virtuels sur une machine virtuelle Linux avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f5b23-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="f5b23-104">La taille par défaut de disque virtuel pour le système d’exploitation est généralement de 30 Go sur une machine virtuelle Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f5b23-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="f5b23-105">Vous pouvez [ajouter des disques de données](add-disk.md) afin d’offrir un espace de stockage supplémentaire, mais vous pouvez également développer un disque de données existant.</span><span class="sxs-lookup"><span data-stu-id="f5b23-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="f5b23-106">Cet article vous explique comment développer les disques gérés pour une machine virtuelle Linux à l’aide de l’interface CLI Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f5b23-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="f5b23-107">Vous pouvez également développer le disque du système d’exploitation non managé avec [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f5b23-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="f5b23-108">Assurez-vous de toujours sauvegarder vos données avant de redimensionner des disques.</span><span class="sxs-lookup"><span data-stu-id="f5b23-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="f5b23-109">Pour plus d’informations, consultez [Back up Linux VMs in Azure](tutorial-backup-vms.md) (Sauvegarder des machines virtuelles Linux dans Azure).</span><span class="sxs-lookup"><span data-stu-id="f5b23-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="f5b23-110">Développer le disque</span><span class="sxs-lookup"><span data-stu-id="f5b23-110">Expand disk</span></span>
<span data-ttu-id="f5b23-111">Assurez-vous que vous avez installé la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et que vous êtes connecté à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f5b23-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f5b23-112">Cet article nécessite une machine virtuelle existante dans Azure avec au moins un disque de données attaché et préparé.</span><span class="sxs-lookup"><span data-stu-id="f5b23-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="f5b23-113">Si vous n’avez pas encore de machine virtuelle à utiliser, consultez [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks) (Créer et préparer une machine virtuelle avec des disques de données).</span><span class="sxs-lookup"><span data-stu-id="f5b23-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="f5b23-114">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f5b23-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="f5b23-115">Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="f5b23-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="f5b23-116">Il est impossible d’exécuter les opérations sur les disques durs virtuels avec la machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f5b23-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="f5b23-117">Libérez la machine virtuelle avec la commande [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="f5b23-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="f5b23-118">L’exemple suivant libère la machine virtuelle nommée *myVM* dans le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="f5b23-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="f5b23-119">`az vm stop` ne publie pas les ressources de calcul.</span><span class="sxs-lookup"><span data-stu-id="f5b23-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="f5b23-120">Pour publier les ressources de calcul, utilisez `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="f5b23-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="f5b23-121">La machine virtuelle doit être libérée pour développer le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f5b23-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="f5b23-122">Affichez la liste des disques gérés dans un groupe de ressources avec la commande [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="f5b23-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="f5b23-123">L’exemple suivant affiche la liste des disques managés dans le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="f5b23-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="f5b23-124">Développez le disque requis avec la commande [az disk update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="f5b23-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="f5b23-125">L’exemple suivant développe le disque managé nommé *myDataDisk* pour qu’il ait une taille de *200* Go :</span><span class="sxs-lookup"><span data-stu-id="f5b23-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="f5b23-126">Lorsque vous développez un disque géré, la taille mise à jour est mappée à la taille de disque géré la plus proche.</span><span class="sxs-lookup"><span data-stu-id="f5b23-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="f5b23-127">Pour obtenir un tableau des tailles et des niveaux de disques gérés disponibles, consultez [Vue d’ensemble des disques gérés Azure - Tarification et facturation](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="f5b23-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="f5b23-128">Démarrez votre machine virtuelle avec [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="f5b23-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="f5b23-129">L’exemple suivant démarre la machine virtuelle nommée *myVM* dans le groupe de ressources nommé *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="f5b23-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="f5b23-130">Établissez une connexion SSH à votre machine virtuelle à l’aide des informations d’identification appropriées.</span><span class="sxs-lookup"><span data-stu-id="f5b23-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="f5b23-131">Vous pouvez obtenir l’adresse IP publique de votre machine virtuelle à l’aide de la commande [az vm show](/cli/azure/vm#show) :</span><span class="sxs-lookup"><span data-stu-id="f5b23-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="f5b23-132">Pour utiliser le disque étendu, vous devez développer la partition et le système de fichiers sous-jacents.</span><span class="sxs-lookup"><span data-stu-id="f5b23-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="f5b23-133">a.</span><span class="sxs-lookup"><span data-stu-id="f5b23-133">a.</span></span> <span data-ttu-id="f5b23-134">Si le disque est déjà monté, démontez-le :</span><span class="sxs-lookup"><span data-stu-id="f5b23-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="f5b23-135">b.</span><span class="sxs-lookup"><span data-stu-id="f5b23-135">b.</span></span> <span data-ttu-id="f5b23-136">Utilisez `parted` pour afficher des informations sur le disque et redimensionner la partition :</span><span class="sxs-lookup"><span data-stu-id="f5b23-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="f5b23-137">Affichez les informations sur la disposition actuelle de la partition avec `print`.</span><span class="sxs-lookup"><span data-stu-id="f5b23-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="f5b23-138">Le résultat est comparable à l’exemple ci-dessous, qui indique que le disque sous-jacent fait 215 Go :</span><span class="sxs-lookup"><span data-stu-id="f5b23-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="f5b23-139">c.</span><span class="sxs-lookup"><span data-stu-id="f5b23-139">c.</span></span> <span data-ttu-id="f5b23-140">Développez la partition avec `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="f5b23-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="f5b23-141">Entrez le numéro de la partition, *1*, et la taille de la nouvelle partition :</span><span class="sxs-lookup"><span data-stu-id="f5b23-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="f5b23-142">d.</span><span class="sxs-lookup"><span data-stu-id="f5b23-142">d.</span></span> <span data-ttu-id="f5b23-143">Pour quitter l’outil, saisissez `quit`.</span><span class="sxs-lookup"><span data-stu-id="f5b23-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="f5b23-144">Une fois la partition redimensionnée, vérifiez la cohérence de la partition avec `e2fsck` :</span><span class="sxs-lookup"><span data-stu-id="f5b23-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="f5b23-145">Redimensionnez ensuite le système de fichiers avec `resize2fs` :</span><span class="sxs-lookup"><span data-stu-id="f5b23-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="f5b23-146">Montez la partition à l’emplacement souhaité, tel que `/datadrive` :</span><span class="sxs-lookup"><span data-stu-id="f5b23-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="f5b23-147">Pour vérifier que le disque du système d’exploitation a été redimensionné, utilisez `df -h`.</span><span class="sxs-lookup"><span data-stu-id="f5b23-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="f5b23-148">L’exemple de sortie suivant indique que le disque de données */dev/sdc1* fait désormais 200 Go :</span><span class="sxs-lookup"><span data-stu-id="f5b23-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="f5b23-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f5b23-149">Next steps</span></span>
<span data-ttu-id="f5b23-150">Si vous avez besoin de stockage supplémentaire, vous pouvez également [ajouter des disques de données à une machine virtuelle Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="f5b23-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="f5b23-151">Pour plus d’informations sur le chiffrement de disque, consultez la section [Chiffrer des disques sur une machine virtuelle Linux à l’aide de l’interface de ligne de commande Azure (CLI)](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="f5b23-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
