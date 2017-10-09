---
title: "aaaReporting sur les bases de données à grande échelle cloud | Documents Microsoft"
description: "Comment tooset les requêtes élastiques sur les partitions horizontales"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Création de rapports sur des bases de données cloud mises à l’échelle (version préliminaire)
![Requête sur plusieurs partitions][1]

Les bases de données partitionnées répartissent des lignes sur une mise à l’échelle vers la couche données. schéma de Hello est identique sur toutes les bases de données participantes, également connus sous le partitionnement horizontal. En utilisant une requête élastique, vous pouvez créer des rapports qui couvrent toutes les bases de données d’une base de données partitionnée.

Pour démarrer rapidement, consultez la rubrique [Création de rapports sur des bases de données cloud mises à l’échelle](sql-database-elastic-query-getting-started.md).

Pour les bases de données non partitionnées, consultez [Interroger plusieurs bases de données cloud avec différents schémas](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Composants requis
* Créer une carte de partitions à l’aide de la bibliothèque cliente de base de données élastique hello. Consultez la rubrique [Gestion des cartes de partitions](sql-database-elastic-scale-shard-map-management.md). Ou utilisez l’exemple d’application hello dans [prise en main des outils de base de données élastique](sql-database-elastic-scale-get-started.md).
* Vous pouvez aussi consulter [existant de la migration des bases de données bases de données tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* utilisateur de Hello doit posséder les autorisations ALTER ANY EXTERNAL DATA SOURCE. Cette autorisation est incluse avec l’autorisation ALTER DATABASE hello.
* Les autorisations ALTER ANY EXTERNAL DATA SOURCE sont toohello nécessaires toorefer source de données sous-jacente.

## <a name="overview"></a>Vue d'ensemble
Ces instructions créent représentation des métadonnées hello de votre couche données partitionnées dans base de données de requête élastique hello. 

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 Créer la clé principale et les informations d’identification de la base de données
informations d’identification Hello sont utilisée par hello requête élastique tooconnect tooyour bases de données distantes.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Vérifiez que hello *»\<nom d’utilisateur\>»* ne comprend aucun *»@servername»* suffixe. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Créer des sources de données externes
Syntaxe :

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Exemple
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Récupérer la liste de hello de sources de données externes en cours : 

    select * from sys.external_data_sources; 

source de données externe Hello fait référence à votre carte de partitions. Une requête élastique utilise ensuite la source de données externe hello et hello sous-jacent partition carte tooenumerate hello bases de données participant à la couche de données hello. carte de partitions hello tooread utilisés sont Hello mêmes informations d’identification et tooaccess hello des données sur les partitions hello lors du traitement de hello d’une requête élastique. 

## <a name="13-create-external-tables"></a>1.3 Créer des tables externes
Syntaxe :  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Exemple**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Récupérer la liste hello des tables externes à partir de la base de données actuelle hello : 

    SELECT * from sys.external_tables; 

toodrop des tables externes :

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Remarques
Hello données\_clause SOURCE définit la source de données externe hello (une carte de partitions) qui est utilisé pour une table externe hello.  

Hello schéma\_nom et l’objet\_mappent les clauses de nom table de tooa de définition de table externe hello dans un schéma différent. Si omis, schéma hello d’objet distant de hello est considéré comme étant toobe « dbo » et son nom est nom de la table externe identiques toohello toobe en cours de définition. Cela est utile si hello nom de votre table distante est déjà utilisé dans la base de données hello où vous souhaitez une table externe toocreate hello. Par exemple, vous toodefine une tooget table externe une vue agrégée des affichages catalogue ou sur vos données à l’échelle des vues de gestion dynamique de niveau. Étant donné que les affichages catalogue et vues de gestion dynamique existent déjà localement, vous ne pouvez pas utiliser leur nom pour la définition de la table externe hello. Au lieu de cela, utilisez un autre nom et d’utiliser la vue de catalogue hello ou hello nom DMV Bonjour schéma\_nom et/ou objet\_clauses de nom. (Consultez l’exemple hello ci-dessous.) 

DISTRIBUTION Hello spécifie la distribution des données hello utilisée pour cette table. processeur de requêtes Hello utilise les informations hello fournies dans le plans de requête plus efficace de hello DISTRIBUTION clause toobuild hello.  

1. **PARTITIONNÉE** signifie que les données sont partitionnées horizontalement sur les bases de données hello. Hello clé de partitionnement pour la distribution des données hello est hello **< sharding_column_name >** paramètre.
2. **RÉPLIQUÉES** signifie que des copies identiques de la table de hello sont présents sur chaque base de données. Il s’agit de votre tooensure responsabilité que les réplicas hello sont identiques entre les bases de données hello.
3. **ROUND\_(Round Robin)** signifie que la table hello est partitionnée horizontalement à l’aide d’une méthode de distribution de dépend de l’application. 

**Couche de données référence**: une table externe hello DDL fait référence la source de données externe tooan. source de données externe Hello spécifie une carte de partitions qui procure une table externe hello toolocate nécessaire des informations de hello toutes les bases de données hello dans votre couche données. 

### <a name="security-considerations"></a>Considérations relatives à la sécurité
Les utilisateurs avec une table externe accès toohello automatiquement accéder toohello les tables distantes sous-jacentes sous les informations d’identification hello donné dans la définition de source de données externe hello. Évitez indésirable élévation de privilèges via les informations d’identification hello hello externe de source de données. Utilisez GRANT ou REVOKE pour une table externe, comme s'il s'agissait d'une table standard.  

Une fois votre table externe et votre source de données externe définies, vous pouvez utiliser l’ensemble T-SQL complet sur vos tables externes.

## <a name="example-querying-horizontal-partitioned-databases"></a>Exemple : interrogation de bases de données partitionnées horizontales
Hello requête suivante effectue une jointure tridirectionnelle entre entrepôts, les commandes et les lignes de commande et utilise plusieurs agrégats et un filtre sélectif. Il suppose que le partitionnement (1) horizontal (partitionnement) et (2) qu’entrepôts, les commandes et les lignes de commande sont partitionnées par la colonne d’id de l’entrepôt hello, et cette requête élastique hello peut colocaliser les jointures hello sur les partitions hello et traiter la partie de la requête hello sur hello coûteuse de hello partitions en parallèle. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Procédure stockée pour l’exécution de T-SQL à distance : sp\_execute_remote
Requête élastique présente également une procédure stockée qui offre un accès direct toohello partitions. Hello procédure stockée est appelée [sp\_exécuter \_distant](https://msdn.microsoft.com/library/mt703714) et peut être utilisé tooexecute des procédures stockées distantes ou le code T-SQL sur des bases de données distantes hello. Il prend hello paramètres suivants : 

* Nom de source de données (nvarchar) : nom hello hello externe de source de données de type SGBDR. 
* Requête (nvarchar) : hello T-SQL toobe de requête exécutée sur chaque partition. 
* Déclaration de paramètre (nvarchar) - facultatif : chaîne avec les définitions de type de données pour les paramètres de hello utilisés dans le paramètre de requête hello (comme sp_executesql). 
* Liste de valeurs de paramètre : facultative : valeurs de paramètre de liste séparées par des virgules (par exemple, sp_executesql).

Hello sp\_exécuter\_distant utilise hello prévue hello appel paramètres tooexecute hello donné l’instruction T-SQL sur des bases de données distantes hello de source de données externe. Elle utilise les informations d’identification hello de hello données externes tooconnect toohello shardmap manager base de données source et de bases de données distantes hello.  

Exemple : 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Connectivité des outils
Utilisez tooconnect de chaînes de connexion SQL Server standard votre application, votre BI et données intégration outils toohello base de données avec vos définitions de table externe. Assurez-vous que SQL Server est pris en charge comme source de données pour votre outil. Ensuite référencer la base de données de requête élastique hello comme tout autre outil de toohello de connexion de base de données SQL Server et utiliser des tables externes à partir de votre application ou un outil comme si elles étaient des tables locales. 

## <a name="best-practices"></a>Meilleures pratiques
* Assurez-vous que cette base de données de point de terminaison de la requête élastique hello a reçu toutes les partitions via hello que pare-feu de base de données SQL et la base de données access toohello shardmap.  
* Valider ou appliquer la distribution des données définie par une table externe hello hello. Si la distribution réelle des données est différente de la distribution hello spécifiée dans votre définition de la table, vos requêtes peuvent donner des résultats inattendus. 
* Requête élastique actuellement n’effectue pas élimination de partition lorsque les prédicats de clé de partitionnement hello elle permettrait toosafely exclure certaines partitions à partir du traitement.
* Requête élastique mieux adaptée pour les requêtes où la plupart des calculs de hello peut être effectuée sur les partitions hello. Vous obtenez généralement hello meilleurs résultats avec des prédicats de filtre sélectif qui peut être évaluée sur les partitions hello ou des jointures sur hello clés qui peuvent être effectuées de manière alignées sur toutes les partitions de partitionnement. Autres modèles de requête peuvent nécessiter des tooload grandes quantités de données à partir du nœud principal hello partitions toohello et peuvent être lent

## <a name="next-steps"></a>Étapes suivantes

* Pour une présentation des requêtes élastiques, consultez [Présentation des requêtes élastiques](sql-database-elastic-query-overview.md).
* Pour le didacticiel sur le partitionnement vertical, consultez [Prise en main des requêtes de bases de données croisées (partitionnement vertical)](sql-database-elastic-query-getting-started-vertical.md).
* Pour la syntaxe et des exemples de requêtes pour des données partitionnées verticalement, consultez [Requêtes sur des données partitionnées verticalement](sql-database-elastic-query-vertical-partitioning.md)
* Pour commencer le didacticiel sur le partitionnement horizontal (sharding), consultez [Prise en main des requêtes élastiques pour le partitionnement horizontal (sharding)](sql-database-elastic-query-getting-started.md).
* Consultez [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) pour une procédure stockée qui exécute une instruction Transact-SQL sur une seule base de données Azure SQL distante ou un ensemble de bases de données servant de partitions dans un schéma de partitionnement horizontal.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
