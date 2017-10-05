---
title: "Sauvegarde et restauration de la base de données Azure Analysis Services | Microsoft Docs"
description: "Explique comment sauvegarder et restaurer une base de données Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: bffa481a498b130ef1f2388a5ba856da5d164ee0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="9646f-103">Sauvegarde et restauration</span><span class="sxs-lookup"><span data-stu-id="9646f-103">Backup and restore</span></span>

<span data-ttu-id="9646f-104">La sauvegarde de bases de données de modèles tabulaires dans Azure Analysis Services est relativement semblable à celle des Analysis Services locaux.</span><span class="sxs-lookup"><span data-stu-id="9646f-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="9646f-105">La principale différence réside dans le lieu où vous enregistrez vos fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="9646f-106">Les fichiers de sauvegarde doivent être enregistrés dans un conteneur dans un [compte de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9646f-106">Backup files must be saved to a container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="9646f-107">Vous pouvez utiliser un compte de stockage et un conteneur que vous avez déjà, ou bien en créer de nouveaux lors de la configuration des paramètres de stockage de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="9646f-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="9646f-108">La création d’un compte de stockage peut entraîner un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="9646f-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="9646f-109">Pour en savoir plus, consultez [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="9646f-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="9646f-110">Les sauvegardes sont enregistrées avec l’extension .abf.</span><span class="sxs-lookup"><span data-stu-id="9646f-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="9646f-111">Pour les modèles tabulaires en mémoire, les données et les métadonnées de modèle sont enregistrées.</span><span class="sxs-lookup"><span data-stu-id="9646f-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="9646f-112">Pour les modèles tabulaires DirectQuery, seules les métadonnées de modèle sont stockées.</span><span class="sxs-lookup"><span data-stu-id="9646f-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="9646f-113">Les sauvegardes peuvent être compressées et chiffrées, en fonction des options que vous avez choisies.</span><span class="sxs-lookup"><span data-stu-id="9646f-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="9646f-114">Configurer les paramètres de stockage</span><span class="sxs-lookup"><span data-stu-id="9646f-114">Configure storage settings</span></span>
<span data-ttu-id="9646f-115">Avant de procéder à la sauvegarde, vous devez configurer les paramètres de stockage de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="9646f-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="9646f-116">Pour configurer les paramètres de stockage</span><span class="sxs-lookup"><span data-stu-id="9646f-116">To configure storage settings</span></span>
1.  <span data-ttu-id="9646f-117">Dans le portail Azure > **Paramètres**, cliquez sur **Sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="9646f-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Sauvegardes dans Paramètres](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="9646f-119">Cliquez sur **Activé**, puis cliquez sur **Paramètres de stockage**.</span><span class="sxs-lookup"><span data-stu-id="9646f-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Activer](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="9646f-121">Sélectionnez un compte de stockage ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="9646f-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="9646f-122">Sélectionnez un conteneur ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="9646f-122">Select a container or create a new one.</span></span>

    ![Sélectionner un conteneur](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="9646f-124">Enregistrez vos paramètres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-124">Save your backup settings.</span></span>

    ![Enregistrer les paramètres de sauvegarde](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="9646f-126">Sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9646f-126">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="9646f-127">Pour effectuer une sauvegarde à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="9646f-127">To backup by using SSMS</span></span>

1. <span data-ttu-id="9646f-128">Dans SSMS, effectuez un clic droit sur une base de données > **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="9646f-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="9646f-129">Dans **Sauvegarder une base de données** > **Fichier de sauvegarde**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="9646f-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="9646f-130">Dans la boîte de dialogue **Enregistrer le fichier sous**, vérifiez le chemin d’accès au dossier, puis saisissez le nom du fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-130">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> 

4. <span data-ttu-id="9646f-131">Dans la boîte de dialogue **Sauvegarder une base de données**, sélectionnez les options.</span><span class="sxs-lookup"><span data-stu-id="9646f-131">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="9646f-132">**Autoriser l’écrasement des fichiers** - Sélectionnez cette option pour remplacer les fichiers de sauvegarde portant le même nom.</span><span class="sxs-lookup"><span data-stu-id="9646f-132">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="9646f-133">Si cette option n’est pas sélectionnée, le fichier que vous tentez d’enregistrer ne peut pas porter le même nom qu’un fichier se trouvant déjà au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="9646f-133">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="9646f-134">**Appliquer la compression** - Sélectionnez cette option pour compresser le fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-134">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="9646f-135">Les fichiers de sauvegarde compressés permettent d’économiser de l’espace disque, mais nécessite une utilisation un peu plus intensive du processeur.</span><span class="sxs-lookup"><span data-stu-id="9646f-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="9646f-136">**Chiffrer le fichier de sauvegarde** - Sélectionnez cette option pour chiffrer le fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-136">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="9646f-137">Cette option nécessite un mot de passe fourni par l’utilisateur pour sécuriser le fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-137">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="9646f-138">Le mot de passe empêche la lecture des données de sauvegarde à des fins autres que les opérations de restauration.</span><span class="sxs-lookup"><span data-stu-id="9646f-138">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="9646f-139">Si vous choisissez de chiffrer les sauvegardes, conservez le mot de passe en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="9646f-139">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="9646f-140">Cliquez sur **OK** pour créer et enregistrer le fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-140">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="9646f-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9646f-141">PowerShell</span></span>
<span data-ttu-id="9646f-142">Utilisez l’applet de commande [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="9646f-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="9646f-143">Restauration</span><span class="sxs-lookup"><span data-stu-id="9646f-143">Restore</span></span>
<span data-ttu-id="9646f-144">Lors de la restauration, votre fichier de sauvegarde doit être dans le compte de stockage que vous avez configuré pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="9646f-144">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="9646f-145">Si vous devez déplacer un fichier de sauvegarde d’un emplacement local vers votre compte de stockage, utilisez [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) ou l’utilitaire de ligne de commande [AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="9646f-145">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="9646f-146">Si vous procédez à une restauration à partir d’un serveur local, vous devez supprimer tous les utilisateurs de domaine des rôles du modèle, puis les rajouter aux rôles en tant qu’utilisateurs Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9646f-146">If you're restoring from an on-premises server, you must remove all the domain users from the model's roles and add them back to the roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="9646f-147">Pour effectuer une restauration à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="9646f-147">To restore by using SSMS</span></span>

1. <span data-ttu-id="9646f-148">Dans SSMS, effectuez un clic droit sur une base de données > **Restaurer**.</span><span class="sxs-lookup"><span data-stu-id="9646f-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="9646f-149">Dans la boîte de dialogue **Sauvegarder une base de données**, dans **Fichier de sauvegarde**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="9646f-149">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="9646f-150">Dans la boîte de dialogue **Rechercher les fichiers de base de données**, sélectionnez le fichier à restaurer.</span><span class="sxs-lookup"><span data-stu-id="9646f-150">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="9646f-151">Dans la boîte de dialogue **Restaurer la base de données**, sélectionnez la base de données.</span><span class="sxs-lookup"><span data-stu-id="9646f-151">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="9646f-152">Spécifiez les options.</span><span class="sxs-lookup"><span data-stu-id="9646f-152">Specify options.</span></span> <span data-ttu-id="9646f-153">Les options de sécurité doivent correspondre aux options de sauvegarde utilisées lors de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9646f-153">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="9646f-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9646f-154">PowerShell</span></span>

<span data-ttu-id="9646f-155">Utilisez l’applet de commande [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="9646f-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="9646f-156">Informations connexes</span><span class="sxs-lookup"><span data-stu-id="9646f-156">Related information</span></span>

[<span data-ttu-id="9646f-157">Des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="9646f-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="9646f-158">[Haute disponibilité](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="9646f-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="9646f-159">Gérer Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="9646f-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
