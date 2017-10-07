---
title: "les sauvegardes déployées par le Gestionnaire de ressources des machines virtuelles aaaManage | Documents Microsoft"
description: "Découvrez comment toomanage et surveiller les sauvegardes déployées par le Gestionnaire de ressources des machines virtuelles"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="5ff53-103">Gestion des sauvegardes de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="5ff53-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ff53-104">Gestion des sauvegardes de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="5ff53-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="5ff53-105">Gestion des sauvegardes de machines virtuelles classiques</span><span class="sxs-lookup"><span data-stu-id="5ff53-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="5ff53-106">Cet article fournit des conseils sur la gestion des sauvegardes de la machine virtuelle et explique les informations d’alertes de sauvegarde hello disponibles dans le tableau de bord de portail hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-106">This article provides guidance on managing VM backups, and explains hello backup alerts information available in hello portal dashboard.</span></span> <span data-ttu-id="5ff53-107">les instructions de Hello dans cet article s’appliquent VMs toousing avec les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="5ff53-107">hello guidance in this article applies toousing VMs with Recovery Services vaults.</span></span> <span data-ttu-id="5ff53-108">Cet article ne couvre pas la création de hello d’ordinateurs virtuels, ni expliquent comment tooprotect virtual machines.</span><span class="sxs-lookup"><span data-stu-id="5ff53-108">This article does not cover hello creation of virtual machines, nor does it explain how tooprotect virtual machines.</span></span> <span data-ttu-id="5ff53-109">Pour une introduction sur la protection Azure Resource Manager déployés de machines virtuelles dans Azure avec un coffre Recovery Services, consultez [tout d’abord rechercher : sauvegardez tooa de machines virtuelles de coffre Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5ff53-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="5ff53-110">Gérer les coffres et les machines virtuelles protégées</span><span class="sxs-lookup"><span data-stu-id="5ff53-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="5ff53-111">Bonjour portail Azure, tableau de bord coffre de Services de récupération hello fournit tooinformation d’accès sur l’inclusion de coffre hello :</span><span class="sxs-lookup"><span data-stu-id="5ff53-111">In hello Azure portal, hello Recovery Services vault dashboard provides access tooinformation about hello vault including:</span></span>

* <span data-ttu-id="5ff53-112">Hello sauvegarde la plus récente d’instantané, qui est également dernier point de restauration hello < br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-112">hello most recent backup snapshot, which is also hello latest restore point <br\></span></span>
* <span data-ttu-id="5ff53-113">stratégie de sauvegarde de Hello < br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-113">hello backup policy <br\></span></span>
* <span data-ttu-id="5ff53-114">la taille totale de tous les instantanés de sauvegarde <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="5ff53-115">nombre d’ordinateurs virtuels qui sont protégées par le coffre hello < br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-115">number of virtual machines that are protected with hello vault <br\></span></span>

<span data-ttu-id="5ff53-116">De nombreuses tâches de gestion avec une sauvegarde de l’ordinateur virtuel commencent avec ouverture hello coffre dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-116">Many management tasks with a virtual machine backup begin with opening hello vault in hello dashboard.</span></span> <span data-ttu-id="5ff53-117">Toutefois, étant coffres tooprotect utilisé plusieurs éléments (ou plusieurs machines virtuelles), tooview des détails sur un ordinateur virtuel, ouvrez tableau de bord coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-117">However, because vaults can be used tooprotect multiple items (or multiple VMs), tooview details about a particular VM, open hello vault item dashboard.</span></span> <span data-ttu-id="5ff53-118">Hello procédure suivante vous montre comment tooopen hello *tableau de bord coffre* , puis continuer toohello *tableau de bord coffre*.</span><span class="sxs-lookup"><span data-stu-id="5ff53-118">hello following procedure shows you how tooopen hello *vault dashboard* and then continue toohello *vault item dashboard*.</span></span> <span data-ttu-id="5ff53-119">Il existe des « conseils » dans les deux procédures qui désignent comment tooadd hello coffre et du coffre, toohello de l’élément du tableau de bord Azure à l’aide de commande de toodashboard hello Pin.</span><span class="sxs-lookup"><span data-stu-id="5ff53-119">There are "tips" in both procedures that point out how tooadd hello vault and vault item toohello Azure dashboard by using hello Pin toodashboard command.</span></span> <span data-ttu-id="5ff53-120">Code confidentiel toodashboard est un moyen de créer un coffre toohello de raccourci ou d’un élément.</span><span class="sxs-lookup"><span data-stu-id="5ff53-120">Pin toodashboard is a way of creating a shortcut toohello vault or item.</span></span> <span data-ttu-id="5ff53-121">Vous pouvez également exécuter des commandes courantes à partir du raccourci de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-121">You can also execute common commands from hello shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="5ff53-122">Si vous disposez de plusieurs tableaux de bord et ouvre des panneaux, utilisez le curseur de bleu foncé et de hello bas hello hello tooslide de fenêtre hello du tableau de bord Azure dans les deux sens.</span><span class="sxs-lookup"><span data-stu-id="5ff53-122">If you have multiple dashboards and blades open, use hello dark-blue slider at hello bottom of hello window tooslide hello Azure dashboard back and forth.</span></span>
>
>

