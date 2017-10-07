---
title: "les scripts aaaExtend U-SQL de R dans Azure données Lake Analytique | Documents Microsoft"
description: "Découvrez comment toorun R code scripts U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Tutoriel : Get started with extending U-SQL with R (Bien démarrer avec l’extension de U-SQL avec R)

Hello l’exemple suivant illustre les étapes de base hello pour le déploiement de code R :
* Hello d’utilisation `REFERENCE ASSEMBLY` extensions tooenable R instruction hello Script U-SQL.
* Utilisez le` REDUCE` hello de toopartition opération d’entrée de données sur une clé.
* extensions de Hello R U-SQL : un réducteur intégré (`Extension.R.Reducer`) qui exécute le code R sur chaque réducteur de toohello sommets attribué. 
* L’utilisation de dédié nommé trames de données appelées `inputFromUSQL` et `outputToUSQL `respectivement les données toopass entre U-SQL et R. entrée et sortie les noms d’identificateur de trame de données sont fixes (autrement dit, les utilisateurs ne peuvent pas modifier ces noms prédéfinis d’entrée et sortie trame de données identificateurs).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>L’incorporation de code R Bonjour script U-SQL

Vous pouvez le code inline hello R votre script U-SQL à l’aide du paramètre de commande hello Hello `Extension.R.Reducer`. Par exemple, vous pouvez déclarer hello script R comme une variable de chaîne et passez-le comme un paramètre de toohello du réducteur.


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Conserver le code hello R dans un fichier distinct et y fait référence script de hello U-SQL

Bonjour à l’exemple suivant illustre une utilisation plus complexe. Dans ce cas, le code de hello R est déployé en tant que ressource est hello script U-SQL.

Enregistrez ce code R dans un fichier distinct.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Utilisez un toodeploy de script U-SQL script R avec hello instruction déployer des ressources.

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a>Intégration de R à U-SQL

### <a name="datatypes"></a>Types de données
* Les colonnes de chaîne et numériques de U-SQL sont converties en l’état entre un tableau de données R et U-SQL [types pris en charge : `double`, `string`, `bool`, `integer`, `byte`].
* Hello `Factor` type de données n’est pas pris en charge dans U-SQL.
* `byte[]` doit être sérialisé sous forme de `string` codé en base64.
* Les chaînes de U-SQL peuvent être toofactors converti dans le code R, une fois que U-SQL create R trame de données d’entrée ou en définissant un paramètre de réducteur de hello `stringsAsFactors: true`.

### <a name="schemas"></a>Schémas
* Les jeux de données U-SQL ne peuvent pas avoir de noms de colonnes en double.
* Les noms de colonnes des jeux de données U-SQL doivent être des chaînes.
* Noms de colonnes doivent être hello même dans les scripts U-SQL et R.
* En lecture seule colonne ne peut pas faire partie de la trame de données de sortie hello. Étant donné que les colonnes en lecture seule sont automatiquement injectés dans hello U-SQL table s’il s’agit d’une partie du schéma de sortie de l’opérateur.

### <a name="functional-limitations"></a>Limitations fonctionnelles
* Hello moteur R ne peut pas être instanciée à deux reprises dans hello même processus. 
* Pour la prédiction, l’utilisation d’opérateurs de combinateur définis par l’utilisateur avec des modèles partitionnés générés à l’aide d’opérateurs de réducteur définis par l’utilisateur n’est pas prise en charge par U-SQL. Les utilisateurs peuvent déclarer des modèles de hello partitionnée en tant que ressource et les utiliser dans leur Script R (consultez l’exemple de code `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Versions de R
Seul R 3.2.2 est pris en charge.

### <a name="standard-r-modules"></a>Modules R standard

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a>Limitations de taille d’entrée et de sortie
Chaque sommet a une quantité limitée de mémoire assignée tooit. Étant donné que hello trames de données d’entrée et de sortie doit exister dans la mémoire dans le code hello R, taille totale hello hello entrée et sortie ne peut pas dépasser 500 Mo.

### <a name="sample-code"></a>Exemple de code
Des exemples de code est disponible dans votre compte Data Lake Store après avoir installé les extensions d’Analytique avancée d’U-SQL hello. chemin d’accès de Hello pour des exemples de code est : `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Déploiement des modules R personnalisés avec U-SQL

Tout d’abord, créer un module personnalisé R et code postal il et ensuite télécharger hello compressé magasin ADL tooyour de fichiers de module personnalisé R. Dans l’exemple de hello, nous téléchargera compte ADLS hello par défaut pour hello compte ADLA nous utilisons magittr_1.5.zip toohello racine. Une fois que vous téléchargez le magasin de tooADL module hello, déclarez-le comme utiliser toomake de déployer des ressources disponibles dans votre script U-SQL et les appeler `install.packages` tooinstall il.

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a>Étapes suivantes
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure](data-lake-analytics-use-window-functions.md)
