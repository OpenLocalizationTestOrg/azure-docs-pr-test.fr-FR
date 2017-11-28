---
title: "Bien démarrer avec le langage U-SQL | Microsoft Docs"
description: "Découvrez les principes de base du langage U-SQL."
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="f55f6-103">Bien démarrer avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="f55f6-103">Get started with U-SQL</span></span>
<span data-ttu-id="f55f6-104">U-SQL est un langage qui combine le langage SQL déclaratif avec le langage C# impératif pour vous permettre de traiter des données quelle que soit l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f55f6-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="f55f6-105">La fonctionnalité évolutive de requête distribuée d’U-SQL vous permet d’analyser efficacement les données entre magasins relationnels comme Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f55f6-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="f55f6-106">Avec U-SQL, vous pouvez traiter des données non structurées en appliquant des schémas de lecture et en insérant une logique personnalisée et des fonctions définies par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f55f6-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="f55f6-107">En outre, U-SQL comprend l’extensibilité qui vous donne un contrôle précis sur l’exécution à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="f55f6-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="f55f6-108">Ressources d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="f55f6-108">Learning resources</span></span>

* <span data-ttu-id="f55f6-109">Le [Didacticiel U-SQL](http://aka.ms/usqltutorial) fournit une procédure pas à pas pour la plupart du langage U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f55f6-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="f55f6-110">La lecture de ce document est recommandée pour tous les développeurs qui veulent apprendre le langage U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f55f6-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="f55f6-111">Pour plus d’informations sur la **syntaxe du langage U-SQL**, consultez la [Référence du langage U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="f55f6-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="f55f6-112">Pour comprendre la [philosophie de conception d’U-SQL](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/), consultez l’article de blog Visual Studio **Présentation d’U-SQL – Un langage qui facilite le traitement du Big Data**.</span><span class="sxs-lookup"><span data-stu-id="f55f6-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f55f6-113">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f55f6-113">Prerequisites</span></span>

<span data-ttu-id="f55f6-114">Avant de parcourir les exemples U-SQL de ce document, lisez et suivez le [Didacticiel : Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f55f6-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="f55f6-115">Ce didacticiel explique les mécanismes de l’utilisation d’U-SQL avec Azure Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f55f6-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="f55f6-116">Votre premier script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f55f6-116">Your first U-SQL script</span></span>

<span data-ttu-id="f55f6-117">Le script U-SQL suivant est simple et nous permet d’explorer de nombreux aspects du langage U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f55f6-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="f55f6-118">Ce script n'a aucune étape de transformation.</span><span class="sxs-lookup"><span data-stu-id="f55f6-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="f55f6-119">Il lit le fichier source nommé `SearchLog.tsv`, le schématise et écrit l’ensemble de lignes dans un fichier nommé SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="f55f6-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="f55f6-120">Notez le point d'interrogation en regard du type de données dans le champ `Duration`.</span><span class="sxs-lookup"><span data-stu-id="f55f6-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="f55f6-121">Il signifie que le champ `Duration` pourrait avoir la valeur Null.</span><span class="sxs-lookup"><span data-stu-id="f55f6-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="f55f6-122">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="f55f6-122">Key concepts</span></span>
* <span data-ttu-id="f55f6-123">**Variables de l'ensemble de lignes**: toute expression de requête qui produit un ensemble de lignes peut être affectée à une variable.</span><span class="sxs-lookup"><span data-stu-id="f55f6-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="f55f6-124">U-SQL suit le modèle d’affectation de noms variable T-SQL (`@searchlog`, par exemple) dans le script.</span><span class="sxs-lookup"><span data-stu-id="f55f6-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="f55f6-125">Le mot-clé **EXTRACT** lit les données d’un fichier et définit le schéma à la lecture.</span><span class="sxs-lookup"><span data-stu-id="f55f6-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="f55f6-126">`Extractors.Tsv` est un extracteur U-SQL intégré pour les fichiers de valeurs séparées par des tabulations.</span><span class="sxs-lookup"><span data-stu-id="f55f6-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="f55f6-127">Vous pouvez développer des extracteurs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f55f6-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="f55f6-128">**OUTPUT** écrit les données dans un fichier à partir d’un ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="f55f6-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="f55f6-129">`Outputters.Csv()` est un générateur de sortie U-SQL intégré pour créer un fichier de valeurs séparées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="f55f6-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="f55f6-130">Vous pouvez développer des générateurs de sortie personnalisés.</span><span class="sxs-lookup"><span data-stu-id="f55f6-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="f55f6-131">Chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="f55f6-131">File paths</span></span>

<span data-ttu-id="f55f6-132">Les instructions EXTRACT et OUTPUT utilisent des chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="f55f6-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="f55f6-133">Les chemins d’accès peuvent être absolus ou relatifs :</span><span class="sxs-lookup"><span data-stu-id="f55f6-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="f55f6-134">Le chemin d’accès absolu suivant fait référence à un fichier dans un Data Lake Store nommé `mystore` :</span><span class="sxs-lookup"><span data-stu-id="f55f6-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="f55f6-135">Le chemin d’accès suivant commence par `"/"`.</span><span class="sxs-lookup"><span data-stu-id="f55f6-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="f55f6-136">Il fait référence à un fichier dans le compte Data Lake Store par défaut :</span><span class="sxs-lookup"><span data-stu-id="f55f6-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="f55f6-137">Utiliser des variables scalaires</span><span class="sxs-lookup"><span data-stu-id="f55f6-137">Use scalar variables</span></span>

<span data-ttu-id="f55f6-138">Vous pouvez également utiliser des variables scalaires pour faciliter la maintenance de votre script.</span><span class="sxs-lookup"><span data-stu-id="f55f6-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="f55f6-139">Le script U-SQL précédent peut également s'écrire comme suit :</span><span class="sxs-lookup"><span data-stu-id="f55f6-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="f55f6-140">Transformer des ensembles de lignes</span><span class="sxs-lookup"><span data-stu-id="f55f6-140">Transform rowsets</span></span>

<span data-ttu-id="f55f6-141">Utilisez **SELECT** pour transformer des ensembles de lignes :</span><span class="sxs-lookup"><span data-stu-id="f55f6-141">Use **SELECT** to transform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="f55f6-142">La clause WHERE utilise une [expression booléenne C#](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="f55f6-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="f55f6-143">Vous pouvez utiliser le langage d'expressions C# pour faire vos propres expressions et fonctions.</span><span class="sxs-lookup"><span data-stu-id="f55f6-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="f55f6-144">Vous pouvez même effectuer un filtrage plus complexe en les combinant avec des conjonctions logiques (AND) et des disjonctions (OR).</span><span class="sxs-lookup"><span data-stu-id="f55f6-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="f55f6-145">Le script suivant utilise la méthode DateTime.Parse() et une conjonction.</span><span class="sxs-lookup"><span data-stu-id="f55f6-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="f55f6-146">La deuxième requête fonctionne sur le résultat du premier ensemble de lignes, ce qui crée une combinaison des deux filtres.</span><span class="sxs-lookup"><span data-stu-id="f55f6-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="f55f6-147">Vous pouvez également réutiliser un nom de variable, et les noms ont une portée lexicale.</span><span class="sxs-lookup"><span data-stu-id="f55f6-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="f55f6-148">Ensembles de lignes agrégés</span><span class="sxs-lookup"><span data-stu-id="f55f6-148">Aggregate rowsets</span></span>
<span data-ttu-id="f55f6-149">U-SQL vous fournit les ORDER BY, GROUP BY et les agrégations que vous connaissez déjà.</span><span class="sxs-lookup"><span data-stu-id="f55f6-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="f55f6-150">La requête suivante recherche la durée totale par région, puis affiche les cinq premières durées dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="f55f6-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="f55f6-151">Les ensembles de lignes U-SQL ne conservent pas leur ordre pour la requête suivante.</span><span class="sxs-lookup"><span data-stu-id="f55f6-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="f55f6-152">Par conséquent, pour ordonner un résultat, vous devez ajouter ORDER BY à l'instruction OUTPUT :</span><span class="sxs-lookup"><span data-stu-id="f55f6-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="f55f6-153">La clause U-SQL ORDER BY exige l’utilisation de la clause FETCH dans une expression SELECT.</span><span class="sxs-lookup"><span data-stu-id="f55f6-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="f55f6-154">La clause U-SQL HAVING peut être utilisée pour restreindre le résultat aux groupes qui remplissent la condition HAVING :</span><span class="sxs-lookup"><span data-stu-id="f55f6-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="f55f6-155">Pour les scénarios d’agrégation avancés, consultez la documentation de référence U-SQL sur les [fonctions d’agrégation, d’analytique et de référence](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="f55f6-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55f6-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f55f6-156">Next steps</span></span>
* [<span data-ttu-id="f55f6-157">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f55f6-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f55f6-158">Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f55f6-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
