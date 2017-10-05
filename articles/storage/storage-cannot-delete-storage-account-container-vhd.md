---
title: "Résoudre les problèmes de suppression de comptes de stockage Azure, de conteneurs ou de disques durs virtuels dans un déploiement classique | Microsoft Docs"
description: "Résoudre les problèmes de suppression de comptes de stockage Azure, de conteneurs ou de disques durs virtuels dans un déploiement classique"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="f452f-103">Résoudre les problèmes de suppression de comptes de stockage Azure, de conteneurs ou de disques durs virtuels dans un déploiement classique</span><span class="sxs-lookup"><span data-stu-id="f452f-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="f452f-104">Il est possible que vous receviez des erreurs quand vous essayez de supprimer le compte de stockage Azure, le conteneur ou le disque dur virtuel dans le [portail Azure](https://portal.azure.com/) ou le [portail Azure Classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f452f-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="f452f-105">Ces problèmes peuvent être causés par les circonstances suivantes :</span><span class="sxs-lookup"><span data-stu-id="f452f-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="f452f-106">Lorsque vous supprimez une machine virtuelle, le disque et le disque dur virtuel ne sont pas automatiquement supprimés.</span><span class="sxs-lookup"><span data-stu-id="f452f-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="f452f-107">Cela peut être la cause de l'échec de la suppression du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f452f-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="f452f-108">Nous ne supprimons pas le disque pour que vous puissiez l’utiliser pour monter une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="f452f-109">Il existe toujours un bail sur un disque ou sur l’objet blob associé au disque.</span><span class="sxs-lookup"><span data-stu-id="f452f-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="f452f-110">Il existe toujours une image de machine virtuelle qui utilise un compte de stockage, un conteneur ou un objet blob.</span><span class="sxs-lookup"><span data-stu-id="f452f-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="f452f-111">Si le problème lié à Azure n’est pas traité dans cet article, parcourez les forums Azure sur [MSDN et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="f452f-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="f452f-112">Vous pouvez publier votre problème sur ces forums ou sur @AzureSupport sur Twitter.</span><span class="sxs-lookup"><span data-stu-id="f452f-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="f452f-113">Vous pouvez également créer une demande de support Azure en sélectionnant **Obtenir de l’aide** sur le site du [support Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="f452f-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="f452f-114">Symptômes</span><span class="sxs-lookup"><span data-stu-id="f452f-114">Symptoms</span></span>
<span data-ttu-id="f452f-115">La section suivante répertorie les erreurs courantes que vous pourriez recevoir quand vous tentez de supprimer les comptes de stockage Azure, les conteneurs ou les disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="f452f-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="f452f-116">Scénario 1 : Impossible de supprimer un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f452f-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="f452f-117">Lorsque vous accédez au compte de stockage classique dans le [portail Azure](https://portal.azure.com/) et que vous sélectionnez **Supprimer**, une liste des objets qui empêchent la suppression du compte de stockage peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="f452f-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Image de l’erreur qui se produit lors de la suppression du compte de stockage](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="f452f-119">Lorsque vous accédez au compte de stockage dans le [portail Azure Classic](https://manage.windowsazure.com/) et que vous sélectionnez **Supprimer**, l’une des erreurs suivantes peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="f452f-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="f452f-120">*Le compte de stockage StorageAccountName contient des images de machine virtuelle. Supprimez ces images de machine virtuelle avant de supprimer ce compte de stockage.*</span><span class="sxs-lookup"><span data-stu-id="f452f-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="f452f-121">*Échec de suppression du compte de stockage <vm-storage-account-name>. Impossible de supprimer le compte de stockage <vm-storage-account-name> : Storage account <vm-storage-account-name> contient des images et/ou des disques actifs. Supprimez ces images et/ou disques avant de supprimer ce compte de stockage. ».*</span><span class="sxs-lookup"><span data-stu-id="f452f-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="f452f-122">*Le compte de stockage <vm-storage-account-name> contient des images et/ou des disques actifs, par exemple, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Supprimez ces images et/ou disques avant de supprimer ce compte de stockage.*</span><span class="sxs-lookup"><span data-stu-id="f452f-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="f452f-123">*Le compte de stockage <vm-storage-account-name> contient 1 ou plusieurs conteneurs avec une image active et/ou des artefacts de disque. Supprimez ces artefacts du dépôt d’images avant de supprimer ce compte de stockage*.</span><span class="sxs-lookup"><span data-stu-id="f452f-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="f452f-124">*Échec d’envoi : le compte de stockage <vm-storage-account-name> contient 1 ou plusieurs conteneurs avec une image active et/ou des artefacts de disque. Supprimez ces artefacts du dépôt d’images avant de supprimer ce compte de stockage. Quand vous essayez de supprimer un compte de stockage auquel sont associés des disques toujours actifs, un message vous informe que des disques actifs doivent être supprimés*.</span><span class="sxs-lookup"><span data-stu-id="f452f-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="f452f-125">Scénario 2 : Impossible de supprimer un conteneur</span><span class="sxs-lookup"><span data-stu-id="f452f-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="f452f-126">Quand vous essayez de supprimer le conteneur de stockage, il est possible que vous rencontriez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="f452f-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="f452f-127">*Échec de la suppression du conteneur de stockage <container name>. Erreur : « Il existe actuellement un bail sur le conteneur et aucun ID de bail n’a été spécifié dans la demande »*.</span><span class="sxs-lookup"><span data-stu-id="f452f-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="f452f-128">Ou</span><span class="sxs-lookup"><span data-stu-id="f452f-128">Or</span></span>

<span data-ttu-id="f452f-129">*Les disques de machines virtuelles suivants utilisent actuellement des objets blob de ce conteneur. Par conséquent, le conteneur ne peut pas être supprimé : VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span><span class="sxs-lookup"><span data-stu-id="f452f-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="f452f-130">Scénario 3 : Impossible de supprimer un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="f452f-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="f452f-131">Après avoir supprimé une machine virtuelle, puis tenté de supprimer les objets blob des disques durs virtuels associés, il est possible que vous receviez le message suivant :</span><span class="sxs-lookup"><span data-stu-id="f452f-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="f452f-132">*Échec de la suppression de l’objet blob « path/XXXXXX-XXXXXX-os-1447379084699.vhd ». Erreur : « Il existe actuellement un bail sur l’objet blob et aucun ID de bail n’a été spécifié dans la demande »*.</span><span class="sxs-lookup"><span data-stu-id="f452f-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="f452f-133">Ou</span><span class="sxs-lookup"><span data-stu-id="f452f-133">Or</span></span>

<span data-ttu-id="f452f-134">*L’objet blob « BlobName.vhd » est en cours d’utilisation en tant que disque de la machine virtuelle « VirtualMachineDiskName », donc il ne peut pas être supprimé.*</span><span class="sxs-lookup"><span data-stu-id="f452f-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="f452f-135">Solution</span><span class="sxs-lookup"><span data-stu-id="f452f-135">Solution</span></span>
<span data-ttu-id="f452f-136">Pour résoudre les problèmes les plus courants, essayez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="f452f-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="f452f-137">Étape 1 : Supprimer les disques qui empêchent la suppression du compte de stockage, du conteneur ou du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="f452f-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="f452f-138">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f452f-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="f452f-139">Sélectionnez **MACHINES VIRTUELLES** > **DISQUES**.</span><span class="sxs-lookup"><span data-stu-id="f452f-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Image de disques sur des machines virtuelles sur le portail Azure Classic.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="f452f-141">Recherchez les disques associés au compte de stockage, au conteneur ou au disque dur virtuel à supprimer.</span><span class="sxs-lookup"><span data-stu-id="f452f-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="f452f-142">En vérifiant l’emplacement du disque, vous trouverez le compte de stockage, le conteneur et le disque dur virtuel associés.</span><span class="sxs-lookup"><span data-stu-id="f452f-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Image qui affiche des informations d'emplacement sur les disques sur le portail Azure Classic](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="f452f-144">Supprimez les disques en utilisant l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f452f-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="f452f-145">Si aucune machine virtuelle n’est indiquée dans le champ **Attaché à** des disques, vous pouvez supprimer le disque directement.</span><span class="sxs-lookup"><span data-stu-id="f452f-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="f452f-146">Si le disque est un disque de données, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f452f-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="f452f-147">Vérifiez le nom de la machine virtuelle à laquelle le disque est attaché.</span><span class="sxs-lookup"><span data-stu-id="f452f-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="f452f-148">Accédez à **Machines virtuelles** > **Instances**, puis recherchez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="f452f-149">Assurez-vous que le disque n’est pas activement utilisé.</span><span class="sxs-lookup"><span data-stu-id="f452f-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="f452f-150">Sélectionnez **Détacher le disque** au bas du portail pour détacher le disque.</span><span class="sxs-lookup"><span data-stu-id="f452f-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="f452f-151">Accédez à **Machines virtuelles** > **Disques** et attendez que le champ **Attaché à** soit vide.</span><span class="sxs-lookup"><span data-stu-id="f452f-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="f452f-152">Cela indique que le disque a été correctement détaché de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="f452f-153">Sélectionnez **Supprimer** sous **Machines virtuelles** > **Disques** pour supprimer le disque.</span><span class="sxs-lookup"><span data-stu-id="f452f-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="f452f-154">Si le disque est un disque du système d’exploitation (le champ **Contient le système d’exploitation** a une valeur telle que Windows) et qu’il est attaché à une machine virtuelle, procédez comme suit pour supprimer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="f452f-155">Le disque du système d’exploitation ne peut pas être détaché. Nous devons donc supprimer la machine virtuelle pour libérer l’attribution.</span><span class="sxs-lookup"><span data-stu-id="f452f-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="f452f-156">Vérifiez le nom de la machine virtuelle à laquelle le disque de données est attaché.</span><span class="sxs-lookup"><span data-stu-id="f452f-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="f452f-157">Accédez à **Machines virtuelles** > **Instances**, puis sélectionnez la machine virtuelle à laquelle le disque est attaché.</span><span class="sxs-lookup"><span data-stu-id="f452f-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="f452f-158">Assurez-vous qu’aucun élément n’utilise activement la machine virtuelle, et que vous n’avez plus besoin de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="f452f-159">Sélectionnez la machine virtuelle à laquelle le disque est attaché, puis sélectionnez **Supprimer** > **Supprimer les disques attachés**.</span><span class="sxs-lookup"><span data-stu-id="f452f-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="f452f-160">Accédez à **Machines virtuelles** > **Disques** et attendez que le disque ne s’affiche plus.</span><span class="sxs-lookup"><span data-stu-id="f452f-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="f452f-161">Cela peut prendre plusieurs minutes. Vous devrez peut-être actualiser la page.</span><span class="sxs-lookup"><span data-stu-id="f452f-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="f452f-162">Si le disque ne disparaît pas, attendez que le champ **Attaché à** soit vide.</span><span class="sxs-lookup"><span data-stu-id="f452f-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="f452f-163">Cela indique que le disque a été entièrement détaché de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="f452f-164">Ensuite, sélectionnez le disque et sélectionnez **Supprimer** en bas de la page pour supprimer le disque.</span><span class="sxs-lookup"><span data-stu-id="f452f-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="f452f-165">Si un disque est attaché à une machine virtuelle, vous ne pouvez pas le supprimer.</span><span class="sxs-lookup"><span data-stu-id="f452f-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="f452f-166">Les disques sont détachés de façon asynchrone d’une machine virtuelle supprimée.</span><span class="sxs-lookup"><span data-stu-id="f452f-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="f452f-167">L’effacement de ce champ peut prendre quelques minutes après la suppression de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f452f-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="f452f-168">Étape 2 : Supprimer les images de machine virtuelle qui empêchent la suppression du compte de stockage ou du conteneur</span><span class="sxs-lookup"><span data-stu-id="f452f-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="f452f-169">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f452f-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="f452f-170">Sélectionnez **MACHINE VIRTUELLE** > **IMAGES**, puis supprimez les images associées au compte de stockage, au conteneur ou au disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f452f-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="f452f-171">Ensuite, réessayez de supprimer le compte de stockage, le conteneur ou le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f452f-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="f452f-172">Veillez à sauvegarder tout ce que vous souhaitez conserver avant de supprimer le compte.</span><span class="sxs-lookup"><span data-stu-id="f452f-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="f452f-173">Lorsque vous supprimez un VHD, un blob, une table, une file d’attente ou un fichier, il est définitivement supprimé.</span><span class="sxs-lookup"><span data-stu-id="f452f-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="f452f-174">Vérifiez que la ressource n’est pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="f452f-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="f452f-175">À propos de l’état Arrêté (Désalloué)</span><span class="sxs-lookup"><span data-stu-id="f452f-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="f452f-176">Les machines virtuelles créées dans le modèle de déploiement classique et conservées auront le statut **Arrêté (Désalloué)** soit sur le [portail Azure](https://portal.azure.com/), soit sur le [portail Azure Classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f452f-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="f452f-177">**Portail Azure Classic**:</span><span class="sxs-lookup"><span data-stu-id="f452f-177">**Azure classic portal**:</span></span>

![Statut Arrêté (désalloué) pour les machines virtuelles sur le portail Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="f452f-179">**Portail Azure**:</span><span class="sxs-lookup"><span data-stu-id="f452f-179">**Azure portal**:</span></span>

![Statut Arrêté (désalloué) pour les machines virtuelles sur le portail Azure Classic.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="f452f-181">Le statut « Arrêté (désalloué) » libère les ressources de l’ordinateur (processeur, mémoire et réseau).</span><span class="sxs-lookup"><span data-stu-id="f452f-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="f452f-182">Les disques, cependant, sont toujours conservés de façon à vous permettre de recréer rapidement la machine virtuelle si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f452f-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="f452f-183">Ces disques sont créés sur les disques durs virtuels sauvegardés par Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f452f-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="f452f-184">Le compte de stockage contient ces disques durs virtuels et les disques ont des baux sur ces disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="f452f-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f452f-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f452f-185">Next steps</span></span>
* [<span data-ttu-id="f452f-186">Suppression d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f452f-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
