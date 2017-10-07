---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (PowerShell) | Documents Microsoft"
description: "PowerShell tâches toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a>Gestion de la puissance de calcul dans Azure SQL Data Warehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Vue d'ensemble](sql-data-warehouse-manage-compute-overview.md)
> * [Portail](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a>Avant de commencer
### <a name="install-hello-latest-version-of-azure-powershell"></a>Installer la version la plus récente d’Azure PowerShell hello
> [!NOTE]
> toouse Azure PowerShell avec l’entrepôt de données SQL, vous avez besoin d’Azure PowerShell version 1.0.3 ou supérieur.  exécution de votre version actuelle de tooverify commande hello **Get-Module - ListAvailable-nom Azure**. Vous pouvez installer la version la plus récente à partir de hello [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a>Prise en main des applets de commande Azure PowerShell
tooget démarré :

1. Ouvrez Azure PowerShell.
2. À l’invite de PowerShell hello, exécutez toosign de ces commandes dans toohello Azure Resource Manager et sélectionnez votre abonnement.

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a>Mise à l’échelle de la puissance de calcul
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange hello Dwu, utilisez hello [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] applet de commande PowerShell. Hello exemple suivant définit hello service niveau objectif tooDW1000 pour la base de données de hello MySQLDW qui est hébergé sur le serveur monserveur.

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Suspension du calcul
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause une base de données, utilisez hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] applet de commande. Hello exemple suivant suspend une base de données appelé base de données02 hébergé sur un serveur nommé Server01. serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.

> [!NOTE]
> Notez que si votre serveur est foo.database.windows.net, utilisez « foo » comme hello - nom du serveur dans les applets de commande PowerShell hello.
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
Une variation, l’exemple suivant récupère la base de données hello en objet de hello $database. Elle redirige ensuite les objets hello trop[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]. résultats de Hello sont stockés dans resultDatabase d’objet hello. commande finale Hello montre les résultats de hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Reprise du calcul
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

toostart une base de données, utilisez hello [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] applet de commande. Hello exemple suivant démarre une base de données appelé base de données02 hébergé sur un serveur nommé Server01. serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

Une variation, l’exemple suivant récupère la base de données hello en objet de hello $database. Elle redirige ensuite les objets hello trop[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] et stocke les résultats de hello dans $resultDatabase. commande finale Hello montre les résultats de hello.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a>Vérifier l’état de base de données

Comme indiqué dans hello exemples ci-dessus, un utilisateur peut employer [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] applet de commande tooget plus d’informations sur une base de données, ainsi la vérification hello l’état, mais également toouse en tant qu’argument. 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

De qui donnera quelque chose comme ceci 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

Où vous pouvez ensuite vérifier toosee hello *état* de base de données hello. Dans ce cas, vous pouvez voir que la base de données est en ligne. 

Lorsque vous exécutez cette commande, vous devriez recevoir une valeur d’état En ligne, Suspension, Reprise, Mise à l’échelle ou Suspendu.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Étapes suivantes
Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
