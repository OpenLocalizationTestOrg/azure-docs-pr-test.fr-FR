---
title: "Attacher un disque de données à une machine virtuelle Linux | Microsoft Docs"
description: "Découvrez comment attacher un disque de données nouveau ou existant à une machine virtuelle Linux dans le portail Azure à l’aide du modèle de déploiement Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="1787b-103">Attachement d’un disque de données à une machine virtuelle Linux dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1787b-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="1787b-104">Cet article vous explique comment attacher des disques nouveaux et existants à une machine virtuelle Linux par le biais du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1787b-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="1787b-105">Vous pouvez également [attacher un disque de données à une machine virtuelle Windows dans le Portail Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1787b-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1787b-106">Vous pouvez utiliser des disques gérés Azure (Azure Managed Disks) ou des disques non gérés.</span><span class="sxs-lookup"><span data-stu-id="1787b-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="1787b-107">Les disques gérés sont traités par la plateforme Azure et ne nécessitent pas de préparation ou d’emplacement pour les stocker.</span><span class="sxs-lookup"><span data-stu-id="1787b-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="1787b-108">Les disques non gérés requièrent un compte de stockage et sont soumis à un certain nombre de [quotas et de limites](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="1787b-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="1787b-109">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1787b-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="1787b-110">Avant d’attacher des disques à votre machine virtuelle, lisez les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="1787b-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="1787b-111">La taille de la machine virtuelle détermine le nombre de disques de données que vous pouvez attacher .</span><span class="sxs-lookup"><span data-stu-id="1787b-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="1787b-112">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1787b-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1787b-113">Pour utiliser le stockage Premium, vous avez besoin d’une machine virtuelle de série DS ou GS.</span><span class="sxs-lookup"><span data-stu-id="1787b-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="1787b-114">Vous pouvez utiliser des disques Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1787b-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="1787b-115">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="1787b-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="1787b-116">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1787b-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="1787b-117">Les disques attachés aux machines virtuelles sont en réalité des fichiers .vhd stockés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1787b-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="1787b-118">Pour en savoir plus, voir la section [À propos des disques et VHD pour machines virtuelles](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1787b-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="1787b-119">Recherchez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1787b-119">Find the virtual machine</span></span>
1. <span data-ttu-id="1787b-120">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1787b-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1787b-121">Dans le menu Hub, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="1787b-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="1787b-122">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="1787b-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="1787b-123">Dans le panneau Machines virtuelles, dans **Essentials**, cliquez sur **Disques**.</span><span class="sxs-lookup"><span data-stu-id="1787b-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Ouverture des paramètres d’un disque](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="1787b-125">Continuez en suivant les instructions pour attacher un [disque géré](#use-azure-managed-disks) ou un [disque non géré](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="1787b-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="1787b-126">Utiliser Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="1787b-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1787b-127">Attacher un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="1787b-127">Attach a new disk</span></span>

1. <span data-ttu-id="1787b-128">Dans le panneau **Disques**, cliquez sur **+ Add data disk** (+ Ajouter un disque de données).</span><span class="sxs-lookup"><span data-stu-id="1787b-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1787b-129">Cliquez sur le menu déroulant **Nom** et sélectionnez **Create disk** (Créer un disque) :</span><span class="sxs-lookup"><span data-stu-id="1787b-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Créer un disque géré Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="1787b-131">Entrez un nom pour votre disque géré.</span><span class="sxs-lookup"><span data-stu-id="1787b-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="1787b-132">Vérifiez les paramètres par défaut, mettez-les à jour le cas échéant, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1787b-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="1787b-134">Cliquez sur **Enregistrer** pour créer le disque géré et mettre à jour la configuration de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="1787b-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Enregistrer le nouveau disque géré Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="1787b-136">Après qu’Azure a créé le disque et l’a attaché à la machine virtuelle, le nouveau disque est répertorié dans les paramètres de disque de la machine virtuelle sous **Disques de données**.</span><span class="sxs-lookup"><span data-stu-id="1787b-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="1787b-137">Étant donné que les disques gérés sont des ressources de niveau supérieur, le disque s’affiche à la racine du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="1787b-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Disque géré Azure dans le groupe de ressources](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1787b-139">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="1787b-139">Attach an existing disk</span></span>
1. <span data-ttu-id="1787b-140">Dans le panneau **Disques**, cliquez sur **+ Add data disk** (+ Ajouter un disque de données).</span><span class="sxs-lookup"><span data-stu-id="1787b-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1787b-141">Cliquez sur le menu déroulant **Nom** pour afficher une liste des disques gérés disponibles dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1787b-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="1787b-142">Sélectionnez le disque géré à attacher :</span><span class="sxs-lookup"><span data-stu-id="1787b-142">Select the managed disk to attach:</span></span>

   ![Attacher un disque géré Azure existant](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="1787b-144">Cliquez sur **Enregistrer** pour attacher le disque géré existant et mettre à jour la configuration de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="1787b-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Enregistrer les mises à jour Azure Managed Disk](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="1787b-146">Après qu’Azure a attaché le disque à la machine virtuelle, le disque est répertorié dans les paramètres de disque de la machine virtuelle sous **Disques de données**.</span><span class="sxs-lookup"><span data-stu-id="1787b-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="1787b-147">Utiliser des disques non gérés</span><span class="sxs-lookup"><span data-stu-id="1787b-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="1787b-148">Attacher un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="1787b-148">Attach a new disk</span></span>

1. <span data-ttu-id="1787b-149">Dans le panneau **Disques**, cliquez sur **+ Add data disk** (+ Ajouter un disque de données).</span><span class="sxs-lookup"><span data-stu-id="1787b-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1787b-150">Passez en revue les paramètres par défaut, mettez-les à jour en fonction des besoins, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1787b-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="1787b-152">Après qu’Azure a créé le disque et l’a attaché à la machine virtuelle, le nouveau disque est répertorié dans les paramètres de disque de la machine virtuelle sous **Disques de données**.</span><span class="sxs-lookup"><span data-stu-id="1787b-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="1787b-153">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="1787b-153">Attach an existing disk</span></span>
1. <span data-ttu-id="1787b-154">Dans le panneau **Disques**, cliquez sur **+ Add data disk** (+ Ajouter un disque de données).</span><span class="sxs-lookup"><span data-stu-id="1787b-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="1787b-155">Sous **Attacher un disque existant**, cliquez sur **Fichier VHD**.</span><span class="sxs-lookup"><span data-stu-id="1787b-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Attachement d’un disque existant](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="1787b-157">Sous **Comptes de stockage**, sélectionnez le compte et le conteneur dans lequel figure le fichier .vhd.</span><span class="sxs-lookup"><span data-stu-id="1787b-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Recherche d’emplacement VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="1787b-159">Sélectionnez le fichier .vhd.</span><span class="sxs-lookup"><span data-stu-id="1787b-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="1787b-160">Sous **Attacher un disque existant**, le fichier que vous venez de sélectionner est répertorié sous **Fichier VHD**.</span><span class="sxs-lookup"><span data-stu-id="1787b-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="1787b-161">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1787b-161">Click **OK**.</span></span>
6. <span data-ttu-id="1787b-162">Après qu’Azure a attaché le disque à la machine virtuelle, le disque est répertorié dans les paramètres de disque de la machine virtuelle sous **Disques de données**.</span><span class="sxs-lookup"><span data-stu-id="1787b-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1787b-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1787b-163">Next steps</span></span>
<span data-ttu-id="1787b-164">Une fois le disque ajouté, vous devez le préparer pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="1787b-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="1787b-165">Pour plus d'informations, consultez [Initialisation d’un nouveau disque de données sous Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1787b-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
