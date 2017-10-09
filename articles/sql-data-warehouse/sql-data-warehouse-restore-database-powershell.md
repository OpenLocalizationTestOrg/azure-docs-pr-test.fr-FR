---
title: "aaaRestore un entrepôt de données SQL Azure (PowerShell) | Documents Microsoft"
description: "Tâches PowerShell permettant de restaurer un Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Restauration d’un Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Vue d’ensemble][Overview]
> * [Portail][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

Dans cet article, vous allez apprendre comment toorestore un Azure SQL Data Warehouse à l’aide de PowerShell.

## <a name="before-you-begin"></a>Avant de commencer
**Vérifiez votre capacité de DTU.** Chaque SQL Data Warehouse est hébergé par un serveur SQL (par exemple, myserver.database.windows.net) qui dispose d’un quota DTU par défaut.  Avant de pouvoir restaurer un entrepôt de données SQL, vérifiez que hello que votre SQL server dispose d’assez restantes du quota UDBD pour base de données hello en cours de restauration. toolearn comment toocalculate DTU nécessaire ou toorequest plus DTU, consultez [demander une modification du quota DTU][Request a DTU quota change].

### <a name="install-powershell"></a>Installer PowerShell
Dans l’ordre toouse Azure PowerShell avec l’entrepôt de données SQL, vous devez tooinstall Azure PowerShell version 1.0 ou supérieure.  Vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name AzureRM**.  version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Restauration d’une base de données active ou en pause
une base de données à partir d’un instantané de toorestore utiliser hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande PowerShell.

1. Ouvrez Windows PowerShell.
2. Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.
3. Sélectionnez l’abonnement hello contenant hello toobe de base de données restaurée.
4. Hello de la liste des points de la base de données hello de restauration.
5. Choisissez un point de restauration hello souhaité à l’aide de hello RestorePointCreationDate.
6. Point de restauration toohello souhaité hello de base de données de restauration.
7. Vérifiez que cette base de données hello restaurée est en ligne.

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>restauration d’une base de données supprimée.
toorestore une base de données supprimée, utilisez hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande.

1. Ouvrez Windows PowerShell.
2. Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.
3. Sélectionnez l’abonnement hello contenant hello supprimé toobe de base de données restaurée.
4. Obtenir de la base de données spécifique de hello supprimé.
5. Restaurer la base de données de hello supprimé.
6. Vérifiez que cette base de données hello restaurée est en ligne.

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> Une fois la restauration de hello est terminée, vous pouvez configurer votre base de données récupérée en suivant [configurer votre base de données après récupération][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Restauration à partir d’une région géographique Azure
toorecover une base de données, utilisez hello [restauration-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] applet de commande.

1. Ouvrez Windows PowerShell.
2. Se connecter tooyour compte Azure et répertorier tous les abonnements hello associés à votre compte.
3. Sélectionnez l’abonnement hello contenant hello toobe de base de données restaurée.
4. Obtenir des toorecover hello base de données.
5. Créer la demande de récupération hello pour la base de données hello.
6. Vérifiez l’état hello de base de données de géo-restauration hello.

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> consultez de votre base de données après restauration de hello, tooconfigure [configurer votre base de données après récupération][Configure your database after recovery].
> 
> 

base de données récupérée Hello sera activée de chiffrement transparent des données à si la base de données source hello est activé de chiffrement transparent des données.

## <a name="next-steps"></a>Étapes suivantes
toolearn sur les fonctionnalités de continuité d’activité d’entreprise hello des éditions de base de données SQL Azure, lisez hello [vue d’ensemble de base de données SQL Azure business la continuité des activités][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
