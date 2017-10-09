---
title: "PowerShell : Créer et gérer un pool élastique Azure SQL | Microsoft Docs"
description: "Découvrez comment toouse PowerShell toomanage un pool élastique."
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
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="197eb-103">Créer et gérer un pool élastique avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="197eb-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="197eb-104">Cette rubrique vous montre comment toocreate et gérer évolutive [pools élastiques](sql-database-elastic-pool.md) avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="197eb-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="197eb-105">Vous pouvez également créer et gérer un pool élastique Azure à l’aide de hello [portail Azure](https://portal.azure.com/), l’API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="197eb-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="197eb-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="197eb-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="197eb-107">Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-107">Create an elastic pool</span></span>
<span data-ttu-id="197eb-108">Hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) applet de commande crée un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="197eb-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="197eb-109">les valeurs Hello pour eDTU par pool, min et max dtu sont limitées par la valeur de niveau de service hello (Basic, Standard, Premium ou Premium RS).</span><span class="sxs-lookup"><span data-stu-id="197eb-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="197eb-110">Consultez l’article [Limites relatives aux eDTU et au stockage pour les pools de bases de données](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="197eb-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="197eb-111">Créer une base de données regroupée dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="197eb-112">Hello d’utilisation [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) applet de commande et ensemble hello **ElasticPoolName** pool de paramètre toohello cible.</span><span class="sxs-lookup"><span data-stu-id="197eb-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="197eb-113">toomove une base de données existante dans un pool élastique, consultez [déplacer une base de données dans un pool élastique](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="197eb-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="197eb-114">Terminer le script</span><span class="sxs-lookup"><span data-stu-id="197eb-114">Complete script</span></span>
<span data-ttu-id="197eb-115">Ce script crée un groupe de ressources Azure et un serveur.</span><span class="sxs-lookup"><span data-stu-id="197eb-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="197eb-116">Lorsque vous y êtes invité, fournissez un nom d’utilisateur administrateur et le mot de passe pour le nouveau serveur de hello (pas vos informations d’identification Azure).</span><span class="sxs-lookup"><span data-stu-id="197eb-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="197eb-117">Créer un pool élastique et ajouter plusieurs bases de données regroupées</span><span class="sxs-lookup"><span data-stu-id="197eb-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="197eb-118">La création de plusieurs bases de données dans un pool élastique peut prendre un temps quand terminé à l’aide du portail de hello ou des applets de commande PowerShell créer uniquement une seule base de données à la fois.</span><span class="sxs-lookup"><span data-stu-id="197eb-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="197eb-119">Création de tooautomate dans un pool élastique, consultez [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="197eb-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="197eb-120">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="197eb-121">Vous pouvez déplacer une base de données dans ou hors d’un pool élastique hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="197eb-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="197eb-122">Modifier les paramètres de performances d'un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="197eb-123">Lorsque les performances sont affectées, vous pouvez modifier les paramètres de hello de croissance de tooaccommodate pool hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="197eb-124">Hello d’utilisation [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="197eb-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="197eb-125">Définissez hello - Dtu paramètre toohello Edtu par pool.</span><span class="sxs-lookup"><span data-stu-id="197eb-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="197eb-126">Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.</span><span class="sxs-lookup"><span data-stu-id="197eb-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="197eb-127">Modifier la limite de stockage hello pour un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="197eb-128">Hello d’utilisation [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) applet de commande tooset hello _- StorageMB_ paramètre.</span><span class="sxs-lookup"><span data-stu-id="197eb-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="197eb-129">Fournir la limite de stockage hello Mo (par exemple, les jeux de 2097152 hello stockage limite too2 to).</span><span class="sxs-lookup"><span data-stu-id="197eb-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="197eb-130">Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.</span><span class="sxs-lookup"><span data-stu-id="197eb-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="197eb-131">stockage de données max Hello par défaut par pool pour les pools Premium avec 1500 Edtu ou plus sont 750 Go.</span><span class="sxs-lookup"><span data-stu-id="197eb-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="197eb-132">hello tooobtain supérieur _nombre maximum de taille de stockage de données par pool_, limite de stockage hello doit être explicitement définie.</span><span class="sxs-lookup"><span data-stu-id="197eb-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="197eb-133">Les pools avec plus de 750 Go de stockage Premium est actuellement en version préliminaire publique Bonjour suivant régions : est des États-Unis 2, ouest des États-Unis, nous Gov Virginie, Europe de l’ouest, Allemagne Central, Asie du Sud-est, est du Japon, est de l’Australie, Canada Central et est du Canada.</span><span class="sxs-lookup"><span data-stu-id="197eb-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="197eb-134">Obtenir l’état de hello d’opérations de pool</span><span class="sxs-lookup"><span data-stu-id="197eb-134">Get hello status of pool operations</span></span>
<span data-ttu-id="197eb-135">Créer un pool élastique peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="197eb-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="197eb-136">état de hello tootrack des opérations, y compris la création et de mises à jour, utilisez hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="197eb-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="197eb-137">Obtenir l’état de hello de déplacement d’une base de données dans et hors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="197eb-138">Déplacer une base de données peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="197eb-138">Moving a database can take time.</span></span> <span data-ttu-id="197eb-139">Effectuer le suivi d’un état de déplacement à l’aide de hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="197eb-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="197eb-140">Obtenir les données d’utilisation des ressources d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="197eb-141">Métriques qui peuvent être récupérés sous forme de pourcentage de limite de pool de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="197eb-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="197eb-142">Nom de métrique</span><span class="sxs-lookup"><span data-stu-id="197eb-142">Metric name</span></span> | <span data-ttu-id="197eb-143">Description</span><span class="sxs-lookup"><span data-stu-id="197eb-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="197eb-144">cpu\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-144">cpu\_percent</span></span> |<span data-ttu-id="197eb-145">Utilisation en pourcentage de limite hello du pool de hello moyenne du calcul.</span><span class="sxs-lookup"><span data-stu-id="197eb-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-146">physical\_data\_read\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="197eb-147">Utilisation d’e/s moyenne en pourcentage de limite hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-148">log\_write\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-148">log\_write\_percent</span></span> |<span data-ttu-id="197eb-149">L’utilisation des ressources d’écriture moyenne en pourcentage de limite hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-150">DTU\_consumption\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="197eb-151">Utilisation des eDTU moyenne en pourcentage de limite d’eDTU de pool de hello</span><span class="sxs-lookup"><span data-stu-id="197eb-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="197eb-152">storage\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-152">storage\_percent</span></span> |<span data-ttu-id="197eb-153">Moyenne de l’utilisation du stockage en pourcentage de limite de stockage hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-154">workers\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-154">workers\_percent</span></span> |<span data-ttu-id="197eb-155">Traitements simultanés maximum (demandes) en pourcentage de limite hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-156">sessions\_percent</span><span class="sxs-lookup"><span data-stu-id="197eb-156">sessions\_percent</span></span> |<span data-ttu-id="197eb-157">Nombre maximal de sessions simultané en pourcentage de limite hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="197eb-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="197eb-158">eDTU_limit</span></span> |<span data-ttu-id="197eb-159">Nombre maximal de DTU de pool élastique pour ce pool élastique au cours de cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="197eb-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="197eb-160">storage\_limit</span><span class="sxs-lookup"><span data-stu-id="197eb-160">storage\_limit</span></span> |<span data-ttu-id="197eb-161">Espace de stockage de pool élastique maximal pour ce pool élastique (en Mo) au cours de cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="197eb-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="197eb-162">eDTU\_used</span><span class="sxs-lookup"><span data-stu-id="197eb-162">eDTU\_used</span></span> |<span data-ttu-id="197eb-163">Edtu moyen utilisé par le pool de hello dans cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="197eb-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="197eb-164">storage\_used</span><span class="sxs-lookup"><span data-stu-id="197eb-164">storage\_used</span></span> |<span data-ttu-id="197eb-165">Stockage moyen utilisé par le pool de hello dans cet intervalle, en octets</span><span class="sxs-lookup"><span data-stu-id="197eb-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="197eb-166">**Granularité des mesures/périodes de rétention :**</span><span class="sxs-lookup"><span data-stu-id="197eb-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="197eb-167">Les données seront renvoyées avec une granularité de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="197eb-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="197eb-168">La durée de conservation des données est de 35 jours.</span><span class="sxs-lookup"><span data-stu-id="197eb-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="197eb-169">Cette applet de commande et les API limite le nombre hello de lignes qui peuvent être récupérées dans un seul appel too1000 lignes (environ 3 jours de données au niveau de granularité de 5 minutes).</span><span class="sxs-lookup"><span data-stu-id="197eb-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="197eb-170">Mais cette commande peut être appelée plusieurs fois avec tooretrieve d’intervalles de temps de début et de fin des données</span><span class="sxs-lookup"><span data-stu-id="197eb-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="197eb-171">métriques de hello tooretrieve :</span><span class="sxs-lookup"><span data-stu-id="197eb-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="197eb-172">Afficher les données d’utilisation des ressources d’une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="197eb-173">Ces API sont hello identique hello API utilisées pour l’analyse de l’utilisation des ressources d’une base de données, à l’exception de hello suivant la différence de sémantique hello : métriques récupérés sont exprimées en pourcentage de hello par Edtu maximale de base de données (ou équivalent cap pour hello sous-jacent métrique de l’UC ou les e/s) définie pour ce pool.</span><span class="sxs-lookup"><span data-stu-id="197eb-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="197eb-174">Par exemple, 50 % d’utilisation d’un de ces métriques indique que la consommation des ressources spécifiques hello est à 50 % de hello par limite d’extrémité de fin de base de données pour cette ressource dans le pool de parent hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="197eb-175">métriques de hello tooretrieve :</span><span class="sxs-lookup"><span data-stu-id="197eb-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="197eb-176">Ajouter une ressource de pool élastique tooan alerte</span><span class="sxs-lookup"><span data-stu-id="197eb-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="197eb-177">Vous pouvez ajouter des règles d’alerte tooan pool élastique toosend notifications par courrier électronique ou les chaînes d’alerte trop[les points de terminaison URL](https://msdn.microsoft.com/library/mt718036.aspx) lorsque pool élastique de hello atteint un seuil d’utilisation que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="197eb-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="197eb-178">Utilisez l’applet de commande Add-AzureRmMetricAlertRule de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="197eb-179">La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="197eb-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="197eb-180">La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="197eb-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="197eb-181">Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="197eb-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="197eb-182">Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="197eb-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="197eb-183">Cet exemple ajoute une alerte pour recevoir une notification lorsque la consommation eDTU d’un pool élastique dépasse un certain seuil.</span><span class="sxs-lookup"><span data-stu-id="197eb-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

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

<span data-ttu-id="197eb-184">Pour plus d'informations, voir [Créer des alertes SQL Database dans le portail Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="197eb-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="197eb-185">Ajouter des bases de données tooall les alertes d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="197eb-186">Vous pouvez ajouter des règles d’alerte tooall de base de données dans un pool élastique de toosend notifications par courrier électronique ou des chaînes d’alerte trop[les points de terminaison URL](https://msdn.microsoft.com/library/mt718036.aspx) lorsqu’une ressource atteint un seuil d’utilisation est configuré par l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="197eb-187">La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="197eb-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="197eb-188">La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="197eb-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="197eb-189">Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée.</span><span class="sxs-lookup"><span data-stu-id="197eb-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="197eb-190">Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.</span><span class="sxs-lookup"><span data-stu-id="197eb-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="197eb-191">Cet exemple ajoute une alerte tooeach des bases de données hello dans un pool élastique pour recevoir une notification lorsque la consommation DTU de cette base de données dépasse certain seuil.</span><span class="sxs-lookup"><span data-stu-id="197eb-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="197eb-192">Collecter et surveiller les données d’utilisation des ressources dans plusieurs pools d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="197eb-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="197eb-193">Lorsque vous avez plusieurs bases de données dans un abonnement, il est fastidieuse toomonitor chaque élastique pool séparément.</span><span class="sxs-lookup"><span data-stu-id="197eb-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="197eb-194">Au lieu de cela, les applets de commande PowerShell de base de données SQL et les requêtes T-SQL peuvent être combiné toocollect ressources des données d’utilisation à partir de plusieurs pools et leurs bases de données pour la surveillance et l’analyse de l’utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="197eb-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="197eb-195">A [exemple d’implémentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) d’un ensemble de powershell scripts sont accessibles dans le référentiel d’exemples hello GitHub SQL Server, ainsi que la documentation sur ce qu’il fait et comment toouse il.</span><span class="sxs-lookup"><span data-stu-id="197eb-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="197eb-196">toouse cet exemple d’implémentation, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="197eb-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="197eb-197">Télécharger hello [des scripts et la documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="197eb-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="197eb-198">Modifier les scripts hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="197eb-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="197eb-199">Spécifiez le ou les serveurs qui hébergent les pools élastiques.</span><span class="sxs-lookup"><span data-stu-id="197eb-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="197eb-200">Spécifiez une base de données de télémétrie où hello métriques collectées sont toobe stockée.</span><span class="sxs-lookup"><span data-stu-id="197eb-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="197eb-201">Personnaliser hello script toospecify hello toute durée de l’exécution des scripts hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="197eb-202">À un niveau élevé, les scripts de hello hello suivant :</span><span class="sxs-lookup"><span data-stu-id="197eb-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="197eb-203">Il énumère tous les serveurs d’un abonnement Azure donné (ou d’une liste spécifiée de serveurs).</span><span class="sxs-lookup"><span data-stu-id="197eb-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="197eb-204">Il exécute une tâche en arrière-plan pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="197eb-204">Runs a background job for each server.</span></span> <span data-ttu-id="197eb-205">travail de Hello s’exécute dans une boucle à intervalles réguliers et collecte les données de télémétrie pour tous les pools hello dans le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="197eb-206">Il charge ensuite les données de salutation collectée dans la base de données de télémétrie spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="197eb-207">Énumère une liste de bases de données dans chaque données d’utilisation de ressources de base de données pool toocollect hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="197eb-208">Il charge ensuite les données de salutation collectée dans la base de données de télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="197eb-209">Hello métriques collectées dans la base de données de télémétrie hello peuvent être analysées toomonitor la santé hello pools élastiques et bases de données hello qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="197eb-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="197eb-210">script de Hello installe également une fonction de valeur de Table (TVF) prédéfinie dans hello de base de données toohelp d’agrégation hello les mesures de télémesure pour une fenêtre de temps spécifié.</span><span class="sxs-lookup"><span data-stu-id="197eb-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="197eb-211">Par exemple, les résultats de hello TVF peuvent être utilisé tooshow « N premiers pools élastiques dont l’utilisation des eDTU maximale hello dans une fenêtre de temps donnée. »</span><span class="sxs-lookup"><span data-stu-id="197eb-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="197eb-212">Si vous le souhaitez, utiliser les outils d’analyse comme tooquery Excel ou Power BI et analyser les données collectée de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="197eb-213">Exemple : obtenir des mesures de consommation des ressources pour un pool élastique et ses bases de données</span><span class="sxs-lookup"><span data-stu-id="197eb-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="197eb-214">Cet exemple récupère des métriques de consommation hello pour un pool élastique donné et toutes ses bases de données.</span><span class="sxs-lookup"><span data-stu-id="197eb-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="197eb-215">Les données collectées sont mis en forme et écrites le fichier au format .csv de tooa.</span><span class="sxs-lookup"><span data-stu-id="197eb-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="197eb-216">fichier de Hello peut être parcouru avec Excel.</span><span class="sxs-lookup"><span data-stu-id="197eb-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
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

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="197eb-217">Latence des opérations du pool élastique</span><span class="sxs-lookup"><span data-stu-id="197eb-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="197eb-218">La modification d’Edtu de min hello par base de données ou max Edtu par base de données généralement se termine dans 5 minutes ou moins.</span><span class="sxs-lookup"><span data-stu-id="197eb-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="197eb-219">Modification des Edtu hello par pool dépend hello total de l’espace utilisé par toutes les bases de données dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="197eb-220">Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="197eb-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="197eb-221">Par exemple, si hello l’espace total utilisé par toutes les bases de données dans le pool de hello est 200 Go, puis hello attendu de latence de modification hello eDTU du pool par pool est de 3 heures au maximum.</span><span class="sxs-lookup"><span data-stu-id="197eb-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="197eb-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="197eb-222">Next steps</span></span>
* <span data-ttu-id="197eb-223">[Créer des travaux élastique](sql-database-elastic-jobs-overview.md) travaux élastique vous permettre d’exécuter des scripts T-SQL par rapport à n’importe quel nombre de bases de données dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="197eb-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="197eb-224">Consultez [montée en puissance parallèle avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utiliser tooscale outils élastique out, de déplacer des données, la requête ou la création des transactions.</span><span class="sxs-lookup"><span data-stu-id="197eb-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
