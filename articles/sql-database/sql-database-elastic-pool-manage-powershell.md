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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Créer et gérer un pool élastique avec PowerShell
Cette rubrique vous montre comment toocreate et gérer évolutive [pools élastiques](sql-database-elastic-pool.md) avec PowerShell.  Vous pouvez également créer et gérer un pool élastique Azure à l’aide de hello [portail Azure](https://portal.azure.com/), l’API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Créer un pool élastique
Hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) applet de commande crée un pool élastique. les valeurs Hello pour eDTU par pool, min et max dtu sont limitées par la valeur de niveau de service hello (Basic, Standard, Premium ou Premium RS). Consultez l’article [Limites relatives aux eDTU et au stockage pour les pools de bases de données](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Créer une base de données regroupée dans un pool élastique
Hello d’utilisation [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) applet de commande et ensemble hello **ElasticPoolName** pool de paramètre toohello cible. toomove une base de données existante dans un pool élastique, consultez [déplacer une base de données dans un pool élastique](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Terminer le script
Ce script crée un groupe de ressources Azure et un serveur. Lorsque vous y êtes invité, fournissez un nom d’utilisateur administrateur et le mot de passe pour le nouveau serveur de hello (pas vos informations d’identification Azure).

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Créer un pool élastique et ajouter plusieurs bases de données regroupées
La création de plusieurs bases de données dans un pool élastique peut prendre un temps quand terminé à l’aide du portail de hello ou des applets de commande PowerShell créer uniquement une seule base de données à la fois. Création de tooautomate dans un pool élastique, consultez [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Déplacer une base de données dans un pool élastique
Vous pouvez déplacer une base de données dans ou hors d’un pool élastique hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Modifier les paramètres de performances d'un pool élastique
Lorsque les performances sont affectées, vous pouvez modifier les paramètres de hello de croissance de tooaccommodate pool hello. Hello d’utilisation [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) applet de commande. Définissez hello - Dtu paramètre toohello Edtu par pool. Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Modifier la limite de stockage hello pour un pool élastique

Hello d’utilisation [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) applet de commande tooset hello _- StorageMB_ paramètre. Fournir la limite de stockage hello Mo (par exemple, les jeux de 2097152 hello stockage limite too2 to). Consultez la section [Limites relatives aux eDTU et au stockage](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) pour connaître les valeurs acceptées.

> [!IMPORTANT]
> stockage de données max Hello par défaut par pool pour les pools Premium avec 1500 Edtu ou plus sont 750 Go. hello tooobtain supérieur _nombre maximum de taille de stockage de données par pool_, limite de stockage hello doit être explicitement définie. Les pools avec plus de 750 Go de stockage Premium est actuellement en version préliminaire publique Bonjour suivant régions : est des États-Unis 2, ouest des États-Unis, nous Gov Virginie, Europe de l’ouest, Allemagne Central, Asie du Sud-est, est du Japon, est de l’Australie, Canada Central et est du Canada.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Obtenir l’état de hello d’opérations de pool
Créer un pool élastique peut prendre un certain temps. état de hello tootrack des opérations, y compris la création et de mises à jour, utilisez hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) applet de commande.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Obtenir l’état de hello de déplacement d’une base de données dans et hors d’un pool élastique
Déplacer une base de données peut prendre un certain temps. Effectuer le suivi d’un état de déplacement à l’aide de hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) applet de commande.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obtenir les données d’utilisation des ressources d’un pool élastique
Métriques qui peuvent être récupérés sous forme de pourcentage de limite de pool de ressources hello :

| Nom de métrique | Description |
|:--- |:--- |
| cpu\_percent |Utilisation en pourcentage de limite hello du pool de hello moyenne du calcul. |
| physical\_data\_read\_percent |Utilisation d’e/s moyenne en pourcentage de limite hello du pool de hello. |
| log\_write\_percent |L’utilisation des ressources d’écriture moyenne en pourcentage de limite hello du pool de hello. |
| DTU\_consumption\_percent |Utilisation des eDTU moyenne en pourcentage de limite d’eDTU de pool de hello |
| storage\_percent |Moyenne de l’utilisation du stockage en pourcentage de limite de stockage hello du pool de hello. |
| workers\_percent |Traitements simultanés maximum (demandes) en pourcentage de limite hello du pool de hello. |
| sessions\_percent |Nombre maximal de sessions simultané en pourcentage de limite hello du pool de hello. |
| eDTU_limit |Nombre maximal de DTU de pool élastique pour ce pool élastique au cours de cet intervalle. |
| storage\_limit |Espace de stockage de pool élastique maximal pour ce pool élastique (en Mo) au cours de cet intervalle. |
| eDTU\_used |Edtu moyen utilisé par le pool de hello dans cet intervalle. |
| storage\_used |Stockage moyen utilisé par le pool de hello dans cet intervalle, en octets |

**Granularité des mesures/périodes de rétention :**

* Les données seront renvoyées avec une granularité de 5 minutes.  
* La durée de conservation des données est de 35 jours.  

Cette applet de commande et les API limite le nombre hello de lignes qui peuvent être récupérées dans un seul appel too1000 lignes (environ 3 jours de données au niveau de granularité de 5 minutes). Mais cette commande peut être appelée plusieurs fois avec tooretrieve d’intervalles de temps de début et de fin des données

métriques de hello tooretrieve :

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Afficher les données d’utilisation des ressources d’une base de données dans un pool élastique
Ces API sont hello identique hello API utilisées pour l’analyse de l’utilisation des ressources d’une base de données, à l’exception de hello suivant la différence de sémantique hello : métriques récupérés sont exprimées en pourcentage de hello par Edtu maximale de base de données (ou équivalent cap pour hello sous-jacent métrique de l’UC ou les e/s) définie pour ce pool. Par exemple, 50 % d’utilisation d’un de ces métriques indique que la consommation des ressources spécifiques hello est à 50 % de hello par limite d’extrémité de fin de base de données pour cette ressource dans le pool de parent hello.

métriques de hello tooretrieve :

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Ajouter une ressource de pool élastique tooan alerte
Vous pouvez ajouter des règles d’alerte tooan pool élastique toosend notifications par courrier électronique ou les chaînes d’alerte trop[les points de terminaison URL](https://msdn.microsoft.com/library/mt718036.aspx) lorsque pool élastique de hello atteint un seuil d’utilisation que vous avez configurée. Utilisez l’applet de commande Add-AzureRmMetricAlertRule de hello.

> [!IMPORTANT]
> La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes. La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge. Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée. Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.
>
>

Cet exemple ajoute une alerte pour recevoir une notification lorsque la consommation eDTU d’un pool élastique dépasse un certain seuil.

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

Pour plus d'informations, voir [Créer des alertes SQL Database dans le portail Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Ajouter des bases de données tooall les alertes d’un pool élastique
Vous pouvez ajouter des règles d’alerte tooall de base de données dans un pool élastique de toosend notifications par courrier électronique ou des chaînes d’alerte trop[les points de terminaison URL](https://msdn.microsoft.com/library/mt718036.aspx) lorsqu’une ressource atteint un seuil d’utilisation est configuré par l’alerte de hello.

> [!IMPORTANT]
> La surveillance de l’utilisation des ressources pour les pools élastiques subit un décalage d’au moins 5 minutes. La définition d’alertes de moins de 10 minutes pour les pools élastiques n’est actuellement pas prise en charge. Toutes les alertes définies pour les pools élastiques avec une période (paramètre appelé «-WindowSize » dans les API PowerShell) de moins de 10 minutes ne peut pas être déclenchée. Assurez-vous que les alertes que vous définissez pour les pools élastiques utilisent une période (WindowSize) de 10 minutes ou plus.
>

Cet exemple ajoute une alerte tooeach des bases de données hello dans un pool élastique pour recevoir une notification lorsque la consommation DTU de cette base de données dépasse certain seuil.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Collecter et surveiller les données d’utilisation des ressources dans plusieurs pools d’un abonnement
Lorsque vous avez plusieurs bases de données dans un abonnement, il est fastidieuse toomonitor chaque élastique pool séparément. Au lieu de cela, les applets de commande PowerShell de base de données SQL et les requêtes T-SQL peuvent être combiné toocollect ressources des données d’utilisation à partir de plusieurs pools et leurs bases de données pour la surveillance et l’analyse de l’utilisation des ressources. A [exemple d’implémentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) d’un ensemble de powershell scripts sont accessibles dans le référentiel d’exemples hello GitHub SQL Server, ainsi que la documentation sur ce qu’il fait et comment toouse il.

toouse cet exemple d’implémentation, procédez comme suit.

1. Télécharger hello [des scripts et la documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modifier les scripts hello pour votre environnement. Spécifiez le ou les serveurs qui hébergent les pools élastiques.
3. Spécifiez une base de données de télémétrie où hello métriques collectées sont toobe stockée.
4. Personnaliser hello script toospecify hello toute durée de l’exécution des scripts hello.

À un niveau élevé, les scripts de hello hello suivant :

* Il énumère tous les serveurs d’un abonnement Azure donné (ou d’une liste spécifiée de serveurs).
* Il exécute une tâche en arrière-plan pour chaque serveur. travail de Hello s’exécute dans une boucle à intervalles réguliers et collecte les données de télémétrie pour tous les pools hello dans le serveur de hello. Il charge ensuite les données de salutation collectée dans la base de données de télémétrie spécifié hello.
* Énumère une liste de bases de données dans chaque données d’utilisation de ressources de base de données pool toocollect hello. Il charge ensuite les données de salutation collectée dans la base de données de télémétrie hello.

Hello métriques collectées dans la base de données de télémétrie hello peuvent être analysées toomonitor la santé hello pools élastiques et bases de données hello qu’elle contient. script de Hello installe également une fonction de valeur de Table (TVF) prédéfinie dans hello de base de données toohelp d’agrégation hello les mesures de télémesure pour une fenêtre de temps spécifié. Par exemple, les résultats de hello TVF peuvent être utilisé tooshow « N premiers pools élastiques dont l’utilisation des eDTU maximale hello dans une fenêtre de temps donnée. » Si vous le souhaitez, utiliser les outils d’analyse comme tooquery Excel ou Power BI et analyser les données collectée de hello.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Exemple : obtenir des mesures de consommation des ressources pour un pool élastique et ses bases de données
Cet exemple récupère des métriques de consommation hello pour un pool élastique donné et toutes ses bases de données. Les données collectées sont mis en forme et écrites le fichier au format .csv de tooa. fichier de Hello peut être parcouru avec Excel.

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

## <a name="latency-of-elastic-pool-operations"></a>Latence des opérations du pool élastique
* La modification d’Edtu de min hello par base de données ou max Edtu par base de données généralement se termine dans 5 minutes ou moins.
* Modification des Edtu hello par pool dépend hello total de l’espace utilisé par toutes les bases de données dans le pool de hello. Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go. Par exemple, si hello l’espace total utilisé par toutes les bases de données dans le pool de hello est 200 Go, puis hello attendu de latence de modification hello eDTU du pool par pool est de 3 heures au maximum.



## <a name="next-steps"></a>Étapes suivantes
* [Créer des travaux élastique](sql-database-elastic-jobs-overview.md) travaux élastique vous permettre d’exécuter des scripts T-SQL par rapport à n’importe quel nombre de bases de données dans le pool de hello.
* Consultez [montée en puissance parallèle avec la base de données SQL Azure](sql-database-elastic-scale-introduction.md): utiliser tooscale outils élastique out, de déplacer des données, la requête ou la création des transactions.
