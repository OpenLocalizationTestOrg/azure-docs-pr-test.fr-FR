---
title: "aaaAttach un tooa de disque des données non managées machine virtuelle Windows - Azure | Documents Microsoft"
description: "Comment tooattach nouvelle ou existante de données non managées disque tooa machine virtuelle Windows dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="65a01-103">Tooattach une données non managées de disque tooa machine virtuelle Windows dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="65a01-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="65a01-104">Cet article explique comment tooattach nouvel et existante non managée de disques virtuels tooWindows via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="65a01-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="65a01-105">Vous pouvez également [attacher un disque de données à l’aide de PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="65a01-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="65a01-106">Avant cela, passez en revue les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="65a01-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="65a01-107">taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données.</span><span class="sxs-lookup"><span data-stu-id="65a01-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="65a01-108">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="65a01-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="65a01-109">toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series.</span><span class="sxs-lookup"><span data-stu-id="65a01-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="65a01-110">Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="65a01-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="65a01-111">Le stockage Premium est disponible dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="65a01-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="65a01-112">Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65a01-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="65a01-113">Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.</span><span class="sxs-lookup"><span data-stu-id="65a01-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="65a01-114">Vous pouvez également [attacher un disque de données à l’aide de PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="65a01-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="65a01-115">Trouver l’ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="65a01-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="65a01-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="65a01-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="65a01-117">Dans le menu hello hello gauche, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="65a01-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="65a01-118">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="65a01-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="65a01-119">Dans le panneau des machines virtuelles hello, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="65a01-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="65a01-120">Continuez en suivant les instructions pour attacher un [nouveau disque](#option-1-attach-a-new-disk) ou un [disque existant](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="65a01-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="65a01-121">Option 1 : attacher et initialiser un nouveau disque</span><span class="sxs-lookup"><span data-stu-id="65a01-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="65a01-122">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="65a01-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="65a01-123">Bonjour **attacher un disque géré** panneau, tapez un nom pour le disque hello dans **nom** , puis sélectionnez **nouveau (disque vide)** dans **type de Source**.</span><span class="sxs-lookup"><span data-stu-id="65a01-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="65a01-124">Sous **conteneur de stockage**, cliquez sur hello **Parcourir** bouton et parcourir le compte de stockage toohello et le conteneur où vous serez hello nouveau disque dur virtuel toobe est stocké et puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="65a01-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="65a01-126">Lorsque vous avez terminé avec les paramètres de hello hello disque de données, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="65a01-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="65a01-127">Dans hello **disques** panneau, cliquez sur **enregistrer** configuration d’ordinateur virtuel toohello disque tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="65a01-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="65a01-128">Initialisation d’un nouveau disque de données</span><span class="sxs-lookup"><span data-stu-id="65a01-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="65a01-129">Connecter l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="65a01-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="65a01-130">Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65a01-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="65a01-131">Cliquez sur hello **Démarrer** menu hello machine virtuelle et type **diskmgmt.msc** puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="65a01-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="65a01-132">Cela démarre le composant logiciel enfichable Gestion des disques hello.</span><span class="sxs-lookup"><span data-stu-id="65a01-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="65a01-133">Gestion des disques reconnaît que vous avez un disque non initialisé et hello initialiser le disque fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="65a01-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="65a01-134">Assurez-vous que le nouveau disque de hello est sélectionné et cliquez sur **OK** tooinitialize il.</span><span class="sxs-lookup"><span data-stu-id="65a01-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="65a01-135">Hello nouveau disque apparaît désormais comme **non alloué**.</span><span class="sxs-lookup"><span data-stu-id="65a01-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="65a01-136">Avec le bouton droit n’importe où sur le disque de hello et sélectionnez **nouveau volume simple**.</span><span class="sxs-lookup"><span data-stu-id="65a01-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="65a01-137">Hello **Assistant de nouveau Volume Simple** démarre.</span><span class="sxs-lookup"><span data-stu-id="65a01-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="65a01-138">Passez en revue l’Assistant hello, conserve toutes les valeurs par défaut de hello, lorsque vous avez terminé de sélectionner **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="65a01-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="65a01-139">Fermez Gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="65a01-139">Close Disk Management.</span></span>
7. <span data-ttu-id="65a01-140">Vous obtenez une fenêtre contextuelle vous devez de nouveau disque de tooformat hello avant que vous puissiez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="65a01-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="65a01-141">Cliquez sur **Formater le disque**.</span><span class="sxs-lookup"><span data-stu-id="65a01-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="65a01-142">Bonjour **nouveau disque de Format** boîte de dialogue, vérifiez les paramètres hello et puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="65a01-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="65a01-143">Vous obtenez un avertissement que le formatage des disques de hello efface toutes les données de salutation, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="65a01-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="65a01-144">Lorsque le format de hello est terminée, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="65a01-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="65a01-145">Option 2 : attacher un disque existant</span><span class="sxs-lookup"><span data-stu-id="65a01-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="65a01-146">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="65a01-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="65a01-147">Sur hello **attacher un disque non managé** panneau, dans **type de Source de** sélectionnez **existant blob**.</span><span class="sxs-lookup"><span data-stu-id="65a01-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="65a01-149">Cliquez sur **Parcourir** toonavigate toohello compte de stockage et le conteneur où hello disque dur virtuel existant se trouve.</span><span class="sxs-lookup"><span data-stu-id="65a01-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="65a01-150">Cliquez sur, hello du disque dur virtuel, puis cliquez **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="65a01-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="65a01-151">Cliquez sur **OK** Bonjour **attacher un disque non managé** panneau.</span><span class="sxs-lookup"><span data-stu-id="65a01-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="65a01-152">Bonjour **disques** panneau, cliquez sur **enregistrer** tooadd hello toohello configuration des hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="65a01-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="65a01-153">Utilisation de TRIM avec le stockage standard</span><span class="sxs-lookup"><span data-stu-id="65a01-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="65a01-154">Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM.</span><span class="sxs-lookup"><span data-stu-id="65a01-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="65a01-155">La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement.</span><span class="sxs-lookup"><span data-stu-id="65a01-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="65a01-156">Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="65a01-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="65a01-157">Vous pouvez exécuter ce paramètre de découpage hello commande toocheck.</span><span class="sxs-lookup"><span data-stu-id="65a01-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="65a01-158">Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :</span><span class="sxs-lookup"><span data-stu-id="65a01-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="65a01-159">Si la commande hello retourne 0, la fonction TRIM est activée correctement.</span><span class="sxs-lookup"><span data-stu-id="65a01-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="65a01-160">Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :</span><span class="sxs-lookup"><span data-stu-id="65a01-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="65a01-161">Après la suppression des données à partir de votre disque, vous pouvez garantir la défragmentation des opérations de découpage hello vidage correctement en exécutant avec la fonction TRIM :</span><span class="sxs-lookup"><span data-stu-id="65a01-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="65a01-162">Vous pouvez également vérifier la totalité du volume hello est tronqué en mettant en forme de volume de hello.</span><span class="sxs-lookup"><span data-stu-id="65a01-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="65a01-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65a01-163">Next steps</span></span>
<span data-ttu-id="65a01-164">Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65a01-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

