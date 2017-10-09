---
title: "bases de données SQL Azure partitionnées aaaQuery | Documents Microsoft"
description: "Exécuter des requêtes entre les partitions à l’aide de la bibliothèque cliente de base de données élastique hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Requête sur plusieurs partitions
## <a name="overview"></a>Vue d'ensemble
Avec hello [outils de base de données élastique](sql-database-elastic-scale-introduction.md), vous pouvez créer des solutions de base de données partitionnée. **Requête sur plusieurs partitions** est utilisée pour des tâches telles que la collecte de données / la création de rapports qui nécessitent l'exécution d'une requête qui s'étend sur plusieurs partitions. (Comparez ceci trop[routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md), qui effectue tout le travail sur une partition unique.) 

1. Obtenir un [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) ou [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) à l’aide de hello [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), ou hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) (méthode). Consultez les rubriques [**Construction d’un objet ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) et [**Obtenir un objet RangeShardMap ou ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Créez un objet **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**.
3. Créez un objet **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Ensemble hello  **[la propriété CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa commande T-SQL.
5. Exécutez la commande hello en appelant hello  **[méthode ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Afficher les résultats de hello à l’aide de hello  **[MultiShardDataReader classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Exemple
Hello de code suivant illustre l’utilisation de hello de recherche à l’aide de partitions multiples une donnée **ShardMap** nommé *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


La principale différence est construction hello de connexions de plusieurs partitions. Où **SqlConnection** opère sur une base de données, hello **MultiShardConnection** prend un ***collection de partitions*** en entrée. Remplir la collection hello de partitions à partir d’une carte de partitions. Hello requête est ensuite exécutée sur la collection hello de partitions à l’aide de **UNION ALL** sémantique tooassemble un résultat global unique. Éventuellement, nom de hello de partition hello où provient de ligne de hello peuvent être ajoutés toohello de sortie à l’aide de hello **ExecutionOptions** propriété sur la commande. 

Notez les appels hello trop**myShardMap.GetShards()**. Cette méthode récupère toutes les partitions à partir de la carte de partitions hello et fournit un moyen simple de toorun une requête sur toutes les bases de données pertinentes. Hello collection de partitions pour une requête de plusieurs partition peut être affinée davantage en effectuant une LINQ interroger collection hello retournée à partir de l’appel de hello trop**myShardMap.GetShards()**. En association avec la stratégie de résultats partiels hello, capacité actuelle de hello lors de l’interrogation de plusieurs partitions a été conçue toowork bien pour des dizaines de toohundreds de partitions.

Une limitation de l’interrogation de plusieurs partitions est actuellement hello manque de validation pour les partitions et les shardlets sont interrogées. Alors que le routage dépendant des données vérifie qu’une partition donnée fait partie de carte de partitions hello au moment de hello d’interrogation, les requêtes de plusieurs partitions n’effectuent pas cette vérification. Cela peut entraîner des requêtes toomulti-partition en cours d’exécution sur les bases de données qui ont été supprimées de la carte de partitions hello.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Requêtes sur plusieurs partitions et opérations de fractionnement et de fusion
Requêtes de plusieurs partitions ne vérifient pas si les shardlets sur la base de données interrogées hello participent à des opérations de fusion et fractionnement en cours. (Consultez [mise à l’échelle à l’aide d’outil de hello fractionnement de base de données élastique-fusion](sql-database-elastic-scale-overview-split-and-merge.md).) Cela peut entraîner des tooinconsistencies où les lignes à partir de hello même afficher shardlet pour plusieurs bases de données Bonjour même requête de plusieurs partition. Prenez en compte ces limitations et prendre en compte la purge continue fusion et fractionnement opérations et des modifications toohello carte de partitions lors de l’exécution des requêtes de plusieurs partitions.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Voir aussi
Classes et méthodes **[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**.

Gérer des partitions à l’aide de hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md). Inclut un espace de noms appelé [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) qui fournit hello capacité tooquery plusieurs partitions à l’aide d’une requête unique et le résultat. Elle fournit une abstraction de requête sur une collection de partitions. Il fournit également des stratégies d’exécution alternatifs, les résultats partiels notamment, toodeal avec des erreurs lors de l’interrogation sur plusieurs partitions.  

