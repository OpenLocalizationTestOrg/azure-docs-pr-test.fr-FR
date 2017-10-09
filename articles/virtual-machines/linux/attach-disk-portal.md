---
title: "aaaAttach un tooa de disque de données Linux VM | Documents Microsoft"
description: "Comment tooattach données nouvelles ou existantes disque tooa Linux VM dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="5c438-103">Tooattach données de disque tooa Linux VM Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="5c438-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="5c438-104">Cet article explique comment tooattach nouveaux et existant disques tooa une machine virtuelle Linux via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5c438-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="5c438-105">Vous pouvez également [attacher un tooa de disque de données machine virtuelle Windows Bonjour Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c438-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5c438-106">Vous pouvez choisir toouse soit des disques Azure géré ou non des disques.</span><span class="sxs-lookup"><span data-stu-id="5c438-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="5c438-107">Disques gérés sont gérés par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les.</span><span class="sxs-lookup"><span data-stu-id="5c438-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="5c438-108">Les disques non gérés requièrent un compte de stockage et sont soumis à un certain nombre de [quotas et de limites](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="5c438-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="5c438-109">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c438-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="5c438-110">Avant de joindre des disques tooyour machine virtuelle, consultez les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="5c438-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="5c438-111">taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données.</span><span class="sxs-lookup"><span data-stu-id="5c438-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="5c438-112">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c438-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="5c438-113">toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series.</span><span class="sxs-lookup"><span data-stu-id="5c438-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="5c438-114">Vous pouvez utiliser des disques Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5c438-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="5c438-115">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="5c438-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="5c438-116">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c438-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="5c438-117">Les disques attachés toovirtual machines sont réellement les fichiers .vhd stockés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5c438-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="5c438-118">Pour en savoir plus, voir la section [À propos des disques et VHD pour machines virtuelles](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c438-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="5c438-119">Trouver l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="5c438-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="5c438-120">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5c438-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5c438-121">Dans le menu du Hub hello, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="5c438-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="5c438-122">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="5c438-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="5c438-123">toohello Virtual machines panneau, dans **Essentials**, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="5c438-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Ouverture des paramètres d’un disque](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="5c438-125">Continuez en suivant les instructions pour attacher un [disque géré](#use-azure-managed-disks) ou un [disque non géré](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="5c438-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="5c438-126">Utiliser Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="5c438-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="5c438-127">Attacher un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="5c438-127">Attach a new disk</span></span>

1. <span data-ttu-id="5c438-128">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c438-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5c438-129">Cliquez sur le menu déroulant de hello pour **nom** et sélectionnez **créer disque**:</span><span class="sxs-lookup"><span data-stu-id="5c438-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Créer un disque géré Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="5c438-131">Entrez un nom pour votre disque géré.</span><span class="sxs-lookup"><span data-stu-id="5c438-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="5c438-132">Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="5c438-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="5c438-134">Cliquez sur **enregistrer** toocreate hello gérés disque et mise à jour de configuration d’ordinateur virtuel hello :</span><span class="sxs-lookup"><span data-stu-id="5c438-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Enregistrer le nouveau disque géré Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="5c438-136">Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="5c438-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="5c438-137">Disques gérés comme une ressource de niveau supérieur, disque de hello apparaît au niveau racine hello hello du groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="5c438-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Disque géré Azure dans le groupe de ressources](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="5c438-139">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="5c438-139">Attach an existing disk</span></span>
1. <span data-ttu-id="5c438-140">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c438-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5c438-141">Cliquez sur le menu déroulant de hello pour **nom** tooview une liste existante géré tooyour de disques accessibles abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5c438-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="5c438-142">Sélectionnez hello géré tooattach de disque :</span><span class="sxs-lookup"><span data-stu-id="5c438-142">Select hello managed disk tooattach:</span></span>

   ![Attacher un disque géré Azure existant](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="5c438-144">Cliquez sur **enregistrer** existant de hello tooattach gérés disque et mise à jour de configuration d’ordinateur virtuel hello :</span><span class="sxs-lookup"><span data-stu-id="5c438-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Enregistrer les mises à jour Azure Managed Disk](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="5c438-146">Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="5c438-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="5c438-147">Utiliser des disques non gérés</span><span class="sxs-lookup"><span data-stu-id="5c438-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="5c438-148">Attacher un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="5c438-148">Attach a new disk</span></span>

1. <span data-ttu-id="5c438-149">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c438-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5c438-150">Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c438-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="5c438-152">Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="5c438-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="5c438-153">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="5c438-153">Attach an existing disk</span></span>
1. <span data-ttu-id="5c438-154">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5c438-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="5c438-155">Sous **Attacher un disque existant**, cliquez sur **Fichier VHD**.</span><span class="sxs-lookup"><span data-stu-id="5c438-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Attachement d’un disque existant](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="5c438-157">Sous **comptes de stockage**, sélectionnez le compte de hello et conteneur qui contient le fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="5c438-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Recherche d’emplacement VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="5c438-159">Sélectionnez le fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="5c438-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="5c438-160">Sous **attachement du disque existant**, fichier hello vous venez de sélectionner est répertorié sous **fichier de disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="5c438-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="5c438-161">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c438-161">Click **OK**.</span></span>
6. <span data-ttu-id="5c438-162">Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="5c438-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c438-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5c438-163">Next steps</span></span>
<span data-ttu-id="5c438-164">Une fois le disque de hello est ajouté, vous devez tooprepare son utilisation.</span><span class="sxs-lookup"><span data-stu-id="5c438-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="5c438-165">Pour plus d'informations, consultez [Initialisation d’un nouveau disque de données sous Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="5c438-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
