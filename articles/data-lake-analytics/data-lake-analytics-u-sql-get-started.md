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
# <a name="get-started-with-u-sql"></a>Bien démarrer avec U-SQL
U-SQL est un langage qui combine SQL déclarative avec impératif c# toolet vous traitez des données à n’importe quelle échelle. Capacité évolutive, les requêtes distribuées hello U-SQL, vous pouvez efficacement analyser des données dans des magasins relationnelles telles que de la base de données SQL Azure. Avec U-SQL, vous pouvez traiter des données non structurées en appliquant des schémas de lecture et en insérant une logique personnalisée et des fonctions définies par l'utilisateur. En outre, U-SQL inclut d’extensibilité qui vous donne un contrôle affiné sur la façon de tooexecute à grande échelle. 

## <a name="learning-resources"></a>Ressources d’apprentissage

* Hello [U-SQL didacticiel](http://aka.ms/usqltutorial) fournit une procédure pas à pas guidée de la plupart de la langue de hello U-SQL. Ce document est recommandé de lecture pour tous les développeurs qui souhaitent toolearn U-SQL.
* Pour plus d’informations sur hello **syntaxe du langage SQL-U**, consultez hello [U-SQL de référence du langage](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* toounderstand hello **philosophie de conception U-SQL**, consultez billet de blog Visual Studio hello [présentation U-SQL – un langage qui facilite le traitement des données de grande procédure](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Composants requis

Avant de passer par le biais des exemples de hello U-SQL dans ce document, lire et effectuer [didacticiel : les scripts de développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Ce didacticiel explique les mécanismes de hello d’à l’aide de U-SQL Azure Data Lake Tools pour Visual Studio.

## <a name="your-first-u-sql-script"></a>Votre premier script U-SQL

Hello script U-SQL suivant est simple et nous permet d’Explorer le langage de hello U-SQL plusieurs aspects.

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

Ce script n'a aucune étape de transformation. Il lit à partir du fichier de source de hello appelée `SearchLog.tsv`, il schematizes et réécrit hello ensemble de lignes dans un fichier appelé SearchLog-premier-u-sql.csv.

Notez hello point d’interrogation suivant toohello type de données Bonjour `Duration` champ. Cela signifie que hello `Duration` champ peut être null.

### <a name="key-concepts"></a>Concepts clés
* **Variables de l’ensemble de lignes**: tooa variable peut être affectée à chaque expression de requête qui produit un ensemble de lignes. U-SQL suit le modèle de désignation variable hello T-SQL (`@searchlog`, par exemple) dans le script de hello.
* Hello **extraire** lit les données à partir d’un fichier de mots clés et définit le schéma de hello lors de la lecture. `Extractors.Tsv` est un extracteur U-SQL intégré pour les fichiers de valeurs séparées par des tabulations. Vous pouvez développer des extracteurs personnalisés.
* Hello **sortie** écrit des données à partir d’un fichier de tooa ensemble de lignes. `Outputters.Csv()`est un toocreate d’outputter U-SQL intégré à un fichier de valeurs séparées par des virgules. Vous pouvez développer des générateurs de sortie personnalisés.

### <a name="file-paths"></a>Chemins d’accès

Hello extrait et instructions de sortie utilisent des chemins d’accès de fichier. Les chemins d’accès peuvent être absolus ou relatifs :

Ce chemin d’accès de fichier absolu suivant fait référence fichier tooa dans un magasin Data Lake Store nommé `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

Le chemin d’accès suivant commence par `"/"`. Il fait référence le fichier tooa dans le compte de Data Lake Store hello par défaut :

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Utiliser des variables scalaires

Vous pouvez utiliser les variables scalaires comme toomake bien vos tâches de maintenance de script plus facile. script U-SQL de la précédent Hello peut également être écrites en tant que :

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

## <a name="transform-rowsets"></a>Transformer des ensembles de lignes

Utilisez **sélectionnez** tootransform les ensembles de lignes :

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

Hello clause WHERE utilise un [expression c# booléenne](https://msdn.microsoft.com/library/6a71f45d.aspx). Vous pouvez utiliser hello c# expression language toodo vos propres expressions et fonctions. Vous pouvez même effectuer un filtrage plus complexe en les combinant avec des conjonctions logiques (AND) et des disjonctions (OR).

Hello le script suivant utilise méthode DateTime.Parse() de hello et une association.

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
 >seconde Hello fonctionne sur le résultat de hello de hello premier ensemble de lignes, ce qui crée un composite des hello deux filtres. Vous pouvez également réutiliser un nom de variable et les noms de hello sont limités lexicalement.

## <a name="aggregate-rowsets"></a>Ensembles de lignes agrégés
Permet de U-SQL vous hello familiers ORDER BY, GROUP BY et les agrégations.

Hello requête suivante recherche la durée totale de hello par région, puis affiche en haut de hello cinq durées dans l’ordre.

Ensembles de lignes U-SQL ne conservent pas leur ordre pour la requête suivante de hello. Par conséquent, tooorder un résultat, vous devez tooadd instruction ORDER BY sortie toohello :

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

Hello U-SQL ORDER BY clause requiert l’utilisation de la clause FETCH hello dans une expression SELECT.

clause d’U-SQL ayant Hello peut être utilisé toorestrict hello sortie toogroups qui satisfont la condition HAVING hello :

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

Pour des scénarios avancés d’agrégation, consultez la documentation de référence hello hello U-SQL pour [agréger, analytique et référencer des fonctions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
