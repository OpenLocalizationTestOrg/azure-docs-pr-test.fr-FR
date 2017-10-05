---
title: "Attacher un disque de données géré à une machine virtuelle Windows - Azure | Microsoft Docs"
description: "Découvrez comment attacher un nouveau disque de données géré à une machine virtuelle Windows dans le portail Azure à l’aide du modèle de déploiement Resource Manager."
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
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="af2e0-103">Attachement d’un disque de données géré à une machine virtuelle Windows dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="af2e0-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="af2e0-104">Cet article explique comment attacher un nouveau disque de données géré à une machine virtuelle Windows par le biais du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="af2e0-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="af2e0-105">Avant cela, passez en revue les conseils suivants :</span><span class="sxs-lookup"><span data-stu-id="af2e0-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="af2e0-106">La taille de la machine virtuelle détermine le nombre de disques de données que vous pouvez attacher .</span><span class="sxs-lookup"><span data-stu-id="af2e0-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="af2e0-107">Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="af2e0-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="af2e0-108">Pour un nouveau disque, vous n’avez pas besoin de le créer au préalable, car Azure le crée lorsque vous l’attachez.</span><span class="sxs-lookup"><span data-stu-id="af2e0-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="af2e0-109">Vous pouvez également [attacher un disque de données à l’aide de PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="af2e0-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="af2e0-110">Ajouter un disque de données</span><span class="sxs-lookup"><span data-stu-id="af2e0-110">Add a data disk</span></span>
1. <span data-ttu-id="af2e0-111">Dans le menu de gauche, cliquez sur **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="af2e0-112">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="af2e0-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="af2e0-113">Dans le panneau de la machine virtuelle, cliquez sur **Disques**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="af2e0-114">Dans le panneau **Disques**, cliquez sur **+ Add data disk** (+ Ajouter un disque de données).</span><span class="sxs-lookup"><span data-stu-id="af2e0-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="af2e0-115">Dans la liste déroulante du nouveau disque, sélectionnez **Créer vide**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="af2e0-116">Dans le panneau **Créer un disque géré**, tapez le nom du disque et ajustez les autres paramètres si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="af2e0-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="af2e0-117">Lorsque vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="af2e0-118">Dans le panneau **Disques**, cliquez sur Enregistrer pour enregistrer la nouvelle configuration de disque pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af2e0-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="af2e0-119">Après qu’Azure a créé le disque et l’a attaché à la machine virtuelle, le nouveau disque est répertorié dans les paramètres de disque de la machine virtuelle sous **Disques de données**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="af2e0-120">Initialisation d’un nouveau disque de données</span><span class="sxs-lookup"><span data-stu-id="af2e0-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="af2e0-121">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af2e0-121">Connect to the VM.</span></span>
1. <span data-ttu-id="af2e0-122">Cliquez sur le menu Démarrer dans la machine virtuelle, tapez sur **diskmgmt.msc** et appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="af2e0-123">Le composant logiciel enfichable Gestion des disques démarre.</span><span class="sxs-lookup"><span data-stu-id="af2e0-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="af2e0-124">L’outil Gestion des disques détermine que votre nouveau disque n’est pas initialisé et affiche la fenêtre Initialiser le disque.</span><span class="sxs-lookup"><span data-stu-id="af2e0-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="af2e0-125">Vérifiez que le nouveau disque est sélectionné, puis cliquez sur **OK** pour l’initialiser.</span><span class="sxs-lookup"><span data-stu-id="af2e0-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="af2e0-126">Le nouveau disque s’affiche comme **non alloué**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="af2e0-127">Cliquez avec le bouton droit n’importe où sur le disque, puis sélectionnez **Nouveau volume simple**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="af2e0-128">L’**Assistant Création d’un volume simple** démarre.</span><span class="sxs-lookup"><span data-stu-id="af2e0-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="af2e0-129">Exécutez l’Assistant en conservant tous les paramètres par défaut. Lorsque vous avez terminé, sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="af2e0-130">Fermez Gestion des disques.</span><span class="sxs-lookup"><span data-stu-id="af2e0-130">Close Disk Management.</span></span>
7. <span data-ttu-id="af2e0-131">Une fenêtre contextuelle s’affiche et vous permet de formater le nouveau disque pour que vous puissiez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="af2e0-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="af2e0-132">Cliquez sur **Formater le disque**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="af2e0-133">Dans la boîte de dialogue **Formater un nouveau disque**, vérifiez les paramètres puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="af2e0-134">Un message vous informe que le formatage des disques va effacer toutes les données. Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="af2e0-135">Lorsque le formatage est terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="af2e0-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="af2e0-136">Utilisation de TRIM avec le stockage standard</span><span class="sxs-lookup"><span data-stu-id="af2e0-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="af2e0-137">Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM.</span><span class="sxs-lookup"><span data-stu-id="af2e0-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="af2e0-138">TRIM ignore les blocs inutilisés sur le disque afin que vous soyez facturé uniquement pour le stockage que vous utilisez réellement.</span><span class="sxs-lookup"><span data-stu-id="af2e0-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="af2e0-139">Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="af2e0-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="af2e0-140">Vous pouvez exécuter cette commande pour vérifier le paramètre TRIM.</span><span class="sxs-lookup"><span data-stu-id="af2e0-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="af2e0-141">Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :</span><span class="sxs-lookup"><span data-stu-id="af2e0-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="af2e0-142">Si la commande renvoie 0, TRIM est bien activé.</span><span class="sxs-lookup"><span data-stu-id="af2e0-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="af2e0-143">Si la valeur 1 est renvoyée, exécutez la commande suivante pour activer TRIM :</span><span class="sxs-lookup"><span data-stu-id="af2e0-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="af2e0-144">Après la suppression de données de votre disque, vous pouvez vous assurer du bon vidage des opérations TRIM en exécutant la défragmentation avec TRIM :</span><span class="sxs-lookup"><span data-stu-id="af2e0-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="af2e0-145">Pour vous assurer que les blocs de données inutilisés sont bien effacés sur tout le volume, vous pouvez également le formater.</span><span class="sxs-lookup"><span data-stu-id="af2e0-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af2e0-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af2e0-146">Next steps</span></span>
<span data-ttu-id="af2e0-147">Si votre application doit utiliser le lecteur D: pour stocker des données, vous pouvez [changer la lettre de lecteur du disque temporaire Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af2e0-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
