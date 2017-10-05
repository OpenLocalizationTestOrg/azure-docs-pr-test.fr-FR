---
title: "PowerShell : Créer et gérer un pool élastique Azure SQL | Microsoft Docs"
description: "Découvrez comment utiliser PowerShell pour gérer un pool élastique."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 5e76397c62e5a6ff7fb356bd81218c307f3fda31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="d98f0-103">Créer et gérer un pool élastique avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d98f0-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="d98f0-104">Cette rubrique montre comment créer et gérer des [pools élastiques](sql-database-elastic-pool.md) évolutifs avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d98f0-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="d98f0-105">Vous pouvez également créer et gérer un pool élastique Azure avec le [portail Azure](https://portal.azure.com/), l’API REST ou [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="d98f0-105">You can also create and manage an Azure elastic pool using the [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="d98f0-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="d98f0-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="d98f0-107">Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-107">Create an elastic pool</span></span>
<span data-ttu-id="d98f0-108">L’applet de commande [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) permet de créer un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="d98f0-108">The [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="d98f0-109">Les valeurs correspondant au nombre d’eDTU par pool, ainsi qu’au nombre de DTU minimal et maximal, sont limitées par la valeur de niveau de service (De base, Standard, Premium ou Premium RS).</span><span class="sxs-lookup"><span data-stu-id="d98f0-109">The values for eDTU per pool, min, and max DTUs are constrained by the service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="d98f0-110">Consultez l’article [Limites relatives aux eDTU et au stockage pour les pools de bases de données](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="d98f0-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="d98f0-111">Créer une base de données regroupée dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="d98f0-112">Utilisez l’applet de commande [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) et définissez le paramètre **ElasticPoolName** sur le pool cible.</span><span class="sxs-lookup"><span data-stu-id="d98f0-112">Use the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set the **ElasticPoolName** parameter to the target pool.</span></span> <span data-ttu-id="d98f0-113">Pour déplacer une base de données existante vers un pool élastique, consultez l’article [Déplacer une base de données dans un pool élastique](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="d98f0-113">To move an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="d98f0-114">Terminer le script</span><span class="sxs-lookup"><span data-stu-id="d98f0-114">Complete script</span></span>
<span data-ttu-id="d98f0-115">Ce script crée un groupe de ressources Azure et un serveur.</span><span class="sxs-lookup"><span data-stu-id="d98f0-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="d98f0-116">Lorsque vous y êtes invité, fournissez un nom d’utilisateur de l’administrateur et un mot de passe pour le nouveau serveur (différents de vos informations d’identification Azure).</span><span class="sxs-lookup"><span data-stu-id="d98f0-116">When prompted, supply an administrator username and password for the new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="d98f0-117">Créer un pool élastique et ajouter plusieurs bases de données regroupées</span><span class="sxs-lookup"><span data-stu-id="d98f0-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="d98f0-118">La création d’un grand nombre de bases de données dans un pool élastique peut prendre du temps si elle se fait par le biais du portail ou d’applets de commande PowerShell qui créent une seule base de données à la fois.</span><span class="sxs-lookup"><span data-stu-id="d98f0-118">Creation of many databases in an elastic pool can take time when done using the portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="d98f0-119">Pour automatiser la création dans un pool élastique, consultez l’article [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="d98f0-119">To automate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="d98f0-120">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="d98f0-121">Vous pouvez ajouter ou retirer une base de données d’un pool élastique avec l’applet de commande [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="d98f0-121">You can move a database into or out of an elastic pool with the [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="d98f0-122">Modifier les paramètres de performances d'un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="d98f0-123">Lorsque les performances sont insuffisantes, vous pouvez modifier les paramètres du pool pour faire face à l’augmentation de l’activité.</span><span class="sxs-lookup"><span data-stu-id="d98f0-123">When performance suffers, you can change the settings of the pool to accommodate growth.</span></span> <span data-ttu-id="d98f0-124">Utilisez l’applet de commande [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) .</span><span class="sxs-lookup"><span data-stu-id="d98f0-124">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="d98f0-125">Définissez la valeur du paramètre -Dtu sur le nombre d’eDTU par pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-125">Set the -Dtu parameter to the eDTUs per pool.</span></span> <span data-ttu-id="d98f0-126">Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.</span><span class="sxs-lookup"><span data-stu-id="d98f0-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-the-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="d98f0-127">Modifier la limite de stockage d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-127">Change the storage limit for an elastic pool</span></span>

<span data-ttu-id="d98f0-128">Utilisez la cmdlet [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) pour définir le paramètre _-StorageMB_.</span><span class="sxs-lookup"><span data-stu-id="d98f0-128">Use the [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet to set the _-StorageMB_ parameter.</span></span> <span data-ttu-id="d98f0-129">Indiquez la limite de stockage en Mo (p. ex. 2097152 définit la limite de stockage sur 2 To).</span><span class="sxs-lookup"><span data-stu-id="d98f0-129">Provide the storage limit in MB (for example, 2097152 sets the storage limit to 2 TB).</span></span> <span data-ttu-id="d98f0-130">Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.</span><span class="sxs-lookup"><span data-stu-id="d98f0-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d98f0-131">Le stockage de données max. par défaut par pool pour les pools Premium avec 1 500 eDTU ou plus est de 750 Go.</span><span class="sxs-lookup"><span data-stu-id="d98f0-131">The default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="d98f0-132">Pour obtenir la _taille de stockage de données max. par pool_ la plus élevée, la limite de stockage doit être définie explicitement.</span><span class="sxs-lookup"><span data-stu-id="d98f0-132">To obtain the higher _max data storage size per pool_, the storage limit must be explicitly set.</span></span> <span data-ttu-id="d98f0-133">Les pools Premium avec plus de 750 To de stockage sont actuellement en version préliminaire publique dans les régions suivantes : Est des États-Unis 2, États-Unis de l’Ouest, Gouvernement des États-Unis - Virginie, Europe de l’Ouest, Centre de l’Allemagne, Asie du Sud-Est, Japon de l’Est, Est de l’Australie, Canada Centre et Canada Est.</span><span class="sxs-lookup"><span data-stu-id="d98f0-133">Premium pools with more than 750 GB of storage is currently in public preview in the following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-the-status-of-pool-operations"></a><span data-ttu-id="d98f0-134">Obtenir l’état des opérations de pool</span><span class="sxs-lookup"><span data-stu-id="d98f0-134">Get the status of pool operations</span></span>
<span data-ttu-id="d98f0-135">Créer un pool élastique peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d98f0-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="d98f0-136">Pour suivre l’état des opérations de pool, notamment la création et les mises à jour, utilisez l’applet de commande [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity).</span><span class="sxs-lookup"><span data-stu-id="d98f0-136">To track the status of pool operations including creation and updates, use the [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-the-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="d98f0-137">Obtenir l’état du déplacement d’une base de données en direction et à partir d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-137">Get the status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="d98f0-138">Déplacer une base de données peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="d98f0-138">Moving a database can take time.</span></span> <span data-ttu-id="d98f0-139">Pour suivre l’état du déplacement, utilisez l’applet de commande [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity).</span><span class="sxs-lookup"><span data-stu-id="d98f0-139">Track a move status using the [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="d98f0-140">Obtenir les données d’utilisation des ressources d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="d98f0-141">Mesures récupérables sous la forme d'un pourcentage de la limite de pool de ressources :</span><span class="sxs-lookup"><span data-stu-id="d98f0-141">Metrics that can be retrieved as a percentage of the resource pool limit:</span></span>

| <span data-ttu-id="d98f0-142">Nom de métrique</span><span class="sxs-lookup"><span data-stu-id="d98f0-142">Metric name</span></span> | <span data-ttu-id="d98f0-143">Description</span><span class="sxs-lookup"><span data-stu-id="d98f0-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d98f0-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-144">cpu\_percent</span></span> |<span data-ttu-id="d98f0-145">Utilisation moyenne des ressources de calcul en pourcentage de la limite du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-145">Average compute utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="d98f0-147">Utilisation moyenne des E/S en pourcentage de la limite du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-147">Average I/O utilization in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-148">log\_write\_percent</span></span> |<span data-ttu-id="d98f0-149">Utilisation moyenne des ressources d’écriture en pourcentage de la limite du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-149">Average write resource utilization in percentage of the limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="d98f0-151">Utilisation moyenne des eDTU en pourcentage de la limite d’eDTU du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-151">Average eDTU utilization in percentage of eDTU limit for the pool</span></span> |
| <span data-ttu-id="d98f0-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-152">storage\_percent</span></span> |<span data-ttu-id="d98f0-153">Utilisation moyenne du stockage en pourcentage de la limite de stockage du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-153">Average storage utilization in percentage of the storage limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-154">workers\_percent</span></span> |<span data-ttu-id="d98f0-155">Nombre maximal d’ouvriers simultanés (demandes) en pourcentage de la limite du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-155">Maximum concurrent workers (requests) in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="d98f0-156">sessions\_percent</span></span> |<span data-ttu-id="d98f0-157">Nombre maximal de sessions simultanées en pourcentage de la limite du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-157">Maximum concurrent sessions in percentage based on the limit of the pool.</span></span> |
| <span data-ttu-id="d98f0-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="d98f0-158">eDTU_limit</span></span> |<span data-ttu-id="d98f0-159">Nombre maximal de DTU de pool élastique pour ce pool élastique au cours de cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="d98f0-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="d98f0-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="d98f0-160">storage\_limit</span></span> |<span data-ttu-id="d98f0-161">Espace de stockage de pool élastique maximal pour ce pool élastique (en Mo) au cours de cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="d98f0-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="d98f0-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="d98f0-162">eDTU\_used</span></span> |<span data-ttu-id="d98f0-163">Nombre moyen d’eDTU utilisées par le pool au cours de cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="d98f0-163">Average eDTUs used by the pool in this interval.</span></span> |
| <span data-ttu-id="d98f0-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="d98f0-164">storage\_used</span></span> |<span data-ttu-id="d98f0-165">Espace de stockage moyen utilisé par le pool au cours de cet intervalle (en octets).</span><span class="sxs-lookup"><span data-stu-id="d98f0-165">Average storage used by the pool in this interval in bytes</span></span> |

<span data-ttu-id="d98f0-166">**Granularité des mesures/périodes de rétention :**</span><span class="sxs-lookup"><span data-stu-id="d98f0-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="d98f0-167">Les données seront renvoyées avec une granularité de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d98f0-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="d98f0-168">La durée de conservation des données est de 35 jours.</span><span class="sxs-lookup"><span data-stu-id="d98f0-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="d98f0-169">Cette applet de commande et API limite le nombre de lignes pouvant être récupérées au cours d'un seul appel à 1000 (environ 3 jours de données avec une granularité de 5 minutes).</span><span class="sxs-lookup"><span data-stu-id="d98f0-169">This cmdlet and API limits the number of rows that can be retrieved in one call to 1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="d98f0-170">Mais cette commande peut être appelée plusieurs fois avec des intervalles de temps de début / fin différents pour récupérer plus de données.</span><span class="sxs-lookup"><span data-stu-id="d98f0-170">But this command can be called multiple times with different start/end time intervals to retrieve more data</span></span>

<span data-ttu-id="d98f0-171">Pour obtenir les mesures :</span><span class="sxs-lookup"><span data-stu-id="d98f0-171">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="d98f0-172">Afficher les données d’utilisation des ressources d’une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="d98f0-173">Ces API sont les mêmes que celles utilisées pour analyser l’utilisation des ressources d’une base de données, à l’exception de la différence sémantique suivante : les métriques récupérées sont exprimées sous forme d’un pourcentage du nombre maximal d’eDTU par base de données (ou du nombre maximal équivalent pour la métrique sous-jacente telle que le processeur ou les E/S) défini pour ce pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-173">These APIs are the same as the APIs used for monitoring the resource utilization of a single database, except for the following semantic difference: metrics retrieved are expressed as a percentage of the per database max eDTUs (or equivalent cap for the underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="d98f0-174">Par exemple, une utilisation de 50 % de l’une de ces mesures indique que la consommation des ressources spécifiques est de 50 % de la limite supérieure par base de données définie pour cette ressource dans le pool parent.</span><span class="sxs-lookup"><span data-stu-id="d98f0-174">For example, 50% utilization of any of these metrics indicates that the specific resource consumption is at 50% of the per database cap limit for that resource in the parent pool.</span></span>

<span data-ttu-id="d98f0-175">Pour obtenir les mesures :</span><span class="sxs-lookup"><span data-stu-id="d98f0-175">To retrieve the metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="d98f0-176">Ajouter une alerte à une ressource de pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-176">Add an alert to an elastic pool resource</span></span>
<span data-ttu-id="d98f0-177">Vous pouvez ajouter des règles d’alerte à un pool élastique qui envoient des notifications par message électronique ou des chaînes d’alertes à des [points de terminaison d’URL](https://msdn.microsoft.com/library/mt718036.aspx) quand le pool élastique atteint un seuil d’utilisation que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="d98f0-177">You can add alert rules to an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when the elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="d98f0-178">Utilisez l’applet de commande Add-AzureRmMetricAlertRule.</span><span class="sxs-lookup"><span data-stu-id="d98f0-178">Use the Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d98f0-179">La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d98f0-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="d98f0-180">La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="d98f0-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="d98f0-181">Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d98f0-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="d98f0-182">Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="d98f0-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="d98f0-183">Cet exemple ajoute une alerte pour recevoir une notification lorsque la consommation eDTU d’un pool élastique dépasse un certain seuil.</span><span class="sxs-lookup"><span data-stu-id="d98f0-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="d98f0-184">Pour plus d’informations, voir [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md) (Créer des alertes SQL Database dans le Portail Azure).</span><span class="sxs-lookup"><span data-stu-id="d98f0-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-to-all-databases-in-an-elastic-pool"></a><span data-ttu-id="d98f0-185">Ajouter des alertes à toutes les bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-185">Add alerts to all databases in an elastic pool</span></span>
<span data-ttu-id="d98f0-186">Vous pouvez ajouter des règles d’alerte à toutes les bases de données dans un pool élastique qui envoient des notifications par message électronique ou des chaînes d’alertes à des [points de terminaison d’URL](https://msdn.microsoft.com/library/mt718036.aspx) quand une ressource atteint un seuil d’utilisation configuré par l’alerte.</span><span class="sxs-lookup"><span data-stu-id="d98f0-186">You can add alert rules to all database in an elastic pool to send email notifications or alert strings to [URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by the alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d98f0-187">La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="d98f0-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="d98f0-188">La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="d98f0-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="d98f0-189">Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d98f0-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="d98f0-190">Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="d98f0-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="d98f0-191">Cet exemple ajoute une alerte à chacune des bases de données dans un pool élastique pour obtenir une notification lorsque la consommation DTU de cette base de données dépasse un certain seuil.</span><span class="sxs-lookup"><span data-stu-id="d98f0-191">This example adds an alert to each of the databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop the alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="d98f0-192">Collecter et surveiller les données d’utilisation des ressources dans plusieurs pools d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="d98f0-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="d98f0-193">Lorsque vous disposez d’un grand nombre de bases de données dans un abonnement, il est fastidieux d’analyser chaque pool élastique séparément.</span><span class="sxs-lookup"><span data-stu-id="d98f0-193">When you have many databases in a subscription, it is cumbersome to monitor each elastic pool separately.</span></span> <span data-ttu-id="d98f0-194">Au lieu de cela, vous pouvez associer les applets de commande PowerShell de la base de données SQL et les requêtes T-SQL pour collecter les données d’utilisation des ressources de plusieurs pools et de leurs bases de données pour la surveillance et l’analyse de l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="d98f0-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined to collect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="d98f0-195">Un [exemple d’implémentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) d’un ensemble de scripts PowerShell de ce type est disponible dans le référentiel d’exemples SQL Server GitHub, accompagné d’une documentation sur sa fonction et son utilisation.</span><span class="sxs-lookup"><span data-stu-id="d98f0-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in the GitHub SQL Server samples repository along with documentation on what it does and how to use it.</span></span>

<span data-ttu-id="d98f0-196">Pour utiliser cet exemple d’implémentation, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="d98f0-196">To use this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="d98f0-197">Téléchargez les [scripts et la documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="d98f0-197">Download the [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="d98f0-198">Modifiez les scripts pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d98f0-198">Modify the scripts for your environment.</span></span> <span data-ttu-id="d98f0-199">Spécifiez le ou les serveurs qui hébergent les pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="d98f0-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="d98f0-200">Spécifiez une base de données de télémétrie où les métriques collectées doivent être stockées.</span><span class="sxs-lookup"><span data-stu-id="d98f0-200">Specify a telemetry database where the collected metrics are to be stored.</span></span>
4. <span data-ttu-id="d98f0-201">Personnalisez le script pour spécifier la durée de l’exécution des scripts.</span><span class="sxs-lookup"><span data-stu-id="d98f0-201">Customize the script to specify the duration of the scripts' execution.</span></span>

<span data-ttu-id="d98f0-202">D’un point de vue global, le script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d98f0-202">At a high level, the scripts do the following:</span></span>

* <span data-ttu-id="d98f0-203">Il énumère tous les serveurs d’un abonnement Azure donné (ou d’une liste spécifiée de serveurs).</span><span class="sxs-lookup"><span data-stu-id="d98f0-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="d98f0-204">Il exécute une tâche en arrière-plan pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="d98f0-204">Runs a background job for each server.</span></span> <span data-ttu-id="d98f0-205">La tâche s’exécute en boucle à intervalles réguliers et collecte les données de télémétrie pour tous les pools du serveur.</span><span class="sxs-lookup"><span data-stu-id="d98f0-205">The job runs in a loop at regular intervals and collects telemetry data for all the pools in the server.</span></span> <span data-ttu-id="d98f0-206">Il charge ensuite les données collectées dans la base de données de télémétrie spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d98f0-206">It then loads the collected data into the specified telemetry database.</span></span>
* <span data-ttu-id="d98f0-207">Il énumère la liste des bases de données de chaque pool pour collecter les données d’utilisation des ressources des bases de données.</span><span class="sxs-lookup"><span data-stu-id="d98f0-207">Enumerates a list of databases in each pool to collect the database resource usage data.</span></span> <span data-ttu-id="d98f0-208">Il charge ensuite les données collectées dans la base de données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="d98f0-208">It then loads the collected data into the telemetry database.</span></span>

<span data-ttu-id="d98f0-209">Les métriques collectées chargées dans la base de données de télémétrie peuvent être analysées pour surveiller l’intégrité des pools élastiques et des bases de données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="d98f0-209">The collected metrics in the telemetry database can be analyzed to monitor the health of elastic pools and the databases in it.</span></span> <span data-ttu-id="d98f0-210">Le script installe également une fonction table prédéfinie dans la base de données de télémétrie pour faciliter l’agrégation des métriques d’une plage de temps spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d98f0-210">The script also installs a pre-defined Table-Value function (TVF) in the telemetry database to help aggregate the metrics for a specified time window.</span></span> <span data-ttu-id="d98f0-211">Par exemple, les résultats de la fonction table peuvent servir à afficher les N premiers pools élastiques en termes d’utilisation des eDTU au cours d’une plage de temps donnée.</span><span class="sxs-lookup"><span data-stu-id="d98f0-211">For example, results of the TVF can be used to show “top N elastic pools with the maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="d98f0-212">Si vous le souhaitez, vous pouvez utiliser des outils analytiques tels que Excel ou Power BI pour interroger et analyser les données collectées.</span><span class="sxs-lookup"><span data-stu-id="d98f0-212">Optionally, use analytic tools like Excel or Power BI to query and analyze the collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="d98f0-213">Exemple : obtenir des mesures de consommation des ressources pour un pool élastique et ses bases de données</span><span class="sxs-lookup"><span data-stu-id="d98f0-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="d98f0-214">Cet exemple consiste à récupérer les mesures de consommation pour un pool donné et l’ensemble de ses bases de données.</span><span class="sxs-lookup"><span data-stu-id="d98f0-214">This example retrieves the consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="d98f0-215">Les données collectées sont mises en forme et écrites dans un fichier au format .csv.</span><span class="sxs-lookup"><span data-stu-id="d98f0-215">Collected data is formatted and written to a .csv formatted file.</span></span> <span data-ttu-id="d98f0-216">Le fichier peut être consulté à l’aide d’Excel.</span><span class="sxs-lookup"><span data-stu-id="d98f0-216">The file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login to Azure account and select the subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for the specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct the pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get the list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for the specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format the metrics and output as .csv file using the following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output the metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="d98f0-217">Latence des opérations du pool élastique</span><span class="sxs-lookup"><span data-stu-id="d98f0-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="d98f0-218">En général, le processus de modification du nombre minimal d’eDTU par base de données ou du nombre maximal d’eDTU par base de données prend 5 minutes au maximum.</span><span class="sxs-lookup"><span data-stu-id="d98f0-218">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="d98f0-219">Le processus de modification du nombre d’eDTU par pool dépend quant à lui de la quantité totale d’espace utilisé par toutes les bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-219">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="d98f0-220">Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="d98f0-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="d98f0-221">Par exemple, si l’espace total utilisé par toutes les bases de données du pool est égal à 200 Go, une opération de modification du nombre d’eDTU par pool prend 3 heures au maximum.</span><span class="sxs-lookup"><span data-stu-id="d98f0-221">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d98f0-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d98f0-222">Next steps</span></span>
* <span data-ttu-id="d98f0-223">[Créer des tâches élastiques](sql-database-elastic-jobs-overview.md) : les tâches élastiques vous permettent d’exécuter des scripts T-SQL, quel que soit le nombre de bases de données contenues dans le pool.</span><span class="sxs-lookup"><span data-stu-id="d98f0-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in the pool.</span></span>
* <span data-ttu-id="d98f0-224">Consultez [Montée en charge avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utilisez les outils élastiques pour monter en charge, déplacer des données, exécuter des requêtes ou créer des transactions.</span><span class="sxs-lookup"><span data-stu-id="d98f0-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools to scale out, move data, query, or create transactions.</span></span>
