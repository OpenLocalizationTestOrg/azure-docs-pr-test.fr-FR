---
title: aaaAttach un tooa disque classique Azure VM | Documents Microsoft
description: "Attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique hello et son initialisation."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="3d9c7-103">Attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="3d9c7-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="3d9c7-104">Cet article vous explique comment tooattach les disques nouveaux et existants créés avec hello classique déploiement modèle tooa machine virtuelle Windows à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="3d9c7-105">Vous pouvez également [attacher un tooa de disque de données Linux VM Bonjour Azure portal](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="3d9c7-106">Avant d’attacher un disque, lisez les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="3d9c7-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="3d9c7-107">taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="3d9c7-108">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="3d9c7-109">toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="3d9c7-110">Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="3d9c7-111">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="3d9c7-112">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="3d9c7-113">Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="3d9c7-114">Vous pouvez également [attacher un disque de données à l’aide de PowerShell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d9c7-115">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="3d9c7-116">Trouver l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="3d9c7-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="3d9c7-117">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3d9c7-118">Machine virtuelle de hello SELECT à partir de la ressource hello répertorié dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="3d9c7-119">Dans le volet gauche, hello sous **paramètres**, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Ouverture des paramètres d’un disque](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="3d9c7-121">Continuez en suivant les instructions pour attacher un [nouveau disque](#option-1-attach-a-new-disk) ou un [disque existant](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="3d9c7-122">Option 1 : attacher et initialiser un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="3d9c7-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="3d9c7-123">Sur hello **disques** panneau, cliquez sur **attacher nouvelle**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="3d9c7-124">Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Examen des paramètres d’un disque](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="3d9c7-126">Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="3d9c7-127">Initialisation d’un nouveau disque de données</span><span class="sxs-lookup"><span data-stu-id="3d9c7-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="3d9c7-128">Connecter l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="3d9c7-129">Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="3d9c7-130">Une fois que vous ouvrez une session sur l’ordinateur virtuel de toohello, ouvrez **le Gestionnaire de serveur**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="3d9c7-131">Dans le volet gauche de hello, sélectionnez **File and Storage Services**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Ouvrir le gestionnaire de serveur](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="3d9c7-133">Sélectionnez **Disques**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-133">Select **Disks**.</span></span>
4. <span data-ttu-id="3d9c7-134">Hello **disques** section répertorie les disques hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="3d9c7-135">En règle générale, une machine virtuelle contient le disque 0, le disque 1 et le disque 2.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="3d9c7-136">Le disque 0 est le disque du système d’exploitation hello, disque 1 est le disque temporaire de hello et le disque 2 est le disque de données hello nouvellement attachés toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="3d9c7-137">listes de disque de données Hello hello Partition en tant que **inconnu**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="3d9c7-138">Cliquez sur le disque de hello et sélectionnez **initialiser**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="3d9c7-139">Vous êtes averti que toutes les données seront effacées lors de l’initialisation de disque de hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="3d9c7-140">Cliquez sur **Oui** disque hello tooacknowledge hello avertissement et d’initialisation.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="3d9c7-141">Une fois terminé, partition de hello est répertoriée comme **GPT**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="3d9c7-142">Avec le bouton droit à nouveau de disque de hello et sélectionnez **nouveau Volume**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="3d9c7-143">Exécutez l’Assistant hello à l’aide des valeurs par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="3d9c7-144">Une fois terminé, Assistant de hello hello **Volumes** section répertorie le nouveau volume de hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="3d9c7-145">Hello disque est maintenant en ligne et prêt toostore données.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-145">hello disk is now online and ready toostore data.</span></span>

    ![Volume correctement initialisé](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="3d9c7-147">Option 2 : attacher un disque existant</span><span class="sxs-lookup"><span data-stu-id="3d9c7-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="3d9c7-148">Sur hello **disques** panneau, cliquez sur **attacher existant**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="3d9c7-149">Sous **Attacher un disque existant**, cliquez sur **Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Attachement d’un disque existant](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="3d9c7-151">Sous **comptes de stockage**, sélectionnez le compte de hello et conteneur qui contient le fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Recherche d’emplacement VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="3d9c7-153">Sélectionnez le fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="3d9c7-154">Sous **attachement du disque existant**, fichier hello vous venez de sélectionner est répertorié sous **fichier de disque dur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="3d9c7-155">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-155">Click **OK**.</span></span>
6. <span data-ttu-id="3d9c7-156">Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="3d9c7-157">Utilisation de TRIM avec le stockage standard</span><span class="sxs-lookup"><span data-stu-id="3d9c7-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="3d9c7-158">Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="3d9c7-159">La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="3d9c7-160">La fonction TRIM peut réduire les coûts, notamment les blocs inutilisés qui résultent de la suppression de fichiers volumineux.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="3d9c7-161">Vous pouvez exécuter ce paramètre de découpage hello commande toocheck.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="3d9c7-162">Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :</span><span class="sxs-lookup"><span data-stu-id="3d9c7-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="3d9c7-163">Si la commande hello retourne 0, la fonction TRIM est activée correctement.</span><span class="sxs-lookup"><span data-stu-id="3d9c7-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="3d9c7-164">Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :</span><span class="sxs-lookup"><span data-stu-id="3d9c7-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="3d9c7-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3d9c7-165">Next steps</span></span>
<span data-ttu-id="3d9c7-166">Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="3d9c7-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d9c7-167">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3d9c7-167">Additional resources</span></span>
[<span data-ttu-id="3d9c7-168">À propos des disques et VHD pour machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3d9c7-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
