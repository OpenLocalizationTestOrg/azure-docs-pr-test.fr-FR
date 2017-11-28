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
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a><span data-ttu-id="d39a3-103">Applets de commande PowerShell et API REST pour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d39a3-103">PowerShell cmdlets and REST APIs for SQL Data Warehouse</span></span>
<span data-ttu-id="d39a3-104">De nombreuses tâches d’administration de SQL Data Warehouse peuvent être gérées à l’aide d’applets de commande Azure PowerShell ou d’API REST.</span><span class="sxs-lookup"><span data-stu-id="d39a3-104">Many SQL Data Warehouse administration tasks can be managed using either Azure PowerShell cmdlets or REST APIs.</span></span>  <span data-ttu-id="d39a3-105">Voici quelques exemples de fonctionnement des commandes toouse PowerShell tooautomate des tâches courantes dans votre entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="d39a3-105">Below are some examples of how toouse PowerShell commands tooautomate common tasks in your SQL Data Warehouse.</span></span>  <span data-ttu-id="d39a3-106">Pour certains exemples REST, consultez l’article de hello [gérer l’évolutivité avec reste][Manage scalability with REST].</span><span class="sxs-lookup"><span data-stu-id="d39a3-106">For some good REST examples, see hello article [Manage scalability with REST][Manage scalability with REST].</span></span>

> [!NOTE]
> <span data-ttu-id="d39a3-107">Dans l’ordre toouse Azure PowerShell avec l’entrepôt de données SQL, vous avez besoin d’Azure PowerShell version 1.0.3 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="d39a3-107">In order toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="d39a3-108">Vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="d39a3-108">You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="d39a3-109">version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="d39a3-109">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="d39a3-110">Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="d39a3-110">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="d39a3-111">Prise en main des applets de commande Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d39a3-111">Get started with Azure PowerShell cmdlets</span></span>
1. <span data-ttu-id="d39a3-112">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d39a3-112">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="d39a3-113">À l’invite de PowerShell hello, exécutez toosign de ces commandes dans toohello Azure Resource Manager et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d39a3-113">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a><span data-ttu-id="d39a3-114">Exemple : suspendre une base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d39a3-114">Pause SQL Data Warehouse Example</span></span>
<span data-ttu-id="d39a3-115">Une base de données appelée « Database02 » et hébergée sur un serveur appelé « Server01 » est interrompue.</span><span class="sxs-lookup"><span data-stu-id="d39a3-115">Pause a database named "Database02" hosted on a server named "Server01."</span></span>  <span data-ttu-id="d39a3-116">serveur de Hello est dans un groupe de ressources Azure nommé « ResourceGroup1 ».</span><span class="sxs-lookup"><span data-stu-id="d39a3-116">hello server is in an Azure resource group named "ResourceGroup1."</span></span>

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="d39a3-117">Une variation, cet exemple canalise hello récupérée objet trop[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="d39a3-117">A variation, this example pipes hello retrieved object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span>  <span data-ttu-id="d39a3-118">Par conséquent, la base de données hello est suspendu.</span><span class="sxs-lookup"><span data-stu-id="d39a3-118">As a result, hello database is paused.</span></span> <span data-ttu-id="d39a3-119">commande finale Hello montre les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="d39a3-119">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a><span data-ttu-id="d39a3-120">Exemple : démarrer une base de données SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d39a3-120">Start SQL Data Warehouse Example</span></span>
<span data-ttu-id="d39a3-121">Les opérations d’une base de données appelée « Database02 » et hébergée sur un serveur « Server01 » sont reprises.</span><span class="sxs-lookup"><span data-stu-id="d39a3-121">Resume operation of a database named "Database02" hosted on a server named "Server01."</span></span> <span data-ttu-id="d39a3-122">serveur de Hello est contenue dans un groupe de ressources nommé « ResourceGroup1 ».</span><span class="sxs-lookup"><span data-stu-id="d39a3-122">hello server is contained in a resource group named "ResourceGroup1."</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="d39a3-123">Une variante, dans cet exemple une base de données appelée « Database02 » est récupérée d’un serveur appelé « Server01 » hébergé dans un groupe de ressources appelé « ResourceGroup1 ».</span><span class="sxs-lookup"><span data-stu-id="d39a3-123">A variation, this example retrieves a database named "Database02" from a server named "Server01" that is contained in a resource group named "ResourceGroup1."</span></span> <span data-ttu-id="d39a3-124">Elle dirige hello récupérée objet trop[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="d39a3-124">It pipes hello retrieved object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> <span data-ttu-id="d39a3-125">Notez que si votre serveur est foo.database.windows.net, utilisez « foo » comme hello - nom du serveur dans les applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d39a3-125">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
> 
> 

## <a name="other-supported-powershell-cmdlets"></a><span data-ttu-id="d39a3-126">Autres applets de commande PowerShell prises en charge</span><span class="sxs-lookup"><span data-stu-id="d39a3-126">Other supported PowerShell cmdlets</span></span>
<span data-ttu-id="d39a3-127">Ces applets de commande PowerShell sont prises en charge avec Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d39a3-127">These PowerShell cmdlets are supported with Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="d39a3-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-128">[Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span><span class="sxs-lookup"><span data-stu-id="d39a3-129">[Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]</span></span>
* <span data-ttu-id="d39a3-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span><span class="sxs-lookup"><span data-stu-id="d39a3-130">[Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]</span></span>
* <span data-ttu-id="d39a3-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-131">[New-AzureRmSqlDatabase][New-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-132">[Remove-AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-133">[Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-134">[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span><span class="sxs-lookup"><span data-stu-id="d39a3-135">[Select-AzureRmSubscription][Select-AzureRmSubscription]</span></span>
* <span data-ttu-id="d39a3-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-136">[Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]</span></span>
* <span data-ttu-id="d39a3-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span><span class="sxs-lookup"><span data-stu-id="d39a3-137">[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]</span></span>

## <a name="next-steps"></a><span data-ttu-id="d39a3-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d39a3-138">Next steps</span></span>
<span data-ttu-id="d39a3-139">Pour plus d’exemples PowerShell, consultez :</span><span class="sxs-lookup"><span data-stu-id="d39a3-139">For more PowerShell examples, see:</span></span>

* <span data-ttu-id="d39a3-140">[Création de SQL Data Warehouse à l’aide de PowerShell][Create a SQL Data Warehouse using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="d39a3-140">[Create a SQL Data Warehouse using PowerShell][Create a SQL Data Warehouse using PowerShell]</span></span>
* <span data-ttu-id="d39a3-141">[Restauration de base de données][Database restore]</span><span class="sxs-lookup"><span data-stu-id="d39a3-141">[Database restore][Database restore]</span></span>

<span data-ttu-id="d39a3-142">Pour d’autres tâches pouvant être automatisées avec PowerShell, consultez [Applets de commande d’Azure SQL Database][Azure SQL Database Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="d39a3-142">For other tasks which can be automated with PowerShell, see [Azure SQL Database Cmdlets][Azure SQL Database Cmdlets].</span></span> <span data-ttu-id="d39a3-143">Notez que certaines applets de commande d’Azure SQL Database ne sont pas prises en charge pour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d39a3-143">Note that not all Azure SQL Database cmdlets are supported for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="d39a3-144">Pour obtenir la liste des tâches pouvant être automatisées avec REST, consultez [Opérations pour Azure SQL Database][Operations for Azure SQL Databases].</span><span class="sxs-lookup"><span data-stu-id="d39a3-144">For a list of tasks which can be automated with REST, see [Operations for Azure SQL Databases][Operations for Azure SQL Databases].</span></span>

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
