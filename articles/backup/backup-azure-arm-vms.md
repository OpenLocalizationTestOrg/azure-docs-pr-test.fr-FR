---
title: Sauvegarde de machines virtuelles Azure | Microsoft Docs
description: "Détectez, inscrivez et sauvegardez des machines virtuelles Azure dans un coffre Recovery Services."
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
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="a9638-104">Sauvegarder des machines virtuelles Azure dans un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a9638-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9638-105">Back up VMs to Recovery Services vault</span><span class="sxs-lookup"><span data-stu-id="a9638-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="a9638-106">Back up VMs to Backup vault</span><span class="sxs-lookup"><span data-stu-id="a9638-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="a9638-107">Cet article décrit la procédure de sauvegarde des machines virtuelles Azure (déployées à l’aide du modèle Resource Manager ou du modèle Classic) dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="a9638-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="a9638-108">La plupart du travail requis pour la sauvegarde des machines virtuelles repose sur la préparation.</span><span class="sxs-lookup"><span data-stu-id="a9638-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="a9638-109">Avant de sauvegarder ou de protéger une machine virtuelle, vous devez remplir les [conditions préalables](backup-azure-arm-vms-prepare.md) pour préparer votre environnement à la protection de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a9638-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="a9638-110">Une fois que vous avez rempli les conditions préalables, vous pouvez lancer l’opération de sauvegarde pour prendre des instantanés de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9638-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="a9638-111">Pour plus d’informations, consultez les articles sur la [planification de votre infrastructure de sauvegarde des machines virtuelles dans Azure](backup-azure-vms-introduction.md) et les [machines virtuelles Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="a9638-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="a9638-112">Déclenchement du travail de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="a9638-112">Triggering the backup job</span></span>
<span data-ttu-id="a9638-113">La stratégie de sauvegarde associée au coffre Recovery Services définit la fréquence et à quel moment l’opération de sauvegarde s’exécute.</span><span class="sxs-lookup"><span data-stu-id="a9638-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="a9638-114">Par défaut, la première sauvegarde planifiée est la sauvegarde initiale.</span><span class="sxs-lookup"><span data-stu-id="a9638-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="a9638-115">Jusqu’à celle-ci, l’état de la dernière sauvegarde dans le panneau **Travaux de sauvegarde** est défini sur **Avertissement (sauvegarde initiale en attente)**.</span><span class="sxs-lookup"><span data-stu-id="a9638-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Sauvegarde en attente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="a9638-117">À moins que votre sauvegarde initiale ne soit prévue prochainement, il est recommandé de sélectionner l’option **Sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="a9638-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="a9638-118">La procédure suivante commence à partir du tableau de bord du coffre.</span><span class="sxs-lookup"><span data-stu-id="a9638-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="a9638-119">Cette procédure est utilisée pour l’exécution du travail de sauvegarde initial une fois les conditions préalables remplies.</span><span class="sxs-lookup"><span data-stu-id="a9638-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="a9638-120">Si le travail de sauvegarde initial a déjà été exécuté, cette procédure n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="a9638-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="a9638-121">La stratégie de sauvegarde associée détermine le prochain travail de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a9638-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="a9638-122">Pour exécuter le travail de sauvegarde initial :</span><span class="sxs-lookup"><span data-stu-id="a9638-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="a9638-123">Dans le tableau de bord du coffre, cliquez sur le numéro sous **Éléments de sauvegarde** ou cliquez sur la vignette **Éléments de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="a9638-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="a9638-124">
  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="a9638-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="a9638-125">Le panneau **Éléments de sauvegarde** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a9638-125">The **Backup Items** blade opens.</span></span>

  ![Éléments de sauvegarde](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="a9638-127">Dans le panneau **Éléments de sauvegarde**, sélectionnez l’élément.</span><span class="sxs-lookup"><span data-stu-id="a9638-127">On the **Backup Items** blade, select the item.</span></span>

  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="a9638-129">La liste **Éléments de sauvegarde** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a9638-129">The **Backup Items** list opens.</span></span> <br/>

  ![Travail de sauvegarde déclenché](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="a9638-131">Dans la liste **Éléments de sauvegarde**, cliquez sur le bouton de sélection **...** pour ouvrir le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="a9638-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="a9638-133">Le menu contextuel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a9638-133">The Context menu appears.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="a9638-135">Dans le menu contextuel, cliquez sur **Sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="a9638-135">On the Context menu, click **Backup now**.</span></span>

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="a9638-137">Le panneau Sauvegarder maintenant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a9638-137">The Backup Now blade opens.</span></span>

  ![Affichage du panneau Sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="a9638-139">Dans le panneau Sauvegarder maintenant, cliquez sur l’icône de calendrier. Utilisez le contrôle de calendrier pour sélectionner le dernier jour de conservation de ce point de récupération, puis cliquez sur **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="a9638-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![Définition du dernier jour de conservation du point de récupération dans le panneau Sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="a9638-141">Les notifications de déploiement vous informent que la sauvegarde a été déclenchée et que vous pouvez surveiller la progression du travail sur la page Travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a9638-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="a9638-142">Selon la taille de votre machine virtuelle, la création de la sauvegarde initiale peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="a9638-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="a9638-143">Pour afficher ou suivre l’état de la sauvegarde initiale, dans le tableau de bord du coffre, au niveau de la vignette **Travaux de sauvegarde**, cliquez sur **En cours**.</span><span class="sxs-lookup"><span data-stu-id="a9638-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="a9638-145">Le panneau Travaux de sauvegarde s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="a9638-145">The Backup Jobs blade opens.</span></span>

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="a9638-147">Le panneau **Travaux de sauvegarde** indique l’état de tous les travaux.</span><span class="sxs-lookup"><span data-stu-id="a9638-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="a9638-148">Vérifiez si le travail de sauvegarde de votre machine virtuelle est en cours d’exécution ou s’il est terminé.</span><span class="sxs-lookup"><span data-stu-id="a9638-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="a9638-149">Lorsqu’un travail de sauvegarde est achevé, il présente l’état *Terminé*.</span><span class="sxs-lookup"><span data-stu-id="a9638-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a9638-150">Dans le cadre de l’opération de sauvegarde, le service Azure Backup émet une commande vers l’extension de sauvegarde de chaque machine virtuelle pour vider toutes les écritures et prendre un instantané cohérent.</span><span class="sxs-lookup"><span data-stu-id="a9638-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="a9638-151">Résolution des erreurs</span><span class="sxs-lookup"><span data-stu-id="a9638-151">Troubleshooting errors</span></span>
<span data-ttu-id="a9638-152">Si vous rencontrez des problèmes pendant la sauvegarde de votre machine virtuelle, consultez [l’article sur le dépannage des machines virtuelles](backup-azure-vms-troubleshoot.md) pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="a9638-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9638-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9638-153">Next steps</span></span>
<span data-ttu-id="a9638-154">Vous avez protégé votre machine virtuelle. Vous pouvez maintenant consulter les articles suivants pour en savoir plus sur les tâches de gestion de machine virtuelle et la restauration des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a9638-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="a9638-155">Gestion et surveillance de vos machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a9638-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="a9638-156">Restauration des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a9638-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
