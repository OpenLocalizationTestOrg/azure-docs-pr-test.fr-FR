---
title: "Configurer la rétention des sauvegardes à long terme - Base de données SQL Azure | Microsoft Docs"
description: "Découvrez comment stocker des sauvegardes automatisées dans le coffre Azure Recovery Services et comment restaurer des bases de données à partir du coffre Azure Recovery Services"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: ed9f74a59f0ca512e2758c6db4c5c9075030f859
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="f51e8-103">Configurer et restaurer à partir de la rétention des sauvegardes à long terme de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f51e8-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="f51e8-104">Vous pouvez configurer le coffre Azure Recovery Services pour stocker les sauvegardes de base de données SQL Azure, puis récupérer une base de données à l’aide des sauvegardes conservées dans le coffre avec le portail Azure ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f51e8-104">You can configure the Azure Recovery Services vault to store Azure SQL database backups and then recover a database using backups retained in the vault using the Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="f51e8-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f51e8-105">Azure portal</span></span>

<span data-ttu-id="f51e8-106">Les sections suivantes vous montrent comment utiliser le portail Azure pour configurer le coffre Azure Recovery Services, afficher les sauvegardes dans le coffre et restaurer à partir du coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-106">The following sections show you how to use the Azure portal to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="configure-the-vault-register-the-server-and-select-databases"></a><span data-ttu-id="f51e8-107">Configurer le coffre, inscrire le serveur et sélectionner les bases de données</span><span class="sxs-lookup"><span data-stu-id="f51e8-107">Configure the vault, register the server, and select databases</span></span>

<span data-ttu-id="f51e8-108">Vous [configurez un coffre Azure Recovery Services de façon à conserver des sauvegardes automatisées](sql-database-long-term-retention.md) sur une période plus longue que la période de rétention associée à votre niveau de service.</span><span class="sxs-lookup"><span data-stu-id="f51e8-108">You [configure an Azure Recovery Services vault to retain automated backups](sql-database-long-term-retention.md) for a period longer than the retention period for your service tier.</span></span> 

