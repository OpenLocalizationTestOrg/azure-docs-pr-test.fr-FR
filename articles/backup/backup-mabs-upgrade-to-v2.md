---
title: "aaaInstall v2 d’Azure Backup Server | Documents Microsoft"
description: "Le serveur de sauvegarde Azure v2 offre des capacités de sauvegarde améliorées pour protéger les machines virtuelles, les fichiers et dossiers, les charges de travail, et plus encore. Découvrez comment tooinstall ou mise à niveau tooAzure v2 de sauvegarde du serveur."
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="62067-104">Installer le serveur de sauvegarde Azure v2</span><span class="sxs-lookup"><span data-stu-id="62067-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="62067-105">Le serveur de sauvegarde Azure contribue à protéger vos machines virtuelles, vos charges de travail, vos fichiers et dossiers, et plus encore.</span><span class="sxs-lookup"><span data-stu-id="62067-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="62067-106">Reposant sur le serveur de sauvegarde v1, le serveur de sauvegarde Azure v2 offre des fonctionnalités qui ne sont pas disponibles dans la première version.</span><span class="sxs-lookup"><span data-stu-id="62067-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="62067-107">Pour connaître les différences entre les versions v1 et v2, consultez [Matrice de protection du serveur de sauvegarde Azure](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="62067-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="62067-108">fonctionnalités supplémentaires de Hello dans v2 de sauvegarde du serveur sont une mise à niveau à partir de la sauvegarde du serveur v1.</span><span class="sxs-lookup"><span data-stu-id="62067-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="62067-109">Cependant, le serveur de sauvegarde v1 n’est pas requis pour installer le serveur de sauvegarde v2.</span><span class="sxs-lookup"><span data-stu-id="62067-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="62067-110">Si vous souhaitez tooupgrade à partir de la sauvegarde du serveur v1 tooBackup v2 de serveur, installez v2 de sauvegarde du serveur sur le serveur de protection du serveur de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="62067-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="62067-111">Vos paramètres de serveur de sauvegarde existants seront conservés.</span><span class="sxs-lookup"><span data-stu-id="62067-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="62067-112">Vous pouvez installer le serveur de sauvegarde v2 sur Windows Server 2012 R2 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="62067-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="62067-113">tootake les parti des nouvelles fonctionnalités telles que le stockage de sauvegarde moderne données Protection Manager System Center 2016, vous devez installer le serveur de sauvegarde v2 sur Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="62067-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="62067-114">Mettre à niveau l’installation tooor v2 de sauvegarde du serveur, en savoir plus sur hello [conditions préalables d’installation](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="62067-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="62067-115">Sauvegarde du serveur Azure a hello même code de base en tant que System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="62067-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="62067-116">Sauvegarde serveur v1 est équivalent tooData Protection Manager 2012 R2 et v2 de sauvegarde du serveur est équivalent tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="62067-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="62067-117">Cet article fait parfois référence à la documentation de Data Protection Manager hello.</span><span class="sxs-lookup"><span data-stu-id="62067-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="62067-118">Mise à niveau du serveur de sauvegarde toov2</span><span class="sxs-lookup"><span data-stu-id="62067-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="62067-119">tooupgrade à partir de la sauvegarde du serveur v1 tooBackup v2 de serveur, assurez-vous que votre installation comprend des mises à jour hello requis :</span><span class="sxs-lookup"><span data-stu-id="62067-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="62067-120">[Mettre à jour les agents de protection hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) sur hello des serveurs protégés.</span><span class="sxs-lookup"><span data-stu-id="62067-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="62067-121">Mise à niveau de Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="62067-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="62067-122">Mettez à niveau l’outil d’administration à distance du serveur de sauvegarde Azure sur tous les serveurs de production.</span><span class="sxs-lookup"><span data-stu-id="62067-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="62067-123">Assurez-vous que les sauvegardes sont définies toocontinue sans avoir à redémarrer votre serveur de production.</span><span class="sxs-lookup"><span data-stu-id="62067-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="62067-124">Procédure de mise à niveau vers le serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="62067-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="62067-125">Dans le centre de téléchargement de hello [télécharger le programme d’installation de la mise à niveau hello](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="62067-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="62067-126">Après avoir extrait Assistant hello, assurez-vous que **exécuter setup.exe** est sélectionné, puis sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="62067-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Programme d’installation - Exécuter l’installation](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="62067-128">Dans l’Assistant de Microsoft Azure Backup Server hello, sous **installer**, sélectionnez **Microsoft Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="62067-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Programme d’installation - Sélectionner l’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="62067-130">Sur hello **Bienvenue** , examinez les avertissements hello, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Programme d’installation - Page Bienvenue](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="62067-132">Assistant Installation de Hello effectue toomake vérifications des conditions préalables que votre environnement peut mettre à niveau.</span><span class="sxs-lookup"><span data-stu-id="62067-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="62067-133">Sur hello **Prerequisite Checks** page, sélectionnez **vérifier**.</span><span class="sxs-lookup"><span data-stu-id="62067-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Programme d’installation - Page Vérifications des conditions requises](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="62067-135">Votre environnement doit passer les vérifications hello.</span><span class="sxs-lookup"><span data-stu-id="62067-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="62067-136">Si votre environnement ne remplit pas les vérifications de hello, notez les problèmes de hello et de les corriger.</span><span class="sxs-lookup"><span data-stu-id="62067-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="62067-137">Ensuite, sélectionnez **Revérifier**.</span><span class="sxs-lookup"><span data-stu-id="62067-137">Then, select **Check Again**.</span></span> <span data-ttu-id="62067-138">Une fois que vous passez des vérifications des conditions préalables hello, sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Programme d’installation - Bouton Revérifier](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="62067-140">Sur hello **paramètres SQL** page, l’option hello pertinentes pour votre installation de SQL, puis sélectionnez **vérifier et installer**.</span><span class="sxs-lookup"><span data-stu-id="62067-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Programme d’installation - Page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="62067-142">vérifications de Hello peuvent prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="62067-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="62067-143">Lorsque les vérifications de hello sont terminé, sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-143">When hello checks are finished, select **Next**.</span></span>

  ![Programme d’installation - Bouton Vérifier et installer de la page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="62067-145">Sur hello **les paramètres d’Installation** page, de modifier n’importe quel emplacement de toohello modifications où la sauvegarde du serveur est installé, ou toohello emplacement de travail.</span><span class="sxs-lookup"><span data-stu-id="62067-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="62067-146">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-146">Select **Next**.</span></span>

  ![Programme d’installation - Page Paramètres d’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="62067-148">toofinish hello Assistant installation, sélectionnez **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="62067-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Programme d’installation - Terminer](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="62067-150">Ajouter un stockage pour Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="62067-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="62067-151">l’efficacité du stockage de sauvegarde tooimprove, v2 de sauvegarde du serveur ajoute la prise en charge des volumes.</span><span class="sxs-lookup"><span data-stu-id="62067-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="62067-152">Comme le serveur de sauvegarde v1, le serveur de sauvegarde v2 prend en charge les disques.</span><span class="sxs-lookup"><span data-stu-id="62067-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="62067-153">Ajouter des volumes et des disques</span><span class="sxs-lookup"><span data-stu-id="62067-153">Add volumes and disks</span></span>
<span data-ttu-id="62067-154">Si vous exécutez le serveur de sauvegarde v2 sur Windows Server 2016, vous pouvez utiliser les données de sauvegarde de volumes toostore.</span><span class="sxs-lookup"><span data-stu-id="62067-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="62067-155">Les volumes assurent des économies en stockage et des sauvegardes plus rapides.</span><span class="sxs-lookup"><span data-stu-id="62067-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="62067-156">Étant donné que les volumes sont tooBackup nouveau serveur, vous devez les ajouter.</span><span class="sxs-lookup"><span data-stu-id="62067-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="62067-157">Lorsque vous ajoutez un serveur de tooBackup volume, vous pouvez donner un nom convivial volume de hello.</span><span class="sxs-lookup"><span data-stu-id="62067-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="62067-158">Cliquez sur hello **nom convivial** colonne du volume de hello souhaité tooname.</span><span class="sxs-lookup"><span data-stu-id="62067-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="62067-159">Vous pouvez modifier le nom de hello plus tard, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="62067-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="62067-160">Vous pouvez également utiliser PowerShell tooadd ou modifier les noms conviviaux pour les volumes.</span><span class="sxs-lookup"><span data-stu-id="62067-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="62067-161">tooadd un volume Bonjour la Console Administrateur :</span><span class="sxs-lookup"><span data-stu-id="62067-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="62067-162">Dans la Console Administrateur de serveur de sauvegarde Azure de hello, sélectionnez **gestion** > **le stockage sur disque** > **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62067-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Assistant Ajouter un stockage sur disque de hello ouvert](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="62067-164">Assistant Ajouter un stockage sur disque de hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="62067-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="62067-165">Sur hello **ajouter un stockage sur disque** page hello **volumes disponibles** zone, sélectionnez un volume, puis **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62067-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="62067-166">Bonjour **des volumes sélectionnés** zone, entrez un nom convivial pour le volume de hello, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="62067-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Assistant Ajouter un stockage sur disque - Ajouter un volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="62067-168">Si vous souhaitez tooadd une disquette, disque de hello doit appartenir à groupe de protection tooa ayant un stockage hérité.</span><span class="sxs-lookup"><span data-stu-id="62067-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="62067-169">Ces disques peuvent uniquement être utilisés pour ces groupes de protection.</span><span class="sxs-lookup"><span data-stu-id="62067-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="62067-170">Si le serveur de sauvegarde n’a pas sources dont la protection héritée, disque de hello n’est pas répertorié.</span><span class="sxs-lookup"><span data-stu-id="62067-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="62067-171">Pour plus d’informations sur l’ajout de disques, consultez [Ajout des disques de stockage hérité tooincrease](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="62067-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="62067-172">Vous ne pouvez pas donner de nom convivial à un disque.</span><span class="sxs-lookup"><span data-stu-id="62067-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="62067-173">Affecter des charges de travail toovolumes</span><span class="sxs-lookup"><span data-stu-id="62067-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="62067-174">Dans la sauvegarde du serveur, vous spécifiez des charges de travail assignés toowhich volumes.</span><span class="sxs-lookup"><span data-stu-id="62067-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="62067-175">Par exemple, vous pouvez définir des volumes coûteuses qui prennent en charge un grand nombre d’opérations d’entrée/sortie par seconde (IOPS) toostore uniquement les charges de travail qui nécessitent des sauvegardes fréquentes et élevées.</span><span class="sxs-lookup"><span data-stu-id="62067-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="62067-176">Un exemple est SQL Server avec les journaux des transactions.</span><span class="sxs-lookup"><span data-stu-id="62067-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="62067-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="62067-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="62067-178">les propriétés de hello de tooupdate d’un volume dans le pool de stockage de hello au serveur de sauvegarde, utiliser l’applet de commande PowerShell hello DPMDiskStorage de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="62067-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="62067-179">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="62067-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="62067-180">Toutes les modifications que vous apportez à l’aide de PowerShell sont répercutées dans l’interface utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="62067-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="62067-181">Protéger les sources de données</span><span class="sxs-lookup"><span data-stu-id="62067-181">Protect data sources</span></span>
<span data-ttu-id="62067-182">toobegin protégeant les sources de données, créez un groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="62067-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="62067-183">Hello suivant Assistant par mise en surbrillance étapes changements ou ajouts nouveau groupe de Protection de toohello.</span><span class="sxs-lookup"><span data-stu-id="62067-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="62067-184">toocreate un groupe de protection :</span><span class="sxs-lookup"><span data-stu-id="62067-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="62067-185">Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **Protection**.</span><span class="sxs-lookup"><span data-stu-id="62067-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="62067-186">Dans la barre d’outils hello, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="62067-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="62067-187">Assistant créer un nouveau groupe de Protection de hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="62067-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Assistant Création d’un nouveau groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="62067-189">Sur hello **Bienvenue** page, sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="62067-190">Sur hello **sélectionner le Type de groupe de Protection** , sélectionnez le type de hello du groupe de protection, vous souhaitez toocreate, puis sélectionnez **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Page Sélectionner le type de groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="62067-192">Sur hello **sélectionner les membres du groupe** page hello **membres disponibles** volet, les membres de hello avec protection agents sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="62067-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="62067-193">Dans cet exemple, sélectionnez le volume D:\ et E:\ et ajoutez-les toohello **membres sélectionnés** volet.</span><span class="sxs-lookup"><span data-stu-id="62067-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="62067-194">Sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-194">Select **Next**.</span></span>

  ![Page Sélectionner les membres du groupe](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="62067-196">Sur hello **sélectionner la méthode de Protection des données** , entrez un **nom de groupe de Protection**, sélectionnez la méthode de protection hello, puis **suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="62067-197">Si vous souhaitez une protection à court terme, vous devez sélectionner hello **disque** méthode de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="62067-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Page Sélectionner la méthode de protection des données](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="62067-199">Sur hello **spécifier les objectifs à court terme** mise en page, sélectionnez hello pour **de rétention** et **la fréquence de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="62067-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="62067-200">Ensuite, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="62067-200">Then, select **Next**.</span></span> <span data-ttu-id="62067-201">Si vous le souhaitez, toochange planification de hello pour lorsque les points de récupération sont prises, sélectionnez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="62067-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Page Spécifier les objectifs à court terme](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="62067-203">Sur hello **vérifier l’Allocation de stockage disque** , examinez les détails sur les sources de données hello choisie, leur taille et valeurs hello espace toobe est configuré, hello du volume de stockage cible.</span><span class="sxs-lookup"><span data-stu-id="62067-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Page Vérifier l’allocation de stockage sur disque](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="62067-205">Volumes de stockage sont basés sur l’allocation de volume de charge de travail hello (définie à l’aide de PowerShell) et hello du stockage disponible.</span><span class="sxs-lookup"><span data-stu-id="62067-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="62067-206">Vous pouvez modifier les volumes de stockage hello en sélectionnant les autres volumes dans le menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="62067-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="62067-207">Si vous modifiez la valeur hello pour **stockage cible**, hello valeur pour **stockage de disque disponible** modifie de façon dynamique les valeurs tooreflect sous **espace** et **Underprovisioned espace**.</span><span class="sxs-lookup"><span data-stu-id="62067-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="62067-208">Si la croissance des sources de données hello comme prévu, hello valeur hello **Underprovisioned l’espace** colonne **stockage de disque disponible** reflète la quantité de hello de stockage supplémentaire que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="62067-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="62067-209">Utiliser ce plan de toohelp valeur vos besoins de stockage pour les sauvegardes lisses.</span><span class="sxs-lookup"><span data-stu-id="62067-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="62067-210">Si la valeur de hello est égal à zéro, il n’existe aucun problème potentiel avec le stockage dans un futur prévisible hello.</span><span class="sxs-lookup"><span data-stu-id="62067-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="62067-211">Si la valeur de hello est un nombre différent de zéro, vous n’avez pas de suffisamment de stockage alloué (basé sur la protection de stratégie et hello taille de vos données de vos membres protégés).</span><span class="sxs-lookup"><span data-stu-id="62067-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Stockage sur disque sous-alloué](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="62067-213">toofinish création de l’Assistant hello groupe, complète de votre protection.</span><span class="sxs-lookup"><span data-stu-id="62067-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="62067-214">Migrer le stockage existant tooModern le stockage de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="62067-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="62067-215">Une fois que vous mettez à niveau tooor installation v2 de sauvegarde du serveur et mise à niveau hello tooWindows de système d’exploitation Server 2016, mettre à jour votre toouse de groupes de protection moderne le stockage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="62067-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="62067-216">Par défaut, les groupes de protection ne sont pas modifiés.</span><span class="sxs-lookup"><span data-stu-id="62067-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="62067-217">Ils continuent toofunction comme elles ont été initialement définis.</span><span class="sxs-lookup"><span data-stu-id="62067-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="62067-218">Mise à jour de groupes de protection toouse moderne le stockage de sauvegarde est facultative.</span><span class="sxs-lookup"><span data-stu-id="62067-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="62067-219">groupe de protection tooupdate hello, arrêtez la protection de toutes les sources de données à l’aide de hello conserver option de données.</span><span class="sxs-lookup"><span data-stu-id="62067-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="62067-220">Ajoutez ensuite hello données sources tooa nouveau groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="62067-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="62067-221">Dans la Console Administrateur de hello, sélectionnez hello **Protection** fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="62067-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="62067-222">Bonjour **membre du groupe de Protection** liste, cliquez sur le membre de hello et sélectionnez **arrêter la protection du membre**.</span><span class="sxs-lookup"><span data-stu-id="62067-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Arrêter la protection du membre](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="62067-224">Bonjour **supprimer du groupe** boîte de dialogue, l’espace de disque hello utilisée revue et hello d’espace libre pour le pool de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="62067-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="62067-225">valeur par défaut Hello est de points de récupération hello tooleave sur le disque de hello et leur tooexpire par leur stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="62067-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="62067-226">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="62067-226">Click **OK**.</span></span>

  <span data-ttu-id="62067-227">Si vous souhaitez que le pool de stockage libre du disque espace toohello tooimmediately hello retour utilisé, sélectionnez hello **supprimer le réplica sur disque** case toodelete les données de sauvegarde hello (et les points de récupération) associé à ce membre.</span><span class="sxs-lookup"><span data-stu-id="62067-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Boîte de dialogue Supprimer du groupe](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="62067-229">Créez un groupe de protection qui utilise Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="62067-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="62067-230">Inclure des sources de données hello non protégé.</span><span class="sxs-lookup"><span data-stu-id="62067-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="62067-231">Ajouter des disques du stockage hérité tooincrease</span><span class="sxs-lookup"><span data-stu-id="62067-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="62067-232">Si vous souhaitez toouse de stockage existant avec le serveur de sauvegarde, vous devrez peut-être stockage hérité de tooadd disques tooincrease.</span><span class="sxs-lookup"><span data-stu-id="62067-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="62067-233">stockage sur disque tooadd :</span><span class="sxs-lookup"><span data-stu-id="62067-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="62067-234">Dans la Console Administrateur de hello, sélectionnez **gestion** > **le stockage sur disque** > **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="62067-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Boîte de dialogue Ajouter un stockage sur disque](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="62067-236">Bonjour **ajouter un stockage sur disque** boîte de dialogue, sélectionnez **ajouter des disques**.</span><span class="sxs-lookup"><span data-stu-id="62067-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="62067-237">Dans la liste hello de disques disponibles, sélectionnez les disques hello tooadd, sélectionnez **ajouter**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="62067-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="62067-238">Mettre à jour l’agent de protection hello Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="62067-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="62067-239">Sauvegarde du serveur utilise un agent de protection de System Center Data Protection Manager hello des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="62067-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="62067-240">Si vous mettez à niveau un agent de protection n’est pas connecté toohello réseau, vous ne pouvez pas utiliser hello Console d’administration DPM toocomplete une mise à niveau de l’agent.</span><span class="sxs-lookup"><span data-stu-id="62067-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="62067-241">Vous devez mettre à niveau l’agent de protection hello dans un environnement de domaine non actif.</span><span class="sxs-lookup"><span data-stu-id="62067-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="62067-242">Jusqu'à ce que l’ordinateur client de hello est connecté toohello réseau, hello que console d’administration DPM affiche cette mise à jour de l’agent de protection hello est en attente.</span><span class="sxs-lookup"><span data-stu-id="62067-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="62067-243">Hello sections suivantes décrivent comment tooupdate les agents de protection pour les ordinateurs clients qui sont connectés et les ordinateurs clients qui ne sont pas connectés.</span><span class="sxs-lookup"><span data-stu-id="62067-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="62067-244">Mettre à jour un agent de protection pour un ordinateur client connecté</span><span class="sxs-lookup"><span data-stu-id="62067-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="62067-245">Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **gestion** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="62067-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="62067-246">Dans le volet d’informations hello, sélectionnez les ordinateurs clients hello pour lequel vous souhaitez l’agent de protection tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="62067-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="62067-247">Hello **mises à jour de l’Agent** colonne indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé.</span><span class="sxs-lookup"><span data-stu-id="62067-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="62067-248">Bonjour **Actions** volet, hello **mise à jour** action est disponible uniquement lorsqu’un ordinateur protégé est sélectionné et les mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="62067-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="62067-249">tooinstall mis à jour les agents de protection sur les ordinateurs de hello sélectionné, Bonjour **Actions** volet, sélectionnez **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="62067-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="62067-250">Mettre à jour un agent de protection pour un ordinateur client qui n’est pas connecté</span><span class="sxs-lookup"><span data-stu-id="62067-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="62067-251">Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **gestion** > **Agents**.</span><span class="sxs-lookup"><span data-stu-id="62067-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="62067-252">Dans le volet d’informations hello, sélectionnez les ordinateurs clients hello pour lequel vous souhaitez l’agent de protection tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="62067-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="62067-253">Hello **mises à jour de l’Agent** colonne indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé.</span><span class="sxs-lookup"><span data-stu-id="62067-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="62067-254">Bonjour **Actions** volet, hello **mise à jour** action n’est pas disponible lorsqu’un ordinateur protégé est sélectionné sauf si les mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="62067-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="62067-255">tooinstall mis à jour les agents de protection sur les ordinateurs hello sélectionné, sélectionnez **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="62067-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="62067-256">Pour un ordinateur client qui n’est pas connecté toohello réseau, jusqu'à ce que l’ordinateur de hello est connecté toohello réseau, hello **état de l’Agent** colonne présente l’état de **mise à jour en attente**.</span><span class="sxs-lookup"><span data-stu-id="62067-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="62067-257">Une fois un ordinateur client connecté toohello réseau, hello **mises à jour de l’Agent** présente l’état de colonne pour l’ordinateur client de hello **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="62067-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="62067-258">Déplacer des groupes de Protection hérités à partir de l’ancienne et la synchronisation hello nouvelle version avec Azure</span><span class="sxs-lookup"><span data-stu-id="62067-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="62067-259">Une fois que le serveur de sauvegarde Azure et hello du système d’exploitation sont à jour, vous êtes prêt tooprotect nouvelles sources de données à l’aide du stockage de sauvegarde moderne.</span><span class="sxs-lookup"><span data-stu-id="62067-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="62067-260">Toutefois déjà protégé des sources de données continue toobe protégé dans hello hérité de façon qu’ils étaient dans Azure Backup Server mais toute nouvelle protection utilise le stockage de sauvegarde modernes.</span><span class="sxs-lookup"><span data-stu-id="62067-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="62067-261">Étapes ci-dessous sont des sources de données toomigrate du mode hérité protection tooModern de stockage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="62067-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="62067-262">• Ajoutez hello nouveau ou les volumes toohello DPM pool de stockage et affecter des balises de source de données et les noms conviviales si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="62067-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="62067-263">• Pour chaque source de données est en mode CAS hérité, arrêtez la protection des sources de données hello et « Conserver les données protégées ».</span><span class="sxs-lookup"><span data-stu-id="62067-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="62067-264">Ainsi, les anciens points de récupération peuvent être récupérés après la migration.</span><span class="sxs-lookup"><span data-stu-id="62067-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="62067-265">• Créer un nouveau groupe de protection et sélectionnez les sources de données hello qui sont stocké à l’aide du nouveau format de toobe.</span><span class="sxs-lookup"><span data-stu-id="62067-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="62067-266">• DPM effectuera une copie du réplica de stockage de sauvegarde hérité hello en hello volume de stockage de sauvegarde moderne localement.</span><span class="sxs-lookup"><span data-stu-id="62067-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="62067-267">Remarque : Cela est considéré comme un travail d’opération de postrécupération • Tous les nouveaux points de synchronisation et de récupération sont ensuite stockés dans Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="62067-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="62067-268">• Anciens points de récupération seront nettoyés qu’ils expirent et finalement libérer de l’espace disque hello.</span><span class="sxs-lookup"><span data-stu-id="62067-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="62067-269">• Une fois que tous les volumes hérités hello sont supprimées du stockage ancien hello, disque de hello peut être supprimée à partir du système de sauvegarde et de hello Azure.</span><span class="sxs-lookup"><span data-stu-id="62067-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="62067-270">• Créer une sauvegarde de hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="62067-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="62067-271">Partie 2 :-des éléments importants > nouveau serveur de hello devez toobe même nommé en tant que serveur de sauvegarde Azure hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="62067-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="62067-272">Vous ne pouvez pas modifier le nom hello du serveur de sauvegarde Azure nouveau hello si vous voulez toouse ancien pool de stockage des points de récupération de tooretain DPMDB - devez avoir la sauvegarde de base de données DPM que vous devez toobe restauré</span><span class="sxs-lookup"><span data-stu-id="62067-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="62067-273">Arrêt hello du serveur de sauvegarde Azure d’origine ou mettez-la câble hello.</span><span class="sxs-lookup"><span data-stu-id="62067-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="62067-274">Réinitialiser le compte d’ordinateur hello dans active directory.</span><span class="sxs-lookup"><span data-stu-id="62067-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="62067-275">Installer Server 2016 sur le nouvel ordinateur, nom il hello le même nom de l’ordinateur en tant que serveur de sauvegarde Azure hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="62067-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="62067-276">Joindre le domaine de hello</span><span class="sxs-lookup"><span data-stu-id="62067-276">Join hello Domain</span></span>
5) <span data-ttu-id="62067-277">Installez le serveur de sauvegarde Azure, version 2 (déplacez les disques du pool de stockage de DPM depuis l’ancien serveur et effectuez l’importation).</span><span class="sxs-lookup"><span data-stu-id="62067-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="62067-278">Restaurer hello DPMDB obtenue à partir de la fin de la partie 2</span><span class="sxs-lookup"><span data-stu-id="62067-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="62067-279">Connectez le périphérique de stockage de hello hello d’origine sauvegarde toohello nouveau serveur.</span><span class="sxs-lookup"><span data-stu-id="62067-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="62067-280">À partir de la restauration SQL hello DPMDB</span><span class="sxs-lookup"><span data-stu-id="62067-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="62067-281">À partir de la ligne de commande d’administration sur le nouveau serveur de cd tooMicrosoft Azure Backup installer emplacement et le dossier bin</span><span class="sxs-lookup"><span data-stu-id="62067-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="62067-282">Exemple de chemin : C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="62067-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="62067-283">tooAzure sauvegarde exécutez DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="62067-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="62067-284">Exécutez DPMSYNC-SYNC Remarque Si vous avez ajouté le nouveau pool de stockage DPM disques toohello au lieu de déplacer hello anciens, puis exécutez DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="62067-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="62067-285">Nouveaux cmdlets PowerShell dans la version 2</span><span class="sxs-lookup"><span data-stu-id="62067-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="62067-286">Lorsque vous installez le serveur de sauvegarde Azure v2, deux nouveaux cmdlets sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="62067-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="62067-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="62067-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="62067-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="62067-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="62067-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62067-289">Next steps</span></span>

<span data-ttu-id="62067-290">Découvrez comment tooprepare votre serveur ou pour commencer à protéger une charge de travail :</span><span class="sxs-lookup"><span data-stu-id="62067-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="62067-291">Préparer les charges de travail du serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="62067-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="62067-292">Utilisez tooback du serveur de sauvegarde d’un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="62067-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="62067-293">Utilisez tooback de sauvegarde du serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="62067-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="62067-294">Utiliser Modern Backup Storage avec le serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="62067-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

