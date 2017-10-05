---
title: "Gestion des sauvegardes de machines virtuelles déployées via le Gestionnaire de ressources | Microsoft Docs"
description: "Découvrez comment gérer et surveiller les sauvegardes d’une machine virtuelle déployée via Resource Manager"
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
ms.openlocfilehash: 35a21cb99ca4bad124a9f764cef9da453e1fe47f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-virtual-machine-backups"></a><span data-ttu-id="ce91b-103">Gestion des sauvegardes de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ce91b-103">Manage Azure virtual machine backups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce91b-104">Gestion des sauvegardes de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ce91b-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="ce91b-105">Gestion des sauvegardes de machines virtuelles classiques</span><span class="sxs-lookup"><span data-stu-id="ce91b-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="ce91b-106">Cet article fournit des conseils sur la gestion des sauvegardes de machines virtuelles et décrit les données d’alertes de sauvegarde disponibles dans le tableau de bord du portail.</span><span class="sxs-lookup"><span data-stu-id="ce91b-106">This article provides guidance on managing VM backups, and explains the backup alerts information available in the portal dashboard.</span></span> <span data-ttu-id="ce91b-107">Les instructions contenues dans cet article s’appliquent à l’utilisation de machines virtuelles avec des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ce91b-107">The guidance in this article applies to using VMs with Recovery Services vaults.</span></span> <span data-ttu-id="ce91b-108">Cet article ne couvre pas la création des machines virtuelles et n’explique pas comment protéger les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="ce91b-108">This article does not cover the creation of virtual machines, nor does it explain how to protect virtual machines.</span></span> <span data-ttu-id="ce91b-109">Pour une introduction à la protection des machines virtuelles déployées via Azure Resource Manager dans Azure à l’aide d’un coffre Recovery Services, consultez la page [Premier aperçu : sauvegarder les machines virtuelles ARM dans un archivage de Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ce91b-109">For a primer on protecting Azure Resource Manager-deployed VMs in Azure with a Recovery Services vault, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span>

## <a name="manage-vaults-and-protected-virtual-machines"></a><span data-ttu-id="ce91b-110">Gérer les coffres et les machines virtuelles protégées</span><span class="sxs-lookup"><span data-stu-id="ce91b-110">Manage vaults and protected virtual machines</span></span>
<span data-ttu-id="ce91b-111">Dans le portail Azure, le tableau de bord Coffre Recovery Services permet d’accéder à des informations concernant le coffre, notamment :</span><span class="sxs-lookup"><span data-stu-id="ce91b-111">In the Azure portal, the Recovery Services vault dashboard provides access to information about the vault including:</span></span>

* <span data-ttu-id="ce91b-112">l’instantané de sauvegarde le plus récent, c’est-à-dire le dernier point de restauration <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-112">the most recent backup snapshot, which is also the latest restore point <br\></span></span>
* <span data-ttu-id="ce91b-113">la stratégie de sauvegarde <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-113">the backup policy <br\></span></span>
* <span data-ttu-id="ce91b-114">la taille totale de tous les instantanés de sauvegarde <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-114">total size of all backup snapshots <br\></span></span>
* <span data-ttu-id="ce91b-115">le nombre de machines virtuelles protégées par le coffre <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-115">number of virtual machines that are protected with the vault <br\></span></span>

