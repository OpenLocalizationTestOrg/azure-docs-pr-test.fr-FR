---
title: aaaUse le stockage de sauvegarde moderne avec Azure Backup Server v2 | Documents Microsoft
description: "En savoir plus sur les nouvelles fonctionnalités de hello dans Azure Backup Server v2. Cet article décrit comment tooupgrade votre installation du serveur de sauvegarde."
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
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="952cc-104">Ajouter du stockage tooAzure v2 de sauvegarde du serveur</span><span class="sxs-lookup"><span data-stu-id="952cc-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="952cc-105">Le Serveur de sauvegarde Azure v2 est fourni avec le stockage de sauvegarde moderne du Data Protection Manager de System Center 2016.</span><span class="sxs-lookup"><span data-stu-id="952cc-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="952cc-106">Le stockage de sauvegarde moderne offre des économies de stockage de 50 %, des sauvegardes trois fois plus rapides et un stockage plus efficace.</span><span class="sxs-lookup"><span data-stu-id="952cc-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="952cc-107">Il s’agit également d’un stockage prenant en compte la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="952cc-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="952cc-108">toouse moderne le stockage de sauvegarde, vous devez exécuter v2 de sauvegarde du serveur sur Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="952cc-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="952cc-109">Si vous exécutez le Serveur de sauvegarde v2 sur une version antérieure de Windows Server, le Serveur de sauvegarde Azure ne peut pas tirer parti du stockage de sauvegarde moderne.</span><span class="sxs-lookup"><span data-stu-id="952cc-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="952cc-110">Au lieu de cela, il protège les charges de travail comme il le fait avec le Serveur de sauvegarde v1.</span><span class="sxs-lookup"><span data-stu-id="952cc-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="952cc-111">Pour plus d’informations, consultez la version du serveur de sauvegarde hello [matrice protection](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="952cc-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="952cc-112">Volumes dans le Serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="952cc-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="952cc-113">Le Serveur de sauvegarde v2 accepte les volumes de stockage.</span><span class="sxs-lookup"><span data-stu-id="952cc-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="952cc-114">Lorsque vous ajoutez un volume, serveur de sauvegarde met en forme hello volume tooResilient système de fichiers (ReFS), qui nécessite de stockage de sauvegarde moderne.</span><span class="sxs-lookup"><span data-stu-id="952cc-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="952cc-115">tooadd un volume et tooexpand ultérieurement si vous le souhaitez, nous vous suggérons d’utiliser ce flux de travail :</span><span class="sxs-lookup"><span data-stu-id="952cc-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="952cc-116">Configurez le Serveur de sauvegarde v2 sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="952cc-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="952cc-117">Créez un volume sur un disque virtuel dans un pool de stockage :</span><span class="sxs-lookup"><span data-stu-id="952cc-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="952cc-118">Ajouter un pool de stockage de disque tooa et créer un disque virtuel de la mise en page simple.</span><span class="sxs-lookup"><span data-stu-id="952cc-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="952cc-119">Ajouter des disques supplémentaires et d’étendre le disque virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="952cc-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="952cc-120">Créer des volumes sur le disque virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="952cc-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="952cc-121">Ajoutez hello volumes tooBackup Server.</span><span class="sxs-lookup"><span data-stu-id="952cc-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="952cc-122">Configurez un stockage prenant en compte la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="952cc-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="952cc-123">Créer un volume pour le stockage de sauvegarde moderne</span><span class="sxs-lookup"><span data-stu-id="952cc-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="952cc-124">L’utilisation du Serveur de sauvegarde v2 avec des volumes tels qu’un stockage sur disque peut vous aider à contrôler le stockage.</span><span class="sxs-lookup"><span data-stu-id="952cc-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="952cc-125">Un volume peut être un disque unique.</span><span class="sxs-lookup"><span data-stu-id="952cc-125">A volume can be a single disk.</span></span> <span data-ttu-id="952cc-126">Toutefois, si vous souhaitez stockage tooextend Bonjour future, créer un volume en dehors d’un disque créé à l’aide des espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="952cc-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="952cc-127">Cela peut être utile si vous souhaitez le volume de hello tooexpand pour le stockage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="952cc-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="952cc-128">Cette section présente les meilleures pratiques en matière de création de volume avec ce programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="952cc-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="952cc-129">Dans le Gestionnaire de serveur, sélectionnez **Services de fichiers et de stockage** > **Volumes** > **Pools de stockage**.</span><span class="sxs-lookup"><span data-stu-id="952cc-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="952cc-130">Sous **Disques physiques**, sélectionnez **Nouveau pool de stockage**.</span><span class="sxs-lookup"><span data-stu-id="952cc-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Créer un pool de stockage](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="952cc-132">Bonjour **tâches** zone de liste déroulante, sélectionnez **nouveau disque virtuel**.</span><span class="sxs-lookup"><span data-stu-id="952cc-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Ajouter un disque virtuel](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="952cc-134">Sélectionnez le pool de stockage hello et sélectionnez **ajouter un disque physique**.</span><span class="sxs-lookup"><span data-stu-id="952cc-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Ajouter un disque physique](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="952cc-136">Sélectionnez les disques physiques hello, puis **étendre un disque virtuel**.</span><span class="sxs-lookup"><span data-stu-id="952cc-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Étendre le disque virtuel de hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="952cc-138">Sélectionnez le disque virtuel de hello et sélectionnez **nouveau Volume**.</span><span class="sxs-lookup"><span data-stu-id="952cc-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Créer un volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="952cc-140">Bonjour **sélectionnez hello serveur et disque** boîte de dialogue, serveur de select hello et nouveau disque de hello.</span><span class="sxs-lookup"><span data-stu-id="952cc-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="952cc-141">Ensuite, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="952cc-141">Then, select **Next**.</span></span>

    ![Sélectionnez le disque et le serveur de hello](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="952cc-143">Ajouter du stockage sur disque des volumes tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="952cc-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="952cc-144">tooadd un tooBackup volume Server, Bonjour **gestion** volet, effectuez une nouvelle analyse de stockage de hello, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="952cc-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="952cc-145">Une liste de tous les hello volumes disponibles toobe ajouté pour le stockage de serveur de sauvegarde s’affiche.</span><span class="sxs-lookup"><span data-stu-id="952cc-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="952cc-146">Une fois que les volumes disponibles sont ajoutés à la liste toohello des volumes sélectionnés, vous pouvez lui attribuer un toohelp nom convivial les gérer.</span><span class="sxs-lookup"><span data-stu-id="952cc-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="952cc-147">tooformat tooReFS de ces volumes afin de la sauvegarde du serveur peuvent profiter des avantages de hello du stockage de sauvegarde moderne, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="952cc-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Ajouter des volumes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="952cc-149">Configurer un stockage prenant en compte la charge de travail</span><span class="sxs-lookup"><span data-stu-id="952cc-149">Set up workload-aware storage</span></span>

<span data-ttu-id="952cc-150">Avec un stockage prenant en charge les charges de travail, vous pouvez sélectionner les volumes hello préférence stocker certains types de charges de travail.</span><span class="sxs-lookup"><span data-stu-id="952cc-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="952cc-151">Par exemple, vous pouvez définir des volumes coûteuses qui prennent en charge un grand nombre d’opérations d’entrée/sortie par seconde (IOPS) toostore uniquement hello les charges de travail qui nécessitent des sauvegardes fréquentes et élevées.</span><span class="sxs-lookup"><span data-stu-id="952cc-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="952cc-152">Un exemple est SQL Server avec les journaux des transactions.</span><span class="sxs-lookup"><span data-stu-id="952cc-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="952cc-153">Autres charges de travail qui sont sauvegardés moins fréquemment, telles que des machines virtuelles, peuvent être sauvegardées coût toolow volumes.</span><span class="sxs-lookup"><span data-stu-id="952cc-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="952cc-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="952cc-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="952cc-155">Vous pouvez définir l’espace de stockage prenant en charge les charges de travail à l’aide d’applet de commande PowerShell hello DPMDiskStorage de la mise à jour, ce qui met à jour les propriétés de hello d’un volume dans le pool de stockage hello sur un serveur Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="952cc-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="952cc-156">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="952cc-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="952cc-157">Hello capture d’écran suivante montre hello DPMDiskStorage de mise à jour applet de commande dans la fenêtre de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="952cc-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Hello commande DPMDiskStorage de mise à jour dans la fenêtre de PowerShell hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="952cc-159">Hello apportée à l’aide de PowerShell est répercutées dans hello Console de l’administrateur du serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="952cc-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Disques et volumes de hello Console Administrateur](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="952cc-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="952cc-161">Next steps</span></span>
<span data-ttu-id="952cc-162">Après avoir installé le serveur de sauvegarde, découvrez comment tooprepare votre serveur, ou pour commencer à protéger une charge de travail.</span><span class="sxs-lookup"><span data-stu-id="952cc-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="952cc-163">Préparer les charges de travail du serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="952cc-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="952cc-164">Utilisez tooback du serveur de sauvegarde d’un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="952cc-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="952cc-165">Utilisez tooback de sauvegarde du serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="952cc-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

