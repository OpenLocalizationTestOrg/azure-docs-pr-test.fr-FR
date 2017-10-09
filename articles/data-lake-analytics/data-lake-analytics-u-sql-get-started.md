---
title: "Bien démarrer avec le langage U-SQL | Microsoft Docs"
description: "Découvrez les principes de base de hello Hello langage U-SQL."
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="fb2d0-103">Bien démarrer avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="fb2d0-103">Get started with U-SQL</span></span>
<span data-ttu-id="fb2d0-104">U-SQL est un langage qui combine SQL déclarative avec impératif c# toolet vous traitez des données à n’importe quelle échelle.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="fb2d0-105">Capacité évolutive, les requêtes distribuées hello U-SQL, vous pouvez efficacement analyser des données dans des magasins relationnelles telles que de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="fb2d0-106">Avec U-SQL, vous pouvez traiter des données non structurées en appliquant des schémas de lecture et en insérant une logique personnalisée et des fonctions définies par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="fb2d0-107">En outre, U-SQL inclut d’extensibilité qui vous donne un contrôle affiné sur la façon de tooexecute à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="fb2d0-108">Ressources d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="fb2d0-108">Learning resources</span></span>

* <span data-ttu-id="fb2d0-109">Hello [U-SQL didacticiel](http://aka.ms/usqltutorial) fournit une procédure pas à pas guidée de la plupart de la langue de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="fb2d0-110">Ce document est recommandé de lecture pour tous les développeurs qui souhaitent toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="fb2d0-111">Pour plus d’informations sur hello **syntaxe du langage SQL-U**, consultez hello [U-SQL de référence du langage](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="fb2d0-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="fb2d0-112">toounderstand hello **philosophie de conception U-SQL**, consultez billet de blog Visual Studio hello [présentation U-SQL – un langage qui facilite le traitement des données de grande procédure](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="fb2d0-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb2d0-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fb2d0-113">Prerequisites</span></span>

<span data-ttu-id="fb2d0-114">Avant de passer par le biais des exemples de hello U-SQL dans ce document, lire et effectuer [didacticiel : les scripts de développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb2d0-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="fb2d0-115">Ce didacticiel explique les mécanismes de hello d’à l’aide de U-SQL Azure Data Lake Tools pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="fb2d0-116">Votre premier script U-SQL</span><span class="sxs-lookup"><span data-stu-id="fb2d0-116">Your first U-SQL script</span></span>

<span data-ttu-id="fb2d0-117">Hello script U-SQL suivant est simple et nous permet d’Explorer le langage de hello U-SQL plusieurs aspects.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="fb2d0-118">Ce script n'a aucune étape de transformation.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="fb2d0-119">Il lit à partir du fichier de source de hello appelée `SearchLog.tsv`, il schematizes et réécrit hello ensemble de lignes dans un fichier appelé SearchLog-premier-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="fb2d0-120">Notez hello point d’interrogation suivant toohello type de données Bonjour `Duration` champ.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="fb2d0-121">Cela signifie que hello `Duration` champ peut être null.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="fb2d0-122">Concepts clés</span><span class="sxs-lookup"><span data-stu-id="fb2d0-122">Key concepts</span></span>
* <span data-ttu-id="fb2d0-123">**Variables de l’ensemble de lignes**: tooa variable peut être affectée à chaque expression de requête qui produit un ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="fb2d0-124">U-SQL suit le modèle de désignation variable hello T-SQL (`@searchlog`, par exemple) dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="fb2d0-125">Hello **extraire** lit les données à partir d’un fichier de mots clés et définit le schéma de hello lors de la lecture.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="fb2d0-126">`Extractors.Tsv` est un extracteur U-SQL intégré pour les fichiers de valeurs séparées par des tabulations.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="fb2d0-127">Vous pouvez développer des extracteurs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="fb2d0-128">Hello **sortie** écrit des données à partir d’un fichier de tooa ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="fb2d0-129">`Outputters.Csv()`est un toocreate d’outputter U-SQL intégré à un fichier de valeurs séparées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="fb2d0-130">Vous pouvez développer des générateurs de sortie personnalisés.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="fb2d0-131">Chemins d’accès</span><span class="sxs-lookup"><span data-stu-id="fb2d0-131">File paths</span></span>

<span data-ttu-id="fb2d0-132">Hello extrait et instructions de sortie utilisent des chemins d’accès de fichier.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="fb2d0-133">Les chemins d’accès peuvent être absolus ou relatifs :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="fb2d0-134">Ce chemin d’accès de fichier absolu suivant fait référence fichier tooa dans un magasin Data Lake Store nommé `mystore`:</span><span class="sxs-lookup"><span data-stu-id="fb2d0-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="fb2d0-135">Le chemin d’accès suivant commence par `"/"`.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="fb2d0-136">Il fait référence le fichier tooa dans le compte de Data Lake Store hello par défaut :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="fb2d0-137">Utiliser des variables scalaires</span><span class="sxs-lookup"><span data-stu-id="fb2d0-137">Use scalar variables</span></span>

<span data-ttu-id="fb2d0-138">Vous pouvez utiliser les variables scalaires comme toomake bien vos tâches de maintenance de script plus facile.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="fb2d0-139">script U-SQL de la précédent Hello peut également être écrites en tant que :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="fb2d0-140">Transformer des ensembles de lignes</span><span class="sxs-lookup"><span data-stu-id="fb2d0-140">Transform rowsets</span></span>

<span data-ttu-id="fb2d0-141">Utilisez **sélectionnez** tootransform les ensembles de lignes :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="fb2d0-142">Hello clause WHERE utilise un [expression c# booléenne](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb2d0-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="fb2d0-143">Vous pouvez utiliser hello c# expression language toodo vos propres expressions et fonctions.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="fb2d0-144">Vous pouvez même effectuer un filtrage plus complexe en les combinant avec des conjonctions logiques (AND) et des disjonctions (OR).</span><span class="sxs-lookup"><span data-stu-id="fb2d0-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="fb2d0-145">Hello le script suivant utilise méthode DateTime.Parse() de hello et une association.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="fb2d0-146">seconde Hello fonctionne sur le résultat de hello de hello premier ensemble de lignes, ce qui crée un composite des hello deux filtres.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="fb2d0-147">Vous pouvez également réutiliser un nom de variable et les noms de hello sont limités lexicalement.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="fb2d0-148">Ensembles de lignes agrégés</span><span class="sxs-lookup"><span data-stu-id="fb2d0-148">Aggregate rowsets</span></span>
<span data-ttu-id="fb2d0-149">Permet de U-SQL vous hello familiers ORDER BY, GROUP BY et les agrégations.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="fb2d0-150">Hello requête suivante recherche la durée totale de hello par région, puis affiche en haut de hello cinq durées dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="fb2d0-151">Ensembles de lignes U-SQL ne conservent pas leur ordre pour la requête suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="fb2d0-152">Par conséquent, tooorder un résultat, vous devez tooadd instruction ORDER BY sortie toohello :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="fb2d0-153">Hello U-SQL ORDER BY clause requiert l’utilisation de la clause FETCH hello dans une expression SELECT.</span><span class="sxs-lookup"><span data-stu-id="fb2d0-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="fb2d0-154">clause d’U-SQL ayant Hello peut être utilisé toorestrict hello sortie toogroups qui satisfont la condition HAVING hello :</span><span class="sxs-lookup"><span data-stu-id="fb2d0-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="fb2d0-155">Pour des scénarios avancés d’agrégation, consultez la documentation de référence hello hello U-SQL pour [agréger, analytique et référencer des fonctions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="fb2d0-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb2d0-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb2d0-156">Next steps</span></span>
* [<span data-ttu-id="fb2d0-157">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="fb2d0-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="fb2d0-158">Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb2d0-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
