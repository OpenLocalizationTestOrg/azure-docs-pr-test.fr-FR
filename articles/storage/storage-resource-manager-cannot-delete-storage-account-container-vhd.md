---
title: "Résoudre les erreurs lorsque vous supprimez des comptes de stockage Azure, des conteneurs ou des disques durs virtuels | Microsoft Docs"
description: "Résoudre les erreurs lorsque vous supprimez des comptes de stockage Azure, des conteneurs ou des disques durs virtuels"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="84e82-103">Résoudre les erreurs lorsque vous supprimez des comptes de stockage Azure, des conteneurs ou des disques durs virtuels</span><span class="sxs-lookup"><span data-stu-id="84e82-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="84e82-104">Il est possible que vous receviez des erreurs quand vous essayez de supprimer un compte de stockage Azure, un conteneur ou un disque dur virtuel dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84e82-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="84e82-105">Cet article fournit des conseils de dépannage pour vous aider à résoudre le problème dans un déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="84e82-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="84e82-106">Si cet article ne traite pas de votre problème avec Azure, parcourez les forums Azure sur [MSDN et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="84e82-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="84e82-107">Vous pouvez publier votre problème sur ces forums ou sur @AzureSupport sur Twitter.</span><span class="sxs-lookup"><span data-stu-id="84e82-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="84e82-108">Vous pouvez également créer une demande de support Azure en sélectionnant **Obtenir de l’aide** sur le site du [support Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="84e82-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="84e82-109">Symptômes</span><span class="sxs-lookup"><span data-stu-id="84e82-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="84e82-110">Scénario 1</span><span class="sxs-lookup"><span data-stu-id="84e82-110">Scenario 1</span></span>
<span data-ttu-id="84e82-111">Lorsque vous essayez de supprimer un disque dur virtuel d’un compte de stockage dans un déploiement Resource Manager, le message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="84e82-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="84e82-112">**Échec de la suppression de l’objet blob « vhds/BlobName.vhd » Erreur : Il existe actuellement un bail sur l’objet blob et aucun ID de bail n’a été spécifié dans la demande.**</span><span class="sxs-lookup"><span data-stu-id="84e82-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="84e82-113">Ce problème peut survenir lorsqu’une machine virtuelle dispose d’un bail sur le disque dur virtuel que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="84e82-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="84e82-114">Scénario 2</span><span class="sxs-lookup"><span data-stu-id="84e82-114">Scenario 2</span></span>
<span data-ttu-id="84e82-115">Lorsque vous essayez de supprimer un conteneur d’un compte de stockage dans un déploiement Resource Manager, le message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="84e82-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="84e82-116">**Échec de la suppression du conteneur de stockage « vhds ». Erreur : Il existe actuellement un bail sur le conteneur et aucun ID de bail n’a été spécifié dans la demande.**</span><span class="sxs-lookup"><span data-stu-id="84e82-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="84e82-117">Ce problème peut se produire lorsque le conteneur possède un disque dur virtuel qui est verrouillé à l’état de bail.</span><span class="sxs-lookup"><span data-stu-id="84e82-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="84e82-118">Scénario 3</span><span class="sxs-lookup"><span data-stu-id="84e82-118">Scenario 3</span></span>
<span data-ttu-id="84e82-119">Lorsque vous essayez de supprimer un compte de stockage dans un déploiement Resource Manager, le message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="84e82-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="84e82-120">**Échec de la suppression du compte de stockage « StorageAccountName ». Erreur : Le compte de stockage ne peut pas être supprimé en raison de ses artefacts en cours d’utilisation.**</span><span class="sxs-lookup"><span data-stu-id="84e82-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="84e82-121">Ce problème peut se produire lorsque le compte de stockage contient un disque dur virtuel qui est à l’état du bail.</span><span class="sxs-lookup"><span data-stu-id="84e82-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="84e82-122">Solution</span><span class="sxs-lookup"><span data-stu-id="84e82-122">Solution</span></span> 
<span data-ttu-id="84e82-123">Pour résoudre ces problèmes, vous devez identifier le disque dur virtuel qui a provoqué l’erreur et la machine virtuelle associée.</span><span class="sxs-lookup"><span data-stu-id="84e82-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="84e82-124">Ensuite, détachez le disque dur virtuel de la machine virtuelle (pour les disques de données) ou supprimez la machine virtuelle qui utilise le disque dur virtuel (pour les disques de système d’exploitation).</span><span class="sxs-lookup"><span data-stu-id="84e82-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="84e82-125">Cela supprime le bail du disque dur virtuel et permet la suppression de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="84e82-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="84e82-126">Pour ce faire, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="84e82-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="84e82-127">Méthode 1 - Utiliser l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="84e82-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="84e82-128">Étape 1 : Identifier le disque dur virtuel qui empêche la suppression du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="84e82-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="84e82-129">Lorsque vous supprimez le compte de stockage, une boîte de dialogue contenant le type de message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="84e82-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![message lors de la suppression du compte de stockage](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="84e82-131">Vérifiez **l’URL du disque** pour identifier le compte de stockage et le disque dur virtuel qui vous empêchent de supprimer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="84e82-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="84e82-132">Dans l’exemple suivant, la chaîne précédant « .blob.core.windows.net » correspond au nom du compte de stockage et « SCCM2012-2015-08-28.vhd » est le nom du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="84e82-133">Étape 2 : Supprimer le disque dur virtuel à l’aide de l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="84e82-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="84e82-134">Téléchargez et installez la version la plus récente de [l’Explorateur de stockage Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="84e82-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="84e82-135">Cet outil est une application autonome de Microsoft qui vous permet d’utiliser facilement des données du stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="84e82-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="84e82-136">Ouvrez l’Explorateur de stockage Azure, sélectionnez</span><span class="sxs-lookup"><span data-stu-id="84e82-136">Open Azure Storage Explorer, select</span></span> ![l’icône de compte](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="84e82-138">dans la barre de gauche, sélectionnez ensuite votre environnement Azure, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="84e82-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="84e82-139">Sélectionnez tous les abonnements ou l’abonnement qui contient le compte de stockage que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="84e82-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![ajouter un abonnement](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="84e82-141">Accédez au compte de stockage que nous avons précédemment obtenu à partir de l’URL du disque, sélectionnez **Conteneurs d’objets blob** > **Disques durs virtuels** et recherchez le disque dur virtuel qui vous empêche de supprimer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="84e82-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="84e82-142">Si le disque dur virtuel est trouvé, consultez la colonne **Nom de la machine virtuelle** pour rechercher la machine virtuelle utilisant ce disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Rechercher la machine virtuelle](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="84e82-144">Supprimez le bail du disque dur virtuel à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="84e82-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="84e82-145">Pour plus d’informations, consultez [Remove the lease from the VHD](#remove-the-lease-from-the-vhd) (Supprimer le bail du disque dur virtuel).</span><span class="sxs-lookup"><span data-stu-id="84e82-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="84e82-146">Accédez à l’Explorateur de stockage Azure, cliquez avec le bouton droit sur le disque dur virtuel, puis sélectionnez Supprimer.</span><span class="sxs-lookup"><span data-stu-id="84e82-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="84e82-147">Supprime le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="84e82-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="84e82-148">Méthode 2 - Utiliser le portail Azure</span><span class="sxs-lookup"><span data-stu-id="84e82-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="84e82-149">Étape 1 : Identifier le disque dur virtuel qui empêche la suppression du compte de stockage</span><span class="sxs-lookup"><span data-stu-id="84e82-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="84e82-150">Lorsque vous supprimez le compte de stockage, une boîte de dialogue contenant le type de message suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="84e82-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![message lors de la suppression du compte de stockage](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="84e82-152">Vérifiez **l’URL du disque** pour identifier le compte de stockage et le disque dur virtuel qui vous empêchent de supprimer le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="84e82-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="84e82-153">Dans l’exemple suivant, la chaîne précédant « .blob.core.windows.net » correspond au nom du compte de stockage et « SCCM2012-2015-08-28.vhd » est le nom du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="84e82-154">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84e82-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="84e82-155">Dans le menu Hub, sélectionnez **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="84e82-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="84e82-156">Accédez au compte de stockage, puis sélectionnez **Objets blob** > **Disques durs virtuels**.</span><span class="sxs-lookup"><span data-stu-id="84e82-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Capture d’écran du portail, où le compte de stockage et le conteneur « vhds » apparaissent en surbrillance](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="84e82-158">Recherchez le disque dur virtuel que nous avons précédemment obtenu à partir de l’URL du disque.</span><span class="sxs-lookup"><span data-stu-id="84e82-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="84e82-159">Ensuite, déterminez quelle machine virtuelle utilise le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="84e82-160">En règle générale, vous pouvez déterminer les machines virtuelles que contient le disque dur virtuel en vérifiant le nom de ce dernier :</span><span class="sxs-lookup"><span data-stu-id="84e82-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="84e82-161">Machine virtuelle dans le modèle de développement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="84e82-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="84e82-162">Généralement, les disques de système d’exploitation respectent la convention d’affectation de noms suivante : NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="84e82-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="84e82-163">Généralement, les disques de données respectent la convention d’affectation de noms suivante : NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="84e82-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="84e82-164">Machine virtuelle dans le modèle de développement classique</span><span class="sxs-lookup"><span data-stu-id="84e82-164">VM in Classic development model</span></span>

   * <span data-ttu-id="84e82-165">Généralement, les disques de système d’exploitation respectent la convention d’affectation de noms suivante : NomServiceCloud-NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="84e82-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="84e82-166">Généralement, les disques de données respectent la convention d’affectation de noms suivante : NomServiceCloud-NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="84e82-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="84e82-167">Étape 2 : Supprimer le bail du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="84e82-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="84e82-168">[Supprimez le bail du disque dur virtuel](#remove-the-lease-from-the-vhd), puis supprimez le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="84e82-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="84e82-169">Qu’est-ce qu’un bail ?</span><span class="sxs-lookup"><span data-stu-id="84e82-169">What is a lease?</span></span>
<span data-ttu-id="84e82-170">Un bail est un verrou qui peut être utilisé pour contrôler l’accès à un objet blob (par exemple, un disque dur virtuel).</span><span class="sxs-lookup"><span data-stu-id="84e82-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="84e82-171">Quand un objet blob est loué, seuls les propriétaires du bail peuvent accéder à l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="84e82-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="84e82-172">Un bail est important pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="84e82-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="84e82-173">Il empêche la corruption des données si plusieurs propriétaires essaient d’écrire sur la même partie de l’objet blob en même temps.</span><span class="sxs-lookup"><span data-stu-id="84e82-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="84e82-174">Il empêche la suppression de l’objet blob d’être supprimé si un élément l’utilise activement (par exemple, une machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="84e82-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="84e82-175">Il empêche la suppression du compte de stockage si un élément l’utilise activement (par exemple, une machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="84e82-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="84e82-176">Supprimer le bail du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="84e82-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="84e82-177">Si le disque dur virtuel est un disque de système d’exploitation, vous devez supprimer la machine virtuelle pour supprimer le bail :</span><span class="sxs-lookup"><span data-stu-id="84e82-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="84e82-178">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84e82-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="84e82-179">Dans le menu **Hub**, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="84e82-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="84e82-180">Sélectionnez la machine virtuelle qui détient un bail sur le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="84e82-181">Assurez-vous qu’aucun élément n’utilise activement la machine virtuelle, et que vous n’avez plus besoin de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="84e82-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="84e82-182">En haut du panneau **Détails de la machine virtuelle**, sélectionnez **Supprimer**, puis cliquez sur **Oui** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="84e82-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="84e82-183">La machine virtuelle doit être supprimée, mais le disque dur virtuel peut être conservé.</span><span class="sxs-lookup"><span data-stu-id="84e82-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="84e82-184">Toutefois, le disque dur virtuel ne devrait plus avoir de bail associé.</span><span class="sxs-lookup"><span data-stu-id="84e82-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="84e82-185">La publication du bail peut nécessiter quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="84e82-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="84e82-186">Pour vérifier que le bail est publié, accédez à **Toutes les ressources** > **Nom du compte de stockage** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="84e82-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="84e82-187">Dans le volet **Propriétés Blob**, la valeur **Statut du bail** doit être **Déverrouillé**.</span><span class="sxs-lookup"><span data-stu-id="84e82-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="84e82-188">Si le disque dur virtuel est un disque de données, détachez le disque dur virtuel de la machine virtuelle pour supprimer le bail :</span><span class="sxs-lookup"><span data-stu-id="84e82-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="84e82-189">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84e82-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="84e82-190">Dans le menu **Hub**, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="84e82-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="84e82-191">Sélectionnez la machine virtuelle qui détient un bail sur le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="84e82-192">Sélectionnez **Disques** sur le panneau **Détails de la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="84e82-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="84e82-193">Sélectionnez le disque de données qui détient un bail sur le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="84e82-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="84e82-194">Vous pouvez déterminer le disque dur virtuel attaché dans le disque en vérifiant son URL.</span><span class="sxs-lookup"><span data-stu-id="84e82-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="84e82-195">Déterminez avec certitude que rien n’utilise le disque de données.</span><span class="sxs-lookup"><span data-stu-id="84e82-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="84e82-196">Cliquez sur **Détacher** sur le panneau **Détails concernant le disque**.</span><span class="sxs-lookup"><span data-stu-id="84e82-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="84e82-197">Le disque doit maintenant être détaché de la machine virtuelle, et le disque dur virtuel ne doit plus avoir de bail.</span><span class="sxs-lookup"><span data-stu-id="84e82-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="84e82-198">La publication du bail peut nécessiter quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="84e82-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="84e82-199">Pour vérifier que le bail a été publié, accédez à **Toutes les ressources** > **Nom du compte de stockage** > **Blobs** > **vhds**.</span><span class="sxs-lookup"><span data-stu-id="84e82-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="84e82-200">Dans le volet **Propriétés Blob**, la valeur **Statut du bail** doit être **Déverrouillé**.</span><span class="sxs-lookup"><span data-stu-id="84e82-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84e82-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84e82-201">Next steps</span></span>
* [<span data-ttu-id="84e82-202">Suppression d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="84e82-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="84e82-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell) (Interruption du bail verrouillé du stockage d’objets blob dans Microsoft Azure (PowerShell))</span><span class="sxs-lookup"><span data-stu-id="84e82-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
