---
title: les sauvegardes de machine virtuelle Azure aaaManage et analyse | Documents Microsoft
description: "Découvrez comment toomanage et analyse Azure virtual machine de sauvegardes"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="f77b8-103">Gérer les travaux de sauvegarde Azure courants et de déclencher des alertes dans le portail classique de hello</span><span class="sxs-lookup"><span data-stu-id="f77b8-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f77b8-104">Gestion des sauvegardes de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="f77b8-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="f77b8-105">Gestion des sauvegardes de machines virtuelles classiques</span><span class="sxs-lookup"><span data-stu-id="f77b8-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="f77b8-106">Cet article fournit des informations sur les tâches de gestion et de surveillance courantes des machines virtuelles déployées avec le modèle Classic protégées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f77b8-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="f77b8-107">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f77b8-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f77b8-108">Consultez [préparer votre tooback environnement des machines virtuelles](backup-azure-vms-prepare.md) pour plus d’informations sur l’utilisation de déploiement de classique des machines virtuelles de modèle.</span><span class="sxs-lookup"><span data-stu-id="f77b8-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="f77b8-109">À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.</span><span class="sxs-lookup"><span data-stu-id="f77b8-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="f77b8-110">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="f77b8-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="f77b8-111">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f77b8-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f77b8-112">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="f77b8-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="f77b8-113">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f77b8-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="f77b8-114">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="f77b8-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f77b8-115">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="f77b8-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="f77b8-116">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="f77b8-117">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="f77b8-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="f77b8-118">Gérer des machines virtuelles protégées</span><span class="sxs-lookup"><span data-stu-id="f77b8-118">Manage protected virtual machines</span></span>
<span data-ttu-id="f77b8-119">toomanage des ordinateurs virtuels protégés :</span><span class="sxs-lookup"><span data-stu-id="f77b8-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="f77b8-120">tooview et gérer les paramètres de sauvegarde pour un ordinateur virtuel, cliquez sur hello **éléments protégés** onglet.</span><span class="sxs-lookup"><span data-stu-id="f77b8-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="f77b8-121">Cliquez sur le nom hello un Hello de toosee élément protégé **détails de la sauvegarde** onglet, qui présente des informations sur la dernière sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Sauvegarde de machine virtuelle](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="f77b8-123">tooview et gérer les paramètres de stratégie de sauvegarde pour un ordinateur virtuel, cliquez sur hello **stratégies** onglet.</span><span class="sxs-lookup"><span data-stu-id="f77b8-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Stratégie de machine virtuelle](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="f77b8-125">Hello **stratégies de sauvegarde** onglet affiche hello de stratégie existante.</span><span class="sxs-lookup"><span data-stu-id="f77b8-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="f77b8-126">Vous pouvez la modifier en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f77b8-126">You can modify as needed.</span></span> <span data-ttu-id="f77b8-127">Si vous avez besoin d’une nouvelle stratégie de toocreate cliquez sur **créer** sur hello **stratégies** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="f77b8-128">Notez que si vous souhaitez tooremove une stratégie qu’il ne doit pas avoir toutes les machines virtuelles associées.</span><span class="sxs-lookup"><span data-stu-id="f77b8-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Stratégie de machine virtuelle](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="f77b8-130">Vous pouvez obtenir plus d’informations sur l’état ou les actions pour un ordinateur virtuel sur hello **travaux** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="f77b8-131">Cliquez sur une tâche dans hello liste tooget davantage de détails ou filtre les travaux pour un ordinateur virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="f77b8-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Tâches](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="f77b8-133">Sauvegarde à la demande d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f77b8-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="f77b8-134">Vous pouvez effectuer une sauvegarde à la demande d’une machine virtuelle une fois que celle-ci est configurée pour la protection.</span><span class="sxs-lookup"><span data-stu-id="f77b8-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="f77b8-135">Si la sauvegarde initiale hello est en attente pour l’ordinateur virtuel de hello, sauvegarde créera une copie complète de la machine virtuelle de hello dans le coffre de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="f77b8-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="f77b8-136">Si la première sauvegarde est terminée, à la demande de sauvegarde aura uniquement l’envoi des modifications à partir de la sauvegarde tooAzure sauvegarde précédente de coffre autrement dit, il est toujours incrémentiel.</span><span class="sxs-lookup"><span data-stu-id="f77b8-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="f77b8-137">Durée de rétention d’une sauvegarde à la demande est valeur tooretention spécifiée pour le délai de rétention quotidienne toohello correspondante de stratégie de sauvegarde virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f77b8-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="f77b8-138">sauvegarde tootake une demande d’un ordinateur virtuel :</span><span class="sxs-lookup"><span data-stu-id="f77b8-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="f77b8-139">Accédez toohello **éléments protégés** page et sélectionnez **Machine virtuelle Azure** en tant que **Type** (le cas échéant), puis cliquez sur **sélectionnez**bouton.</span><span class="sxs-lookup"><span data-stu-id="f77b8-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="f77b8-141">Sélectionnez la machine virtuelle hello sur lequel vous souhaitez tootake une demande de sauvegarde et cliquez sur **sauvegarder maintenant** bouton bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="f77b8-143">Cela crée un travail de sauvegarde sur l’ordinateur virtuel de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="f77b8-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="f77b8-144">Durée de rétention du point de récupération créé via ce travail sera identique à celui spécifié dans la stratégie hello associé avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Création du travail de sauvegarde](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="f77b8-146">stratégie de hello tooview associé à un ordinateur virtuel, exploration vers le bas dans la machine virtuelle dans hello **éléments protégés** page et l’onglet de stratégie toobackup accédez.</span><span class="sxs-lookup"><span data-stu-id="f77b8-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="f77b8-147">Une fois le travail de hello est créé, vous pouvez cliquer sur **afficher le travail** bouton toast hello barre la tâche de hello toosee correspondante dans la page des travaux hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Travail de sauvegarde créé](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="f77b8-149">Après l’achèvement réussi de la tâche de hello, un point de récupération sera créé que vous pouvez utiliser toorestore hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f77b8-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="f77b8-150">Cela permet également d’incrémenter la valeur de la colonne de hello de point de récupération par 1 dans **éléments protégés** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="f77b8-151">Arrêt de la protection des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f77b8-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="f77b8-152">Vous pouvez choisir toostop hello futures sauvegardes d’une machine virtuelle avec hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="f77b8-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="f77b8-153">Conserver les données de sauvegarde associées à la machine virtuelle dans l’archivage de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="f77b8-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="f77b8-154">Supprimer les données de sauvegarde associées à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f77b8-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="f77b8-155">Si vous avez sélectionné des données de sauvegarde tooretain associées avec l’ordinateur virtuel, vous pouvez utiliser hello les données de sauvegarde toorestore hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f77b8-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="f77b8-156">Pour connaître les détails de la tarification de ces machines virtuelles, cliquez [ici](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="f77b8-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="f77b8-157">protection tooStop pour un ordinateur virtuel :</span><span class="sxs-lookup"><span data-stu-id="f77b8-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="f77b8-158">Accédez trop**éléments protégés** page et sélectionnez **machine virtuelle Azure** en tant que type de filtre hello (le cas échéant), puis cliquez sur **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="f77b8-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="f77b8-160">Sélectionnez l’ordinateur virtuel de hello et cliquez sur **arrêter la Protection** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Arrêter la protection](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="f77b8-162">Par défaut, Azure Backup ne supprime pas les données de sauvegarde hello associées avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Confirmation l’arrêt de la protection](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="f77b8-164">Si vous souhaitez que les données de sauvegarde toodelete, sélectionnez la case hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Case à cocher](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="f77b8-166">Sélectionnez la raison de l’arrêt de la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="f77b8-167">Bien que cela soit facultatif, fournir une raison aideront toowork Azure Backup sur les commentaires hello et hiérarchiser les scénarios de client hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="f77b8-168">Cliquez sur **Submit** hello toosubmit de bouton **arrêter la protection** travail.</span><span class="sxs-lookup"><span data-stu-id="f77b8-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="f77b8-169">Cliquez sur **afficher le travail** toosee hello travail hello correspondant dans **travaux** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Arrêter la protection](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="f77b8-171">Si vous n’avez pas sélectionné **supprimer les données de sauvegarde associées** option pendant **arrêter la Protection** Assistant, puis sur Poste de travail terminé, de protection devient trop**Protection arrêtée**.</span><span class="sxs-lookup"><span data-stu-id="f77b8-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="f77b8-172">les données de salutation restent avec Azure Backup jusqu'à ce qu’il est supprimé explicitement.</span><span class="sxs-lookup"><span data-stu-id="f77b8-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="f77b8-173">Vous pouvez toujours supprimer les données de salutation en sélectionnant la machine virtuelle de hello Bonjour **éléments protégés** page, en cliquant sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f77b8-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Protection arrêtée](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="f77b8-175">Si vous avez sélectionné hello **supprimer les données de sauvegarde associées** option, hello machine virtuelle ne seront pas partie de hello **éléments protégés** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="f77b8-176">Application d’une nouvelle protection à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f77b8-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="f77b8-177">Si vous n’avez pas sélectionné de hello **les données de sauvegarde associer Delete** option dans **arrêter la Protection**, vous pouvez protéger de nouveau hello virtual machine en suivant toobacking similaire de hello suit les inscrit virtuel machines.</span><span class="sxs-lookup"><span data-stu-id="f77b8-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="f77b8-178">Une fois protégé, cet ordinateur virtuel, les données de sauvegarde conservées toostop préalable la protection est et points de récupération créé après la protéger de nouveau.</span><span class="sxs-lookup"><span data-stu-id="f77b8-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="f77b8-179">Protégez de nouveau après l’état de protection de l’ordinateur virtuel de hello est modifiée trop**protégé** s’il existe des points de récupération antérieurs trop**arrêter la Protection**.</span><span class="sxs-lookup"><span data-stu-id="f77b8-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Machine virtuelle à nouveau protégée](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="f77b8-181">Lors de la nouvelle protection hello virtual machine, vous pouvez choisir une autre stratégie que stratégie hello avec laquelle machine virtuelle a été initialement protégée.</span><span class="sxs-lookup"><span data-stu-id="f77b8-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="f77b8-182">Annulation de l’inscription des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f77b8-182">Unregister virtual machines</span></span>
<span data-ttu-id="f77b8-183">Si vous souhaitez virtuels tooremove hello hello coffre de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="f77b8-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="f77b8-184">Cliquez sur hello **UNREGISTER** bouton bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Désactiver la protection](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="f77b8-186">Une notification toast s’affiche en bas hello d’écran hello demander la confirmation.</span><span class="sxs-lookup"><span data-stu-id="f77b8-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="f77b8-187">Cliquez sur **Oui** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f77b8-187">Click **YES** toocontinue.</span></span>

    ![Désactiver la protection](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="f77b8-189">Suppression des données de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f77b8-189">Delete Backup data</span></span>
<span data-ttu-id="f77b8-190">Vous pouvez supprimer les données de sauvegarde hello associées à un ordinateur virtuel, soit :</span><span class="sxs-lookup"><span data-stu-id="f77b8-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="f77b8-191">Au cours du travail Arrêter la protection</span><span class="sxs-lookup"><span data-stu-id="f77b8-191">During Stop Protection Job</span></span>
* <span data-ttu-id="f77b8-192">Après la fin du travail d’arrêt de la protection sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f77b8-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="f77b8-193">toodelete les données de sauvegarde sur un ordinateur virtuel, qui se trouve dans hello *Protection arrêtée* état valider la réussite d’une **arrêter la sauvegarde** travail :</span><span class="sxs-lookup"><span data-stu-id="f77b8-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="f77b8-194">Accédez toohello **éléments protégés** page et sélectionnez **Machine virtuelle Azure** en tant que *type* et cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="f77b8-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="f77b8-196">Sélectionnez la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-196">Select hello virtual machine.</span></span> <span data-ttu-id="f77b8-197">machine virtuelle de Hello sera dans **Protection arrêtée** état.</span><span class="sxs-lookup"><span data-stu-id="f77b8-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Protection arrêtée](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="f77b8-199">Cliquez sur hello **supprimer** bouton bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Supprimer la sauvegarde](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="f77b8-201">Bonjour **supprimer les données de sauvegarde** Assistant, sélectionnez un motif pour la suppression des données de sauvegarde (hautement recommandées), cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="f77b8-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Supprimer les données de sauvegarde](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="f77b8-203">Cela va créer un travail toodelete sauvegarde de données de la machine virtuelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="f77b8-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="f77b8-204">Cliquez sur **afficher le travail** toosee la tâche correspondante dans la page tâches.</span><span class="sxs-lookup"><span data-stu-id="f77b8-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Suppression de données réussie](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="f77b8-206">Une fois le travail de hello est terminé, hello entrée de machine virtuelle de toohello correspondante sera retiré **éléments protégés** page.</span><span class="sxs-lookup"><span data-stu-id="f77b8-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="f77b8-207">tableau de bord</span><span class="sxs-lookup"><span data-stu-id="f77b8-207">Dashboard</span></span>
<span data-ttu-id="f77b8-208">Sur hello **tableau de bord** page, vous pouvez consulter des informations sur les machines virtuelles, de leur stockage et les travaux qui s’y rapportent dans hello des dernières 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f77b8-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="f77b8-209">Vous pouvez afficher l’état de la sauvegarde et les éventuelles erreurs de sauvegarde associées.</span><span class="sxs-lookup"><span data-stu-id="f77b8-209">You can view backup status and any associated backup errors.</span></span>

![tableau de bord](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="f77b8-211">Les valeurs dans le tableau de bord hello sont actualisés toutes les 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f77b8-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="f77b8-212">Audit des opérations</span><span class="sxs-lookup"><span data-stu-id="f77b8-212">Auditing Operations</span></span>
<span data-ttu-id="f77b8-213">Azure backup offre la révision de hello « journaux des opérations « des opérations de sauvegarde déclenchées par le client hello rend facile toosee exactement les opérations de gestion ont été effectuées sur le coffre de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="f77b8-214">Journaux des opérations d’audit prise en charge des opérations de sauvegarde hello et activer excellent post-mortem.</span><span class="sxs-lookup"><span data-stu-id="f77b8-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="f77b8-215">Hello opérations suivantes est consignée dans les journaux des opérations :</span><span class="sxs-lookup"><span data-stu-id="f77b8-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="f77b8-216">S’inscrire</span><span class="sxs-lookup"><span data-stu-id="f77b8-216">Register</span></span>
* <span data-ttu-id="f77b8-217">Unregister </span><span class="sxs-lookup"><span data-stu-id="f77b8-217">Unregister</span></span>
* <span data-ttu-id="f77b8-218">Configurer la protection</span><span class="sxs-lookup"><span data-stu-id="f77b8-218">Configure protection</span></span>
* <span data-ttu-id="f77b8-219">Sauvegarde (planifiée et à la demande via BackupNow)</span><span class="sxs-lookup"><span data-stu-id="f77b8-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="f77b8-220">Restauration</span><span class="sxs-lookup"><span data-stu-id="f77b8-220">Restore</span></span>
* <span data-ttu-id="f77b8-221">Arrêter la protection</span><span class="sxs-lookup"><span data-stu-id="f77b8-221">Stop protection</span></span>
* <span data-ttu-id="f77b8-222">Supprimer les données de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f77b8-222">Delete backup data</span></span>
* <span data-ttu-id="f77b8-223">Add policy</span><span class="sxs-lookup"><span data-stu-id="f77b8-223">Add policy</span></span>
* <span data-ttu-id="f77b8-224">Supprimer la stratégie</span><span class="sxs-lookup"><span data-stu-id="f77b8-224">Delete policy</span></span>
* <span data-ttu-id="f77b8-225">Mettre à jour la stratégie</span><span class="sxs-lookup"><span data-stu-id="f77b8-225">Update policy</span></span>
* <span data-ttu-id="f77b8-226">Annuler le travail</span><span class="sxs-lookup"><span data-stu-id="f77b8-226">Cancel job</span></span>

<span data-ttu-id="f77b8-227">tooview opération enregistre le coffre de sauvegarde tooa correspondante :</span><span class="sxs-lookup"><span data-stu-id="f77b8-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="f77b8-228">Accédez trop**des services de gestion** dans le portail Azure, puis cliquez sur hello **journaux des opérations** onglet.</span><span class="sxs-lookup"><span data-stu-id="f77b8-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Journaux des opérations](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="f77b8-230">Dans les filtres de hello, sélectionnez **sauvegarde** en tant que *Type* et spécifiez le nom de coffre de sauvegarde hello dans *nom du service* , puis cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="f77b8-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtre des journaux des opérations](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="f77b8-232">Dans les journaux des opérations de hello, sélectionnez n’importe quelle opération, puis cliquez sur **détails** toosee détails opération tooan correspondante.</span><span class="sxs-lookup"><span data-stu-id="f77b8-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Détails de l’extraction des journaux d’opérations](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="f77b8-234">Hello **Assistant de détails** contient des informations sur l’opération de hello déclenchée, tâche, Id de ressource sur lequel cette opération est déclenchée et l’heure de début de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Détails de l'opération](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="f77b8-236">Notifications d’alerte</span><span class="sxs-lookup"><span data-stu-id="f77b8-236">Alert notifications</span></span>
<span data-ttu-id="f77b8-237">Vous pouvez obtenir des notifications d’alerte personnalisées pour les travaux de hello dans le portail.</span><span class="sxs-lookup"><span data-stu-id="f77b8-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="f77b8-238">Pour cela, vous devez définir des règles d’alerte basées sur PowerShell sur les événements de journaux des opérations.</span><span class="sxs-lookup"><span data-stu-id="f77b8-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="f77b8-239">Nous vous recommandons d’utiliser *PowerShell version 1.3.0 ou version ultérieure*.</span><span class="sxs-lookup"><span data-stu-id="f77b8-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="f77b8-240">toodefine un tooalert de notification personnalisée pour les échecs de sauvegarde, un exemple de commande doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="f77b8-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="f77b8-241">**ResourceId**: vous pouvez obtenir cela à partir de la fenêtre contextuelle Journaux des opérations, comme indiqué dans la section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f77b8-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="f77b8-242">ResourceUri dans la fenêtre contextuelle de détails d’une opération est hello ResourceId toobe est fournie pour cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f77b8-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="f77b8-243">**NomOpération**: il s’agit du format de hello « Microsoft.Backup/backupvault/<EventName>» où EventName est inscrire, désinscrire, ConfigureProtection, sauvegarde, restauration, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="f77b8-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="f77b8-244">**État**: les valeurs prises en charge sont Démarré, Réussi et Échec.</span><span class="sxs-lookup"><span data-stu-id="f77b8-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="f77b8-245">**Le groupe de ressources**: le groupe de ressources de ressource hello sur lequel l’opération est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="f77b8-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="f77b8-246">Vous pouvez l’obtenir à partir de la valeur ResourceId.</span><span class="sxs-lookup"><span data-stu-id="f77b8-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="f77b8-247">Valeur comprise entre les champs */resourceGroups/* et */providers/* dans ResourceId valeur est hello pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f77b8-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="f77b8-248">**Nom**: nom de la règle d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="f77b8-249">**CustomEmail**: spécifiez toowhich d’adresse e-mail personnalisé hello souhaité toosend notification d’alerte</span><span class="sxs-lookup"><span data-stu-id="f77b8-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="f77b8-250">**SendToServiceOwners**: cette option envoie la notification d’alerte tooall administrateurs et coadministrateurs d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="f77b8-251">Elle peut être utilisée dans l’applet de commande **New-AzureRmAlertRuleEmail** .</span><span class="sxs-lookup"><span data-stu-id="f77b8-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="f77b8-252">Limitations sur les alertes</span><span class="sxs-lookup"><span data-stu-id="f77b8-252">Limitations on Alerts</span></span>
<span data-ttu-id="f77b8-253">Alertes basées sur les événements sont soumis toohello limites suivantes :</span><span class="sxs-lookup"><span data-stu-id="f77b8-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="f77b8-254">Des alertes sont déclenchées sur tous les ordinateurs virtuels dans le coffre de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="f77b8-255">Vous ne pouvez pas personnaliser tooget des alertes pour un ensemble spécifique d’ordinateurs virtuels dans un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="f77b8-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="f77b8-256">Cette fonctionnalité est en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="f77b8-256">This feature is in Preview.</span></span> [<span data-ttu-id="f77b8-257">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="f77b8-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="f77b8-258">Vous recevez des alertes de « alerts-noreply@mail.windowsazure.com ».</span><span class="sxs-lookup"><span data-stu-id="f77b8-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="f77b8-259">Actuellement, vous ne pouvez pas modifier expéditeur du courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="f77b8-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f77b8-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f77b8-260">Next steps</span></span>
* [<span data-ttu-id="f77b8-261">Restauration de machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="f77b8-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
