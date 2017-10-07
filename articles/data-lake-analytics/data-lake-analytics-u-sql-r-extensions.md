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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="4e017-103">Tutoriel : Get started with extending U-SQL with R (Bien démarrer avec l’extension de U-SQL avec R)</span><span class="sxs-lookup"><span data-stu-id="4e017-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="4e017-104">Hello l’exemple suivant illustre les étapes de base hello pour le déploiement de code R :</span><span class="sxs-lookup"><span data-stu-id="4e017-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="4e017-105">Hello d’utilisation `REFERENCE ASSEMBLY` extensions tooenable R instruction hello Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e017-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="4e017-106">Utilisez le` REDUCE` hello de toopartition opération d’entrée de données sur une clé.</span><span class="sxs-lookup"><span data-stu-id="4e017-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="4e017-107">extensions de Hello R U-SQL : un réducteur intégré (`Extension.R.Reducer`) qui exécute le code R sur chaque réducteur de toohello sommets attribué.</span><span class="sxs-lookup"><span data-stu-id="4e017-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="4e017-108">L’utilisation de dédié nommé trames de données appelées `inputFromUSQL` et `outputToUSQL `respectivement les données toopass entre U-SQL et R. entrée et sortie les noms d’identificateur de trame de données sont fixes (autrement dit, les utilisateurs ne peuvent pas modifier ces noms prédéfinis d’entrée et sortie trame de données identificateurs).</span><span class="sxs-lookup"><span data-stu-id="4e017-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="4e017-109">L’incorporation de code R Bonjour script U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e017-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="4e017-110">Vous pouvez le code inline hello R votre script U-SQL à l’aide du paramètre de commande hello Hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="4e017-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="4e017-111">Par exemple, vous pouvez déclarer hello script R comme une variable de chaîne et passez-le comme un paramètre de toohello du réducteur.</span><span class="sxs-lookup"><span data-stu-id="4e017-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="4e017-112">Conserver le code hello R dans un fichier distinct et y fait référence script de hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e017-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="4e017-113">Bonjour à l’exemple suivant illustre une utilisation plus complexe.</span><span class="sxs-lookup"><span data-stu-id="4e017-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="4e017-114">Dans ce cas, le code de hello R est déployé en tant que ressource est hello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e017-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="4e017-115">Enregistrez ce code R dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="4e017-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="4e017-116">Utilisez un toodeploy de script U-SQL script R avec hello instruction déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="4e017-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="4e017-117">Intégration de R à U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e017-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="4e017-118">Types de données</span><span class="sxs-lookup"><span data-stu-id="4e017-118">Datatypes</span></span>
* <span data-ttu-id="4e017-119">Les colonnes de chaîne et numériques de U-SQL sont converties en l’état entre un tableau de données R et U-SQL [types pris en charge : `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="4e017-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="4e017-120">Hello `Factor` type de données n’est pas pris en charge dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e017-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="4e017-121">`byte[]` doit être sérialisé sous forme de `string` codé en base64.</span><span class="sxs-lookup"><span data-stu-id="4e017-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="4e017-122">Les chaînes de U-SQL peuvent être toofactors converti dans le code R, une fois que U-SQL create R trame de données d’entrée ou en définissant un paramètre de réducteur de hello `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="4e017-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="4e017-123">Schémas</span><span class="sxs-lookup"><span data-stu-id="4e017-123">Schemas</span></span>
* <span data-ttu-id="4e017-124">Les jeux de données U-SQL ne peuvent pas avoir de noms de colonnes en double.</span><span class="sxs-lookup"><span data-stu-id="4e017-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="4e017-125">Les noms de colonnes des jeux de données U-SQL doivent être des chaînes.</span><span class="sxs-lookup"><span data-stu-id="4e017-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="4e017-126">Noms de colonnes doivent être hello même dans les scripts U-SQL et R.</span><span class="sxs-lookup"><span data-stu-id="4e017-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="4e017-127">En lecture seule colonne ne peut pas faire partie de la trame de données de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4e017-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="4e017-128">Étant donné que les colonnes en lecture seule sont automatiquement injectés dans hello U-SQL table s’il s’agit d’une partie du schéma de sortie de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="4e017-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="4e017-129">Limitations fonctionnelles</span><span class="sxs-lookup"><span data-stu-id="4e017-129">Functional limitations</span></span>
* <span data-ttu-id="4e017-130">Hello moteur R ne peut pas être instanciée à deux reprises dans hello même processus.</span><span class="sxs-lookup"><span data-stu-id="4e017-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="4e017-131">Pour la prédiction, l’utilisation d’opérateurs de combinateur définis par l’utilisateur avec des modèles partitionnés générés à l’aide d’opérateurs de réducteur définis par l’utilisateur n’est pas prise en charge par U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e017-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="4e017-132">Les utilisateurs peuvent déclarer des modèles de hello partitionnée en tant que ressource et les utiliser dans leur Script R (consultez l’exemple de code `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="4e017-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="4e017-133">Versions de R</span><span class="sxs-lookup"><span data-stu-id="4e017-133">R Versions</span></span>
<span data-ttu-id="4e017-134">Seul R 3.2.2 est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4e017-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="4e017-135">Modules R standard</span><span class="sxs-lookup"><span data-stu-id="4e017-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="4e017-136">Limitations de taille d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="4e017-136">Input and Output size limitations</span></span>
<span data-ttu-id="4e017-137">Chaque sommet a une quantité limitée de mémoire assignée tooit.</span><span class="sxs-lookup"><span data-stu-id="4e017-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="4e017-138">Étant donné que hello trames de données d’entrée et de sortie doit exister dans la mémoire dans le code hello R, taille totale hello hello entrée et sortie ne peut pas dépasser 500 Mo.</span><span class="sxs-lookup"><span data-stu-id="4e017-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="4e017-139">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="4e017-139">Sample Code</span></span>
<span data-ttu-id="4e017-140">Des exemples de code est disponible dans votre compte Data Lake Store après avoir installé les extensions d’Analytique avancée d’U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="4e017-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="4e017-141">chemin d’accès de Hello pour des exemples de code est : `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="4e017-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="4e017-142">Déploiement des modules R personnalisés avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="4e017-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="4e017-143">Tout d’abord, créer un module personnalisé R et code postal il et ensuite télécharger hello compressé magasin ADL tooyour de fichiers de module personnalisé R.</span><span class="sxs-lookup"><span data-stu-id="4e017-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="4e017-144">Dans l’exemple de hello, nous téléchargera compte ADLS hello par défaut pour hello compte ADLA nous utilisons magittr_1.5.zip toohello racine.</span><span class="sxs-lookup"><span data-stu-id="4e017-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="4e017-145">Une fois que vous téléchargez le magasin de tooADL module hello, déclarez-le comme utiliser toomake de déployer des ressources disponibles dans votre script U-SQL et les appeler `install.packages` tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="4e017-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4e017-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e017-146">Next Steps</span></span>
* [<span data-ttu-id="4e017-147">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4e017-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="4e017-148">Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e017-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="4e017-149">Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="4e017-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
