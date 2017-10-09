---
title: "aaaAttach un tooa disque données managées machine virtuelle Windows - Azure | Documents Microsoft"
description: "La méthode de tooattach nouvelle gestion des données disque tooa virtuelle Windows dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="e76fa-103">Tooattach une données managées de disque tooa machine virtuelle Windows dans hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e76fa-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="e76fa-104">Cet article explique de tooattach une nouvelle données managées de disque virtuels tooWindows via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e76fa-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="e76fa-105">Avant cela, passez en revue les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="e76fa-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="e76fa-106">taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données.</span><span class="sxs-lookup"><span data-stu-id="e76fa-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="e76fa-107">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e76fa-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="e76fa-108">Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.</span><span class="sxs-lookup"><span data-stu-id="e76fa-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="e76fa-109">Vous pouvez également [attacher un disque de données à l’aide de PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e76fa-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="e76fa-110">Ajouter un disque de données</span><span class="sxs-lookup"><span data-stu-id="e76fa-110">Add a data disk</span></span>
1. <span data-ttu-id="e76fa-111">Dans le menu hello hello gauche, cliquez sur **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="e76fa-112">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e76fa-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="e76fa-113">Dans le panneau de la machine virtuelle hello, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="e76fa-114">Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="e76fa-115">Bonjour pour le nouveau disque de hello liste déroulante, sélectionnez **créer vide**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="e76fa-116">Bonjour **disque géré de créer** panneau, tapez un nom pour le disque de hello et ajustez hello autres paramètres si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e76fa-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="e76fa-117">Lorsque vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="e76fa-118">Bonjour **disques** panneau, cliquez sur Enregistrer toosave hello nouvelle configuration de disque pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e76fa-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="e76fa-119">Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="e76fa-120">Initialisation d’un nouveau disque de données</span><span class="sxs-lookup"><span data-stu-id="e76fa-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="e76fa-121">Se connecter toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e76fa-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="e76fa-122">Cliquez sur le menu Démarrer hello hello machine virtuelle et le type **diskmgmt.msc** puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="e76fa-123">Ceci démarrera hello composant logiciel enfichable Gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="e76fa-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="e76fa-124">Gestion des disques reconnaît que vous disposez d’un nouveau disque sans être initialisé et hello initialiser le disque fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e76fa-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="e76fa-125">Assurez-vous que le nouveau disque de hello est sélectionné et cliquez sur **OK** tooinitialize il.</span><span class="sxs-lookup"><span data-stu-id="e76fa-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="e76fa-126">nouveau disque de Hello sera **non alloué**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="e76fa-127">Avec le bouton droit n’importe où sur le disque de hello et sélectionnez **nouveau volume simple**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="e76fa-128">Hello **Assistant de nouveau Volume Simple** démarre.</span><span class="sxs-lookup"><span data-stu-id="e76fa-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="e76fa-129">Passez en revue l’Assistant hello, conserve toutes les valeurs par défaut de hello, lorsque vous avez terminé de sélectionner **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="e76fa-130">Fermez Gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="e76fa-130">Close Disk Management.</span></span>
7. <span data-ttu-id="e76fa-131">Vous obtenez un menu contextuel que vous avez besoin de nouveau disque de tooformat hello avant que vous puissiez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="e76fa-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="e76fa-132">Cliquez sur **Formater le disque**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="e76fa-133">Bonjour **nouveau disque de Format** boîte de dialogue, vérifiez les paramètres hello et puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="e76fa-134">Vous serez averti que formatage des disques de hello supprimera toutes les données de hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="e76fa-135">Lorsque le format de hello est terminée, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e76fa-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="e76fa-136">Utilisation de TRIM avec le stockage standard</span><span class="sxs-lookup"><span data-stu-id="e76fa-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="e76fa-137">Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM.</span><span class="sxs-lookup"><span data-stu-id="e76fa-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="e76fa-138">La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement.</span><span class="sxs-lookup"><span data-stu-id="e76fa-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="e76fa-139">Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="e76fa-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="e76fa-140">Vous pouvez exécuter ce paramètre de découpage hello commande toocheck.</span><span class="sxs-lookup"><span data-stu-id="e76fa-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="e76fa-141">Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :</span><span class="sxs-lookup"><span data-stu-id="e76fa-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="e76fa-142">Si la commande hello retourne 0, la fonction TRIM est activée correctement.</span><span class="sxs-lookup"><span data-stu-id="e76fa-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="e76fa-143">Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :</span><span class="sxs-lookup"><span data-stu-id="e76fa-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="e76fa-144">Après la suppression des données à partir de votre disque, vous pouvez garantir la défragmentation des opérations de découpage hello vidage correctement en exécutant avec la fonction TRIM :</span><span class="sxs-lookup"><span data-stu-id="e76fa-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="e76fa-145">Vous pouvez également vérifier la totalité du volume hello est tronqué en mettant en forme de volume de hello.</span><span class="sxs-lookup"><span data-stu-id="e76fa-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e76fa-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e76fa-146">Next steps</span></span>
<span data-ttu-id="e76fa-147">Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e76fa-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
