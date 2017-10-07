---
title: "aaaMigrate existant de bases de données montée tooscale | Documents Microsoft"
description: "Convertir des outils de bases de données partitionnées toouse élastique de base de données en créant un gestionnaire de carte de partitions"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Migrer tooscale-out de bases de données existant
Gérer facilement à grande échelle partitionnées bases de données existantes à l’aide des outils de base de données de base de données SQL Azure (par exemple hello [bibliothèque cliente de base de données élastique](sql-database-elastic-database-client-library.md)). Vous devez d’abord convertir un ensemble existant de hello toouse de bases de données [Gestionnaire de carte de partitions](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Vue d'ensemble
toomigrate une base de données partitionnée existante : 

1. Préparer hello [base de données de partition carte manager](sql-database-elastic-scale-shard-map-management.md).
2. Créer la carte de partitions hello.
3. Préparez les partitions hello.  
4. Ajoutez la carte de partitions toohello mappages.

Ces techniques peuvent être implémentés en utilisant soit hello [bibliothèque cliente .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), ou des scripts PowerShell hello trouvé à [Azure SQL DB - scripts d’outils de base de données élastique](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). exemples de Hello ici utilisent des scripts PowerShell de hello.

Pour plus d’informations sur hello ShardMapManager, consultez [gestion de carte de partitions](sql-database-elastic-scale-shard-map-management.md). Pour une vue d’ensemble d’outils de base de données élastique hello, consultez [vue d’ensemble des fonctionnalités de base de données élastique](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Préparer hello partition carte manager base de données
Gestionnaire de cartes de partitions Hello est une base de données spécial qui contient les bases de données à grande échelle hello données toomanage. Vous pouvez utiliser une base de données existante ou en créer une. Notez qu’une base de données qui agit comme gestionnaire de carte de partitions ne doit pas être hello même base de données comme une partition. Notez également que de script PowerShell hello ne crée pas de base de données hello pour vous. 

## <a name="step-1-create-a-shard-map-manager"></a>Étape 1 : créer un gestionnaire de cartes de partitions
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>Gestionnaire de cartes de partitions hello tooretrieve
Après la création, vous pouvez récupérer le Gestionnaire de carte de partitions hello avec cette applet de commande. Cette étape est nécessaire chaque fois que vous avez besoin toouse hello ShardMapManager objet.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Étape 2 : créer la carte de partitions hello
Vous devez sélectionner le type hello de toocreate de carte de partitions. choix de Hello dépend de l’architecture de base de données hello : 

1. Un seul locataire par base de données (pour les termes du contrat, consultez hello [glossaire](sql-database-elastic-scale-glossary.md).) 
2. Plusieurs clients par base de données (deux types) :
   1. Mappage de liste
   2. Mappage de plage

Pour un modèle de client unique, créez une carte de partitions de **mappage de liste** . modèle de locataire unique Hello assigne une base de données par client. Il s’agit d’un modèle efficace pour les développeurs SaaS, car il simplifie la gestion.

![Mappage de liste][1]

modèle d’architecture mutualisée Hello affecte plusieurs clients tooa une seule base de données (et vous pouvez distribuer des groupes de clients sur plusieurs bases de données). Utilisez ce modèle lorsque vous attendez que chaque données de petite taille toohave client a besoin. Dans ce modèle, nous affectons une plage d’utilisation de base de données clients tooa **mappage de plage**. 

![Mappage de plage][2]

Ou vous pouvez implémenter un modèle de base de données à l’aide un *mappage de liste* tooassign plusieurs locataires tooa base de données unique. Par exemple, DB1 est toostore utilisé plus d’informations sur l’id de client 1 et 5, et DB2 stocke des données pour les locataires 7 et client 10. 

![Plusieurs clients sur une base de données unique][3] 

**Selon votre choix, procédez de l’une des manières suivantes :**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Option 1 : Créer une carte de partitions pour un mappage de liste
Créer une carte de partitions à l’aide hello ShardMapManager objet. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Option 2 : Créer une carte de partitions pour un mappage de plage
Notez que tooutilize ce modèle de mappage, plages continue de toobe a besoin de valeurs d’id client il est donc écart toohave acceptable dans des plages hello en ignorant simplement des limites de hello lors de la création de bases de données hello.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Option 3 : Mappages de liste sur une base de données unique
La configuration de ce modèle nécessite également la création d’un mappage de liste comme indiqué à l’étape 2, option 1.

## <a name="step-3-prepare-individual-shards"></a>Étape 3 : préparer les partitions individuelles
Ajoutez chaque gestionnaire de carte de partitions toohello partitions (base de données). Elle prépare les bases de données individuelles hello pour le stockage des informations de mappage. Exécutez cette méthode sur chaque partition.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Étape 4 : Ajouter des mappages
Ajout de Hello de mappages dépend de type hello de carte de partitions que vous avez créé. Si vous avez créé un mappage de liste, vous ajoutez des mappages de liste. Si vous avez créé un mappage de plage, vous ajoutez des mappages de plage.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Option 1 : mapper des données hello pour un mappage de liste
Mapper les données de hello en ajoutant un mappage de liste pour chaque client.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Option 2 : mapper des données hello pour un mappage de plage
Ajouter des mappages de plage hello pour tous les hello client plage d’id - associations de base de données :

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Étape 4 option 3 : mapper des données de hello pour plusieurs clients sur une base de données
Pour chaque client, exécutez hello Add-ListMapping (option 1, ci-dessus). 

## <a name="checking-hello-mappings"></a>Vérification des mappages de hello
Pour plus d’informations sur les partitions existantes hello et les mappages de hello associées peuvent être interrogés à l’aide de commandes suivantes :  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Résumé
Une fois que vous avez terminé le programme d’installation hello, vous pouvez commencer la bibliothèque cliente de toouse hello élastique de base de données. Vous pouvez également utiliser le [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) et la [requête sur plusieurs partitions](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Étapes suivantes
Obtenir les scripts PowerShell hello [sripts des outils de base de données élastique de base de données Azure SQL](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

Hello outils sont également sur GitHub : [Azure/élastique-db-tools](https://github.com/Azure/elastic-db-tools).

Utilisez hello outil de fusion et fractionnement toomove données tooor d’un modèle de client unique tooa modèle mutualisé. Consultez [Outil de fractionnement et de fusion](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Ressources supplémentaires
Pour plus d’informations sur les modèles d’architecture de données des applications de base de données de logiciels en tant que service (SaaS) mutualisés, consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Questions et demandes de fonctionnalités
Pour toute question, veuillez contacter toous sur hello [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et pour les demandes de fonctionnalités, ajoutez-les toohello [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

