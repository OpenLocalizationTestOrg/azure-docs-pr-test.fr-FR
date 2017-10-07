---
title: "aaaImport un fichier BACPAC fichier toocreate une base de données SQL Azure | Documents Microsoft"
description: "Créez une base de données SQL Azure en important un fichier BACPAC."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a>Importer un tooa de fichier BACPAC nouvelle base de données de SQL Azure

Lorsque vous avez besoin d’une base de données à partir d’une archive de tooimport ou lors de la migration à partir d’une autre plateforme, vous pouvez importer des schémas hello et les données à partir d’un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) fichier. Un fichier BACPAC est un fichier ZIP avec une extension de fichier BACPAC qui contient les métadonnées de hello et les données à partir d’une base de données SQL Server. Il peut être importé à partir du Stockage Blob Azure (stockage standard uniquement) ou à partir du stockage local dans un emplacement local. vitesse d’importation toomaximize hello, nous recommandons que vous spécifiez des performances et le niveau de niveau de service, par exemple un P6 et puis mettre à l’échelle toodown selon une fois l’importation de hello réussie. En outre, le niveau de compatibilité de base de données hello après l’importation de hello est basé sur le niveau de compatibilité hello de base de données source hello. 

> [!IMPORTANT] 
> Après avoir migré votre tooAzure de base de données de la base de données SQL, vous pouvez choisir la base de données toooperate hello à son niveau de compatibilité actuel (niveau 100 pour la base de données AdventureWorks2008R2 hello) ou à un niveau supérieur. Pour plus d’informations sur les implications en matière de hello et les options pour l’exploitation d’une base de données à un niveau de compatibilité spécifiques, consultez [niveau de compatibilité ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Voir aussi [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) pour plus d’informations sur les paramètres de niveau de base de données supplémentaires liées toocompatibility niveaux.   >

> [!NOTE]
> tooimport un BACPAC tooa nouvelle base de données, vous devez d’abord créer un serveur logique de base de données SQL Azure. Pour obtenir un didacticiel montrant comment toomigrate un serveur SQL Server de base de données tooAzure base de données SQL à l’aide de SQLPackage, consultez [migrer une base de données SQL Server](sql-database-migrate-your-sql-server-database.md)
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a>Importation à partir d’un fichier BACPAC à l’aide du portail Azure

Cet article fournit des instructions pour la création d’une base de données SQL Azure à partir d’un fichier BACPAC stocké dans le stockage blob Azure à l’aide de hello [portail Azure](https://portal.azure.com). Importation à l’aide de hello uniquement le portail Azure prend en charge l’importation d’un fichier BACPAC à partir du stockage d’objets blob Azure.

une base de données à l’aide de tooimport hello portail Azure, page hello ouvert pour votre base de données cliquez sur **importation** sur la barre d’outils hello. Spécifiez le compte de stockage hello et un conteneur et sélectionnez hello BACPAC fichier tooimport. Sélectionnez la taille de base de données hello hello (généralement hello même origine) et fournissent des informations d’identification de SQL Server de destination hello.  

   ![Importation de base de données](./media/sql-database-import/import.png)

progression de hello toomonitor Hello l’opération d’importation, ouvrez une page hello pour hello serveur logique contenant hello de base de données en cours d’importation. Faites défiler la liste trop**Operations** puis cliquez sur **Import/Export** l’historique.

### <a name="monitor-hello-progress-of-an-import-operation"></a>Surveiller la progression d’une opération d’importation hello

progression de hello toomonitor Hello l’opération d’importation, ouvrez une page hello pour hello serveur logique dans le hello base de données est en cours d’importation importé. Faites défiler la liste trop**Operations** puis cliquez sur **Import/Export** l’historique.
   
   ![importer](./media/sql-database-import/import-history.png)![état d’importation](./media/sql-database-import/import-status.png)

base de données tooverify hello est actif sur le serveur de hello, cliquez sur **bases de données SQL** et vérifiez que la nouvelle base de données hello **Online**.

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a>Importer à partir d’un fichier BACPAC à l’aide de SQLPackage

tooimport SQL de base de données à l’aide de hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitaire de ligne de commande, consultez [importer les paramètres et les propriétés](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties). Hello SQLPackage utilitaire est fourni avec les versions les plus récentes de hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) et [SQL Server Data Tools pour Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou vous pouvez télécharger la version la plus récente de hello [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directement hello Microsoft Centre de téléchargement.

Nous vous recommandons d’utiliser hello Hello SQLPackage utilitaire pour l’évolutivité et de performances dans la plupart des environnements de production. Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Consultez hello commande SQLPackage pour un exemple de script de la façon suivante tooimport hello **AdventureWorks2008R2** base de données à partir du stockage local tooan base de données SQL Azure serveur logique, appelée **mynewserver20170403** dans cet exemple. Ce script illustre la création d’une base de données appelée hello **myMigratedDatabase**, avec un niveau de service de **Premium**et un objectif de Service de **P6**. Modifiez ces valeurs comme environnement de tooyour appropriée.

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importer sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Un serveur logique Azure SQL Database écoute sur le port 1433. Si vous essayez de tooconnect tooan base de données SQL Azure serveur logique au sein d’un pare-feu d’entreprise, ce port doit être ouvert dans le pare-feu d’entreprise hello pour toosuccessfully de vous connecter.
>

Cet exemple montre comment tooimport une base de données à l’aide de SqlPackage.exe avec l’authentification universelle Active Directory :

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a>Importer à partir d’un fichier BACPAC à l’aide de PowerShell

Hello d’utilisation [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit de l’applet de commande un toohello de requête de base de données importation service de base de données SQL Azure. Selon la taille de hello de votre base de données, opération d’importation hello peut prendre quelques toocomplete de temps.

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

état de hello toocheck Hello la demande d’importation, utilisez hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) applet de commande. Cela exécute immédiatement après hello demande généralement retourne **état : InProgress**. Lorsque vous consultez **état : a réussi** hello l’importation est terminée.

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
Pour un autre exemple de script, consultez [Importation d’une base de données à partir d’un fichier BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).

## <a name="next-steps"></a>Étapes suivantes
* toolearn tooconnect tooand interroger une base de données SQL importée, voir [connecter tooSQL de base de données avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md).
* Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Pour en savoir plus sur hello entière SQL Server de base de données du processus de migration, y compris les recommandations relatives aux performances, consultez [migrer un tooAzure de base de données SQL Server de la base de données SQL](sql-database-cloud-migrate.md).



