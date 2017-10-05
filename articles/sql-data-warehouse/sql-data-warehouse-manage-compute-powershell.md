---
title: Gestion de la puissance de calcul dans Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
description: "Tâches PowerShell permettant de gérer la puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou suspendez et reprenez des ressources de calcul pour réduire les coûts."
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
ms.openlocfilehash: 6a185d96447c2e1b0b463439dd062081e783da5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="9bbd0-105">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9bbd0-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bbd0-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9bbd0-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="9bbd0-107">Portail</span><span class="sxs-lookup"><span data-stu-id="9bbd0-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="9bbd0-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bbd0-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="9bbd0-109">REST</span><span class="sxs-lookup"><span data-stu-id="9bbd0-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="9bbd0-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="9bbd0-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="9bbd0-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9bbd0-111">Before you begin</span></span>
### <a name="install-the-latest-version-of-azure-powershell"></a><span data-ttu-id="9bbd0-112">Installer la dernière version d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bbd0-112">Install the latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="9bbd0-113">Pour utiliser Azure PowerShell avec SQL Data Warehouse, vous devez installer Azure PowerShell version 1.0.3 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-113">To use Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="9bbd0-114">Pour vérifier votre version, exécutez la commande **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-114">To verify your current version run the command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="9bbd0-115">Vous pouvez installer la version la plus récente à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-115">You can install the latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="9bbd0-116">Pour plus d’informations, consultez [Installation et configuration d’Azure PowerShell][How to install and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-116">For more information, see [How to install and configure Azure PowerShell][How to install and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="9bbd0-117">Prise en main des applets de commande Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bbd0-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="9bbd0-118">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="9bbd0-118">To get started:</span></span>

1. <span data-ttu-id="9bbd0-119">Ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="9bbd0-120">À l’invite de PowerShell, exécutez les commandes suivantes pour vous connecter à Azure Resource Manager et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-120">At the PowerShell prompt, run these commands to sign in to the Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="9bbd0-121">Mise à l’échelle de la puissance de calcul</span><span class="sxs-lookup"><span data-stu-id="9bbd0-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="9bbd0-122">Pour modifier les unités DWU, utilisez l’applet de commande PowerShell [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-122">To change the DWUs, use the [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="9bbd0-123">L'exemple suivant définit l'objectif de niveau de service sur DW1000 pour la base de données MySQLDW hébergée sur le serveur MyServer.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-123">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="9bbd0-124">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="9bbd0-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="9bbd0-125">Pour interrompre une base de données, utilisez l’applet de commande [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-125">To pause a database, use the [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="9bbd0-126">Dans l’exemple suivant, une base de données appelée Database02 et hébergée sur un serveur appelé Server01 est interrompue.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-126">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="9bbd0-127">Le serveur est un groupe de ressources Azure appelé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-127">The server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="9bbd0-128">Si votre serveur est nommé foo.database.windows.net, utilisez « foo » en tant que nom du serveur dans les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-128">Note that if your server is foo.database.windows.net, use "foo" as the -ServerName in the PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="9bbd0-129">Une variante, l'exemple suivant récupère la base de données dans l'objet $database.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-129">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="9bbd0-130">Puis il redirige l’objet récupéré vers [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-130">It then pipes the object to [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="9bbd0-131">Les résultats sont stockés dans l'objet resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-131">The results are stored in the object resultDatabase.</span></span> <span data-ttu-id="9bbd0-132">La dernière commande affiche les résultats.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-132">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="9bbd0-133">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="9bbd0-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="9bbd0-134">Pour démarrer une base de données, utilisez l’applet de commande [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-134">To start a database, use the [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="9bbd0-135">Dans l’exemple suivant, une base de données appelée Database02 et hébergée sur un serveur appelé Server01 est démarrée.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-135">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="9bbd0-136">Le serveur est un groupe de ressources Azure appelé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-136">The server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="9bbd0-137">Une variante, l'exemple suivant récupère la base de données dans l'objet $database.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-137">A variation, this next example retrieves the database into the $database object.</span></span> <span data-ttu-id="9bbd0-138">Il redirige ensuite l’objet [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] et stocke les résultats dans $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-138">It then pipes the object to [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores the results in $resultDatabase.</span></span> <span data-ttu-id="9bbd0-139">La dernière commande affiche les résultats.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-139">The final command shows the results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="9bbd0-140">Vérifier l’état de base de données</span><span class="sxs-lookup"><span data-stu-id="9bbd0-140">Check database state</span></span>

<span data-ttu-id="9bbd0-141">Comme indiqué dans les exemples ci-dessus, vous pouvez utiliser l’applet de commande [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] pour obtenir des informations sur une base de données, pour vérifier ainsi son état mais aussi pour l’utiliser en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-141">As shown in the above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet to get information on a database, thereby checking the status, but also to use as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="9bbd0-142">De qui donnera quelque chose comme ceci</span><span class="sxs-lookup"><span data-stu-id="9bbd0-142">Which will result in something like</span></span> 

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

<span data-ttu-id="9bbd0-143">Où vous pouvez ensuite vérifier *l’état* de la base de données.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-143">Where you can then check to see the *Status* of the database.</span></span> <span data-ttu-id="9bbd0-144">Dans ce cas, vous pouvez voir que la base de données est en ligne.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="9bbd0-145">Lorsque vous exécutez cette commande, vous devriez recevoir une valeur d’état En ligne, Suspension, Reprise, Mise à l’échelle ou Suspendu.</span><span class="sxs-lookup"><span data-stu-id="9bbd0-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="9bbd0-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9bbd0-146">Next steps</span></span>
<span data-ttu-id="9bbd0-147">Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="9bbd0-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
