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
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="82126-103">Prise en main hello catalogue U-SQL</span><span class="sxs-lookup"><span data-stu-id="82126-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="82126-104">Création d'une TVF</span><span class="sxs-lookup"><span data-stu-id="82126-104">Create a TVF</span></span>

<span data-ttu-id="82126-105">Dans le script U-SQL de la précédente hello, vous répété utiliser hello tooread extrait à partir de hello même fichier source.</span><span class="sxs-lookup"><span data-stu-id="82126-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="82126-106">Avec la fonction table hello U-SQL (TVF), vous pouvez encapsuler des données hello pour une réutilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="82126-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="82126-107">Hello script suivant crée une fonction table appelée `Searchlog()` dans la base de données par défaut hello et le schéma :</span><span class="sxs-lookup"><span data-stu-id="82126-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="82126-108">Hello script suivant vous montre comment toouse hello fonction table qui a été défini dans le script précédent de hello :</span><span class="sxs-lookup"><span data-stu-id="82126-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

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

## <a name="create-views"></a><span data-ttu-id="82126-109">Créer des vues</span><span class="sxs-lookup"><span data-stu-id="82126-109">Create views</span></span>

<span data-ttu-id="82126-110">Si vous avez une expression de requête unique, au lieu d’une fonction table vous pouvez utiliser une vue U-SQL de tooencapsulate cette expression.</span><span class="sxs-lookup"><span data-stu-id="82126-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="82126-111">Hello script suivant crée une vue appelée `SearchlogView` dans la base de données par défaut hello et le schéma :</span><span class="sxs-lookup"><span data-stu-id="82126-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="82126-112">Hello script suivant illustre l’utilisation de hello de vue de hello définis :</span><span class="sxs-lookup"><span data-stu-id="82126-112">hello following script demonstrates hello use of hello defined view:</span></span>

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

## <a name="create-tables"></a><span data-ttu-id="82126-113">créez des tables</span><span class="sxs-lookup"><span data-stu-id="82126-113">Create tables</span></span>
<span data-ttu-id="82126-114">Comme avec les tables de base de données relationnelle, avec U-SQL vous pouvez créer une table avec un schéma prédéfini ou créer une table qui déduit schéma hello requête hello qui remplit la table hello (également appelé CREATE TABLE AS SELECT ou SACT).</span><span class="sxs-lookup"><span data-stu-id="82126-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="82126-115">Créer une base de données et deux tables à l’aide de hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="82126-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="82126-116">Tables de requête</span><span class="sxs-lookup"><span data-stu-id="82126-116">Query tables</span></span>
<span data-ttu-id="82126-117">Vous pouvez interroger les tables, telles que celles créées dans le script précédent hello, Bonjour même façon que vous interrogez des fichiers de données hello.</span><span class="sxs-lookup"><span data-stu-id="82126-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="82126-118">Au lieu de créer un ensemble de lignes à l’aide d’extraction, vous pouvez maintenant faire toohello nom de la table.</span><span class="sxs-lookup"><span data-stu-id="82126-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="82126-119">tooread à partir des tables de hello, modifier le script de transformation hello que vous avez utilisé précédemment :</span><span class="sxs-lookup"><span data-stu-id="82126-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
 ><span data-ttu-id="82126-120">Actuellement, vous ne peut pas exécuter une instruction SELECT sur une table Bonjour même script comme un hello où vous avez créé la table de hello.</span><span class="sxs-lookup"><span data-stu-id="82126-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82126-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82126-121">Next Steps</span></span>
* [<span data-ttu-id="82126-122">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="82126-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="82126-123">Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82126-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="82126-124">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="82126-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
