---
title: "base de données Analysis Services aaaAzure de sauvegarde et de restauration | Documents Microsoft"
description: "Décrit comment toobackup et restauration un Azure Analysis Services base de données."
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
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="dbac1-103">Sauvegarde et restauration</span><span class="sxs-lookup"><span data-stu-id="dbac1-103">Backup and restore</span></span>

<span data-ttu-id="dbac1-104">Sauvegarde des bases de données de modèle tabulaire dans Azure Analysis Services est une grande partie hello même que pour les Services d’analyse local.</span><span class="sxs-lookup"><span data-stu-id="dbac1-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="dbac1-105">Hello principale différence est l’endroit où vous stockez vos fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="dbac1-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="dbac1-106">Fichiers de sauvegarde doivent être enregistrés conteneur tooa dans un [compte de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="dbac1-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="dbac1-107">Vous pouvez utiliser un compte de stockage et un conteneur que vous avez déjà, ou bien en créer de nouveaux lors de la configuration des paramètres de stockage de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="dbac1-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="dbac1-108">La création d’un compte de stockage peut entraîner un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="dbac1-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="dbac1-109">toolearn, voir [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="dbac1-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="dbac1-110">Les sauvegardes sont enregistrées avec l’extension .abf.</span><span class="sxs-lookup"><span data-stu-id="dbac1-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="dbac1-111">Pour les modèles tabulaires en mémoire, les données et les métadonnées de modèle sont enregistrées.</span><span class="sxs-lookup"><span data-stu-id="dbac1-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="dbac1-112">Pour les modèles tabulaires DirectQuery, seules les métadonnées de modèle sont stockées.</span><span class="sxs-lookup"><span data-stu-id="dbac1-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="dbac1-113">Les sauvegardes peuvent être compressées et chiffrées, en fonction des options que vous choisissez hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="dbac1-114">Configurer les paramètres de stockage</span><span class="sxs-lookup"><span data-stu-id="dbac1-114">Configure storage settings</span></span>
<span data-ttu-id="dbac1-115">Avant de sauvegarder, vous devez tooconfigure les paramètres de stockage pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="dbac1-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="dbac1-116">paramètres de stockage tooconfigure</span><span class="sxs-lookup"><span data-stu-id="dbac1-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="dbac1-117">Dans le portail Azure > **Paramètres**, cliquez sur **Sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Sauvegardes dans Paramètres](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="dbac1-119">Cliquez sur **Activé**, puis cliquez sur **Paramètres de stockage**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Activer](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="dbac1-121">Sélectionnez un compte de stockage ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="dbac1-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="dbac1-122">Sélectionnez un conteneur ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="dbac1-122">Select a container or create a new one.</span></span>

    ![Sélectionner un conteneur](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="dbac1-124">Enregistrez vos paramètres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="dbac1-124">Save your backup settings.</span></span>

    ![Enregistrer les paramètres de sauvegarde](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="dbac1-126">Sauvegarde</span><span class="sxs-lookup"><span data-stu-id="dbac1-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="dbac1-127">toobackup à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="dbac1-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="dbac1-128">Dans SSMS, effectuez un clic droit sur une base de données > **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="dbac1-129">Dans **Sauvegarder une base de données** > **Fichier de sauvegarde**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="dbac1-130">Bonjour **enregistrer le fichier sous** boîte de dialogue, vérifiez le chemin d’accès du dossier hello et tapez un nom pour le fichier de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="dbac1-131">Bonjour **Backup Database** boîte de dialogue, sélectionnez les options.</span><span class="sxs-lookup"><span data-stu-id="dbac1-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="dbac1-132">**Autoriser les fichiers remplacer** -Sélectionnez cette option toooverwrite sauvegarde de fichiers hello même nom.</span><span class="sxs-lookup"><span data-stu-id="dbac1-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="dbac1-133">Si cette option n’est pas sélectionnée, hello fichier que vous utilisez ne peut pas avoir hello même nom en tant que fichier figurant déjà dans hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="dbac1-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="dbac1-134">**Appliquer la compression** -Sélectionnez ce fichier de sauvegarde option toocompress hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="dbac1-135">Les fichiers de sauvegarde compressés permettent d’économiser de l’espace disque, mais nécessite une utilisation un peu plus intensive du processeur.</span><span class="sxs-lookup"><span data-stu-id="dbac1-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="dbac1-136">**Chiffrer le fichier de sauvegarde** -Sélectionnez ce fichier de sauvegarde option tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="dbac1-137">Cette option nécessite un fichier de sauvegarde de mot de passe fourni par l’utilisateur toosecure hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="dbac1-138">mot de passe Hello empêche la lecture des données de sauvegarde hello autrement qu’une opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="dbac1-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="dbac1-139">Si vous choisissez les sauvegardes tooencrypt, stocker hello le mot de passe dans un endroit sûr.</span><span class="sxs-lookup"><span data-stu-id="dbac1-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="dbac1-140">Cliquez sur **OK** toocreate et enregistrez le fichier de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="dbac1-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbac1-141">PowerShell</span></span>
<span data-ttu-id="dbac1-142">Utilisez l’applet de commande [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="dbac1-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="dbac1-143">Restauration</span><span class="sxs-lookup"><span data-stu-id="dbac1-143">Restore</span></span>
<span data-ttu-id="dbac1-144">Lors de la restauration, votre fichier de sauvegarde doit être hello compte de stockage que vous avez configurée pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="dbac1-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="dbac1-145">Si vous devez toomove un fichier de sauvegarde à partir d’un compte de stockage tooyour emplacement local, utilisez [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) ou hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitaire de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="dbac1-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="dbac1-146">Si vous restaurez à partir d’un serveur local, vous devez supprimer tous les utilisateurs de domaine hello les rôles du modèle hello et ajoutez-les sauvegarder rôles toohello en tant qu’utilisateurs d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dbac1-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="dbac1-147">toorestore à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="dbac1-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="dbac1-148">Dans SSMS, effectuez un clic droit sur une base de données > **Restaurer**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="dbac1-149">Bonjour **Backup Database** boîte de dialogue, dans **le fichier de sauvegarde**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="dbac1-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="dbac1-150">Bonjour **rechercher les fichiers de base de données** boîte de dialogue, fichier hello sélectionnez toorestore.</span><span class="sxs-lookup"><span data-stu-id="dbac1-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="dbac1-151">Dans **restauration de base de données**, sélectionnez base de données hello.</span><span class="sxs-lookup"><span data-stu-id="dbac1-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="dbac1-152">Spécifiez les options.</span><span class="sxs-lookup"><span data-stu-id="dbac1-152">Specify options.</span></span> <span data-ttu-id="dbac1-153">Options de sécurité doivent correspondre à des options de sauvegarde hello utilisées lors de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="dbac1-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="dbac1-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dbac1-154">PowerShell</span></span>

<span data-ttu-id="dbac1-155">Utilisez l’applet de commande [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="dbac1-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="dbac1-156">Informations connexes</span><span class="sxs-lookup"><span data-stu-id="dbac1-156">Related information</span></span>

[<span data-ttu-id="dbac1-157">Des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="dbac1-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="dbac1-158">[Haute disponibilité](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="dbac1-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="dbac1-159">Gérer Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="dbac1-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
