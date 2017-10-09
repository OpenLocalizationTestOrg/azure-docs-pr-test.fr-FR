---
title: Prise en main les catalogue hello U-SQL | Documents Microsoft
description: "Découvrez comment toouse hello U-SQL catalogue tooshare code et des données."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a>Prise en main hello catalogue U-SQL

## <a name="create-a-tvf"></a>Création d'une TVF

Dans le script U-SQL de la précédente hello, vous répété utiliser hello tooread extrait à partir de hello même fichier source. Avec la fonction table hello U-SQL (TVF), vous pouvez encapsuler des données hello pour une réutilisation ultérieure.  

Hello script suivant crée une fonction table appelée `Searchlog()` dans la base de données par défaut hello et le schéma :

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

Hello script suivant vous montre comment toouse hello fonction table qui a été défini dans le script précédent de hello :

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a>Créer des vues

Si vous avez une expression de requête unique, au lieu d’une fonction table vous pouvez utiliser une vue U-SQL de tooencapsulate cette expression.

Hello script suivant crée une vue appelée `SearchlogView` dans la base de données par défaut hello et le schéma :

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

Hello script suivant illustre l’utilisation de hello de vue de hello définis :

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a>créez des tables
Comme avec les tables de base de données relationnelle, avec U-SQL vous pouvez créer une table avec un schéma prédéfini ou créer une table qui déduit schéma hello requête hello qui remplit la table hello (également appelé CREATE TABLE AS SELECT ou SACT).

Créer une base de données et deux tables à l’aide de hello script suivant :

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a>Tables de requête
Vous pouvez interroger les tables, telles que celles créées dans le script précédent hello, Bonjour même façon que vous interrogez des fichiers de données hello. Au lieu de créer un ensemble de lignes à l’aide d’extraction, vous pouvez maintenant faire toohello nom de la table.

tooread à partir des tables de hello, modifier le script de transformation hello que vous avez utilisé précédemment :

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 >Actuellement, vous ne peut pas exécuter une instruction SELECT sur une table Bonjour même script comme un hello où vous avez créé la table de hello.

## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
