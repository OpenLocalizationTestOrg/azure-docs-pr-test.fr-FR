---
title: aaaBack des machines virtuelles Azure | Documents Microsoft
description: "Permet de découvrir, d’enregistrer et de sauvegarder des machines virtuelles tooa coffre recovery services."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegarde de machine virtuelle ; sauvegarder la machine virtuelle ; sauvegarde et récupération d’urgence ; sauvegarde de machine virtuelle arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="bfb76-104">Sauvegarder les machines virtuelles de coffre de Services de récupération tooa</span><span class="sxs-lookup"><span data-stu-id="bfb76-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfb76-105">Sauvegarder le coffre de Services tooRecovery de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bfb76-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="bfb76-106">Sauvegarder des machines virtuelles tooBackup coffre</span><span class="sxs-lookup"><span data-stu-id="bfb76-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="bfb76-107">Cet article décrit en détail comment tooback des machines virtuelles de Azure (déployées par le Gestionnaire de ressources et déployés classique) tooa Services de récupération de coffre.</span><span class="sxs-lookup"><span data-stu-id="bfb76-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="bfb76-108">La plupart du travail hello pour la sauvegarde d’ordinateurs virtuels est préparation de hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="bfb76-109">Avant de pouvoir sauvegarder ou protéger un ordinateur virtuel, vous devez effectuer hello [conditions préalables](backup-azure-arm-vms-prepare.md) tooprepare votre environnement de protection de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bfb76-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="bfb76-110">Une fois que vous avez terminé la configuration requise de hello, vous pouvez lancer hello opération de sauvegarde tootake des instantanés de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bfb76-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="bfb76-111">Pour plus d’informations, consultez les articles hello sur [planification de votre infrastructure de sauvegarde de machine virtuelle dans Azure](backup-azure-vms-introduction.md) et [machines virtuelles](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="bfb76-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="bfb76-112">Déclenchement hello tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="bfb76-112">Triggering hello backup job</span></span>
<span data-ttu-id="bfb76-113">stratégie de sauvegarde Hello associé hello que coffre des Services de récupération définit la fréquence et à quel moment la sauvegarde hello s’exécute.</span><span class="sxs-lookup"><span data-stu-id="bfb76-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="bfb76-114">Par défaut, hello première planifiée est hello initiale sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="bfb76-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="bfb76-115">Jusqu'à ce que la sauvegarde initiale de hello se produit, hello état de la dernière sauvegarde sur hello **les travaux de sauvegarde** panneau affiche sous la forme **avertissement (sauvegarde initiale en attente)**.</span><span class="sxs-lookup"><span data-stu-id="bfb76-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Sauvegarde en attente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="bfb76-117">Sauf si votre sauvegarde initiale est due toobegin bientôt, il est recommandé d’exécuter **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="bfb76-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="bfb76-118">Hello procédure suivante commence à partir du tableau de bord coffre hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="bfb76-119">Cette procédure remplit pour l’exécution du travail de sauvegarde initiale hello après avoir terminé toutes les conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="bfb76-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="bfb76-120">Si la tâche de sauvegarde initiale hello a déjà été exécutée, cette procédure n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="bfb76-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="bfb76-121">Hello stratégie de sauvegarde associée détermine prochaine tâche de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="bfb76-122">toorun hello initiale travail de sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="bfb76-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="bfb76-123">Tableau de bord du coffre hello, cliquez sur nombre hello sous **des éléments de sauvegarde**, ou cliquez sur hello **des éléments de sauvegarde** vignette.</span><span class="sxs-lookup"><span data-stu-id="bfb76-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="bfb76-124">
  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="bfb76-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="bfb76-125">Hello **des éléments de sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bfb76-125">hello **Backup Items** blade opens.</span></span>

  ![Éléments de sauvegarde](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="bfb76-127">Sur hello **des éléments de sauvegarde** les lames, les éléments select hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="bfb76-129">Hello **des éléments de sauvegarde** liste s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bfb76-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Travail de sauvegarde déclenché](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="bfb76-131">Sur hello **des éléments de sauvegarde** , cliquez sur le bouton de sélection hello **...**  menu de contexte tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="bfb76-133">menu contextuel de Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="bfb76-133">hello Context menu appears.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="bfb76-135">Dans le menu contextuel de hello, cliquez sur **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="bfb76-135">On hello Context menu, click **Backup now**.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="bfb76-137">panneau Hello sauvegarder maintenant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bfb76-137">hello Backup Now blade opens.</span></span>

  ![Affiche le panneau hello sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="bfb76-139">Dans Panneau de sauvegarder maintenant du hello, cliquez l’icône de calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="bfb76-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![définir hello dernier jour hello sauvegarder maintenant point de récupération est conservé.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="bfb76-141">Notifications de déploiement vous permettent de connaître la tâche de sauvegarde hello a été déclenchée, et que vous pouvez surveiller la progression hello de hello de page de travaux de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="bfb76-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="bfb76-142">Selon la taille de hello de votre machine virtuelle, la création de sauvegarde initiale de hello peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="bfb76-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="bfb76-143">état de hello tooview ou le suivi de la sauvegarde initiale hello, tableau de bord du coffre hello, sur hello **les travaux de sauvegarde** cliquez sur la vignette **en cours d’exécution**.</span><span class="sxs-lookup"><span data-stu-id="bfb76-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="bfb76-145">Panneau de travaux de sauvegarde Hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bfb76-145">hello Backup Jobs blade opens.</span></span>

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="bfb76-147">Bonjour **travaux de sauvegarde** panneau, vous pouvez voir État hello de tous les travaux.</span><span class="sxs-lookup"><span data-stu-id="bfb76-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="bfb76-148">Vérifiez si le travail de sauvegarde hello pour votre machine virtuelle est toujours en cours ou s’il s’est terminé.</span><span class="sxs-lookup"><span data-stu-id="bfb76-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="bfb76-149">Une opération de sauvegarde est terminée, le statut de hello est *terminé*.</span><span class="sxs-lookup"><span data-stu-id="bfb76-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bfb76-150">Dans le cadre de l’opération de sauvegarde hello, hello Azure Backup service émet une extension de sauvegarde commande toohello dans chaque tooflush de machine virtuelle, toutes les écritures et prendre un instantané cohérent.</span><span class="sxs-lookup"><span data-stu-id="bfb76-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="bfb76-151">Résolution des erreurs</span><span class="sxs-lookup"><span data-stu-id="bfb76-151">Troubleshooting errors</span></span>
<span data-ttu-id="bfb76-152">Si vous rencontrez des problèmes pendant la sauvegarde de votre machine virtuelle, consultez hello [article de résolution des problèmes de machine virtuelle](backup-azure-vms-troubleshoot.md) de l’aide.</span><span class="sxs-lookup"><span data-stu-id="bfb76-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfb76-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bfb76-153">Next steps</span></span>
<span data-ttu-id="bfb76-154">Maintenant que vous avez protégé votre machine virtuelle, consultez hello suivant toolearn des articles sur les tâches de gestion de machine virtuelle et comment toorestore machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="bfb76-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="bfb76-155">Gestion et surveillance de vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bfb76-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="bfb76-156">Restauration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="bfb76-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