<span data-ttu-id="ce91b-116">L’ouverture du coffre dans le tableau de bord permet d’initier de nombreuses tâches de gestion associées à une sauvegarde de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce91b-116">Many management tasks with a virtual machine backup begin with opening the vault in the dashboard.</span></span> <span data-ttu-id="ce91b-117">Dans la mesure où les coffres peuvent être utilisés pour protéger plusieurs éléments (ou plusieurs machines virtuelles), vous devez cependant ouvrir le tableau de bord de l’élément du coffre pour afficher les détails d’une machine virtuelle spécifique.</span><span class="sxs-lookup"><span data-stu-id="ce91b-117">However, because vaults can be used to protect multiple items (or multiple VMs), to view details about a particular VM, open the vault item dashboard.</span></span> <span data-ttu-id="ce91b-118">La procédure suivante vous montre comment ouvrir le *tableau de bord du coffre* puis le *tableau de bord de l’élément du coffre*.</span><span class="sxs-lookup"><span data-stu-id="ce91b-118">The following procedure shows you how to open the *vault dashboard* and then continue to the *vault item dashboard*.</span></span> <span data-ttu-id="ce91b-119">Pour les deux procédures, nous vous proposons des « astuces » pour vous aider à ajouter le coffre et l’élément du coffre au tableau de bord Azure à l’aide de la commande Épingler au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="ce91b-119">There are "tips" in both procedures that point out how to add the vault and vault item to the Azure dashboard by using the Pin to dashboard command.</span></span> <span data-ttu-id="ce91b-120">La commande Épingler au tableau de bord permet de créer un raccourci vers le coffre ou l’élément.</span><span class="sxs-lookup"><span data-stu-id="ce91b-120">Pin to dashboard is a way of creating a shortcut to the vault or item.</span></span> <span data-ttu-id="ce91b-121">Vous pouvez également utiliser le raccourci pour exécuter des commandes courantes.</span><span class="sxs-lookup"><span data-stu-id="ce91b-121">You can also execute common commands from the shortcut.</span></span>

> [!TIP]
> <span data-ttu-id="ce91b-122">Si vous avez ouvert plusieurs tableaux de bord et panneaux, utilisez le curseur bleu foncé situé en bas de la fenêtre pour faire défiler le tableau de bord Azure.</span><span class="sxs-lookup"><span data-stu-id="ce91b-122">If you have multiple dashboards and blades open, use the dark-blue slider at the bottom of the window to slide the Azure dashboard back and forth.</span></span>
>
>

