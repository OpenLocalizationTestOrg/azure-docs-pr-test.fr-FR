---
title: "aaaAdding une partition à l’aide des outils de base de données élastique | Documents Microsoft"
description: "Comment toouse API infrastructure élastique tooadd nouvelle partitions tooa partition définie."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a>Ajout d’une partition à l’aide des outils de base de données élastique
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd une partition pour une nouvelle plage ou une clé
Applications souvent besoin toosimply ajouter de nouvelles partitions toohandle données qui sont attendues de nouvelles clés ou des plages de clés pour une carte de partitions qui existe déjà. Par exemple, une application partitionnée par ID client peut-être tooprovision une nouvelle partition pour un nouveau client, ou mensuelle partitionnée de données peut-être une nouvelle partition configurée avant le début de hello de chaque nouveau mois. 

Si hello nouvelle plage de valeurs de clé n’est pas déjà partie d’un mappage existant, il est très simple tooadd hello nouvelle partition et associer hello nouvelle clé ou une plage toothat partition. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Exemple : ajout d’une partition et sa table de partition range tooan existant
Cet exemple utilise hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) méthodes et crée une instance de hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) classe. Dans l’exemple hello ci-dessous, une base de données nommée **sample_shard_2** et tous les objets de schéma nécessaires à l’intérieur ont été créées toohold plage [300, 400).  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


En guise d’alternative, vous pouvez utiliser Powershell toocreate un nouveau gestionnaire de carte de partitions. Un exemple est disponible [ici](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd une partition pour une partie vide d’une plage existante
Dans certains cas, vous avez déjà mappée une partition tooa de plage et partiellement avec des données, mais vous souhaitez maintenant différentes partitions de données à venir toobe tooa dirigée. Par exemple, vous partitions par jour de plage et avez déjà alloué partition tooa de 50 jours, mais le jour 24, que vous souhaitez tooland ultérieure de données dans une autre partition. base de données élastique Hello [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) peuvent effectuer cette opération, mais si le déplacement des données n’est pas nécessaire (par exemple, les données de la plage de hello de jours [25, 50), c'est-à-dire, too50 inclusive de jour 25 exclusive, n’existe pas encore) que vous pouvez effectuer Cette exclusivement à l’aide de hello directement API de gestion de carte de partitions.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Exemple : fractionnement d’une plage et l’affectation de hello vide partitions de nouvellement ajouté tooa partie
Une base de données nommée « sample_shard_2 » et tous les objets de schéma nécessaires qu’elle contient ont été créés.  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

**Important**: utilisez cette technique uniquement si vous êtes certain qu’hello plage pour le mappage de hello mis à jour est vide.  méthodes Hello ci-dessus ne vérifient pas les données de la plage de hello déplacé, il est donc préférable tooinclude vérifie dans votre code.  S’il existe des lignes dans la plage de hello en cours de déplacement, distribution des données réelles hello ne correspondre pas de carte de partitions mis à jour de hello. Hello d’utilisation [outil de fusion et fractionnement](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello opération au lieu de cela dans ces cas.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

