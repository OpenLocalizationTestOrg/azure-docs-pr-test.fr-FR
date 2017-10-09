---
title: "aaaExport un fichier BACPAC de tooa de base de données SQL Azure | Documents Microsoft"
description: "Exporter un fichier BACPAC SQL Azure de base de données tooa à l’aide de hello portail Azure"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 41d63a97-37db-4e40-b652-77c2fd1c09b7
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: cb3b4227318e0fd2114529c86c9792615fe7fd1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-sql-database-tooa-bacpac-file"></a>Exporter un fichier BACPAC de tooa de base de données SQL Azure

Lorsque vous devez tooexport une base de données d’archivage ou pour la plateforme de tooanother mobile, vous pouvez exporter tooa de schéma et les données de la base de données hello [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) fichier. Un fichier BACPAC est un fichier ZIP avec une extension de fichier BACPAC qui contient les métadonnées de hello et les données à partir d’une base de données SQL Server. Il peut être stocké dans le Stockage Blob Azure ou un stockage local dans un emplacement local, puis importé dans Azure SQL Database ou une installation locale SQL Server. 

> [!IMPORTANT] 
> L’exportation automatisée Azure SQL Database a été retirée le 1er mars 2017. Vous pouvez utiliser [rétention de sauvegarde à long terme](sql-database-long-term-retention.md
) ou [Azure Automation](https://github.com/Microsoft/azure-docs-pr/blob/2461f706f8fc1150e69312098640c0676206a531/articles/automation/automation-intro.md) bases de données SQL d’archive tooperiodically à l’aide de PowerShell selon planification tooa de votre choix. Pour obtenir un exemple, téléchargez hello [exemple de script PowerShell](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export) à partir de Github.
>

## <a name="considerations-when-exporting-an-azure-sql-database"></a>Considérations à prendre en compte lors de l’exportation d’une base de données SQL Azure

* Pour une exportation toobe cohérente, vous devez vous assurer qu’aucune activité d’écriture ne se produit lors de l’exportation de hello, ou que vous exportez à partir d’un [copie transactionnellement cohérente](sql-database-copy.md) de votre base de données SQL Azure.
* Si vous exportez tooblob stockage, taille maximale de hello d’un fichier BACPAC est de 200 Go. tooarchive un fichier BACPAC plus volumineux, exportez toolocal stockage.
* Exportation d’un stockage de premium de tooAzure de fichier BACPAC à l’aide de méthodes de hello présentées dans cet article n’est pas prise en charge.
* Si l’opération d’exportation à partir de la base de données SQL Azure hello dépasse 20 heures, il peut être annulé. tooincrease des performances lors de l’exportation, vous pouvez :
  * Augmentez temporairement votre niveau de service.
  * Cesser de tous les lire et écrire des activités lors de l’exportation de hello.
  * Utilisez un [index cluster](https://msdn.microsoft.com/library/ms190457.aspx) avec des valeurs non nulles sur toutes les tables de grande taille. Sans index cluster, une exportation peut échouer si elle dure plus de 6 à 12 heures. Il s’agit, car le service d’exportation hello doit toocomplete une table entière de table analyse tootry tooexport. Un toodetermine efficace si vos tables sont optimisés pour l’exportation est toorun **DBCC SHOW_STATISTICS** et assurez-vous que hello *RANGE_HI_KEY* n’est pas null et sa valeur est une bonne distribution. Pour plus d’informations, consultez [DBCC SHOW_STATISTICS](https://msdn.microsoft.com/library/ms174384.aspx).

> [!NOTE]
> Fichiers Bacpac n’est pas prévu toobe utilisé pour les opérations de sauvegarde et de restauration. La base de données SQL Azure crée automatiquement des sauvegardes pour chaque base de données utilisateur. Pour plus d’informations, consultez [Vue d’ensemble de la continuité de l’activité avec la base de données SQL Azure](sql-database-business-continuity.md) et [Découvrir les sauvegardes SQL Database](sql-database-automated-backups.md).  
> 

## <a name="export-tooa-bacpac-file-using-hello-azure-portal"></a>Exporter le fichier BACPAC tooa à l’aide de hello portail Azure

une base de données à l’aide de tooexport hello [portail Azure](https://portal.azure.com), ouvrez la page hello pour votre base de données, cliquez sur **exporter** sur la barre d’outils hello. Spécifiez le nom de fichier BACPAC hello et fournir le compte de stockage Azure hello et conteneur pour l’exportation de hello hello informations d’identification tooconnect toohello source de base de données.  

![Exportation de base de données](./media/sql-database-export/database-export.png)

progression de hello toomonitor Hello l’opération d’exportation, ouvrez une page hello pour hello serveur logique contenant hello de base de données en cours d’exportation. Faites défiler la liste trop**Operations** puis cliquez sur **Import/Export** l’historique.

![exporter l’historique](./media/sql-database-export/export-history.png)
![exporter l’état de l’historique](./media/sql-database-export/export-history2.png)

## <a name="export-tooa-bacpac-file-using-hello-sqlpackage-utility"></a>Exporter le fichier BACPAC tooa à l’aide d’utilitaire de SQLPackage hello

tooexport SQL de base de données à l’aide de hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitaire de ligne de commande, consultez [exporter les paramètres et les propriétés](https://msdn.microsoft.com/library/hh550080.aspx#Export Parameters and Properties). Hello SQLPackage utilitaire est fourni avec les versions les plus récentes de hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) et [SQL Server Data Tools pour Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou vous pouvez télécharger la version la plus récente de hello [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directement hello Microsoft Centre de téléchargement.

Nous vous recommandons d’utiliser hello Hello SQLPackage utilitaire pour l’évolutivité et de performances dans la plupart des environnements de production. Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

Cet exemple montre comment tooexport une base de données à l’aide de SqlPackage.exe avec l’authentification universelle Active Directory :

```cmd
SqlPackage.exe /a:Export /tf:testExport.bacpac /scs:"Data Source=apptestserver.database.windows.net;Initial Catalog=MyDB;" /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="export-tooa-bacpac-file-using-sql-server-management-studio-ssms"></a>Exporter le fichier BACPAC tooa à l’aide de SQL Server Management Studio (SSMS)

versions les plus récentes de SQL Server Management Studio Hello fournissent également un Assistant tooexport un fichier BACPAC de tooa de base de données SQL Azure. Consultez hello [exporter une Application de couche données](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application).

## <a name="export-tooa-bacpac-file-using-powershell"></a>Exporter le fichier BACPAC tooa à l’aide de PowerShell

Hello d’utilisation [New-AzureRmSqlDatabaseExport](/powershell/module/azurerm.sql/new-azurermsqldatabaseexport) toosubmit de l’applet de commande un toohello de demande exportation de base de données service de base de données SQL Azure. Selon la taille de hello de votre base de données, l’opération d’exportation hello peut prendre quelques toocomplete de temps.

 ```powershell
 $exportRequest = New-AzureRmSqlDatabaseExport -ResourceGroupName $ResourceGroupName -ServerName $ServerName `
   -DatabaseName $DatabaseName -StorageKeytype $StorageKeytype -StorageKey $StorageKey -StorageUri $BacpacUri `
   -AdministratorLogin $creds.UserName -AdministratorLoginPassword $creds.Password
 ```

état de hello toocheck Hello demande d’exportation, utilisez hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) applet de commande. Cela exécute immédiatement après hello demande généralement retourne **état : InProgress**. Lorsque vous consultez **état : a réussi** hello exportation est terminée.

```powershell
$exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
[Console]::Write("Exporting")
while ($exportStatus.Status -eq "InProgress")
{
    $exportStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $exportRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$exportStatus
```

## <a name="next-steps"></a>Étapes suivantes

* toolearn sur la rétention de sauvegarde à long terme d’une sauvegarde de base de données SQL Azure en tant qu’une autre tooexported une base de données à des fins d’archivage, consultez [rétention de sauvegarde à long terme](sql-database-long-term-retention.md).
- Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* toolearn sur l’importation d’une base de données BACPAC tooa SQL Server, consultez [importer une base de données SQL Server de tooa BACPCAC](https://msdn.microsoft.com/library/hh710052.aspx).
* toolearn sur l’exportation d’un fichier BACPAC à partir d’une base de données SQL Server, consultez [exporter une Application de couche données](https://docs.microsoft.com/sql/relational-databases/data-tier-applications/export-a-data-tier-application) et [migrer votre première base de données](sql-database-migrate-your-sql-server-database.md).
* Si vous exportez à partir de SQL Server comme un tooAzure de toomigration prélude base de données SQL, consultez [migrer un tooAzure de base de données SQL Server de la base de données SQL](sql-database-cloud-migrate.md).
