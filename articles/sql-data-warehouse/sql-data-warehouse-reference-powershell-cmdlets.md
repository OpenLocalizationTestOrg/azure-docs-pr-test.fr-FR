---
title: applets de commande aaaPowerShell pour Azure SQL Data Warehouse
description: "Rechercher les applets de commande PowerShell supérieur hello pour Azure SQL Data Warehouse notamment toopause et reprendre une base de données."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>Applets de commande PowerShell et API REST pour SQL Data Warehouse
De nombreuses tâches d’administration de SQL Data Warehouse peuvent être gérées à l’aide d’applets de commande Azure PowerShell ou d’API REST.  Voici quelques exemples de fonctionnement des commandes toouse PowerShell tooautomate des tâches courantes dans votre entrepôt de données SQL.  Pour certains exemples REST, consultez l’article de hello [gérer l’évolutivité avec reste][Manage scalability with REST].

> [!NOTE]
> Dans l’ordre toouse Azure PowerShell avec l’entrepôt de données SQL, vous avez besoin d’Azure PowerShell version 1.0.3 ou supérieur.  Vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name Azure**.  version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Prise en main des applets de commande Azure PowerShell
1. Ouvrez Windows PowerShell.
2. À l’invite de PowerShell hello, exécutez toosign de ces commandes dans toohello Azure Resource Manager et sélectionnez votre abonnement.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Exemple : suspendre une base de données SQL Data Warehouse
Une base de données appelée « Database02 » et hébergée sur un serveur appelé « Server01 » est interrompue.  serveur de Hello est dans un groupe de ressources Azure nommé « ResourceGroup1 ».

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Une variation, cet exemple canalise hello récupérée objet trop[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  Par conséquent, la base de données hello est suspendu. commande finale Hello montre les résultats de hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Exemple : démarrer une base de données SQL Data Warehouse
Les opérations d’une base de données appelée « Database02 » et hébergée sur un serveur « Server01 » sont reprises. serveur de Hello est contenue dans un groupe de ressources nommé « ResourceGroup1 ».

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Une variante, dans cet exemple une base de données appelée « Database02 » est récupérée d’un serveur appelé « Server01 » hébergé dans un groupe de ressources appelé « ResourceGroup1 ». Elle dirige hello récupérée objet trop[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Notez que si votre serveur est foo.database.windows.net, utilisez « foo » comme hello - nom du serveur dans les applets de commande PowerShell hello.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Autres applets de commande PowerShell prises en charge
Ces applets de commande PowerShell sont prises en charge avec Azure SQL Data Warehouse.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [Select-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’exemples PowerShell, consultez :

* [Création de SQL Data Warehouse à l’aide de PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Restauration de base de données][Database restore]

Pour d’autres tâches pouvant être automatisées avec PowerShell, consultez [Applets de commande d’Azure SQL Database][Azure SQL Database Cmdlets]. Notez que certaines applets de commande d’Azure SQL Database ne sont pas prises en charge pour Azure SQL Data Warehouse.  Pour obtenir la liste des tâches pouvant être automatisées avec REST, consultez [Opérations pour Azure SQL Database][Operations for Azure SQL Databases].

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