![Vue complète avec curseur](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a><span data-ttu-id="5ff53-124">Ouvrez un coffre Recovery Services dans le tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="5ff53-124">Open a Recovery Services vault in hello dashboard:</span></span>
1. <span data-ttu-id="5ff53-125">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5ff53-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5ff53-126">Dans le menu du Hub hello, cliquez sur **Parcourir** et, dans la liste hello des ressources, tapez **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-126">On hello Hub menu, click **Browse** and in hello list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="5ff53-127">Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée.</span><span class="sxs-lookup"><span data-stu-id="5ff53-127">As you begin typing, hello list filters based on your input.</span></span> <span data-ttu-id="5ff53-128">Cliquez sur **Coffre Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-128">Click **Recovery Services vault**.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="5ff53-130">liste Hello des archivages de Recovery Services s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5ff53-130">hello list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="5ff53-131">Liste des coffres Recovery Services</span><span class="sxs-lookup"><span data-stu-id="5ff53-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="5ff53-132">Si vous épinglez un toohello coffre Azure le tableau de bord, ce coffre est immédiatement accessible lorsque vous ouvrez hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff53-132">If you pin a vault toohello Azure Dashboard, that vault is immediately accessible when you open hello Azure portal.</span></span> <span data-ttu-id="5ff53-133">toopin un tableau de bord coffre toohello dans la liste de coffre hello, cliquez sur le coffre de hello, puis sélectionnez **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-133">toopin a vault toohello dashboard, in hello vault list, right-click hello vault, and select **Pin toodashboard**.</span></span>
   >
   >
3. <span data-ttu-id="5ff53-134">À partir de la liste de hello des coffres, sélectionnez hello coffre tooopen son tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5ff53-134">From hello list of vaults, select hello vault tooopen its dashboard.</span></span> <span data-ttu-id="5ff53-135">Lorsque vous sélectionnez le coffre de hello, tableau de bord coffre hello et hello **paramètres** panneau ouvert.</span><span class="sxs-lookup"><span data-stu-id="5ff53-135">When you select hello vault, hello vault dashboard and hello **Settings** blade open.</span></span> <span data-ttu-id="5ff53-136">Bonjour suivant image, hello **Contoso-coffre** tableau de bord est mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="5ff53-136">In hello following image, hello **Contoso-vault** dashboard is highlighted.</span></span>

    ![Ouvrir le tableau de bord du coffre et le panneau Paramètres](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="5ff53-138">Ouvrir le tableau de bord d’un élément du coffre</span><span class="sxs-lookup"><span data-stu-id="5ff53-138">Open a vault item dashboard</span></span>
<span data-ttu-id="5ff53-139">Dans la procédure précédente de hello, vous avez ouvert le tableau de bord hello coffre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-139">In hello previous procedure you opened hello vault dashboard.</span></span> <span data-ttu-id="5ff53-140">tooopen hello coffre tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="5ff53-140">tooopen hello vault item dashboard:</span></span>

1. <span data-ttu-id="5ff53-141">Tableau de bord du coffre hello, sur hello **des éléments de sauvegarde** vignette, cliquez sur **des Machines virtuelles Azure**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-141">In hello vault dashboard, on hello **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Ouvrir la mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="5ff53-143">Hello **des éléments de sauvegarde** panneau répertorie hello dernière tâche de sauvegarde de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="5ff53-143">hello **Backup Items** blade lists hello last backup job for each item.</span></span> <span data-ttu-id="5ff53-144">Dans cet exemple, une machine virtuelle nommée demovm-markgal est protégée par ce coffre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="5ff53-146">Pour faciliter l’accès, vous pouvez épingler un toohello d’élément de coffre Azure le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5ff53-146">For ease of access, you can pin a vault item toohello Azure Dashboard.</span></span> <span data-ttu-id="5ff53-147">toopin un élément de coffre, dans la liste d’éléments de coffre hello, élément de hello avec le bouton droit et sélectionnez **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-147">toopin a vault item, in hello vault item list, right-click hello item and select **Pin toodashboard**.</span></span>
   >
   >
2. <span data-ttu-id="5ff53-148">Bonjour **des éléments de sauvegarde** panneau, cliquez sur hello élément tooopen hello coffre élément du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5ff53-148">In hello **Backup Items** blade, click hello item tooopen hello vault item dashboard.</span></span>

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="5ff53-150">tableau de bord coffre Hello et son **paramètres** panneau ouvert.</span><span class="sxs-lookup"><span data-stu-id="5ff53-150">hello vault item dashboard and its **Settings** blade open.</span></span>

    ![Tableau de bord Éléments de sauvegarde avec panneau Paramètres](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="5ff53-152">À partir de hello coffre élément du tableau de bord, vous pouvez accomplir plusieurs tâches de gestion de clés, telles que :</span><span class="sxs-lookup"><span data-stu-id="5ff53-152">From hello vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="5ff53-153">modifier des stratégies ou créer une stratégie de sauvegarde <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="5ff53-154">afficher les points de restauration et vérifier leur état de cohérence <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="5ff53-155">sauvegarde à la demande d’une machine virtuelle <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="5ff53-156">suspendre la protection des machines virtuelles <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="5ff53-157">reprendre la protection d’une machine virtuelle <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="5ff53-158">supprimer des données de sauvegarde (ou un point de récupération) <br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="5ff53-159">[restaurer des disques de sauvegarde](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  &lt;br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="5ff53-160">Pourquoi les procédures suivantes, hello point de départ est tableau de bord coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-160">For hello following procedures, hello starting point is hello vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="5ff53-161">Gestion des stratégies de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ff53-161">Manage backup policies</span></span>
1. <span data-ttu-id="5ff53-162">Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **tous les paramètres** tooopen hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="5ff53-162">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** tooopen hello **Settings** blade.</span></span>

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="5ff53-164">Sur hello **paramètres** panneau, cliquez sur **stratégie de sauvegarde** tooopen ce panneau.</span><span class="sxs-lookup"><span data-stu-id="5ff53-164">On hello **Settings** blade, click **Backup policy** tooopen that blade.</span></span>

    <span data-ttu-id="5ff53-165">Dans Panneau de hello, hello sauvegarde fréquence et rétention détails de la plage sont affichés.</span><span class="sxs-lookup"><span data-stu-id="5ff53-165">On hello blade, hello backup frequency and retention range details are shown.</span></span>

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="5ff53-167">À partir de hello **choisir la stratégie de sauvegarde** menu :</span><span class="sxs-lookup"><span data-stu-id="5ff53-167">From hello **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="5ff53-168">sélectionner une autre stratégie de toochange stratégies, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-168">toochange policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="5ff53-169">Hello nouvelle stratégie est appliquée immédiatement toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-169">hello new policy is immediately applied toohello vault.</span></span> <span data-ttu-id="5ff53-170"><br\></span><span class="sxs-lookup"><span data-stu-id="5ff53-170"><br\></span></span>
   * <span data-ttu-id="5ff53-171">toocreate une stratégie, sélectionnez **créer un nouveau**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-171">toocreate a policy, select **Create New**.</span></span>

     ![Sauvegarde de machine virtuelle](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="5ff53-173">Pour savoir comment créer une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="5ff53-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="5ff53-174">Lors de la gestion des stratégies de sauvegarde, vérifiez que toofollow hello [meilleures pratiques](backup-azure-vms-introduction.md#best-practices) pour des performances optimales de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ff53-174">While managing backup policies, make sure toofollow hello [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="5ff53-175">Sauvegarde à la demande d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ff53-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="5ff53-176">Vous pouvez effectuer une sauvegarde à la demande d’une machine virtuelle une fois que celle-ci est configurée pour la protection.</span><span class="sxs-lookup"><span data-stu-id="5ff53-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="5ff53-177">Si la sauvegarde initiale de hello est en attente, à la demande de sauvegarde crée une copie complète de la machine virtuelle de hello Bonjour de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5ff53-177">If hello initial backup is pending, on-demand backup creates a full copy of hello virtual machine in hello Recovery Services vault.</span></span> <span data-ttu-id="5ff53-178">Si la sauvegarde initiale de hello est terminée, une sauvegarde à la demande envoyer uniquement les modifications à partir de l’instantané précédent hello, toohello le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="5ff53-178">If hello initial backup is completed, an on-demand backup will only send changes from hello previous snapshot, toohello Recovery Services vault.</span></span> <span data-ttu-id="5ff53-179">Autrement dit, les sauvegardes suivantes sont toujours incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="5ff53-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="5ff53-180">Hello de rétention pour une sauvegarde à la demande est la valeur de rétention hello spécifié pour le point de sauvegarde quotidien hello dans la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-180">hello retention range for an on-demand backup is hello retention value specified for hello Daily backup point in hello policy.</span></span> <span data-ttu-id="5ff53-181">Si aucun point de sauvegarde quotidien n’est sélectionnée, point de sauvegarde hebdomadaire hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="5ff53-181">If no Daily backup point is selected, then hello weekly backup point is used.</span></span>
>
>

<span data-ttu-id="5ff53-182">sauvegarde tootrigger une demande d’un ordinateur virtuel :</span><span class="sxs-lookup"><span data-stu-id="5ff53-182">tootrigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="5ff53-183">Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-183">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="5ff53-185">portail de Hello permet de s’assurer que vous souhaitez toostart un travail de sauvegarde à la demande.</span><span class="sxs-lookup"><span data-stu-id="5ff53-185">hello portal makes sure that you want toostart an on-demand backup job.</span></span> <span data-ttu-id="5ff53-186">Cliquez sur **Oui** toostart du travail de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-186">Click **Yes** toostart hello backup job.</span></span>

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="5ff53-188">travail de sauvegarde Hello crée un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="5ff53-188">hello backup job creates a recovery point.</span></span> <span data-ttu-id="5ff53-189">durée de rétention Hello hello du point de récupération est hello identique à la durée de rétention spécifiée dans la stratégie de hello associée à une machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-189">hello retention range of hello recovery point is hello same as retention range specified in hello policy associated with hello virtual machine.</span></span> <span data-ttu-id="5ff53-190">progression de hello tootrack pour travail hello, dans le tableau de bord du coffre hello, cliquez sur hello **des tâches de sauvegarde** vignette.</span><span class="sxs-lookup"><span data-stu-id="5ff53-190">tootrack hello progress for hello job, in hello vault dashboard, click hello **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="5ff53-191">Arrêt de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="5ff53-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="5ff53-192">Si vous choisissez toostop protéger un ordinateur virtuel, vous êtes invité si vous souhaitez que les points de récupération tooretain hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-192">If you choose toostop protecting a virtual machine, you are asked if you want tooretain hello recovery points.</span></span> <span data-ttu-id="5ff53-193">Il existe deux façons de machines virtuelles de la protection toostop :</span><span class="sxs-lookup"><span data-stu-id="5ff53-193">There are two ways toostop protecting virtual machines:</span></span>

* <span data-ttu-id="5ff53-194">arrêter tous les travaux de sauvegarde à venir et supprimer tous les points de récupération, ou</span><span class="sxs-lookup"><span data-stu-id="5ff53-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="5ff53-195">arrêter toutes les tâches futures de sauvegarde, mais laissez hello points de récupération</span><span class="sxs-lookup"><span data-stu-id="5ff53-195">stop all future backup jobs but leave hello recovery points</span></span> <br/>

<span data-ttu-id="5ff53-196">Il existe un coût associé en laissant hello des points de récupération dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="5ff53-196">There is a cost associated with leaving hello recovery points in storage.</span></span> <span data-ttu-id="5ff53-197">Toutefois, avantage hello de laisser des points de récupération hello est que vous pouvez restaurer une version ultérieure, hello virtual machine si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="5ff53-197">However, hello benefit of leaving hello recovery points is you can restore hello virtual machine later, if desired.</span></span> <span data-ttu-id="5ff53-198">Pour plus d’informations sur les coûts de hello de laisser hello des points de récupération, consultez hello [tarification](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="5ff53-198">For information about hello cost of leaving hello recovery points, see hello  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="5ff53-199">Si vous choisissez toodelete tous les points de récupération, vous ne pouvez pas restaurer hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ff53-199">If you choose toodelete all recovery points, you cannot restore hello virtual machine.</span></span>

<span data-ttu-id="5ff53-200">protection toostop pour un ordinateur virtuel :</span><span class="sxs-lookup"><span data-stu-id="5ff53-200">toostop protection for a virtual machine:</span></span>

1. <span data-ttu-id="5ff53-201">Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **arrêter la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-201">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Bouton Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="5ff53-203">panneau d’arrêter la sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-203">hello Stop Backup blade opens.</span></span>

    ![Panneau Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="5ff53-205">Sur hello **arrêter la sauvegarde** panneau, choisissez si tooretain ou delete hello des données de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="5ff53-205">On hello **Stop Backup** blade, choose whether tooretain or delete hello backup data.</span></span> <span data-ttu-id="5ff53-206">zone d’informations Hello fournit des détails sur votre choix.</span><span class="sxs-lookup"><span data-stu-id="5ff53-206">hello information box provides details about your choice.</span></span>

    ![Arrêter la protection](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="5ff53-208">Si vous avez choisi de données de sauvegarde tooretain hello, ignorez toostep 4.</span><span class="sxs-lookup"><span data-stu-id="5ff53-208">If you chose tooretain hello backup data, skip toostep 4.</span></span> <span data-ttu-id="5ff53-209">Si vous avez choisi de sauvegarder des données toodelete, confirmez que vous souhaitez que les travaux de sauvegarde toostop hello et supprimez des points de récupération hello - nom hello du type d’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-209">If you chose toodelete backup data, confirm that you want toostop hello backup jobs and delete hello recovery points - type hello name of hello item.</span></span>

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5ff53-211">Si vous n’êtes pas sûr du nom de l’élément hello, pointez sur le nom de hello tooview hello point d’exclamation.</span><span class="sxs-lookup"><span data-stu-id="5ff53-211">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5ff53-212">En outre, le nom hello d’élément de hello est sous **arrêter la sauvegarde** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-212">Also, hello name of hello item is under **Stop Backup** at hello top of hello blade.</span></span>
4. <span data-ttu-id="5ff53-213">Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="5ff53-214">Cliquez sur le travail de sauvegarde toostop hello pour l’élément en cours de hello, ![sauvegarde bouton d’arrêt](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="5ff53-214">toostop hello backup job for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="5ff53-215">Un message de notification vous informe des travaux de sauvegarde hello ont été arrêtés.</span><span class="sxs-lookup"><span data-stu-id="5ff53-215">A notification message lets you know hello backup jobs have been stopped.</span></span>

    ![Confirmation l’arrêt de la protection](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="5ff53-217">Reprendre la protection d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5ff53-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="5ff53-218">Si hello **conserver les données de sauvegarde** option choisie lors de la protection pour la machine virtuelle de hello a été arrêtée, il est possible de tooresume protection.</span><span class="sxs-lookup"><span data-stu-id="5ff53-218">If hello **Retain Backup Data** option was chosen when protection for hello virtual machine was stopped, then it is possible tooresume protection.</span></span> <span data-ttu-id="5ff53-219">Si hello **supprimer les données de sauvegarde** option a été choisie, puis ne peut pas reprendre la protection pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-219">If hello **Delete Backup Data** option was chosen, then protection for hello virtual machine cannot resume.</span></span>

<span data-ttu-id="5ff53-220">protection tooresume pour la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="5ff53-220">tooresume protection for hello virtual machine</span></span>

1. <span data-ttu-id="5ff53-221">Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **reprendre la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-221">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Reprendre la protection](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="5ff53-223">Panneau de la stratégie de sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-223">hello Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5ff53-224">Lors de la nouvelle protection hello virtual machine, vous pouvez choisir une autre stratégie que stratégie hello avec laquelle machine virtuelle a été initialement protégée.</span><span class="sxs-lookup"><span data-stu-id="5ff53-224">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="5ff53-225">Suivez les étapes de hello dans [gérer les stratégies de sauvegarde](backup-azure-manage-vms.md#manage-backup-policies) stratégie de hello tooassign pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-225">Follow hello steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) tooassign hello policy for hello virtual machine.</span></span>

    <span data-ttu-id="5ff53-226">Une fois appliqué toohello virtual machine, stratégie de sauvegarde hello vous consultez hello message suivant.</span><span class="sxs-lookup"><span data-stu-id="5ff53-226">Once hello backup policy is applied toohello virtual machine, you see hello following message.</span></span>

    ![Machine virtuelle protégée](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="5ff53-228">Suppression des données de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="5ff53-228">Delete Backup data</span></span>
<span data-ttu-id="5ff53-229">Vous pouvez supprimer les données de sauvegarde hello associées à un ordinateur virtuel pendant hello **arrêter la sauvegarde** travail, ou à tout moment après hello du travail de sauvegarde est terminée.</span><span class="sxs-lookup"><span data-stu-id="5ff53-229">You can delete hello backup data associated with a virtual machine during hello **Stop backup** job, or anytime after hello backup job has completed.</span></span> <span data-ttu-id="5ff53-230">Il peut même être bénéfiques toowait jours ou semaines avant de supprimer des points de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-230">It may even be beneficial toowait days or weeks before deleting hello recovery points.</span></span> <span data-ttu-id="5ff53-231">Contrairement à la restauration des points de récupération, lors de la suppression des données de sauvegarde, vous ne pouvez pas choisir toodelete de points de récupération spécifique.</span><span class="sxs-lookup"><span data-stu-id="5ff53-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points toodelete.</span></span> <span data-ttu-id="5ff53-232">Si vous choisissez toodelete vos données de sauvegarde, vous supprimez tous les points de récupération associés à des éléments de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-232">If you choose toodelete your backup data, you delete all recovery points associated with hello item.</span></span>

<span data-ttu-id="5ff53-233">Hello procédure suivante suppose que le travail de sauvegarde hello pour la machine virtuelle de hello a été arrêté ou désactivé.</span><span class="sxs-lookup"><span data-stu-id="5ff53-233">hello following procedure assumes hello Backup job for hello virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="5ff53-234">Une fois le travail de sauvegarde hello est désactivé, hello **reprendre la sauvegarde** et **supprimer la sauvegarde** options sont disponibles dans le tableau de bord coffre hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-234">Once hello Backup job is disabled, hello **Resume backup** and **Delete backup** options are available in hello vault item dashboard.</span></span>

![Boutons Reprendre et Supprimer](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="5ff53-236">toodelete les données de sauvegarde sur un ordinateur virtuel avec hello *sauvegarde désactivé*:</span><span class="sxs-lookup"><span data-stu-id="5ff53-236">toodelete backup data on a virtual machine with hello *Backup disabled*:</span></span>

1. <span data-ttu-id="5ff53-237">Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **supprimer la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-237">On hello [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="5ff53-239">Hello **supprimer les données de sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="5ff53-239">hello **Delete Backup Data** blade opens.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="5ff53-241">Nom de type hello de hello élément tooconfirm vous souhaitez que les points de récupération toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-241">Type hello name of hello item tooconfirm you want toodelete hello recovery points.</span></span>

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="5ff53-243">Si vous n’êtes pas sûr du nom de l’élément hello, pointez sur le nom de hello tooview hello point d’exclamation.</span><span class="sxs-lookup"><span data-stu-id="5ff53-243">If you aren't sure of hello item name, hover over hello exclamation mark tooview hello name.</span></span> <span data-ttu-id="5ff53-244">En outre, le nom hello d’élément de hello est sous **supprimer les données de sauvegarde** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="5ff53-244">Also, hello name of hello item is under **Delete Backup Data** at hello top of hello blade.</span></span>
3. <span data-ttu-id="5ff53-245">Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.</span><span class="sxs-lookup"><span data-stu-id="5ff53-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="5ff53-246">Cliquez sur les données de sauvegarde toodelete hello pour l’élément en cours de hello, ![sauvegarde bouton d’arrêt](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="5ff53-246">toodelete hello backup data for hello current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="5ff53-247">Un message de notification vous informe des données de sauvegarde hello a été supprimées.</span><span class="sxs-lookup"><span data-stu-id="5ff53-247">A notification message lets you know hello backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ff53-248">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ff53-248">Next steps</span></span>
<span data-ttu-id="5ff53-249">Pour plus d’informations sur la manière de recréer une machine virtuelle à partir d’un point de récupération, consultez [Restauration de machines virtuelles Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5ff53-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="5ff53-250">Si vous avez besoin d’informations sur la protection de vos machines virtuelles, consultez [tout d’abord rechercher : sauvegardez tooa de machines virtuelles de coffre Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5ff53-250">If you need information on protecting your virtual machines, see [First look: Back up VMs tooa Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="5ff53-251">Pour plus d’informations sur la surveillance des événements, consultez [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Surveiller les alertes des sauvegardes de machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="5ff53-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
