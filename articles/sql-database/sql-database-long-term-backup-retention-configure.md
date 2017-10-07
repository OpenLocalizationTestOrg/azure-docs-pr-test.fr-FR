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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>Configurer et restaurer à partir de la rétention des sauvegardes à long terme de base de données SQL Azure

Vous pouvez configurer des sauvegardes de base de données du coffre toostore SQL Azure hello Azure Recovery Services et puis récupérer une base de données à l’aide de sauvegardes conservée à l’aide du coffre hello hello portail Azure ou PowerShell.

## <a name="azure-portal"></a>Portail Azure

Hello suivant afficher des sections vous comment toouse Bonjour Azure tooconfigure portail Bonjour Azure Recovery Services coffre, afficher des sauvegardes dans le coffre hello et restaurez à partir du coffre de hello.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Configurer le coffre de hello, inscrire hello serveur et sélectionnez les bases de données

Vous [configurer un coffre Azure Recovery Services tooretain automatisée des sauvegardes](sql-database-long-term-retention.md) pour une période plus longue que la période de rétention hello pour votre niveau de service. 

1. Ouvrez hello **SQL Server** page de votre serveur.

   ![page sql server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Cliquez sur **Long-term backup retention (Rétention des sauvegardes à long terme)**.

   ![lien de rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. Sur hello **rétention de sauvegarde à long terme** page de votre serveur, passez en revue et accepter les termes du contrat de l’aperçu de hello (sauf si vous avez déjà fait - ou cette fonctionnalité n’est plus en version préliminaire).

   ![accepter les termes du contrat de la version préliminaire hello](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure rétention de sauvegarde à long terme, sélectionnez cette base de données dans la grille de hello puis **configurer** sur la barre d’outils hello.

   ![sélectionner la base de données pour la rétention des sauvegardes à long terme](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. Sur hello **configurer** , cliquez sur **configurer les paramètres requis** sous **le coffre de récupération service**.

   ![lien de configuration du coffre](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. Sur hello **coffre Recovery services** , sélectionnez un coffre existant, le cas échéant. Sinon, si aucun coffre recovery services trouvé pour votre abonnement, cliquez sur le flux de hello tooexit et créer un coffre recovery services.

   ![créer un lien vers le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. Sur hello **les coffres de Services de récupération** , cliquez sur **ajouter**.

   ![ajouter le lien vers le coffre](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. Sur hello **de coffre Recovery Services** , fournissez un nom valide pour les Services de récupération hello coffre.

   ![nom du nouveau coffre](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Sélectionnez votre abonnement et le groupe de ressources, puis emplacement hello pour le coffre hello. Une fois que vous avez terminé, cliquez sur **Créer**.

   ![créer le coffre](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > coffre de Hello doit se trouver dans hello même région que le serveur logique de SQL Azure hello et doit utiliser hello même groupe de ressources que le serveur logique de hello.
   >

10. Après la création de coffre hello, exécutez hello étapes nécessaires tooreturn toohello **coffre Recovery services** page.

11. Sur hello **coffre Recovery services** page, cliquez sur le coffre hello puis **sélectionnez**.

   ![sélectionner un coffre existant](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. Sur hello **configurer** page, fournissez un nom valid pour la nouvelle stratégie de rétention hello, modifier la stratégie de rétention par défaut hello comme il convient, puis cliquez sur **OK**.

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Sur hello **rétention de sauvegarde à long terme** pour votre base de données, cliquez sur **enregistrer** puis cliquez sur **OK** tooapply hello à long terme tooall de stratégie de rétention de sauvegarde sélectionnée bases de données.

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Cliquez sur **enregistrer** tooenable à long terme rétention de sauvegarde à l’aide de ce nouveau coffre Azure Recovery Services toohello stratégie que vous avez configuré.

   ![définir la stratégie de rétention](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Une fois configuré, les sauvegardes apparaissent dans le coffre hello dans les sept prochains jours. Ne passez pas de ce didacticiel jusqu'à ce que les sauvegardes s’afficheront dans le coffre hello.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Visualiser les sauvegardes de la rétention à long terme à l’aide du portail Azure

Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md). 

1. Dans hello portail Azure, ouvrez votre coffre Azure Recovery Services pour vos sauvegardes de base de données (passez trop**toutes les ressources** et sélectionnez-le dans la liste de hello des ressources pour votre abonnement) montant de hello tooview de stockage utilisé par votre base de données sauvegardes dans le coffre hello.

   ![visualiser le coffre Recovery Services avec les sauvegardes](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Ouvrez hello **base de données SQL** page de votre base de données.

   ![page nouvel exemple de base de données](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Dans la barre d’outils de hello, cliquez sur **restaurer**.

   ![barre d’outils Restaurer](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Sur la page de restauration hello, cliquez sur **à long terme**.

5. Sauvegardes de l’archivage Azure, cliquez sur **sélectionner une sauvegarde** tooview les sauvegardes de base de données disponible hello de rétention de sauvegarde à long terme.

   ![sauvegardes dans le coffre](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Restaurer une base de données à partir d’une sauvegarde de la rétention à long terme des sauvegardes à l’aide de hello portail Azure

Vous restaurez une sauvegarde Bonjour Qu'azure Recovery Services coffre hello tooa nouvelle base de données.

1. Sur hello **les sauvegardes Azure coffre** page, cliquez sur toorestore de sauvegarde hello puis **sélectionnez**.

   ![sélectionner une sauvegarde dans le coffre](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. Bonjour **nom de la base de données** texte Entrez le nom hello pour base de données restaurée de hello.

   ![nom de la nouvelle base de données](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Cliquez sur **OK** toorestore votre base de données à partir de la sauvegarde hello hello coffre toohello nouvelle base de données.

4. Barre d’outils hello, cliquez sur hello icône tooview hello état de notification de travail de restauration hello.

   ![progression du travail de restauration à partir du coffre](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Lorsque le travail de restauration hello est terminée, ouvrez hello **bases de données SQL** base de données de page tooview hello qui vient d’être restaurée.

   ![base de données restaurée à partir du coffre](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> À ce stade, vous pouvez vous connecter toohello restauré de base de données à l’aide de tâches tooperform nécessité de SQL Server Management Studio, comme trop[extraire un peu de données toocopy de base de données hello restauré dans la base de données existante hello ou existant de hello toodelete nom de base de données de base de données et existant de changement de nom hello restaurée de base de données toohello](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Hello les sections suivantes vous montrent comment toouse PowerShell tooconfigure hello Azure Recovery Services coffre, afficher des sauvegardes dans le coffre hello et restaurez à partir du coffre de hello.

### <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

Hello d’utilisation [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate une récupération coffre des services.

> [!IMPORTANT]
> coffre de Hello doit se trouver dans hello même région que le serveur logique de SQL Azure hello et doit utiliser hello même groupe de ressources que le serveur logique de hello.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Définir votre coffre de récupération de serveur toouse hello pour ses sauvegardes de rétention à long terme

Hello d’utilisation [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) tooassociate d’applet de commande créé précédemment de coffre de services de récupération avec un serveur SQL Azure spécifique.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Créer une stratégie de rétention

Une stratégie de rétention est où vous avez défini tookeep la durée pendant laquelle une sauvegarde de base de données. Hello d’utilisation [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) applet de commande tooget hello par défaut rétention stratégie toouse en tant que modèle hello pour créer des stratégies. Dans ce modèle, la période de rétention hello a la valeur de 2 ans. Ensuite, exécutez hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally créer une stratégie de hello. 

> [!NOTE]
> Certaines applets de commande nécessitent que vous définissez le contexte de coffre hello avant d’exécuter ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) afin de voir cette applet de commande dans quelques extraits de code connexes. Pour définir un contexte de hello, car la stratégie de hello fait partie de l’archivage de hello. Vous pouvez créer plusieurs stratégies de rétention pour chaque archivage, puis appliquez hello souhaité stratégie toospecific bases de données. 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Configurer une stratégie de rétention de base de données toouse hello précédemment défini

Hello d’utilisation [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) applet de commande tooapply hello nouvelle stratégie tooa base de données spécifique.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Visualiser les sauvegardes de la rétention à long terme et les informations sur les sauvegardes

Visualisez les informations relatives à vos sauvegardes de base de données dans la [rétention des sauvegardes à long terme](sql-database-long-term-retention.md). 

Utilisez hello informations de sauvegarde tooview applets de commande suivantes :

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Restaurer une base de données à partir d’une sauvegarde dans la rétention des sauvegardes à long terme

Restauration à partir de la rétention de sauvegarde à long terme utilise hello [AzureRmSqlDatabase de restauration](/powershell/module/azurerm.sql/restore-azurermsqldatabase) applet de commande.

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
> À ce stade, vous pouvez vous connecter toohello restauration de base de données à l’aide des tâches SQL Server Management Studio tooperform nécessaire, telles que tooextract un peu de données à partir de hello restauré toocopy de la base de données dans la base de données existante hello ou base de données existante toodelete hello et changement de nom Hello base de données restaurée toohello existant nom base de données. Consultez [Restauration dans le temps](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Étapes suivantes

- toolearn sur les sauvegardes automatiques générés par le service, consultez [sauvegardes automatiques](sql-database-automated-backups.md)
- toolearn sur la rétention de sauvegarde à long terme, consultez [rétention de sauvegarde à long terme](sql-database-long-term-retention.md)
- toolearn sur la restauration à partir de sauvegardes, consultez [restaurer à partir de la sauvegarde](sql-database-recovery-using-backups.md)