![Vue complète avec curseur](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-the-dashboard"></a><span data-ttu-id="ce91b-124">Ouvrez un coffre Recovery Services dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="ce91b-124">Open a Recovery Services vault in the dashboard:</span></span>
1. <span data-ttu-id="ce91b-125">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ce91b-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ce91b-126">Dans le menu Hub, cliquez sur **Parcourir** et, dans la liste des ressources, tapez **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-126">On the Hub menu, click **Browse** and in the list of resources, type **Recovery Services**.</span></span> <span data-ttu-id="ce91b-127">Au fur et à mesure de la saisie, la liste est filtrée.</span><span class="sxs-lookup"><span data-stu-id="ce91b-127">As you begin typing, the list filters based on your input.</span></span> <span data-ttu-id="ce91b-128">Cliquez sur **Coffre Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-128">Click **Recovery Services vault**.</span></span>

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    <span data-ttu-id="ce91b-130">La liste des archivages de Recovery Services est affichée.</span><span class="sxs-lookup"><span data-stu-id="ce91b-130">The list of Recovery Services vaults are displayed.</span></span>

    ![<span data-ttu-id="ce91b-131">Liste des coffres Recovery Services</span><span class="sxs-lookup"><span data-stu-id="ce91b-131">List of Recovery Services vaults</span></span> ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > <span data-ttu-id="ce91b-132">Si vous épinglez un coffre au tableau de bord Azure, ce coffre est immédiatement accessible à l’ouverture du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ce91b-132">If you pin a vault to the Azure Dashboard, that vault is immediately accessible when you open the Azure portal.</span></span> <span data-ttu-id="ce91b-133">Pour épingler un coffre au tableau de bord, accédez à la liste des coffres, cliquez avec le bouton droit sur le coffre, puis sélectionnez **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-133">To pin a vault to the dashboard, in the vault list, right-click the vault, and select **Pin to dashboard**.</span></span>
   >
   >
3. <span data-ttu-id="ce91b-134">Dans la liste des coffres, sélectionnez le coffre pour ouvrir le tableau de bord correspondant.</span><span class="sxs-lookup"><span data-stu-id="ce91b-134">From the list of vaults, select the vault to open its dashboard.</span></span> <span data-ttu-id="ce91b-135">Lorsque vous sélectionnez le coffre, vous accédez à son tableau de bord et au panneau **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="ce91b-135">When you select the vault, the vault dashboard and the **Settings** blade open.</span></span> <span data-ttu-id="ce91b-136">Dans la capture d’écran ci-dessous, le tableau de bord **Contoso-vault** est mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="ce91b-136">In the following image, the **Contoso-vault** dashboard is highlighted.</span></span>

    ![Ouvrir le tableau de bord du coffre et le panneau Paramètres](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a><span data-ttu-id="ce91b-138">Ouvrir le tableau de bord d’un élément du coffre</span><span class="sxs-lookup"><span data-stu-id="ce91b-138">Open a vault item dashboard</span></span>
<span data-ttu-id="ce91b-139">Dans la procédure précédente, vous avez ouvert le tableau de bord du coffre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-139">In the previous procedure you opened the vault dashboard.</span></span> <span data-ttu-id="ce91b-140">Pour ouvrir maintenant le tableau de bord d’un élément du coffre, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce91b-140">To open the vault item dashboard:</span></span>

1. <span data-ttu-id="ce91b-141">Sur la vignette **Éléments de sauvegarde** du tableau de bord du coffre, cliquez sur **Machines virtuelles Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-141">In the vault dashboard, on the **Backup Items** tile, click **Azure Virtual Machines**.</span></span>

    ![Ouvrir la mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    <span data-ttu-id="ce91b-143">Le panneau **Éléments de sauvegarde** affiche la dernière tâche de sauvegarde pour chaque élément.</span><span class="sxs-lookup"><span data-stu-id="ce91b-143">The **Backup Items** blade lists the last backup job for each item.</span></span> <span data-ttu-id="ce91b-144">Dans cet exemple, une machine virtuelle nommée demovm-markgal est protégée par ce coffre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-144">In this example, there is one virtual machine, demovm-markgal, protected by this vault.</span></span>  

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > <span data-ttu-id="ce91b-146">Pour y accéder plus facilement, vous pouvez épingler un élément du coffre au tableau de bord Azure.</span><span class="sxs-lookup"><span data-stu-id="ce91b-146">For ease of access, you can pin a vault item to the Azure Dashboard.</span></span> <span data-ttu-id="ce91b-147">Pour épingler un élément du coffre, accédez à la liste des éléments du coffre, cliquez avec le bouton droit sur l’élément, puis sélectionnez **Épingler au tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-147">To pin a vault item, in the vault item list, right-click the item and select **Pin to dashboard**.</span></span>
   >
   >
2. <span data-ttu-id="ce91b-148">Dans le panneau **Éléments de sauvegarde** , cliquez sur l’élément pour ouvrir le tableau de bord correspondant.</span><span class="sxs-lookup"><span data-stu-id="ce91b-148">In the **Backup Items** blade, click the item to open the vault item dashboard.</span></span>

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    <span data-ttu-id="ce91b-150">Le tableau de bord de l’élément du coffre s’ouvre sur le panneau **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="ce91b-150">The vault item dashboard and its **Settings** blade open.</span></span>

    ![Tableau de bord Éléments de sauvegarde avec panneau Paramètres](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    <span data-ttu-id="ce91b-152">Le tableau de bord de l’élément du coffre vous permet d’accomplir plusieurs tâches de gestion essentielles, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ce91b-152">From the vault item dashboard, you can accomplish many key management tasks, such as:</span></span>

   * <span data-ttu-id="ce91b-153">modifier des stratégies ou créer une stratégie de sauvegarde <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-153">change policies or create a new backup policy<br\></span></span>
   * <span data-ttu-id="ce91b-154">afficher les points de restauration et vérifier leur état de cohérence <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-154">view restore points, and see their consistency state <br\></span></span>
   * <span data-ttu-id="ce91b-155">sauvegarde à la demande d’une machine virtuelle <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-155">on-demand backup of a virtual machine <br\></span></span>
   * <span data-ttu-id="ce91b-156">suspendre la protection des machines virtuelles <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-156">stop protecting virtual machines <br\></span></span>
   * <span data-ttu-id="ce91b-157">reprendre la protection d’une machine virtuelle <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-157">resume protection of a virtual machine <br\></span></span>
   * <span data-ttu-id="ce91b-158">supprimer des données de sauvegarde (ou un point de récupération) <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-158">delete a backup data (or recovery point) <br\></span></span>
   * <span data-ttu-id="ce91b-159">[restaurer des disques de sauvegarde](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-159">[restore backup disks](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\></span></span>

<span data-ttu-id="ce91b-160">Pour les procédures suivantes, nous allons travailler à partir du tableau de bord de l’élément du coffre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-160">For the following procedures, the starting point is the vault item dashboard.</span></span>

## <a name="manage-backup-policies"></a><span data-ttu-id="ce91b-161">Gestion des stratégies de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="ce91b-161">Manage backup policies</span></span>
1. <span data-ttu-id="ce91b-162">Dans le [tableau de bord de l’élément du coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **Tous les paramètres** pour ouvrir le panneau **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-162">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **All Settings** to open the **Settings** blade.</span></span>

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/all-settings-button.png)
2. <span data-ttu-id="ce91b-164">Dans le panneau **Paramètres**, cliquez sur **Stratégie de sauvegarde** pour ouvrir le panneau correspondant.</span><span class="sxs-lookup"><span data-stu-id="ce91b-164">On the **Settings** blade, click **Backup policy** to open that blade.</span></span>

    <span data-ttu-id="ce91b-165">Ce panneau affiche les détails de la plage de rétention et de la fréquence de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce91b-165">On the blade, the backup frequency and retention range details are shown.</span></span>

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. <span data-ttu-id="ce91b-167">Dans le menu **Choisir une stratégie de sauvegarde** :</span><span class="sxs-lookup"><span data-stu-id="ce91b-167">From the **Choose backup policy** menu:</span></span>

   * <span data-ttu-id="ce91b-168">Pour modifier les stratégies, sélectionnez une autre stratégie, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-168">To change policies, select a different policy and click **Save**.</span></span> <span data-ttu-id="ce91b-169">La nouvelle stratégie est appliquée immédiatement au coffre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-169">The new policy is immediately applied to the vault.</span></span> <span data-ttu-id="ce91b-170"><br\></span><span class="sxs-lookup"><span data-stu-id="ce91b-170"><br\></span></span>
   * <span data-ttu-id="ce91b-171">Pour créer une stratégie, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-171">To create a policy, select **Create New**.</span></span>

     ![Sauvegarde de machine virtuelle](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     <span data-ttu-id="ce91b-173">Pour savoir comment créer une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-manage-vms.md#defining-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="ce91b-173">For instructions on creating a backup policy, see [Defining a backup policy](backup-azure-manage-vms.md#defining-a-backup-policy).</span></span>

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> <span data-ttu-id="ce91b-174">Pour des performances de sauvegarde optimales, veillez à suivre les [meilleures pratiques](backup-azure-vms-introduction.md#best-practices) lorsque vous gérez des stratégies de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce91b-174">While managing backup policies, make sure to follow the [best practices](backup-azure-vms-introduction.md#best-practices) for optimal backup performance</span></span>
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="ce91b-175">Sauvegarde à la demande d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ce91b-175">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="ce91b-176">Vous pouvez effectuer une sauvegarde à la demande d’une machine virtuelle une fois que celle-ci est configurée pour la protection.</span><span class="sxs-lookup"><span data-stu-id="ce91b-176">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="ce91b-177">Si la sauvegarde initiale est en attente, la sauvegarde à la demande crée une copie complète de la machine virtuelle dans le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="ce91b-177">If the initial backup is pending, on-demand backup creates a full copy of the virtual machine in the Recovery Services vault.</span></span> <span data-ttu-id="ce91b-178">Si la sauvegarde initiale est terminée, une sauvegarde à la demande enverra au coffre Recovery Services uniquement les modifications par rapport à l’instantané précédent.</span><span class="sxs-lookup"><span data-stu-id="ce91b-178">If the initial backup is completed, an on-demand backup will only send changes from the previous snapshot, to the Recovery Services vault.</span></span> <span data-ttu-id="ce91b-179">Autrement dit, les sauvegardes suivantes sont toujours incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="ce91b-179">That is, subsequent backups are always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="ce91b-180">La plage de rétention pour une sauvegarde à la demande correspond à la valeur de rétention spécifiée pour le point de sauvegarde quotidien de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="ce91b-180">The retention range for an on-demand backup is the retention value specified for the Daily backup point in the policy.</span></span> <span data-ttu-id="ce91b-181">Si aucun point de sauvegarde quotidien n’est sélectionné, le point de sauvegarde hebdomadaire est utilisé.</span><span class="sxs-lookup"><span data-stu-id="ce91b-181">If no Daily backup point is selected, then the weekly backup point is used.</span></span>
>
>

<span data-ttu-id="ce91b-182">Pour déclencher une sauvegarde à la demande d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ce91b-182">To trigger an on-demand backup of a virtual machine:</span></span>

* <span data-ttu-id="ce91b-183">Sur le [tableau de bord de l’élément du coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **Sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-183">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Backup now**.</span></span>

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-button.png)

    <span data-ttu-id="ce91b-185">Le portail vous demande de confirmer que vous souhaitez démarrer un travail de sauvegarde à la demande.</span><span class="sxs-lookup"><span data-stu-id="ce91b-185">The portal makes sure that you want to start an on-demand backup job.</span></span> <span data-ttu-id="ce91b-186">Cliquez sur **Oui** pour démarrer le travail de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce91b-186">Click **Yes** to start the backup job.</span></span>

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-check.png)

    <span data-ttu-id="ce91b-188">Le travail de sauvegarde crée un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="ce91b-188">The backup job creates a recovery point.</span></span> <span data-ttu-id="ce91b-189">La plage de rétention du point de récupération est identique à celle spécifiée dans la stratégie associée à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce91b-189">The retention range of the recovery point is the same as retention range specified in the policy associated with the virtual machine.</span></span> <span data-ttu-id="ce91b-190">Pour suivre la progression du travail, dans le tableau de bord du coffre, cliquez sur la mosaïque **Travaux de sauvegarde** .</span><span class="sxs-lookup"><span data-stu-id="ce91b-190">To track the progress for the job, in the vault dashboard, click the **Backup Jobs** tile.</span></span>  

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="ce91b-191">Arrêt de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ce91b-191">Stop protecting virtual machines</span></span>
<span data-ttu-id="ce91b-192">Si vous décidez d’arrêter la protection d’une machine virtuelle, vous devrez indiquer si vous souhaitez conserver les points de récupération.</span><span class="sxs-lookup"><span data-stu-id="ce91b-192">If you choose to stop protecting a virtual machine, you are asked if you want to retain the recovery points.</span></span> <span data-ttu-id="ce91b-193">Il existe deux façons de suspendre la protection des machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="ce91b-193">There are two ways to stop protecting virtual machines:</span></span>

* <span data-ttu-id="ce91b-194">arrêter tous les travaux de sauvegarde à venir et supprimer tous les points de récupération, ou</span><span class="sxs-lookup"><span data-stu-id="ce91b-194">stop all future backup jobs and delete all recovery points, or</span></span>
* <span data-ttu-id="ce91b-195">arrêter tous les travaux de sauvegarde à venir en conservant les points de récupération </span><span class="sxs-lookup"><span data-stu-id="ce91b-195">stop all future backup jobs but leave the recovery points</span></span> <br/>

<span data-ttu-id="ce91b-196">La conservation des points de récupération dans le stockage présente un coût,</span><span class="sxs-lookup"><span data-stu-id="ce91b-196">There is a cost associated with leaving the recovery points in storage.</span></span> <span data-ttu-id="ce91b-197">mais elle a l’avantage de vous permettre de restaurer ultérieurement la machine virtuelle, si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ce91b-197">However, the benefit of leaving the recovery points is you can restore the virtual machine later, if desired.</span></span> <span data-ttu-id="ce91b-198">Pour plus d’informations sur les coûts de conservation des points de récupération, consultez la [tarification](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="ce91b-198">For information about the cost of leaving the recovery points, see the  [pricing details](https://azure.microsoft.com/pricing/details/backup/).</span></span> <span data-ttu-id="ce91b-199">Si vous choisissez de supprimer tous les points de récupération, vous ne pourrez pas restaurer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce91b-199">If you choose to delete all recovery points, you cannot restore the virtual machine.</span></span>

<span data-ttu-id="ce91b-200">Pour arrêter la protection d’une machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="ce91b-200">To stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="ce91b-201">Sur le [tableau de bord de l’élément du coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **Arrêter la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-201">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Stop backup**.</span></span>

    ![Bouton Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-button.png)

    <span data-ttu-id="ce91b-203">Le panneau Arrêter la sauvegarde s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-203">The Stop Backup blade opens.</span></span>

    ![Panneau Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. <span data-ttu-id="ce91b-205">Dans le panneau **Arrêter la sauvegarde** , indiquez si vous souhaitez conserver ou supprimer les données de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce91b-205">On the **Stop Backup** blade, choose whether to retain or delete the backup data.</span></span> <span data-ttu-id="ce91b-206">La zone d’informations fournit des détails pour vous guider dans votre choix.</span><span class="sxs-lookup"><span data-stu-id="ce91b-206">The information box provides details about your choice.</span></span>

    ![Arrêter la protection](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. <span data-ttu-id="ce91b-208">Si vous avez choisi de conserver les données de sauvegarde, passez à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="ce91b-208">If you chose to retain the backup data, skip to step 4.</span></span> <span data-ttu-id="ce91b-209">Si vous avez choisi de supprimer les données de sauvegarde, confirmez que vous souhaitez bien arrêter les travaux de sauvegarde et supprimer les points de récupération. Saisissez le nom de l’élément.</span><span class="sxs-lookup"><span data-stu-id="ce91b-209">If you chose to delete backup data, confirm that you want to stop the backup jobs and delete the recovery points - type the name of the item.</span></span>

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="ce91b-211">Si vous n’êtes pas sûr du nom de l’élément, survolez le point d’exclamation pour en afficher le nom.</span><span class="sxs-lookup"><span data-stu-id="ce91b-211">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="ce91b-212">Le nom de l’élément figure également sous **Arrêter la sauvegarde** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="ce91b-212">Also, the name of the item is under **Stop Backup** at the top of the blade.</span></span>
4. <span data-ttu-id="ce91b-213">Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-213">Optionally provide a **Reason** or **Comment**.</span></span>
5. <span data-ttu-id="ce91b-214">Pour arrêter le travail de sauvegarde pour l’élément actif, cliquez sur ![bouton sauvegarde arrêter](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span><span class="sxs-lookup"><span data-stu-id="ce91b-214">To stop the backup job for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/stop-backup-button-blue.png)</span></span>

    <span data-ttu-id="ce91b-215">Un message de notification vous informe que les travaux de sauvegarde ont été interrompus.</span><span class="sxs-lookup"><span data-stu-id="ce91b-215">A notification message lets you know the backup jobs have been stopped.</span></span>

    ![Confirmation l’arrêt de la protection](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a><span data-ttu-id="ce91b-217">Reprendre la protection d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ce91b-217">Resume protection of a virtual machine</span></span>
<span data-ttu-id="ce91b-218">Si vous avez choisi l’option **Conserver les données de sauvegarde** au moment de l’arrêt de la protection de la machine virtuelle, vous avez la possibilité de restaurer la protection.</span><span class="sxs-lookup"><span data-stu-id="ce91b-218">If the **Retain Backup Data** option was chosen when protection for the virtual machine was stopped, then it is possible to resume protection.</span></span> <span data-ttu-id="ce91b-219">Si vous avez choisi l’option **Supprimer les données de sauvegarde** , vous ne pourrez pas restaurer la protection de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce91b-219">If the **Delete Backup Data** option was chosen, then protection for the virtual machine cannot resume.</span></span>

<span data-ttu-id="ce91b-220">Pour reprendre la protection de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ce91b-220">To resume protection for the virtual machine</span></span>

1. <span data-ttu-id="ce91b-221">Sur le [tableau de bord de l’élément du coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **Reprendre la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-221">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Resume backup**.</span></span>

    ![Reprendre la protection](./media/backup-azure-manage-vms/resume-backup-button.png)

    <span data-ttu-id="ce91b-223">Le panneau Stratégie de sauvegarde s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-223">The Backup Policy blade opens.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce91b-224">Lors de l’application d’une nouvelle protection à la machine virtuelle, vous pouvez choisir une autre stratégie que la stratégie avec laquelle la machine virtuelle a été initialement protégée.</span><span class="sxs-lookup"><span data-stu-id="ce91b-224">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
   >
   >
2. <span data-ttu-id="ce91b-225">Suivez les étapes de la section [Modifier les stratégies de sauvegarde](backup-azure-manage-vms.md#manage-backup-policies) pour affecter la stratégie de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce91b-225">Follow the steps in [Manage backup policies](backup-azure-manage-vms.md#manage-backup-policies) to assign the policy for the virtual machine.</span></span>

    <span data-ttu-id="ce91b-226">Une fois la stratégie de sauvegarde appliquée à la machine virtuelle, le message suivant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ce91b-226">Once the backup policy is applied to the virtual machine, you see the following message.</span></span>

    ![Machine virtuelle protégée](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a><span data-ttu-id="ce91b-228">Supprimer les données de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="ce91b-228">Delete Backup data</span></span>
<span data-ttu-id="ce91b-229">Vous pouvez supprimer les données de sauvegarde associées à une machine virtuelle au cours du travail **Arrêter la sauvegarde** , ou à tout moment après la fin du travail de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="ce91b-229">You can delete the backup data associated with a virtual machine during the **Stop backup** job, or anytime after the backup job has completed.</span></span> <span data-ttu-id="ce91b-230">Il peut même être préférable d’attendre plusieurs jours ou semaines avant de supprimer les points de récupération.</span><span class="sxs-lookup"><span data-stu-id="ce91b-230">It may even be beneficial to wait days or weeks before deleting the recovery points.</span></span> <span data-ttu-id="ce91b-231">Contrairement à la restauration des points de récupération, lors de la suppression des données de sauvegarde, vous ne pouvez pas choisir des points de récupération spécifiques à supprimer.</span><span class="sxs-lookup"><span data-stu-id="ce91b-231">Unlike restoring recovery points, when deleting backup data, you cannot choose specific recovery points to delete.</span></span> <span data-ttu-id="ce91b-232">Si vous choisissez de supprimer vos données de sauvegarde, vous supprimerez tous les points de récupération associés à l’élément.</span><span class="sxs-lookup"><span data-stu-id="ce91b-232">If you choose to delete your backup data, you delete all recovery points associated with the item.</span></span>

<span data-ttu-id="ce91b-233">La procédure suivante suppose que le travail de sauvegarde de la machine virtuelle a été arrêté ou désactivé.</span><span class="sxs-lookup"><span data-stu-id="ce91b-233">The following procedure assumes the Backup job for the virtual machine has been stopped or disabled.</span></span> <span data-ttu-id="ce91b-234">Les options **Reprendre la sauvegarde** et **Supprimer la sauvegarde** sont accessibles dans le tableau de bord de l’élément du coffre seulement lorsque le travail de sauvegarde a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="ce91b-234">Once the Backup job is disabled, the **Resume backup** and **Delete backup** options are available in the vault item dashboard.</span></span>

![Boutons Reprendre et Supprimer](./media/backup-azure-manage-vms/resume-delete-buttons.png)

<span data-ttu-id="ce91b-236">Pour supprimer les données de sauvegarde d’une machine virtuelle avec l’option *Sauvegarde désactivée*:</span><span class="sxs-lookup"><span data-stu-id="ce91b-236">To delete backup data on a virtual machine with the *Backup disabled*:</span></span>

1. <span data-ttu-id="ce91b-237">Sur le [tableau de bord de l’élément du coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **Supprimer la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-237">On the [vault item dashboard](backup-azure-manage-vms.md#open-a-vault-item-dashboard), click **Delete backup**.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    <span data-ttu-id="ce91b-239">Le panneau **Supprimer les données de sauvegarde** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="ce91b-239">The **Delete Backup Data** blade opens.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. <span data-ttu-id="ce91b-241">Saisissez le nom de l’élément pour confirmer la suppression des points de récupération.</span><span class="sxs-lookup"><span data-stu-id="ce91b-241">Type the name of the item to confirm you want to delete the recovery points.</span></span>

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    <span data-ttu-id="ce91b-243">Si vous n’êtes pas sûr du nom de l’élément, survolez le point d’exclamation pour en afficher le nom.</span><span class="sxs-lookup"><span data-stu-id="ce91b-243">If you aren't sure of the item name, hover over the exclamation mark to view the name.</span></span> <span data-ttu-id="ce91b-244">Le nom de l’élément figure également sous **Supprimer les données de sauvegarde** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="ce91b-244">Also, the name of the item is under **Delete Backup Data** at the top of the blade.</span></span>
3. <span data-ttu-id="ce91b-245">Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.</span><span class="sxs-lookup"><span data-stu-id="ce91b-245">Optionally provide a **Reason** or **Comment**.</span></span>
4. <span data-ttu-id="ce91b-246">Pour supprimer les données de sauvegarde pour l’élément actif, cliquez sur ![bouton sauvegarde arrêter](./media/backup-azure-manage-vms/delete-button.png)</span><span class="sxs-lookup"><span data-stu-id="ce91b-246">To delete the backup data for the current item, click  ![Stop backup button](./media/backup-azure-manage-vms/delete-button.png)</span></span>

    <span data-ttu-id="ce91b-247">Un message de notification vous informe que les données de sauvegarde ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="ce91b-247">A notification message lets you know the backup data has been deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce91b-248">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce91b-248">Next steps</span></span>
<span data-ttu-id="ce91b-249">Pour plus d’informations sur la manière de recréer une machine virtuelle à partir d’un point de récupération, consultez [Restauration de machines virtuelles Azure](backup-azure-restore-vms.md).</span><span class="sxs-lookup"><span data-stu-id="ce91b-249">For information on re-creating a virtual machine from a recovery point, check out [Restore Azure VMs](backup-azure-restore-vms.md).</span></span> <span data-ttu-id="ce91b-250">Pour plus d’informations sur la protection de vos machines virtuelles, consultez [Premier aperçu : sauvegarder les machines virtuelles ARM dans un archivage de Recovery Services](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ce91b-250">If you need information on protecting your virtual machines, see [First look: Back up VMs to a Recovery Services vault](backup-azure-vms-first-look-arm.md).</span></span> <span data-ttu-id="ce91b-251">Pour plus d’informations sur la surveillance des événements, consultez [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Surveiller les alertes des sauvegardes de machines virtuelles Azure).</span><span class="sxs-lookup"><span data-stu-id="ce91b-251">For information on monitoring events, see [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md).</span></span>
