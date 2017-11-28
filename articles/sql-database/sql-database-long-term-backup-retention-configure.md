---
title: "Configurer la rétention des sauvegardes à long terme - Base de données SQL Azure | Microsoft Docs"
description: "Découvrez comment toostore automatisé sauvegardes Bonjour Qu'azure Recovery Services coffre et toorestore de hello de coffre Azure Recovery Services"
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
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="1ef49-103">Configurer et restaurer à partir de la rétention des sauvegardes à long terme de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1ef49-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="1ef49-104">Vous pouvez configurer des sauvegardes de base de données du coffre toostore SQL Azure hello Azure Recovery Services et puis récupérer une base de données à l’aide de sauvegardes conservée à l’aide du coffre hello hello portail Azure ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ef49-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="1ef49-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ef49-105">Azure portal</span></span>

<span data-ttu-id="1ef49-106">Hello suivant afficher des sections vous comment toouse Bonjour Azure tooconfigure portail Bonjour Azure Recovery Services coffre, afficher des sauvegardes dans le coffre hello et restaurez à partir du coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="1ef49-107">Configurer le coffre de hello, inscrire hello serveur et sélectionnez les bases de données</span><span class="sxs-lookup"><span data-stu-id="1ef49-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="1ef49-108">Vous [configurer un coffre Azure Recovery Services tooretain automatisée des sauvegardes](sql-database-long-term-retention.md) pour une période plus longue que la période de rétention hello pour votre niveau de service.</span><span class="sxs-lookup"><span data-stu-id="1ef49-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="1ef49-109">Ouvrez hello **SQL Server** page de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="1ef49-109">Open hello **SQL Server** page for your server.</span></span>

   ![page sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="1ef49-111">Cliquez sur **Long-term backup retention (Rétention des sauvegardes à long terme)**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-111">Click **Long-term backup retention**.</span></span>

   ![lien de rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="1ef49-113">Sur hello **rétention de sauvegarde à long terme** page de votre serveur, passez en revue et accepter les termes du contrat de l’aperçu de hello (sauf si vous avez déjà fait - ou cette fonctionnalité n’est plus en version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="1ef49-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![accepter les termes du contrat de la version préliminaire hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="1ef49-115">tooconfigure rétention de sauvegarde à long terme, sélectionnez cette base de données dans la grille de hello puis **configurer** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![sélectionner la base de données pour la rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="1ef49-117">Sur hello **configurer** , cliquez sur **configurer les paramètres requis** sous **le coffre de récupération service**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![lien de configuration du coffre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="1ef49-119">Sur hello **coffre Recovery services** , sélectionnez un coffre existant, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="1ef49-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="1ef49-120">Sinon, si aucun coffre recovery services trouvé pour votre abonnement, cliquez sur le flux de hello tooexit et créer un coffre recovery services.</span><span class="sxs-lookup"><span data-stu-id="1ef49-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![créer un lien vers le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="1ef49-122">Sur hello **les coffres de Services de récupération** , cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![ajouter le lien vers le coffre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="1ef49-124">Sur hello **de coffre Recovery Services** , fournissez un nom valide pour les Services de récupération hello coffre.</span><span class="sxs-lookup"><span data-stu-id="1ef49-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![nom du nouveau coffre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="1ef49-126">Sélectionnez votre abonnement et le groupe de ressources, puis emplacement hello pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="1ef49-127">Une fois que vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-127">When done, click **Create**.</span></span>

   ![créer le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="1ef49-129">coffre de Hello doit se trouver dans hello même région que le serveur logique de SQL Azure hello et doit utiliser hello même groupe de ressources que le serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="1ef49-130">Après la création de coffre hello, exécutez hello étapes nécessaires tooreturn toohello **coffre Recovery services** page.</span><span class="sxs-lookup"><span data-stu-id="1ef49-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="1ef49-131">Sur hello **coffre Recovery services** page, cliquez sur le coffre hello puis **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![sélectionner un coffre existant](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="1ef49-133">Sur hello **configurer** page, fournissez un nom valid pour la nouvelle stratégie de rétention hello, modifier la stratégie de rétention par défaut hello comme il convient, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="1ef49-135">Sur hello **rétention de sauvegarde à long terme** pour votre base de données, cliquez sur **enregistrer** puis cliquez sur **OK** tooapply hello à long terme tooall de stratégie de rétention de sauvegarde sélectionnée bases de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="1ef49-137">Cliquez sur **enregistrer** tooenable à long terme rétention de sauvegarde à l’aide de ce nouveau coffre Azure Recovery Services toohello stratégie que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="1ef49-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="1ef49-139">Une fois configuré, les sauvegardes apparaissent dans le coffre hello dans les sept prochains jours.</span><span class="sxs-lookup"><span data-stu-id="1ef49-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="1ef49-140">Ne passez pas de ce didacticiel jusqu'à ce que les sauvegardes s’afficheront dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="1ef49-141">Visualiser les sauvegardes de la rétention à long terme à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ef49-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="1ef49-142">Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="1ef49-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="1ef49-143">Dans hello portail Azure, ouvrez votre coffre Azure Recovery Services pour vos sauvegardes de base de données (passez trop**toutes les ressources** et sélectionnez-le dans la liste de hello des ressources pour votre abonnement) montant de hello tooview de stockage utilisé par votre base de données sauvegardes dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![visualiser le coffre Recovery Services avec les sauvegardes](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="1ef49-145">Ouvrez hello **base de données SQL** page de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-145">Open hello **SQL database** page for your database.</span></span>

   ![page nouvel exemple de base de données](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="1ef49-147">Dans la barre d’outils de hello, cliquez sur **restaurer**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-147">On hello toolbar, click **Restore**.</span></span>

   ![barre d’outils Restaurer](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="1ef49-149">Sur la page de restauration hello, cliquez sur **à long terme**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="1ef49-150">Sauvegardes de l’archivage Azure, cliquez sur **sélectionner une sauvegarde** tooview les sauvegardes de base de données disponible hello de rétention de sauvegarde à long terme.</span><span class="sxs-lookup"><span data-stu-id="1ef49-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![sauvegardes dans le coffre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="1ef49-152">Restaurer une base de données à partir d’une sauvegarde de la rétention à long terme des sauvegardes à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1ef49-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="1ef49-153">Vous restaurez une sauvegarde Bonjour Qu'azure Recovery Services coffre hello tooa nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="1ef49-154">Sur hello **les sauvegardes Azure coffre** page, cliquez sur toorestore de sauvegarde hello puis **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="1ef49-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![sélectionner une sauvegarde dans le coffre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="1ef49-156">Bonjour **nom de la base de données** texte Entrez le nom hello pour base de données restaurée de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![nom de la nouvelle base de données](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="1ef49-158">Cliquez sur **OK** toorestore votre base de données à partir de la sauvegarde hello hello coffre toohello nouvelle base de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="1ef49-159">Barre d’outils hello, cliquez sur hello icône tooview hello état de notification de travail de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![progression du travail de restauration à partir du coffre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="1ef49-161">Lorsque le travail de restauration hello est terminée, ouvrez hello **bases de données SQL** base de données de page tooview hello qui vient d’être restaurée.</span><span class="sxs-lookup"><span data-stu-id="1ef49-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![base de données restaurée à partir du coffre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="1ef49-163">À ce stade, vous pouvez vous connecter toohello restauré de base de données à l’aide de tâches tooperform nécessité de SQL Server Management Studio, comme trop[extraire un peu de données toocopy de base de données hello restauré dans la base de données existante hello ou existant de hello toodelete nom de base de données de base de données et existant de changement de nom hello restaurée de base de données toohello](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="1ef49-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="1ef49-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ef49-164">PowerShell</span></span>

<span data-ttu-id="1ef49-165">Hello les sections suivantes vous montrent comment toouse PowerShell tooconfigure hello Azure Recovery Services coffre, afficher des sauvegardes dans le coffre hello et restaurez à partir du coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="1ef49-166">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="1ef49-166">Create a recovery services vault</span></span>

<span data-ttu-id="1ef49-167">Hello d’utilisation [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate une récupération coffre des services.</span><span class="sxs-lookup"><span data-stu-id="1ef49-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ef49-168">coffre de Hello doit se trouver dans hello même région que le serveur logique de SQL Azure hello et doit utiliser hello même groupe de ressources que le serveur logique de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="1ef49-169">Définir votre coffre de récupération de serveur toouse hello pour ses sauvegardes de rétention à long terme</span><span class="sxs-lookup"><span data-stu-id="1ef49-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="1ef49-170">Hello d’utilisation [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate d’applet de commande créé précédemment de coffre de services de récupération avec un serveur SQL Azure spécifique.</span><span class="sxs-lookup"><span data-stu-id="1ef49-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="1ef49-171">Créer une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="1ef49-171">Create a retention policy</span></span>

<span data-ttu-id="1ef49-172">Une stratégie de rétention est où vous avez défini tookeep la durée pendant laquelle une sauvegarde de base de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="1ef49-173">Hello d’utilisation [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) applet de commande tooget hello par défaut rétention stratégie toouse en tant que modèle hello pour créer des stratégies.</span><span class="sxs-lookup"><span data-stu-id="1ef49-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="1ef49-174">Dans ce modèle, la période de rétention hello a la valeur de 2 ans.</span><span class="sxs-lookup"><span data-stu-id="1ef49-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="1ef49-175">Ensuite, exécutez hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally créer une stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="1ef49-176">Certaines applets de commande nécessitent que vous définissez le contexte de coffre hello avant d’exécuter ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) afin de voir cette applet de commande dans quelques extraits de code connexes.</span><span class="sxs-lookup"><span data-stu-id="1ef49-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="1ef49-177">Pour définir un contexte de hello, car la stratégie de hello fait partie de l’archivage de hello.</span><span class="sxs-lookup"><span data-stu-id="1ef49-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="1ef49-178">Vous pouvez créer plusieurs stratégies de rétention pour chaque archivage, puis appliquez hello souhaité stratégie toospecific bases de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="1ef49-179">Configurer une stratégie de rétention de base de données toouse hello précédemment défini</span><span class="sxs-lookup"><span data-stu-id="1ef49-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="1ef49-180">Hello d’utilisation [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) applet de commande tooapply hello nouvelle stratégie tooa base de données spécifique.</span><span class="sxs-lookup"><span data-stu-id="1ef49-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="1ef49-181">Visualiser les sauvegardes de la rétention à long terme et les informations sur les sauvegardes</span><span class="sxs-lookup"><span data-stu-id="1ef49-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="1ef49-182">Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="1ef49-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="1ef49-183">Utilisez hello informations de sauvegarde tooview applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ef49-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="1ef49-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="1ef49-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="1ef49-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="1ef49-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="1ef49-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="1ef49-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="1ef49-187">Restaurer une base de données à partir d’une sauvegarde dans la rétention des sauvegardes à long terme</span><span class="sxs-lookup"><span data-stu-id="1ef49-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="1ef49-188">Restauration à partir de la rétention de sauvegarde à long terme utilise hello [AzureRmSqlDatabase de restauration](/powershell/module/azurerm.sql/restore-azurermsqldatabase) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1ef49-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
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
> <span data-ttu-id="1ef49-189">À ce stade, vous pouvez vous connecter toohello restauration de base de données à l’aide des tâches SQL Server Management Studio tooperform nécessaire, telles que tooextract un peu de données à partir de hello restauré toocopy de la base de données dans la base de données existante hello ou base de données existante toodelete hello et changement de nom Hello base de données restaurée toohello existant nom base de données.</span><span class="sxs-lookup"><span data-stu-id="1ef49-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="1ef49-190">Consultez [Restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="1ef49-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ef49-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ef49-191">Next steps</span></span>

- <span data-ttu-id="1ef49-192">toolearn sur les sauvegardes automatiques générés par le service, consultez [sauvegardes automatiques](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="1ef49-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="1ef49-193">toolearn sur la rétention de sauvegarde à long terme, consultez [rétention de sauvegarde à long terme](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="1ef49-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="1ef49-194">toolearn sur la restauration à partir de sauvegardes, consultez [restaurer à partir de la sauvegarde](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="1ef49-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
