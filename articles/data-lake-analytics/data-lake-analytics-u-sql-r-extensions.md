---
title: "Extension des scripts U-SQL à l’aide de code R dans Azure Data Lake Analytics | Microsoft Docs"
description: "Découvrez comment exécuter un code R dans des scripts U-SQL"
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
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="ecee8-103">Tutoriel : Get started with extending U-SQL with R (Bien démarrer avec l’extension de U-SQL avec R)</span><span class="sxs-lookup"><span data-stu-id="ecee8-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="ecee8-104">L’exemple suivant illustre les étapes de base pour déployer un code R :</span><span class="sxs-lookup"><span data-stu-id="ecee8-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="ecee8-105">Utilisation de l’instruction `REFERENCE ASSEMBLY` pour activer les extensions R pour le script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="ecee8-106">Utilisation de l’opération ` REDUCE` pour partitionner les données d’entrée sur une clé.</span><span class="sxs-lookup"><span data-stu-id="ecee8-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="ecee8-107">Les extensions R pour U-SQL comprennent un réducteur intégré (`Extension.R.Reducer`) qui exécute le code R sur chaque vertex affecté au réducteur.</span><span class="sxs-lookup"><span data-stu-id="ecee8-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="ecee8-108">Utilisation de tableaux de données nommés dédiés, respectivement intitulés `inputFromUSQL` et `outputToUSQL `, pour transférer des données entre USQL et R. Les noms des identificateurs des tableaux de données d’entrée et de sortie sont fixes. Autrement dit, les utilisateurs ne peuvent pas modifier les noms prédéfinis des identificateurs des tableaux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="ecee8-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="ecee8-109">Incorporation de code R dans le script U-SQL</span><span class="sxs-lookup"><span data-stu-id="ecee8-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="ecee8-110">Vous pouvez incorporer du code R à votre script U-SQL à l’aide du paramètre de commande du réducteur `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="ecee8-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="ecee8-111">Par exemple, vous pouvez déclarer le script R comme une variable de chaîne et le passer en tant que paramètre au raccord de réduction.</span><span class="sxs-lookup"><span data-stu-id="ecee8-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="ecee8-112">Conserver le code R dans un fichier distinct et le référencer dans le script U-SQL</span><span class="sxs-lookup"><span data-stu-id="ecee8-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="ecee8-113">L’exemple suivant illustre un usage plus complexe.</span><span class="sxs-lookup"><span data-stu-id="ecee8-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="ecee8-114">Dans ce cas, le code R est déployé comme une ressource correspondant au script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="ecee8-115">Enregistrez ce code R dans un fichier distinct.</span><span class="sxs-lookup"><span data-stu-id="ecee8-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="ecee8-116">Utilisez un script U-SQL pour déployer ce script R avec l’instruction DEPLOY RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="ecee8-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="ecee8-117">Intégration de R à U-SQL</span><span class="sxs-lookup"><span data-stu-id="ecee8-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="ecee8-118">Types de données</span><span class="sxs-lookup"><span data-stu-id="ecee8-118">Datatypes</span></span>
* <span data-ttu-id="ecee8-119">Les colonnes de chaîne et numériques de U-SQL sont converties en l’état entre un tableau de données R et U-SQL [types pris en charge : `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="ecee8-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="ecee8-120">Le type de données `Factor` n’est pas pris en charge dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="ecee8-121">`byte[]` doit être sérialisé sous forme de `string` codé en base64.</span><span class="sxs-lookup"><span data-stu-id="ecee8-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="ecee8-122">Les chaînes U-SQL peuvent être converties en facteurs dans le code R quand U-SQL crée un tableau de données d’entrée R ou en définissant le paramètre du réducteur sur `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="ecee8-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="ecee8-123">Schémas</span><span class="sxs-lookup"><span data-stu-id="ecee8-123">Schemas</span></span>
* <span data-ttu-id="ecee8-124">Les jeux de données U-SQL ne peuvent pas avoir de noms de colonnes en double.</span><span class="sxs-lookup"><span data-stu-id="ecee8-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="ecee8-125">Les noms de colonnes des jeux de données U-SQL doivent être des chaînes.</span><span class="sxs-lookup"><span data-stu-id="ecee8-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="ecee8-126">Les noms de colonnes doivent être identiques dans U-SQL et dans les scripts R.</span><span class="sxs-lookup"><span data-stu-id="ecee8-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="ecee8-127">Les colonnes en lecture seule ne peuvent pas faire partie du tableau de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="ecee8-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="ecee8-128">Car les colonnes en lecture seule sont automatiquement réinjectées dans la table U-SQL si elles font partie du schéma de sortie de l’opérateur défini par l’utilisateur (UDO).</span><span class="sxs-lookup"><span data-stu-id="ecee8-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="ecee8-129">Limitations fonctionnelles</span><span class="sxs-lookup"><span data-stu-id="ecee8-129">Functional limitations</span></span>
* <span data-ttu-id="ecee8-130">Le moteur R ne peut pas être instancié deux fois dans le même processus.</span><span class="sxs-lookup"><span data-stu-id="ecee8-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="ecee8-131">Pour la prédiction, l’utilisation d’opérateurs de combinateur définis par l’utilisateur avec des modèles partitionnés générés à l’aide d’opérateurs de réducteur définis par l’utilisateur n’est pas prise en charge par U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="ecee8-132">Les utilisateurs peuvent déclarer les modèles partitionnés comme des ressources et les utiliser dans leur script R (voir l’exemple de code `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="ecee8-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="ecee8-133">Versions de R</span><span class="sxs-lookup"><span data-stu-id="ecee8-133">R Versions</span></span>
<span data-ttu-id="ecee8-134">Seul R 3.2.2 est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ecee8-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="ecee8-135">Modules R standard</span><span class="sxs-lookup"><span data-stu-id="ecee8-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="ecee8-136">Limitations de taille d’entrée et de sortie</span><span class="sxs-lookup"><span data-stu-id="ecee8-136">Input and Output size limitations</span></span>
<span data-ttu-id="ecee8-137">Chaque vertex possède une quantité limitée de mémoire qui lui est assignée.</span><span class="sxs-lookup"><span data-stu-id="ecee8-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="ecee8-138">Étant donné que les tableaux de données d’entrée et de sortie doivent exister dans la mémoire dans le code R, la taille totale de l’entrée et de la sortie ne peut pas dépasser 500 Mo.</span><span class="sxs-lookup"><span data-stu-id="ecee8-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="ecee8-139">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="ecee8-139">Sample Code</span></span>
<span data-ttu-id="ecee8-140">Des exemples de code supplémentaires sont mis à disposition dans votre compte Data Lake Store après l’installation des extensions analytiques avancées U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="ecee8-141">Pour obtenir des exemples de code supplémentaires, suivez ce chemin : `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="ecee8-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="ecee8-142">Déploiement des modules R personnalisés avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="ecee8-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="ecee8-143">Tout d’abord, créez un module R personnalisé, incluez-le dans un fichier zip, puis chargez le fichier de module R personnalisé zippé dans votre magasin ADL.</span><span class="sxs-lookup"><span data-stu-id="ecee8-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="ecee8-144">Dans l’exemple, nous allons charger magittr_1.5.zip vers la racine du compte ADLS par défaut pour le compte ADLA que nous utilisons.</span><span class="sxs-lookup"><span data-stu-id="ecee8-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="ecee8-145">Une fois le module chargé dans le magasin ADL, déclarez-le à l’aide de DEPLOY RESOURCE pour le rendre disponible dans votre script U-SQL, puis appelez `install.packages` pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="ecee8-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
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

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="ecee8-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ecee8-146">Next Steps</span></span>
* [<span data-ttu-id="ecee8-147">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ecee8-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="ecee8-148">Développer des scripts U-SQL avec les outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ecee8-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="ecee8-149">Utilisation des fonctions U-SQL dans les travaux Analytique Data Lake Azure</span><span class="sxs-lookup"><span data-stu-id="ecee8-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
