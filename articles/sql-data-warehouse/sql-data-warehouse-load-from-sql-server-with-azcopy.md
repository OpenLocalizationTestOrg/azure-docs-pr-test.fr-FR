---
title: "données aaaLoad à partir de SQL Server dans Azure SQL Data Warehouse (PolyBase) | Documents Microsoft"
description: "Utilise les données de tooexport bcp à partir de fichiers tooflat de SQL Server, le stockage blob tooAzure AZCopy tooimport données et les données de salutation tooingest PolyBase dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a>Charger des données à partir de SQL Server dans Azure SQL Data Warehouse (AZCopy)
Utilisez bcp et des données de tooload d’utilitaires de ligne de commande AZCopy à partir du stockage d’objets blob tooAzure SQL Server. Puis utilisez les données de salutation tooload PolyBase ou Azure Data Factory dans Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Composants requis
toostep dans ce didacticiel, vous devez :

* Base de données SQL Data Warehouse
* utilitaire de ligne de commande bcp Hello installé
* Hello utilitaire de ligne de commande SQLCMD installé

> [!NOTE]
> Vous pouvez télécharger les utilitaires bcp et sqlcmd hello hello [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>Importer des données dans SQL Data Warehouse
Dans ce didacticiel, vous créez une table dans Azure SQL Data Warehouse et importer des données dans la table de hello.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>Étape 1 : Créer une table dans Azure SQL Data Warehouse
À partir d’une invite de commandes, utilisez sqlcmd toorun hello est suivant de requête toocreate une table de votre instance de :

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

> [!NOTE]
> Consultez [vue d’ensemble de la Table] [ Table Overview] ou [syntaxe CREATE TABLE] [ CREATE TABLE syntax] pour plus d’informations sur la création d’une table sur SQL Data Warehouse et hello  options disponibles dans la clause WITH de hello.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>Étape 2 : Créer un fichier de données source
Ouvrez le bloc-notes, puis copiez hello après des lignes de données dans un nouveau fichier texte, puis enregistrez ce fichier tooyour répertoire temp local, C:\Temp\DimDate2.txt.

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

> [!NOTE]
> Il est important tooremember que bcp.exe ne prend pas en charge l’encodage du fichier hello UTF-8. Utilisez des fichiers ASCII ou codés en UTF-16 lors de l’utilisation de bcp.exe.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>Étape 3 : Se connecter et importer des données de hello
À l’aide de bcp, vous pouvez connecter et importer des données hello à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Vous pouvez vérifier les données ont été chargées en exécutant hello suivant la requête à l’aide de sqlcmd de hello :

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Cela doit retourner hello suivant des résultats :

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

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Étape 4 : Créer des statistiques sur vos données nouvellement chargées
Azure SQL Data Warehouse ne prend pas encore en charge les statistiques à création ou mise à jour automatique. Dans l’ordre tooget hello optimiser les performances de vos requêtes, il est important que créer des statistiques sur toutes les colonnes de toutes les tables après le premier chargement de hello ou toutes les modifications importantes se produisent dans les données de salutation. Pour obtenir une explication détaillée des statistiques, consultez hello [statistiques] [ Statistics] rubrique dans le groupe de développement hello de rubriques. Voici un exemple rapide de la façon dont les statistiques toocreate sur hello déposée chargement dans cet exemple

Exécutez hello suivant les instructions CREATE STATISTICS à partir d’une invite de commandes sqlcmd :

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>Exporter des données de SQL Data Warehouse
Dans ce didacticiel, vous allez créer un fichier de données à partir d’une table de SQL Data Warehouse. Vous exporterez les données hello créée précédemment tooa nouveau fichier de données appelé DimDate2_export.txt.

### <a name="step-1-export-hello-data"></a>Étape 1 : Exporter les données de salutation
L’utilitaire bcp de hello, vous pouvez connecter et exporter des données à l’aide de hello commande en remplaçant des valeurs hello comme appropriées suivantes :

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Vous pouvez vérifier hello données a été correctement exportées en ouvrant le fichier hello. les données de salutation dans le fichier de hello doivent correspondre au texte hello ci-dessous :

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

> [!NOTE]
> En raison de la nature toohello des systèmes distribués, ordre des données hello peut-être pas hello même sur les bases de données SQL Data Warehouse. Une autre option consiste à toouse hello **queryout** fonction de bcp toowrite une requête extrait au lieu d’exporter la totalité de la table hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Pour accéder à une vue d’ensemble du chargement, consultez [Charger des données dans SQL Data Warehouse][Load data into SQL Data Warehouse].
Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].

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
