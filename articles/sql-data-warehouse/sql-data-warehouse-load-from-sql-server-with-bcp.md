---
title: "données aaaLoad à partir de SQL Server dans Azure SQL Data Warehouse (bcp) | Documents Microsoft"
description: "Pour une taille de données de petite taille, utilise les données tooexport de bcp à partir de fichiers tooflat de SQL Server et importer des données hello directement dans l’entrepôt de données SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (fichiers plats)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Pour les petits jeux de données, vous pouvez utiliser utilitaire de ligne de commande bcp hello tooexport des données à partir de SQL Server et puis de le charger directement tooAzure SQL Data Warehouse.

Dans ce didacticiel, nous allons utiliser bcp pour :

* Exportez une table à partir de SQL Server à l’aide de bcp hello commande (ou créer un exemple simple de fichier)
* Table hello d’importation à partir d’un fichier plat de tooSQL l’entrepôt de données.
* Créer des statistiques sur les données de salutation chargée.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Avant de commencer
### <a name="prerequisites"></a>Composants requis
toostep dans ce didacticiel, vous devez :

* Base de données SQL Data Warehouse
* utilitaire de ligne de commande de Hello bcp installé
* utilitaire de ligne de commande de Hello sqlcmd installé

Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>Données au format ASCII ou UTF-16
Si vous essayez de ce didacticiel avec vos propres données, vos données doivent toouse hello ASCII ou UTF-16 encodage bcp ne prenant pas en charge UTF-8. 

PolyBase prend en charge UTF-8, mais pas UTF-16 pour l’instant. Notez que si vous souhaitez que bcp toocombine avec PolyBase vous devez tootransform hello données tooUTF-8 après son exportation à partir de SQL Server. 

## <a name="1-create-a-destination-table"></a>1. Créer une table de destination
Définir une table dans l’entrepôt de données SQL qui sera la table de destination hello pour la charge hello. les colonnes dans la table de hello Hello doivent correspondre toohello des données dans chaque ligne de votre fichier de données.

toocreate une table, ouvrez une invite de commandes et utilisez sqlcmd.exe hello de toorun commande suivante :

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a>2. Créer un fichier de données source
Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt. Ces données sont au format ASCII.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

(Facultatif) tooexport vos propres données à partir d’une base de données SQL Server, ouvrez une invite de commandes et exécutez hello commande suivante. Remplacez TableName, ServerName, DatabaseName, Username et Password par vos propres informations.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Charger des données hello
les données de salutation tooload, ouvrez une invite de commandes et exécutez les hello commande suivante, en remplaçant les valeurs hello pour le nom du serveur, nom de base de données, nom d’utilisateur et mot de passe avec vos propres informations.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Utilisez cette commande hello tooverify données a été correctement chargées.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

résultats de Hello doivent ressembler à ceci :

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

## <a name="4-create-statistics"></a>4. Create statistics
SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique. tooget hello meilleures performances des requêtes, il est important toocreate des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation. Pour obtenir une explication détaillée des statistiques, consultez [Statistiques][Statistics]. 

La commande suivante d’exécution hello toocreate des statistiques sur la table qui vient d’être chargée.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. Exporter des données de SQL Data Warehouse
Pour vous amuser, vous pouvez exporter les données de hello chargée hors de l’entrepôt de données SQL.  tooexport de commande Hello est exactement hello identique à l’exportation à partir de SQL Server.

Toutefois, il est d’une différence dans les résultats de hello. Étant donné que les données de salutation sont stockées dans des emplacements distribués au sein de l’entrepôt de données SQL, lorsque vous exportez des données de chaque nœud de calcul écrit fichier de sortie toohello de données. commande Hello de données hello dans le fichier de sortie hello est probablement toobe autre que l’ordre de hello de données hello dans le fichier d’entrée de hello.

### <a name="export-a-table-and-compare-exported-results"></a>Exporter une table et comparer les résultats exportés
toosee hello données exportées, ouvrez une invite de commandes et exécuter cette commande à l’aide de vos propres paramètres. Nom_serveur est le nom hello de votre serveur de SQL Azure logiques.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Vous pouvez vérifier hello données a été correctement exportées en ouvrant le fichier hello. données Hello dans le fichier de hello doivent correspondre au texte hello ci-dessous, mais il seront probablement être triées dans un ordre différent :

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a>Exporter les résultats d’une requête hello
Vous pouvez utiliser hello **queryout** fonction des résultats de hello bcp tooexport d’une requête plutôt que d’exporter la totalité de la table hello. 

## <a name="next-steps"></a>Étapes suivantes
Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].
Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].
Pour plus d’informations sur la création d’une table sur SQL Data Warehouse, consultez [Vue d’ensemble des tables][Table Overview] ou la syntaxe [CREATE TABLE][CREATE TABLE syntax].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
