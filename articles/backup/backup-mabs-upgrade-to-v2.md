---
title: "Installer le serveur de sauvegarde Azure v2 | Microsoft Docs"
description: "Le serveur de sauvegarde Azure v2 offre des capacités de sauvegarde améliorées pour protéger les machines virtuelles, les fichiers et dossiers, les charges de travail, et plus encore. Découvrez comment installer le serveur de sauvegarde Azure v2 ou effectuer la mise à niveau vers ce dernier."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 1bbb16afef7940933b4c3ae23873f212770137e0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="d41d5-104">Installer le serveur de sauvegarde Azure v2</span><span class="sxs-lookup"><span data-stu-id="d41d5-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="d41d5-105">Le serveur de sauvegarde Azure contribue à protéger vos machines virtuelles, vos charges de travail, vos fichiers et dossiers, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="d41d5-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="d41d5-106">Reposant sur le serveur de sauvegarde v1, le serveur de sauvegarde Azure v2 offre des fonctionnalités qui ne sont pas disponibles dans la première version.</span><span class="sxs-lookup"><span data-stu-id="d41d5-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="d41d5-107">Pour connaître les différences entre les versions v1 et v2, consultez [Matrice de protection du serveur de sauvegarde Azure](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="d41d5-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="d41d5-108">Les fonctionnalités supplémentaires du serveur de sauvegarde v2 constituent une mise à niveau du serveur de sauvegarde v1.</span><span class="sxs-lookup"><span data-stu-id="d41d5-108">The additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="d41d5-109">Cependant, le serveur de sauvegarde v1 n’est pas requis pour installer le serveur de sauvegarde v2.</span><span class="sxs-lookup"><span data-stu-id="d41d5-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="d41d5-110">Si vous souhaitez effectuer la mise à niveau du serveur de sauvegarde v1 vers le serveur de sauvegarde v2, installez le serveur de sauvegarde v2 sur le serveur de protection du serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="d41d5-110">If you want to upgrade from Backup Server v1 to Backup Server v2, install Backup Server v2 on the Backup Server protection server.</span></span> <span data-ttu-id="d41d5-111">Vos paramètres de serveur de sauvegarde existants seront conservés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="d41d5-112">Vous pouvez installer le serveur de sauvegarde v2 sur Windows Server 2012 R2 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d41d5-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="d41d5-113">Pour tirer parti des nouvelles fonctionnalités telles que System Center 2016 Data Protection Manager Modern Backup Storage, vous devez installer le serveur de sauvegarde v2 sur Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d41d5-113">To take advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="d41d5-114">Avant d’installer le serveur de sauvegarde v2 ou d’effectuer la mise à niveau vers ce dernier, prenez connaissance des [conditions préalables à l’installation](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="d41d5-114">Before you upgrade to or install Backup Server v2, read about the [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="d41d5-115">Le serveur de sauvegarde Azure présente la même base de code que System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="d41d5-115">Azure Backup Server has the same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="d41d5-116">Le serveur de sauvegarde v1 équivaut à Data Protection Manager 2012 R2 et le serveur de sauvegarde v2 à Data Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="d41d5-116">Backup Server v1 is equivalent to Data Protection Manager 2012 R2, and Backup Server v2 is equivalent to Data Protection Manager 2016.</span></span> <span data-ttu-id="d41d5-117">Cet article fait parfois référence à la documentation de Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="d41d5-117">This article occasionally references the Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-to-v2"></a><span data-ttu-id="d41d5-118">Mettre à niveau le serveur de sauvegarde vers la version 2</span><span class="sxs-lookup"><span data-stu-id="d41d5-118">Upgrade Backup Server to v2</span></span>
<span data-ttu-id="d41d5-119">Pour mettre à niveau le serveur de sauvegarde v1 vers le serveur de sauvegarde v2, assurez-vous que votre installation présente les mises à jour requises :</span><span class="sxs-lookup"><span data-stu-id="d41d5-119">To upgrade from Backup Server v1 to Backup Server v2, make sure your installation has the required updates:</span></span>

- <span data-ttu-id="d41d5-120">[Mettez à jour les agents de protection](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) sur les serveurs protégés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-120">[Update the protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on the protected servers.</span></span>
- <span data-ttu-id="d41d5-121">Mettez à niveau Windows Server 2012 R2 vers Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d41d5-121">Upgrade Windows Server 2012 R2 to Windows Server 2016.</span></span>
- <span data-ttu-id="d41d5-122">Mettez à niveau l’outil d’administration à distance du serveur de sauvegarde Azure sur tous les serveurs de production.</span><span class="sxs-lookup"><span data-stu-id="d41d5-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="d41d5-123">Assurez-vous que les sauvegardes sont définies pour continuer sans redémarrer votre serveur de production.</span><span class="sxs-lookup"><span data-stu-id="d41d5-123">Ensure that backups are set to continue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="d41d5-124">Procédure de mise à niveau vers le serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="d41d5-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="d41d5-125">Dans le Centre de téléchargement, [téléchargez le programme d’installation de la mise à niveau](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="d41d5-125">In the Download Center, [download the upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="d41d5-126">Après avoir extrait l’Assistant d’installation, assurez-vous que la case à cocher **Exécuter setup.exe** est activée, puis sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-126">After you extract the setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Programme d’installation - Exécuter l’installation](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="d41d5-128">Dans l’Assistant d’installation du serveur de sauvegarde Microsoft Azure, sous **Installer**, sélectionnez **Serveur Sauvegarde Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-128">In the Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Programme d’installation - Sélectionner l’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="d41d5-130">Dans la page **Bienvenue**, lisez les avertissements, puis sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-130">On the **Welcome** page, review the warnings, and then select **Next**.</span></span>

  ![Programme d’installation - Page Bienvenue](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="d41d5-132">L’Assistant d’installation effectue des vérifications préalables pour s’assurer que votre environnement peut être mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="d41d5-132">The setup wizard performs prerequisite checks to make sure your environment can upgrade.</span></span> <span data-ttu-id="d41d5-133">Dans la page **Vérifications des conditions requises**, sélectionnez **Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-133">On the **Prerequisite Checks** page, select **Check**.</span></span>

  ![Programme d’installation - Page Vérifications des conditions requises](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="d41d5-135">Votre environnement doit passer les vérifications des conditions requises avec succès.</span><span class="sxs-lookup"><span data-stu-id="d41d5-135">Your environment must pass the prerequisite checks.</span></span> <span data-ttu-id="d41d5-136">Si votre environnement échoue à ces vérifications, notez les problèmes et corrigez-les.</span><span class="sxs-lookup"><span data-stu-id="d41d5-136">If your environment doesn't pass the checks, note the issues and fix them.</span></span> <span data-ttu-id="d41d5-137">Ensuite, sélectionnez **Revérifier**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-137">Then, select **Check Again**.</span></span> <span data-ttu-id="d41d5-138">Une fois les vérifications des conditions requises passées avec succès, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-138">After you pass the prerequisite checks, select **Next**.</span></span>

  ![Programme d’installation - Bouton Revérifier](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="d41d5-140">Dans la page **Paramètres SQL**, sélectionnez l’option appropriée pour votre installation de SQL, puis choisissez **Vérifier et installer**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-140">On the **SQL Settings** page, select the relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Programme d’installation - Page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="d41d5-142">Les vérifications peuvent prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d41d5-142">The checks might take a few minutes.</span></span> <span data-ttu-id="d41d5-143">Une fois les vérifications terminées, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-143">When the checks are finished, select **Next**.</span></span>

  ![Programme d’installation - Bouton Vérifier et installer de la page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="d41d5-145">Dans la page **Paramètres d’installation**, apportez les modifications requises à l’emplacement d’installation du serveur de sauvegarde ou à l’emplacement de la zone temporaire.</span><span class="sxs-lookup"><span data-stu-id="d41d5-145">On the **Installation Settings** page, make any changes to the location where Backup Server is installed, or to the Scratch Location.</span></span> <span data-ttu-id="d41d5-146">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-146">Select **Next**.</span></span>

  ![Programme d’installation - Page Paramètres d’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="d41d5-148">Pour terminer l’Assistant d’installation, sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-148">To finish the setup wizard, select **Finish**.</span></span>

  ![Programme d’installation - Terminer](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="d41d5-150">Ajouter un stockage pour Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="d41d5-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="d41d5-151">Pour améliorer l’efficacité du stockage de sauvegarde, la prise en charge des volumes a été ajoutée à la version 2 du serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="d41d5-151">To improve backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="d41d5-152">Comme le serveur de sauvegarde v1, le serveur de sauvegarde v2 prend en charge les disques.</span><span class="sxs-lookup"><span data-stu-id="d41d5-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="d41d5-153">Ajouter des volumes et des disques</span><span class="sxs-lookup"><span data-stu-id="d41d5-153">Add volumes and disks</span></span>
<span data-ttu-id="d41d5-154">Si vous exécutez le serveur de sauvegarde v2 sur Windows Server 2016, vous pouvez utiliser des volumes pour stocker les données de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="d41d5-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes to store backup data.</span></span> <span data-ttu-id="d41d5-155">Les volumes assurent des économies en stockage et des sauvegardes plus rapides.</span><span class="sxs-lookup"><span data-stu-id="d41d5-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="d41d5-156">Comme les volumes sont une nouveauté du serveur de sauvegarde, vous devez les ajouter.</span><span class="sxs-lookup"><span data-stu-id="d41d5-156">Because volumes are new to Backup Server, you must add them.</span></span> 

<span data-ttu-id="d41d5-157">Lorsque vous ajoutez un volume au serveur de sauvegarde, vous pouvez lui donner un nom convivial.</span><span class="sxs-lookup"><span data-stu-id="d41d5-157">When you add a volume to Backup Server, you can give the volume a friendly name.</span></span> <span data-ttu-id="d41d5-158">Cliquez sur la colonne **Nom convivial** du volume auquel vous souhaitez donner un nom.</span><span class="sxs-lookup"><span data-stu-id="d41d5-158">Click the **Friendly Name** column of the volume you want to name.</span></span> <span data-ttu-id="d41d5-159">Si nécessaire, vous pourrez modifier le nom ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d41d5-159">You can change the name later, if necessary.</span></span> <span data-ttu-id="d41d5-160">Vous pouvez également utiliser PowerShell pour ajouter un nom convivial aux volumes ou le modifier.</span><span class="sxs-lookup"><span data-stu-id="d41d5-160">You also can use PowerShell to add or change friendly names for volumes.</span></span>

<span data-ttu-id="d41d5-161">Pour ajouter un volume dans la console Administrateur :</span><span class="sxs-lookup"><span data-stu-id="d41d5-161">To add a volume in the Administrator Console:</span></span>

1. <span data-ttu-id="d41d5-162">Dans la console Administrateur du serveur de sauvegarde Azure, sélectionnez **Gestion** > **Stockage sur disque** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-162">In the Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Ouvrir l’Assistant Ajouter un stockage sur disque](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="d41d5-164">L’Assistant Ajouter un stockage sur disque s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d41d5-164">This opens the Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="d41d5-165">Dans la page **Ajouter un stockage sur disque**, dans la zone **Volumes disponibles**, sélectionnez un volume, puis choisissez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-165">On the **Add Disk Storage** page, in the **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="d41d5-166">Dans la zone **Volumes sélectionnés**, entrez un nom convivial pour le volume, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-166">In the **Selected volumes** box, enter a friendly name for the volume, and then select **OK**.</span></span>

      ![Assistant Ajouter un stockage sur disque - Ajouter un volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="d41d5-168">Si vous souhaitez ajouter un disque, ce disque doit appartenir à un groupe de protection présentant un stockage existant.</span><span class="sxs-lookup"><span data-stu-id="d41d5-168">If you want to add a disk, the disk must belong to a protection group that has legacy storage.</span></span> <span data-ttu-id="d41d5-169">Ces disques peuvent uniquement être utilisés pour ces groupes de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="d41d5-170">Si aucune source du serveur de sauvegarde ne présente de protection existante, le disque n’est pas répertorié.</span><span class="sxs-lookup"><span data-stu-id="d41d5-170">If Backup Server doesn't have sources that have legacy protection, the disk isn't listed.</span></span>

  <span data-ttu-id="d41d5-171">Pour plus d’informations sur l’ajout de disques, consultez [Ajout de disques pour augmenter le stockage existant](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="d41d5-171">For more information about adding disks, see [Adding disks to increase legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="d41d5-172">Vous ne pouvez pas donner de nom convivial à un disque.</span><span class="sxs-lookup"><span data-stu-id="d41d5-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-to-volumes"></a><span data-ttu-id="d41d5-173">Assigner des charges de travail à des volumes</span><span class="sxs-lookup"><span data-stu-id="d41d5-173">Assign workloads to volumes</span></span>

<span data-ttu-id="d41d5-174">Dans le serveur de sauvegarde, vous indiquez quelles charges de travail sont assignées à quels volumes.</span><span class="sxs-lookup"><span data-stu-id="d41d5-174">In Backup Server, you specify which workloads are assigned to which volumes.</span></span> <span data-ttu-id="d41d5-175">Par exemple, vous pouvez définir des volumes coûteux prenant en charge un nombre élevé d’opérations d’entrée/sortie par seconde (IOPS) pour stocker uniquement les charges de travail qui nécessitent des sauvegardes de volumes importants fréquentes.</span><span class="sxs-lookup"><span data-stu-id="d41d5-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="d41d5-176">Un exemple est SQL Server avec les journaux des transactions.</span><span class="sxs-lookup"><span data-stu-id="d41d5-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="d41d5-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="d41d5-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="d41d5-178">Pour mettre à jour les propriétés d’un volume du pool de stockage dans le serveur de sauvegarde, utilisez le cmdlet PowerShell Update-DPMDiskStorage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-178">To update the properties of a volume in the storage pool in Backup Server, use the PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="d41d5-179">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="d41d5-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="d41d5-180">Toutes les modifications apportées à l’aide de PowerShell sont répercutées dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d41d5-180">All changes that you make by using PowerShell are reflected in the UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="d41d5-181">Protéger les sources de données</span><span class="sxs-lookup"><span data-stu-id="d41d5-181">Protect data sources</span></span>
<span data-ttu-id="d41d5-182">Pour commencer à protéger les sources de données, créez un groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-182">To begin protecting data sources, create a protection group.</span></span> <span data-ttu-id="d41d5-183">Les étapes suivantes mettent en évidence les modifications ou les ajouts de l’Assistant Nouveau groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-183">The following steps highlight changes or additions to the New Protection Group wizard.</span></span>

<span data-ttu-id="d41d5-184">Pour créer un groupe de protection :</span><span class="sxs-lookup"><span data-stu-id="d41d5-184">To create a protection group:</span></span>

1. <span data-ttu-id="d41d5-185">Dans la console Administrateur du serveur de sauvegarde, sélectionnez **Protection**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-185">In the Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="d41d5-186">Dans la barre d’outils, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-186">On the tool ribbon, select **New**.</span></span>

    <span data-ttu-id="d41d5-187">L’Assistant Créer un nouveau groupe de protection s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="d41d5-187">This opens the Create New Protection Group wizard.</span></span>

  ![Assistant Création d’un nouveau groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="d41d5-189">Sur la page d’**accueil**, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-189">On the **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="d41d5-190">Dans la page **Sélectionner le type de groupe de protection**, sélectionnez le type de groupe de protection que vous souhaitez créer, puis choisissez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-190">On the **Select Protection Group Type** page, select the type of protection group you want to create, and then select **Next**.</span></span>

  ![Page Sélectionner le type de groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="d41d5-192">Dans la page **Sélectionner les membres du groupe**, dans le volet **Membres disponibles**, les membres présentant des agents de protection sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-192">On the **Select Group Members** page, in the **Available members** pane, the members with protection agents are listed.</span></span> <span data-ttu-id="d41d5-193">Pour cet exemple, sélectionnez les volumes D:\ et E:\ et ajoutez-les au volet **Membres sélectionnés**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-193">For this example, select volume D:\ and E:\ and add them to the **Selected members** pane.</span></span> <span data-ttu-id="d41d5-194">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-194">Select **Next**.</span></span>

  ![Page Sélectionner les membres du groupe](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="d41d5-196">Dans la page **Sélectionner la méthode de protection des données**, entrez le **nom du groupe de protection**, sélectionnez la méthode de protection, puis choisissez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-196">On the **Select Data Protection Method** page, enter a **Protection group name**, select the protection method, and then select **Next**.</span></span> <span data-ttu-id="d41d5-197">Si vous recherchez une protection à court terme, vous devez sélectionner la méthode de protection **Disque**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-197">If you want short-term protection, you must select the **Disk** backup method.</span></span>

  ![Page Sélectionner la méthode de protection des données](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="d41d5-199">Dans la page **Spécifier les objectifs à court terme**, sélectionnez les détails de la **durée de rétention** et de la **fréquence de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-199">On the **Specify Short-Term Goals** page, select the details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="d41d5-200">Ensuite, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-200">Then, select **Next**.</span></span> <span data-ttu-id="d41d5-201">Si vous le souhaitez, vous pouvez modifier les jours et les heures de création des points de récupération en sélectionnant **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-201">Optionally, to change the schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Page Spécifier les objectifs à court terme](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="d41d5-203">Dans la page **Vérifier l’allocation de stockage sur disque**, passez en revue les détails concernant les sources de données sélectionnées, leur taille, l’espace à provisionner et le volume de stockage cible.</span><span class="sxs-lookup"><span data-stu-id="d41d5-203">On the **Review Disk Storage Allocation** page, review details about the data sources you selected, their size, and  values for the space to be provisioned and the target storage volume.</span></span>

  ![Page Vérifier l’allocation de stockage sur disque](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="d41d5-205">Les volumes de stockage sont basés sur l’allocation de volume de charge de travail (définie à l’aide de PowerShell) et le stockage disponible.</span><span class="sxs-lookup"><span data-stu-id="d41d5-205">Storage volumes are based on the workload volume allocation (set by using PowerShell) and the available storage.</span></span> <span data-ttu-id="d41d5-206">Vous pouvez modifier les volumes de stockage en sélectionnant d’autres volumes dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="d41d5-206">You can change the storage volumes by selecting other volumes in the drop-down menu.</span></span> <span data-ttu-id="d41d5-207">Si vous modifiez la valeur de **Stockage cible**, la valeur de **Stockage sur disque disponible** est modifiée dynamiquement pour refléter les valeurs sous **Espace libre** et **Underprovisioned Space** (Espace sous-provisionné).</span><span class="sxs-lookup"><span data-stu-id="d41d5-207">If you change the value for **Target Storage**, the value for **Available disk storage** dynamically changes to reflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="d41d5-208">Si la taille des sources de données augmente comme prévu, la valeur de la colonne **Underprovisioned Space** (Espace sous-provisionné) dans **Stockage sur disque disponible** reflète la quantité de stockage supplémentaire requise.</span><span class="sxs-lookup"><span data-stu-id="d41d5-208">If the data sources grow as planned, the value for the **Underprovisioned Space** column in **Available disk storage** reflects the amount of additional storage that's needed.</span></span> <span data-ttu-id="d41d5-209">Utilisez cette valeur pour la planification de vos besoins en stockage afin de garantir des sauvegardes fluides.</span><span class="sxs-lookup"><span data-stu-id="d41d5-209">Use this value to help plan your storage needs for smooth backups.</span></span> <span data-ttu-id="d41d5-210">Si la valeur est égale à zéro, il n’y aura aucun problème de stockage dans un avenir proche.</span><span class="sxs-lookup"><span data-stu-id="d41d5-210">If the value is zero, there are no potential problems with storage in the foreseeable future.</span></span> <span data-ttu-id="d41d5-211">Si la valeur est différente de zéro, le stockage alloué est insuffisant (d’après votre stratégie de protection et la taille des données de vos membres protégés).</span><span class="sxs-lookup"><span data-stu-id="d41d5-211">If the value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and the data size of your protected members).</span></span>

  ![Stockage sur disque sous-alloué](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="d41d5-213">Pour finir la création de votre groupe de protection, terminez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="d41d5-213">To finish creating your protection group, complete the wizard.</span></span>

## <a name="migrate-legacy-storage-to-modern-backup-storage"></a><span data-ttu-id="d41d5-214">Migrer un stockage existant vers Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="d41d5-214">Migrate legacy storage to Modern Backup Storage</span></span>
<span data-ttu-id="d41d5-215">Après avoir installé le serveur de sauvegarde v2 ou effectué la mise à niveau vers ce dernier et mis à niveau le système d’exploitation vers Windows Server 2016, mettez à jour vos groupes de protection pour qu’ils utilisent Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-215">After you upgrade to or install Backup Server v2 and upgrade the operating system to Windows Server 2016, update your protection groups to use Modern Backup Storage.</span></span> <span data-ttu-id="d41d5-216">Par défaut, les groupes de protection ne sont pas modifiés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="d41d5-217">Ils continuent de fonctionner comme ils ont été initialement configurés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-217">They continue to function as they were initially set up.</span></span> 

<span data-ttu-id="d41d5-218">La mise à jour des groupes de protection pour qu’ils utilisent Modern Backup Storage est facultative.</span><span class="sxs-lookup"><span data-stu-id="d41d5-218">Updating protection groups to use Modern Backup Storage is optional.</span></span> <span data-ttu-id="d41d5-219">Pour mettre à jour le groupe de protection, arrêtez la protection de toutes les sources de données à l’aide de l’option de conservation des données.</span><span class="sxs-lookup"><span data-stu-id="d41d5-219">To update the protection group, stop protection of all data sources by using the retain data option.</span></span> <span data-ttu-id="d41d5-220">Ensuite, ajoutez les sources de données à un nouveau groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-220">Then, add the data sources to a new protection group.</span></span>

1. <span data-ttu-id="d41d5-221">Dans la console Administrateur du serveur de sauvegarde, sélectionnez la fonctionnalité **Protection**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-221">In the Administrator Console, select the **Protection** feature.</span></span> <span data-ttu-id="d41d5-222">Dans la liste **Membre du groupe de Protection**, cliquez sur le membre, puis sélectionnez **Arrêter la protection du membre**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-222">In the **Protection Group Member** list, right-click the member, and then select **Stop protection of member**.</span></span>

  ![Arrêter la protection du membre](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="d41d5-224">Dans la boîte de dialogue **Supprimer du groupe**, vérifiez l’espace disque utilisé et l’espace libre disponible pour le pool de stockage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-224">In the **Remove from Group** dialog box, review the used disk space and the available free space for the storage pool.</span></span> <span data-ttu-id="d41d5-225">La valeur par défaut consiste à conserver les points de récupération sur le disque et à les laisser expirer suivant la stratégie de rétention associée.</span><span class="sxs-lookup"><span data-stu-id="d41d5-225">The default is to leave the recovery points on the disk and allow them to expire per their associated retention policy.</span></span> <span data-ttu-id="d41d5-226">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-226">Click **OK**.</span></span>

  <span data-ttu-id="d41d5-227">Si vous souhaitez restituer immédiatement l’espace disque utilisé pour le pool de stockage libre, sélectionnez la case à cocher **Supprimer le réplica sur le disque** pour supprimer les données de sauvegarde (et les points de récupération) associées à ce membre.</span><span class="sxs-lookup"><span data-stu-id="d41d5-227">If you want to immediately return the used disk space to the free storage pool, select the **Delete replica on disk** check box to delete the backup data (and recovery points) associated with that member.</span></span>

  ![Boîte de dialogue Supprimer du groupe](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="d41d5-229">Créez un groupe de protection qui utilise Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="d41d5-230">Incluez les sources de données non protégées.</span><span class="sxs-lookup"><span data-stu-id="d41d5-230">Include the unprotected data sources.</span></span>


## <a name="add-disks-to-increase-legacy-storage"></a><span data-ttu-id="d41d5-231">Ajouter des disques pour augmenter le stockage existant</span><span class="sxs-lookup"><span data-stu-id="d41d5-231">Add disks to increase legacy storage</span></span>

<span data-ttu-id="d41d5-232">Si vous souhaitez utiliser un stockage existant avec le serveur de sauvegarde, vous devrez peut-être ajouter des disques pour augmenter la capacité de stockage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-232">If you want to use legacy storage with Backup Server, you might need to add disks to increase legacy storage.</span></span> 

<span data-ttu-id="d41d5-233">Pour ajouter un stockage sur disque :</span><span class="sxs-lookup"><span data-stu-id="d41d5-233">To add disk storage:</span></span>

1. <span data-ttu-id="d41d5-234">Dans la console Administrateur, sélectionnez **Gestion** > **Stockage sur disque** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-234">In the Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Boîte de dialogue Ajouter un stockage sur disque](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="d41d5-236">Dans la boîte de dialogue **Ajouter un stockage sur disque**, sélectionnez **Ajouter des disques**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-236">In the **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="d41d5-237">Dans la liste des disques disponibles, sélectionnez les disques à ajouter, choisissez **Ajouter**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-237">In the list of available disks, select the disks you want to add, select **Add**, and then select **OK**.</span></span>

## <a name="update-the-data-protection-manager-protection-agent"></a><span data-ttu-id="d41d5-238">Mettre à jour l’agent de protection Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="d41d5-238">Update the Data Protection Manager protection agent</span></span>

<span data-ttu-id="d41d5-239">Le serveur de sauvegarde tire parti de l’agent de protection System Center Data Protection Manager pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="d41d5-239">Backup Server uses the System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="d41d5-240">Si vous mettez à niveau un agent de protection qui n’est pas connecté au réseau, vous ne pouvez pas utiliser la console Administrateur de Data Protection Manager pour effectuer une mise à niveau d’agent connecté.</span><span class="sxs-lookup"><span data-stu-id="d41d5-240">If you are upgrading a protection agent that is not connected to the network, you cannot use the Data Protection Manager Administrator Console to complete a connected agent upgrade.</span></span> <span data-ttu-id="d41d5-241">Vous devez mettre à niveau l’agent de protection dans un environnement de domaine non actif.</span><span class="sxs-lookup"><span data-stu-id="d41d5-241">You must upgrade the protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="d41d5-242">Tant que l’ordinateur client n’est pas connecté au réseau, la console Administrateur de Data Protection Manager indique que la mise à jour de l’agent de protection est en attente.</span><span class="sxs-lookup"><span data-stu-id="d41d5-242">Until the client computer is connected to the network, the Data Protection Manager Administrator Console shows that the protection agent update is pending.</span></span>

<span data-ttu-id="d41d5-243">Les sections suivantes expliquent comment mettre à jour les agents de protection pour des ordinateurs clients qui sont connectés et des ordinateurs clients qui ne sont pas connectés.</span><span class="sxs-lookup"><span data-stu-id="d41d5-243">The following sections describe how to update protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="d41d5-244">Mettre à jour un agent de protection pour un ordinateur client connecté</span><span class="sxs-lookup"><span data-stu-id="d41d5-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="d41d5-245">Dans la console Administrateur du serveur de sauvegarde, sélectionnez **Gestion** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-245">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="d41d5-246">Dans le volet d’affichage, sélectionnez les ordinateurs clients dont vous souhaitez mettre à jour l’agent de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-246">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d41d5-247">La colonne **Mises à jour d’agent** indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé.</span><span class="sxs-lookup"><span data-stu-id="d41d5-247">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="d41d5-248">Dans le volet **Actions**, l’action **Mettre à jour** n’est proposée que lorsqu’un ordinateur protégé est sélectionné et que des mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="d41d5-248">In the **Actions** pane, the **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="d41d5-249">Pour installer les agents de protection à jour sur les ordinateurs sélectionnés, dans le volet **Actions**, sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-249">To install updated protection agents on the selected computers, in the **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="d41d5-250">Mettre à jour un agent de protection pour un ordinateur client qui n’est pas connecté</span><span class="sxs-lookup"><span data-stu-id="d41d5-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="d41d5-251">Dans la console Administrateur du serveur de sauvegarde, sélectionnez **Gestion** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-251">In the Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="d41d5-252">Dans le volet d’affichage, sélectionnez les ordinateurs clients dont vous souhaitez mettre à jour l’agent de protection.</span><span class="sxs-lookup"><span data-stu-id="d41d5-252">In the display pane, select the client computers for which you want to update the protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="d41d5-253">La colonne **Mises à jour d’agent** indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé.</span><span class="sxs-lookup"><span data-stu-id="d41d5-253">The **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="d41d5-254">Dans le volet **Actions**, l’action **Mettre à jour** n’est proposée pour un ordinateur protégé sélectionné que lorsque des mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="d41d5-254">In the **Actions** pane, the **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="d41d5-255">Pour installer les agents de protection à jour sur les ordinateurs sélectionnés, sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-255">To install updated protection agents on the selected computers, select **Update**.</span></span>

4. <span data-ttu-id="d41d5-256">Pour un ordinateur client qui n’est pas connecté au réseau, la colonne **État de l’agent** indique **Mise à jour en attente** tant que l’ordinateur n’est pas connecté au réseau.</span><span class="sxs-lookup"><span data-stu-id="d41d5-256">For a client computer that is not connected to the network, until the computer is connected to the network, the **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="d41d5-257">Une fois qu’un ordinateur client est connecté au réseau, la colonne **Mises à jour d’agent** de cet ordinateur indique l’état **Mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="d41d5-257">After a client computer is connected to the network, the **Agent Updates** column for the client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-the-new-version-with-azure"></a><span data-ttu-id="d41d5-258">Déplacer des groupes de protection hérités à partir de l’ancienne version et synchroniser la nouvelle version avec Azure</span><span class="sxs-lookup"><span data-stu-id="d41d5-258">Move legacy Protection groups from old version and sync the new version with Azure</span></span>

<span data-ttu-id="d41d5-259">Une fois le serveur de sauvegarde Azure et le système d’exploitation mis à jour, vous êtes prêt à protéger les nouvelles sources de données à l’aide de Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-259">Once Azure Backup Server and the OS are both updated, you are ready to protect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="d41d5-260">Toutefois, les sources de données déjà protégées continueront d’être protégées selon l’ancienne procédure, car elles se trouvaient sur le serveur de sauvegarde Azure, alors que toute nouvelle protection utilisera Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-260">However already protected data sources will continue to be protected in the legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="d41d5-261">La migration des sources de données depuis le mode de protection hérité vers Modern Backup Storage comprend les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d41d5-261">Below steps are to migrate data sources from legacy  mode of protection to Modern backup storage.</span></span>

<span data-ttu-id="d41d5-262">• Ajoutez le ou les nouveaux volumes au pool de stockage DPM et assignez des balises de source de données et des noms conviviaux si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d41d5-262">• Add the new volume(s) to the DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="d41d5-263">• Pour chaque source de données en mode hérité, arrêtez la protection et conservez les données protégées.</span><span class="sxs-lookup"><span data-stu-id="d41d5-263">• For each data source that is in legacy mode, stop protection of the data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="d41d5-264">Ainsi, les anciens points de récupération peuvent être récupérés après la migration.</span><span class="sxs-lookup"><span data-stu-id="d41d5-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="d41d5-265">• Créez un groupe de protection et sélectionnez les sources de données qui doivent être stockées à l’aide du nouveau format.</span><span class="sxs-lookup"><span data-stu-id="d41d5-265">• Create a new PG and select the data sources that are to be stored using new format.</span></span>
<span data-ttu-id="d41d5-266">• DPM effectue une copie du réplica à partir du stockage de sauvegarde existant dans le volume Modern Backup Storage localement.</span><span class="sxs-lookup"><span data-stu-id="d41d5-266">• DPM will do a replica copy from the legacy backup storage into the Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="d41d5-267">Remarque : Cela est considéré comme un travail d’opération de postrécupération • Tous les nouveaux points de synchronisation et de récupération sont ensuite stockés dans Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="d41d5-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="d41d5-268">• Les anciens points de récupération sont nettoyés quand ils expirent, libérant ainsi l’espace disque.</span><span class="sxs-lookup"><span data-stu-id="d41d5-268">• Old recovery points will be pruned out as they expire and eventually free up the disk space.</span></span>
<span data-ttu-id="d41d5-269">• Une fois tous les volumes existants supprimés de l’ancien stockage, le disque peut être enlevé de la sauvegarde Azure et du système.</span><span class="sxs-lookup"><span data-stu-id="d41d5-269">• Once all the legacy volumes are deleted from the old storage, the disk can be removed from Azure backup and the system.</span></span>
<span data-ttu-id="d41d5-270">• Créez une sauvegarde de la base de données DPM Azure.</span><span class="sxs-lookup"><span data-stu-id="d41d5-270">• Take a backup of the  Azure DPMDB.</span></span>

<span data-ttu-id="d41d5-271">Partie 2 :- Éléments importants > Le nouveau serveur doit porter le même nom que le serveur de sauvegarde Azure d’origine.</span><span class="sxs-lookup"><span data-stu-id="d41d5-271">Part 2: -Important items> The new server will need to be named same as the original Azure Backup server.</span></span> <span data-ttu-id="d41d5-272">Vous ne pouvez pas modifier le nom du nouveau serveur de sauvegarde Azure si vous souhaitez utiliser l’ancien pool de stockage et la base de données DPM pour conserver des points de récupération. Une sauvegarde de la base de données DPM est nécessaire en prévision de sa restauration.</span><span class="sxs-lookup"><span data-stu-id="d41d5-272">You cannot change the name of the new Azure backup server if you want to use old storage pool and DPMDB to retain recovery points -Must have backup of DPMDB  as it will need to be restored</span></span>

1) <span data-ttu-id="d41d5-273">Arrêtez le serveur de sauvegarde Azure d’origine ou mettez-le hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d41d5-273">Shutdown the original Azure backup server or take it off the wire.</span></span>
2) <span data-ttu-id="d41d5-274">Réinitialisez le compte de la machine dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d41d5-274">Reset the machine account in active directory.</span></span>
3) <span data-ttu-id="d41d5-275">Installez Server 2016 sur une nouvelle machine et attribuez à celle-ci le même nom que le serveur de sauvegarde Azure d’origine.</span><span class="sxs-lookup"><span data-stu-id="d41d5-275">Install Server 2016 on new machine and name it the same machine name as the original Azure Backup server.</span></span>
4) <span data-ttu-id="d41d5-276">Joignez le domaine.</span><span class="sxs-lookup"><span data-stu-id="d41d5-276">Join the Domain</span></span>
5) <span data-ttu-id="d41d5-277">Installez le serveur de sauvegarde Azure, version 2 (déplacez les disques du pool de stockage de DPM depuis l’ancien serveur et effectuez l’importation).</span><span class="sxs-lookup"><span data-stu-id="d41d5-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="d41d5-278">Restaurez la base de données DPM obtenue à la fin de la partie 2.</span><span class="sxs-lookup"><span data-stu-id="d41d5-278">Restore the DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="d41d5-279">Attachez le stockage à partir du serveur de sauvegarde d’origine au nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="d41d5-279">Attach the storage from the original backup server to the new server.</span></span>
8) <span data-ttu-id="d41d5-280">Depuis SQL, restaurez la base de données DPM.</span><span class="sxs-lookup"><span data-stu-id="d41d5-280">From SQL Restore the DPMDB</span></span>
9) <span data-ttu-id="d41d5-281">À partir de la ligne de commande d’administration sur le nouveau serveur, accédez au répertoire d’installation de Sauvegarde Microsoft Azure, puis au dossier bin.</span><span class="sxs-lookup"><span data-stu-id="d41d5-281">From admin command line on new server cd to Microsoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="d41d5-282">Exemple de chemin : C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="d41d5-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="d41d5-283">dans Azure sauvegarde exécutez DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="d41d5-283">to Azure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="d41d5-284">Exécutez DPMSYNC-SYNC. Remarque : Si vous avez ajouté de nouveaux disques au pool de stockage DPM au lieu de déplacer les anciens, exécutez DPMSYNC -Reallocatereplica.</span><span class="sxs-lookup"><span data-stu-id="d41d5-284">Run DPMSYNC -SYNC Note If you have added NEW disks to the DPM Storage pool instead of moving the old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="d41d5-285">Nouveaux cmdlets PowerShell dans la version 2</span><span class="sxs-lookup"><span data-stu-id="d41d5-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="d41d5-286">Lorsque vous installez le serveur de sauvegarde Azure v2, deux nouveaux cmdlets sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="d41d5-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="d41d5-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="d41d5-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="d41d5-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="d41d5-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="d41d5-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d41d5-289">Next steps</span></span>

<span data-ttu-id="d41d5-290">Découvrez comment préparer votre serveur ou commencer à protéger une charge de travail :</span><span class="sxs-lookup"><span data-stu-id="d41d5-290">Learn how to prepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="d41d5-291">Préparer les charges de travail du serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="d41d5-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="d41d5-292">Utiliser le Serveur de sauvegarde pour sauvegarder un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="d41d5-292">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="d41d5-293">Utiliser le serveur de sauvegarde pour sauvegarder SQL Server</span><span class="sxs-lookup"><span data-stu-id="d41d5-293">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="d41d5-294">Utiliser Modern Backup Storage avec le serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="d41d5-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

