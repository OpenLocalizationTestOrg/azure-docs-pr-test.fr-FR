---
title: Prise en main du catalogue U-SQL | Microsoft Docs
description: "Découvrez comment utiliser le catalogue U-SQL pour partager du code et des données."
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
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="b0f33-103">Prise en main du catalogue U-SQL</span><span class="sxs-lookup"><span data-stu-id="b0f33-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="b0f33-104">Création d'une TVF</span><span class="sxs-lookup"><span data-stu-id="b0f33-104">Create a TVF</span></span>

<span data-ttu-id="b0f33-105">Dans le script U-SQL précédent, vous avez réutilisé EXTRACT pour lire depuis le même fichier source.</span><span class="sxs-lookup"><span data-stu-id="b0f33-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="b0f33-106">Avec la fonction table U-SQL, vous pouvez encapsuler les données pour une réutilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b0f33-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="b0f33-107">Le script suivant crée une TVF appelée `Searchlog()` dans la base de données et le schéma par défaut :</span><span class="sxs-lookup"><span data-stu-id="b0f33-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

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

<span data-ttu-id="b0f33-108">Le script suivant montre comment utiliser la fonction table définie dans le script précédent :</span><span class="sxs-lookup"><span data-stu-id="b0f33-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="b0f33-109">Créer des vues</span><span class="sxs-lookup"><span data-stu-id="b0f33-109">Create views</span></span>

<span data-ttu-id="b0f33-110">Si vous avez une expression de requête unique, vous pouvez utiliser une vue U-SQL pour encapsuler cette expression, plutôt qu’une TVF.</span><span class="sxs-lookup"><span data-stu-id="b0f33-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="b0f33-111">Le script suivant crée une vue appelée `SearchlogView` dans la base de données et le schéma par défaut :</span><span class="sxs-lookup"><span data-stu-id="b0f33-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

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

<span data-ttu-id="b0f33-112">Le script suivant montre l'utilisation de la vue définie :</span><span class="sxs-lookup"><span data-stu-id="b0f33-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="b0f33-113">créez des tables</span><span class="sxs-lookup"><span data-stu-id="b0f33-113">Create tables</span></span>
<span data-ttu-id="b0f33-114">De façon similaire aux tables de base de données relationnelle, U-SQL vous permet de créer une table avec un schéma prédéfini ou de créer une table et de déduire le schéma à partir de la requête de remplissage de la table (également appelée CREATE TABLE AS SELECT ou CTAS).</span><span class="sxs-lookup"><span data-stu-id="b0f33-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="b0f33-115">Créez une base de données et deux tables avec le script suivant :</span><span class="sxs-lookup"><span data-stu-id="b0f33-115">Create a database and two tables by using the following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="b0f33-116">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="b0f33-116">Query tables</span></span>
<span data-ttu-id="b0f33-117">Vous pouvez interroger des tables, par exemple celles que vous avez créées dans le script précédent, de la même manière que vous interrogez les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="b0f33-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="b0f33-118">Au lieu de créer un ensemble de lignes avec EXTRACT, vous pouvez maintenant faire référence au nom de table.</span><span class="sxs-lookup"><span data-stu-id="b0f33-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="b0f33-119">Pour lire à partir des tables, modifiez le script de transformation que vous avez utilisé précédemment :</span><span class="sxs-lookup"><span data-stu-id="b0f33-119">To read from the tables, modify the transform script that you used previously:</span></span>

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
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="b0f33-120">Actuellement, vous ne pouvez pas exécuter une instruction SELECT sur une table dans le script dans lequel vous avez créé cette table.</span><span class="sxs-lookup"><span data-stu-id="b0f33-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0f33-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b0f33-121">Next Steps</span></span>
* [<span data-ttu-id="b0f33-122">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b0f33-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b0f33-123">Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b0f33-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="b0f33-124">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0f33-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