1. <span data-ttu-id="f51e8-109">Ouvrez la page **SQL Server** de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="f51e8-109">Open the **SQL Server** page for your server.</span></span>

   ![page sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="f51e8-111">Cliquez sur **Long-term backup retention (Rétention des sauvegardes à long terme)**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-111">Click **Long-term backup retention**.</span></span>

   ![lien de rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="f51e8-113">Sur la page **Long-term backup retention** (Rétention des sauvegardes à long terme) de votre serveur, examinez et acceptez les conditions d’utilisation de la version préliminaire (à moins que vous ne l’ayez déjà fait ou que cette fonctionnalité ne soit plus en version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="f51e8-113">On the **Long-term backup retention** page for your server, review and accept the preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![accepter les conditions d’utilisation de la version préliminaire](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="f51e8-115">Pour configurer la rétention des sauvegardes à long terme, sélectionnez cette base de données dans la grille, puis cliquez sur **Configurer** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="f51e8-115">To configure long-term backup retention, select that database in the grid and then click **Configure** on the toolbar.</span></span>

   ![sélectionner la base de données pour la rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="f51e8-117">Sur la page **Configurer**, cliquez sur **Configurer les paramètres requis** sous **Coffre Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-117">On the **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![lien de configuration du coffre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="f51e8-119">Sur la page **Coffre Recovery Services**, sélectionnez un éventuel coffre existant.</span><span class="sxs-lookup"><span data-stu-id="f51e8-119">On the **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="f51e8-120">Dans le cas contraire, si aucun coffre Recovery Services n’a été trouvé pour votre abonnement, cliquez pour quitter le flux, puis créez un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f51e8-120">Otherwise, if no recovery services vault found for your subscription, click to exit the flow and create a recovery services vault.</span></span>

   ![créer un lien vers le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="f51e8-122">Sur la page **Coffres Recovery Services**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-122">On the **Recovery Services vaults** page, click **Add**.</span></span>

   ![ajouter le lien vers le coffre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="f51e8-124">Sur la page **Coffre Recovery Services**, fournissez un nom valide pour le coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f51e8-124">On the **Recovery Services vault** page, provide a valid name for the Recovery Services vault.</span></span>

   ![nom du nouveau coffre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="f51e8-126">Sélectionnez votre abonnement et votre groupe de ressources, puis sélectionnez l’emplacement du coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-126">Select your subscription and resource group, and then select the location for the vault.</span></span> <span data-ttu-id="f51e8-127">Une fois que vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-127">When done, click **Create**.</span></span>

   ![créer le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="f51e8-129">Le coffre doit se trouver dans la même région que le serveur logique SQL Azure et doit utiliser le même groupe de ressources que le serveur logique.</span><span class="sxs-lookup"><span data-stu-id="f51e8-129">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>
   >

10. <span data-ttu-id="f51e8-130">Une fois le nouveau coffre créé, exécutez les étapes nécessaires pour revenir à la page **Coffre Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-130">After the new vault is created, execute the necessary steps to return to the **Recovery services vault** page.</span></span>

11. <span data-ttu-id="f51e8-131">Sur la page **Coffre Recovery Services**, cliquez sur le coffre, puis sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-131">On the **Recovery services vault** page, click the vault and then click **Select**.</span></span>

   ![sélectionner un coffre existant](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="f51e8-133">Sur la page **Configurer**, fournissez un nom valide pour la nouvelle stratégie de rétention, modifiez la stratégie de rétention par défaut à votre convenance, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-133">On the **Configure** page, provide a valid name for the new retention policy, modify the default retention policy as appropriate, and then click **OK**.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="f51e8-135">Sur la page **Long-term backup retention** (Rétention des sauvegardes à long terme) de votre base de données, cliquez sur **Enregistrer**, puis sur **OK** pour appliquer la stratégie de rétention des sauvegardes à long terme à toutes les bases de données sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="f51e8-135">On the **Long-term backup retention** page for your database, click **Save** and then click **OK** to apply the long-term backup retention policy to all selected databases.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="f51e8-137">Cliquez sur **Enregistrer** pour activer la rétention des sauvegardes à long terme à l’aide de cette nouvelle stratégie dans le coffre Azure Recovery Services que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="f51e8-137">Click **Save** to enable long-term backup retention using this new policy to the Azure Recovery Services vault that you configured.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="f51e8-139">Une fois configurées, les sauvegardes s’affichent dans le coffre dans les sept jours qui suivent.</span><span class="sxs-lookup"><span data-stu-id="f51e8-139">Once configured, backups show up in the vault within next seven days.</span></span> <span data-ttu-id="f51e8-140">Ne poursuivez pas ce didacticiel tant que les sauvegardes n’apparaissent pas dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-140">Do not continue this tutorial until backups show up in the vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="f51e8-141">Visualiser les sauvegardes de la rétention à long terme à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f51e8-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="f51e8-142">Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="f51e8-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="f51e8-143">Dans le portail Azure, ouvrez le coffre Azure Recovery Services de vos sauvegardes de base de données (accédez à **Toutes les ressources**, puis sélectionnez cette entrée dans la liste des ressources de votre abonnement) pour visualiser la quantité de stockage utilisée par les sauvegardes de votre base de données dans le coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-143">In the Azure portal, open your Azure Recovery Services vault for your database backups (go to **All resources** and select it from the list of resources for your subscription) to view the amount of storage used by your database backups in the vault.</span></span>

   ![visualiser le coffre Recovery Services avec les sauvegardes](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="f51e8-145">Ouvrez la page **Base de données SQL** de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="f51e8-145">Open the **SQL database** page for your database.</span></span>

   ![page nouvel exemple de base de données](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="f51e8-147">Dans la barre d’outils, cliquez sur **Restaurer**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-147">On the toolbar, click **Restore**.</span></span>

   ![barre d’outils Restaurer](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="f51e8-149">Sur la page Restaurer, cliquez sur **À long terme**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-149">On the Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="f51e8-150">Sous Azure vault backups (Sauvegardes de coffre Azure), cliquez sur **Sélectionner une sauvegarde** pour visualiser les sauvegardes de base de données disponibles dans la rétention des sauvegardes à long terme.</span><span class="sxs-lookup"><span data-stu-id="f51e8-150">Under Azure vault backups, click **Select a backup** to view the available database backups in long-term backup retention.</span></span>

   ![sauvegardes dans le coffre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-the-azure-portal"></a><span data-ttu-id="f51e8-152">Restaurer une base de données à partir d’une sauvegarde dans la rétention des sauvegardes à long terme à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f51e8-152">Restore a database from a backup in long-term backup retention using the Azure portal</span></span>

<span data-ttu-id="f51e8-153">Vous restaurez la base de données sous la forme d’une nouvelle base de données à partir d’une sauvegarde dans le coffre Azure Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f51e8-153">You restore the database to a new database from a backup in the Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="f51e8-154">Sur la page **Azure vault backups (Sauvegardes de coffre Azure)**, cliquez sur la sauvegarde à restaurer, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="f51e8-154">On the **Azure vault backups** page, click the backup to restore and then click **Select**.</span></span>

   ![sélectionner une sauvegarde dans le coffre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="f51e8-156">Dans la zone de texte **Nom de la base de données**, fournissez le nom de la base de données restaurée.</span><span class="sxs-lookup"><span data-stu-id="f51e8-156">In the **Database name** text box, provide the name for the restored database.</span></span>

   ![nom de la nouvelle base de données](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="f51e8-158">Cliquez sur **OK** pour restaurer votre base de données à partir de la sauvegarde dans le coffre sous la forme d’une nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="f51e8-158">Click **OK** to restore your database from the backup in the vault to the new database.</span></span>

4. <span data-ttu-id="f51e8-159">Dans la barre d’outils, cliquez sur l’icône de notification pour visualiser l’état du travail de restauration.</span><span class="sxs-lookup"><span data-stu-id="f51e8-159">On the toolbar, click the notification icon to view the status of the restore job.</span></span>

   ![progression du travail de restauration à partir du coffre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="f51e8-161">Lorsque le travail de restauration est terminé, ouvrez la page **Bases de données SQL** pour visualiser la base de données nouvellement restaurée.</span><span class="sxs-lookup"><span data-stu-id="f51e8-161">When the restore job is completed, open the **SQL databases** page to view the newly restored database.</span></span>

   ![base de données restaurée à partir du coffre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="f51e8-163">À ce stade, vous pouvez vous connecter à la base de données restaurée à l’aide de SQL Server Management Studio pour exécuter les tâches nécessaires, notamment pour [extraire un bit de données de la base de données restaurée à copier dans la base de données existante ou pour supprimer la base de données existante et renommer la base de données restaurée avec le nom de la base de données existante](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="f51e8-163">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to [extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="f51e8-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f51e8-164">PowerShell</span></span>

<span data-ttu-id="f51e8-165">Les sections suivantes vous montrent comment utiliser PowerShell pour configurer le coffre Azure Recovery Services, afficher les sauvegardes dans le coffre et restaurer à partir du coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-165">The following sections show you how to use PowerShell to configure the Azure Recovery Services vault, view backups in the vault, and restore from the vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="f51e8-166">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="f51e8-166">Create a recovery services vault</span></span>

<span data-ttu-id="f51e8-167">Utilisez [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) pour créer un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f51e8-167">Use the [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) to create a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f51e8-168">Le coffre doit se trouver dans la même région que le serveur logique SQL Azure et doit utiliser le même groupe de ressources que le serveur logique.</span><span class="sxs-lookup"><span data-stu-id="f51e8-168">The vault must be located in the same region as the Azure SQL logical server, and must use the same resource group as the logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-to-use-the-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="f51e8-169">Configurer votre serveur de manière à utiliser le coffre Recovery pour les sauvegardes de rétention à long terme</span><span class="sxs-lookup"><span data-stu-id="f51e8-169">Set your server to use the recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="f51e8-170">Utilisez l’applet de commande [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) pour associer un coffre Recovery Services créé précédemment à un serveur SQL Azure spécifique.</span><span class="sxs-lookup"><span data-stu-id="f51e8-170">Use the [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet to associate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server to use the vault to for long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="f51e8-171">Créer une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="f51e8-171">Create a retention policy</span></span>

<span data-ttu-id="f51e8-172">Vous définissez la durée de conservation d’une sauvegarde de base de données dans une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="f51e8-172">A retention policy is where you set how long to keep a database backup.</span></span> <span data-ttu-id="f51e8-173">Utilisez l’applet de commande [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) pour obtenir la stratégie de rétention par défaut à utiliser comme modèle pour la création de stratégies.</span><span class="sxs-lookup"><span data-stu-id="f51e8-173">Use the [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet to get the default retention policy to use as the template for creating policies.</span></span> <span data-ttu-id="f51e8-174">Dans ce modèle, la période de rétention est définie sur 2 ans.</span><span class="sxs-lookup"><span data-stu-id="f51e8-174">In this template, the retention period is set for 2 years.</span></span> <span data-ttu-id="f51e8-175">Ensuite, exécutez [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) pour créer la stratégie.</span><span class="sxs-lookup"><span data-stu-id="f51e8-175">Next, run the [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) to finally create the policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="f51e8-176">Certaines applets de commande nécessitent que vous définissiez le contexte du coffre avant l’exécution ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) afin de voir cette applet de commande dans quelques extraits de code connexes.</span><span class="sxs-lookup"><span data-stu-id="f51e8-176">Some cmdlets require that you set the vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="f51e8-177">Vous définissez le contexte, car la stratégie fait partie du coffre.</span><span class="sxs-lookup"><span data-stu-id="f51e8-177">You set the context because the policy is part of the vault.</span></span> <span data-ttu-id="f51e8-178">Vous pouvez créer plusieurs stratégies de rétention pour chaque coffre, puis appliquer la stratégie souhaitée à des bases de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f51e8-178">You can create multiple retention policies for each vault and then apply the desired policy to specific databases.</span></span> 


```PowerShell
# Retrieve the default retention policy for the AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set the retention value to two years (you can set to any time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set the vault context to the vault you are creating the policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create the new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-to-use-the-previously-defined-retention-policy"></a><span data-ttu-id="f51e8-179">Configurer une base de données de manière à utiliser la stratégie de rétention définie précédemment</span><span class="sxs-lookup"><span data-stu-id="f51e8-179">Configure a database to use the previously defined retention policy</span></span>

<span data-ttu-id="f51e8-180">Utilisez l’applet de commande [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) pour appliquer la nouvelle stratégie à une base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="f51e8-180">Use the [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet to apply the new policy to a specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="f51e8-181">Visualiser les sauvegardes de la rétention à long terme et les informations sur les sauvegardes</span><span class="sxs-lookup"><span data-stu-id="f51e8-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="f51e8-182">Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="f51e8-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="f51e8-183">Utilisez les applets de commande suivantes pour afficher les informations sur la sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="f51e8-183">Use the following cmdlets to view backup information:</span></span>

- [<span data-ttu-id="f51e8-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="f51e8-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="f51e8-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="f51e8-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="f51e8-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="f51e8-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set the vault context to the vault we want to restore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# the following commands find the container associated with the server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get the long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for the previously indicated database
# Optionally, set the -StartDate and -EndDate parameters to return backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="f51e8-187">Restaurer une base de données à partir d’une sauvegarde dans la rétention des sauvegardes à long terme</span><span class="sxs-lookup"><span data-stu-id="f51e8-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="f51e8-188">La restauration à partir de la rétention des sauvegardes à long terme utilise l’applet de commande [AzureRmSqlDatabase de restauration](/powershell/module/azurerm.sql/restore-azurermsqldatabase).</span><span class="sxs-lookup"><span data-stu-id="f51e8-188">Restoring from long-term backup retention uses the [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore the most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> <span data-ttu-id="f51e8-189">À ce stade, vous pouvez vous connecter à la base de données restaurée à l’aide de SQL Server Management Studio pour exécuter les tâches nécessaires, notamment pour extraire un bit de données de la base de données restaurée à copier dans la base de données existante ou pour supprimer la base de données existante et renommer la base de données restaurée avec le nom de la base de données existante.</span><span class="sxs-lookup"><span data-stu-id="f51e8-189">From here, you can connect to the restored database using SQL Server Management Studio to perform needed tasks, such as to extract a bit of data from the restored database to copy into the existing database or to delete the existing database and rename the restored database to the existing database name.</span></span> <span data-ttu-id="f51e8-190">Consultez [Restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="f51e8-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f51e8-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f51e8-191">Next steps</span></span>

- <span data-ttu-id="f51e8-192">Pour plus d’informations sur les sauvegardes automatiques générées par le service, consultez l’article relatif aux [sauvegardes automatiques](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="f51e8-192">To learn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="f51e8-193">Pour plus d’informations sur la rétention des sauvegardes à long terme, consultez l’article décrivant la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="f51e8-193">To learn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="f51e8-194">Pour plus d’informations sur la restauration à partir de sauvegardes, consultez l’article concernant la [restauration à l’aide de sauvegardes](sql-database-recovery-using-backups.md).</span><span class="sxs-lookup"><span data-stu-id="f51e8-194">To learn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
