---
title: Utiliser un stockage de sauvegarde moderne avec un Serveur de sauvegarde Azure v2 | Microsoft Docs
description: "Découvrez les nouvelles fonctionnalités du Serveur de sauvegarde Azure v2. Cet article décrit comment mettre à niveau votre installation de serveur de sauvegarde."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="359e6-104">Ajouter du stockage au Serveur de sauvegarde Azure v2</span><span class="sxs-lookup"><span data-stu-id="359e6-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="359e6-105">Le Serveur de sauvegarde Azure v2 est fourni avec le stockage de sauvegarde moderne du Data Protection Manager de System Center 2016.</span><span class="sxs-lookup"><span data-stu-id="359e6-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="359e6-106">Le stockage de sauvegarde moderne offre des économies de stockage de 50 %, des sauvegardes trois fois plus rapides et un stockage plus efficace.</span><span class="sxs-lookup"><span data-stu-id="359e6-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="359e6-107">Il s’agit également d’un stockage prenant en compte la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="359e6-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="359e6-108">Pour utiliser le stockage de sauvegarde moderne, vous devez exécuter le Serveur de sauvegarde v2 sur Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="359e6-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="359e6-109">Si vous exécutez le Serveur de sauvegarde v2 sur une version antérieure de Windows Server, le Serveur de sauvegarde Azure ne peut pas tirer parti du stockage de sauvegarde moderne.</span><span class="sxs-lookup"><span data-stu-id="359e6-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="359e6-110">Au lieu de cela, il protège les charges de travail comme il le fait avec le Serveur de sauvegarde v1.</span><span class="sxs-lookup"><span data-stu-id="359e6-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="359e6-111">Pour plus d’informations, voir la [matrice protection](backup-mabs-protection-matrix.md) de la version du Serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="359e6-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="359e6-112">Volumes dans le Serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="359e6-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="359e6-113">Le Serveur de sauvegarde v2 accepte les volumes de stockage.</span><span class="sxs-lookup"><span data-stu-id="359e6-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="359e6-114">Lorsque vous ajoutez un volume, le Serveur de sauvegarde formate le volume au format Resilient File System (ReFS) que nécessite le stockage de sauvegarde moderne.</span><span class="sxs-lookup"><span data-stu-id="359e6-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="359e6-115">Pour ajouter un volume et le développer ultérieurement si nécessaire, nous vous suggérons d’utiliser flux de travail suivant :</span><span class="sxs-lookup"><span data-stu-id="359e6-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="359e6-116">Configurez le Serveur de sauvegarde v2 sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="359e6-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="359e6-117">Créez un volume sur un disque virtuel dans un pool de stockage :</span><span class="sxs-lookup"><span data-stu-id="359e6-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="359e6-118">Ajoutez un disque à un pool de stockage, et créez un disque virtuel avec une disposition de stockage simple.</span><span class="sxs-lookup"><span data-stu-id="359e6-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="359e6-119">Ajoutez des disques supplémentaires, puis étendez le disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="359e6-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="359e6-120">Créez des volumes sur le disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="359e6-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="359e6-121">Ajoutez les volumes au Serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="359e6-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="359e6-122">Configurez un stockage prenant en compte la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="359e6-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="359e6-123">Créer un volume pour le stockage de sauvegarde moderne</span><span class="sxs-lookup"><span data-stu-id="359e6-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="359e6-124">L’utilisation du Serveur de sauvegarde v2 avec des volumes tels qu’un stockage sur disque peut vous aider à contrôler le stockage.</span><span class="sxs-lookup"><span data-stu-id="359e6-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="359e6-125">Un volume peut être un disque unique.</span><span class="sxs-lookup"><span data-stu-id="359e6-125">A volume can be a single disk.</span></span> <span data-ttu-id="359e6-126">Toutefois, si vous souhaitez étendre le stockage à l’avenir, créez un volume à partir d’un disque créé à l’aide d’espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="359e6-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="359e6-127">Cela peut être utile si vous souhaitez étendre le volume du stockage de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="359e6-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="359e6-128">Cette section présente les meilleures pratiques en matière de création de volume avec ce programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="359e6-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="359e6-129">Dans le Gestionnaire de serveur, sélectionnez **Services de fichiers et de stockage** > **Volumes** > **Pools de stockage**.</span><span class="sxs-lookup"><span data-stu-id="359e6-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="359e6-130">Sous **Disques physiques**, sélectionnez **Nouveau pool de stockage**.</span><span class="sxs-lookup"><span data-stu-id="359e6-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Créer un pool de stockage](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="359e6-132">Dans la zone de liste déroulante **Tâches**, sélectionnez **Nouveau disque virtuel**.</span><span class="sxs-lookup"><span data-stu-id="359e6-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Ajouter un disque virtuel](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="359e6-134">Sélectionnez le pool de stockage, puis choisissez **Ajouter un disque physique**.</span><span class="sxs-lookup"><span data-stu-id="359e6-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Ajouter un disque physique](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="359e6-136">Sélectionnez le disque physique, puis choisissez **Étendre le disque virtuel**.</span><span class="sxs-lookup"><span data-stu-id="359e6-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Étendre le disque virtuel](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="359e6-138">Sélectionnez le disque virtuel, puis choisissez **Nouveau volume**.</span><span class="sxs-lookup"><span data-stu-id="359e6-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Créer un volume](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="359e6-140">Dans la boîte de dialogue **sélectionner le serveur et le disque**, sélectionnez le serveur et le nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="359e6-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="359e6-141">Ensuite, sélectionnez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="359e6-141">Then, select **Next**.</span></span>

    ![Sélectionner le serveur et le disque](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="359e6-143">Ajouter des volumes de stockage au stockage sur disque du Serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="359e6-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="359e6-144">Pour ajouter un volume au Serveur de sauvegarde, dans le volet **Gestion**, réanalysez le stockage, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="359e6-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="359e6-145">La liste de tous les volumes disponibles pour ajout au stockage du Serveur de sauvegarde s’affiche.</span><span class="sxs-lookup"><span data-stu-id="359e6-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="359e6-146">Une fois les volumes disponibles ajoutés à la liste des volumes sélectionnés, vous pouvez leur donner un nom convivial pour faciliter leur gestion.</span><span class="sxs-lookup"><span data-stu-id="359e6-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="359e6-147">Pour formater ces volumes au format ReFS de façon à ce que le Serveur de sauvegarde puisse tirer parti des avantages du stockage de sauvegarde moderne, sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="359e6-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Ajouter des volumes disponibles](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="359e6-149">Configurer un stockage prenant en compte la charge de travail</span><span class="sxs-lookup"><span data-stu-id="359e6-149">Set up workload-aware storage</span></span>

<span data-ttu-id="359e6-150">Avec un stockage prenant en compte les charges de travail, vous pouvez sélectionner les volumes qui stockent de préférence certains genres de charges de travail.</span><span class="sxs-lookup"><span data-stu-id="359e6-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="359e6-151">Par exemple, vous pouvez définir des volumes coûteux prenant en charge un nombre élevé d’opérations d’entrée/sortie par seconde (IOPS) pour stocker uniquement les charges de travail qui nécessitent des sauvegardes de volumes importants fréquentes.</span><span class="sxs-lookup"><span data-stu-id="359e6-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="359e6-152">Un exemple est SQL Server avec les journaux des transactions.</span><span class="sxs-lookup"><span data-stu-id="359e6-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="359e6-153">D’autres charges de travail sauvegardées moins fréquemment, telles que les machines virtuelles, peuvent être sauvegardées sur des volumes bon marché.</span><span class="sxs-lookup"><span data-stu-id="359e6-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="359e6-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="359e6-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="359e6-155">Vous pouvez configurer un stockage prenant en compte les charges de travail à l’aide de l’applet de commande PowerShell Update-DPMDiskStorage, ce qui a pour effet de mettre à jour les propriétés d’un volume dans le pool de stockage sur un serveur Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="359e6-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="359e6-156">Syntaxe :</span><span class="sxs-lookup"><span data-stu-id="359e6-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="359e6-157">La capture d’écran suivante montre l’applet de commande Update-DPMDiskStorage dans la fenêtre PowerShell.</span><span class="sxs-lookup"><span data-stu-id="359e6-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![Commande Update-DPMDiskStorage dans la fenêtre PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="359e6-159">Les modifications apportées à l’aide de PowerShell apparaissent sur la Console Administrateur du Serveur de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="359e6-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Disques et volumes dans la Console Administrateur](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="359e6-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="359e6-161">Next steps</span></span>
<span data-ttu-id="359e6-162">Après avoir installé le Serveur de sauvegarde, apprenez à préparer votre serveur ou commencez à protéger une charge de travail.</span><span class="sxs-lookup"><span data-stu-id="359e6-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="359e6-163">Préparer les charges de travail du Serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="359e6-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="359e6-164">Utiliser le Serveur de sauvegarde pour sauvegarder un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="359e6-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="359e6-165">Utiliser le serveur de sauvegarde pour sauvegarder SQL Server</span><span class="sxs-lookup"><span data-stu-id="359e6-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

