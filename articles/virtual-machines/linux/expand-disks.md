---
title: aaaExpand des disques durs virtuels sur un VM Linux dans Azure | Documents Microsoft
description: "Découvrez comment tooexpand des disques durs virtuels sur un VM Linux avec hello Azure CLI 2.0"
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
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="5e0ec-103">Comment tooexpand des disques durs virtuels sur un VM Linux avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="5e0ec-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="5e0ec-104">taille de disque dur virtuel par défaut Hello hello système d’exploitation (OS) est généralement 30 Go sur un ordinateur virtuel de Linux (VM) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="5e0ec-105">Vous pouvez [ajouter des disques de données](add-disk.md) tooprovide d’espace de stockage supplémentaire, mais vous souhaiterez également tooexpand un disque de données existant.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="5e0ec-106">Cet article décrit en détail comment tooexpand des disques gérés pour un VM Linux avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="5e0ec-107">Vous pouvez également développer le disque de système d’exploitation hello non managée avec hello [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="5e0ec-108">Assurez-vous de toujours sauvegarder vos données avant de redimensionner des disques.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="5e0ec-109">Pour plus d’informations, consultez [Back up Linux VMs in Azure](tutorial-backup-vms.md) (Sauvegarder des machines virtuelles Linux dans Azure).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="5e0ec-110">Développer le disque</span><span class="sxs-lookup"><span data-stu-id="5e0ec-110">Expand disk</span></span>
<span data-ttu-id="5e0ec-111">Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5e0ec-112">Cet article nécessite une machine virtuelle existante dans Azure avec au moins un disque de données attaché et préparé.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="5e0ec-113">Si vous n’avez pas encore de machine virtuelle à utiliser, consultez [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks) (Créer et préparer une machine virtuelle avec des disques de données).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="5e0ec-114">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5e0ec-115">Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="5e0ec-116">Opérations sur les disques durs virtuels ne peuvent pas être effectuées avec hello machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="5e0ec-117">Libérez la machine virtuelle avec la commande [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="5e0ec-118">exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="5e0ec-119">`az vm stop`ne libère pas de ressources de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="5e0ec-120">toorelease des ressources de calcul, utilisez `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="5e0ec-121">Hello machine virtuelle doit être libérée tooexpand hello un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="5e0ec-122">Affichez la liste des disques gérés dans un groupe de ressources avec la commande [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="5e0ec-123">Hello exemple suivant affiche une liste de disques gérés dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="5e0ec-124">Développez disque hello avec [mise à jour du disque az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="5e0ec-125">exemple Hello développe managé disque hello *myDataDisk* toobe *200*Go :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="5e0ec-126">Lorsque vous développez un disque géré, taille de hello mis à jour est mappé toohello plus proche de la taille de disque géré.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="5e0ec-127">Pour un tableau des tailles de disque géré disponible hello et les niveaux, consultez [présentation des disques Azure géré - tarification et facturation](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="5e0ec-128">Démarrez votre machine virtuelle avec [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="5e0ec-129">Hello après le démarrage de l’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="5e0ec-130">SSH tooyour machine virtuelle avec les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="5e0ec-131">Vous pouvez obtenir hello adresse IP publique de votre machine virtuelle avec [afficher de machine virtuelle az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="5e0ec-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="5e0ec-132">toouse hello développé de disque, vous devez système de fichiers et de la partition de tooexpand hello sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="5e0ec-133">a.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-133">a.</span></span> <span data-ttu-id="5e0ec-134">Si déjà monté, démontez le disque de hello :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="5e0ec-135">b.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-135">b.</span></span> <span data-ttu-id="5e0ec-136">Utilisez `parted` tooview informations de disque et redimensionner hello partition :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="5e0ec-137">Afficher des informations sur la disposition de partition existant hello avec `print`.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="5e0ec-138">la sortie est similaire toohello suivant exemple, qui affiche la taille de disque sous-jacent de hello est 215 Go Hello :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="5e0ec-139">c.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-139">c.</span></span> <span data-ttu-id="5e0ec-140">Développez la partition hello avec `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="5e0ec-141">Entrez le numéro de partition hello, *1*et une taille pour la nouvelle partition de hello :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="5e0ec-142">d.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-142">d.</span></span> <span data-ttu-id="5e0ec-143">tooexit, entrez`quit`</span><span class="sxs-lookup"><span data-stu-id="5e0ec-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="5e0ec-144">Avec partition hello redimensionnée, vérifiez la cohérence de partition hello avec `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="5e0ec-145">Désormais redimensionner filesystem hello avec `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="5e0ec-146">Montage hello partition toohello souhaité emplacement, tel que `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="5e0ec-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="5e0ec-147">disque de hello du système d’exploitation tooverify a été redimensionné, utilisez `df -h`.</span><span class="sxs-lookup"><span data-stu-id="5e0ec-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="5e0ec-148">Hello après la sortie de l’exemple montre le lecteur de données hello, *sdc1/dev/*, est maintenant de 200 Go :</span><span class="sxs-lookup"><span data-stu-id="5e0ec-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="5e0ec-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e0ec-149">Next steps</span></span>
<span data-ttu-id="5e0ec-150">Si vous avez besoin de stockage supplémentaire, vous également [ajouter des disques de données tooa Linux VM](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="5e0ec-151">Pour plus d’informations sur le chiffrement de disque, consultez [crypter les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="5e0ec-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
